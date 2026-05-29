---
title: Info Screen — Raspberry Pi Kiosk
description: Raspberry Pi kiosk info screen setup, CEC TV control, Openlab schedule automation, and barcode scanner service
published: true
date: 2026-05-28T16:59:25.125Z
tags: 
editor: markdown
dateCreated: 2026-04-29T16:27:20.229Z
---

# Info Screen — Raspberry Pi Kiosk

The High Tech Lab entrance TV displays the MaakLeerPlek event dashboard. It is driven by a Raspberry Pi connected via HDMI and turns on/off automatically during Open Lab hours. The same Pi runs the InvenTree barcode scanner script.

## Hardware

| Component | Detail |
|---|---|
| Device | Raspberry Pi 3 Model A+ (512 MB RAM) |
| IP address | DHCP — use `fullpageos.local` to reach it reliably |
| OS | FullPageOS (Bookworm armhf lite 0.14.0) |
| HDMI | Connected to entrance TV |
| CEC | TV controlled over HDMI-CEC (`/dev/cec0`) |
| LCD | Waveshare 2.4inch LCD (ILI9341, SPI) — shows barcode scan output |

## Dashboard

![TV kiosk dashboard screenshot](/u/tv-kiosk-dashboard.png)

The dashboard is a full-screen Next.js app optimised for 4K and divided into three columns:

**Left — Context panel**
Shows the current time and date, live weather from Open-Meteo (temperature, wind speed, humidity, cloud cover), and a "next workshop" widget with a QR code to register. The status widget rotates between the currently running event and the soonest upcoming one, prioritising events matching keywords like "open lab" or "repair café".

**Centre — Event carousel**
Rotates through upcoming workshops and recurring events scraped from the MaakLeerPlek WordPress calendar via the REST API. Each slide shows the event image, title, type badge, date/time, and description. A QR code at the bottom links to the full event page. Navigation dots track the current slide. Transition time is configurable (default 15 s per slide). News articles from `/verhalen/` (up to 14 days old) are also mixed into the carousel.

**Right — Inventory panel**
Displays live stock from InvenTree, grouped by configured location (e.g. HTL-Fridge for drinks, Wood-Supply for materials). Each item shows its name, stock count, price, and a scannable QR code. Stock is refreshed every 5 minutes. A "recent activity" feed at the bottom logs the last few purchases in real time — fed via `POST /api/changelog` from the barcode scanner and the checkout frontend. Confirmation, cancel, and undo buttons appear after a scan.

**Footer**
QR codes linking to `maakleerplek.be` and `wiki.maakleerplek.be`, plus the High Tech Lab logo and app version number.

## What it does

On boot the Pi automatically logs in and launches Chromium in kiosk mode (full screen, no cursor, no address bar). It loads the dashboard at `http://10.72.3.68:8083` and keeps it open continuously.

The TV is turned on and off automatically via **HDMI-CEC**, which lets the Pi send power commands over the HDMI cable — no IR blaster needed.

The Pi also runs the **InvenTree barcode scanner** as a systemd service (`barcode-inventree`), started automatically on boot.

## Open Lab Schedule

The TV follows the Open Lab schedule. Systemd timers on the Pi trigger the CEC commands:

| Timer | Schedule |
|---|---|
| `tv-on.timer` | Daily at 10:00 |
| `tv-off.timer` | Daily at 00:00 |

Timer and service files live in `/home/pi/Interface-stock/systemd/` and are installed to `/etc/systemd/system/`.

## Scripts

All TV scripts live in `/home/pi/Interface-stock/scripts/` on the Pi.

**Turn TV on** (`tv-on.sh`):
```bash
cec-ctl -d /dev/cec0 --playback --to 0 --image-view-on
cec-ctl -d /dev/cec0 --playback --active-source phys-addr=1.0.0.0
```

**Turn TV off** (`tv-off.sh`):
```bash
cec-ctl -d /dev/cec0 --playback --to 0 --standby
```

**Kiosk URL** is set in `/boot/firmware/fullpageos.txt`. To change it, edit that file and reboot.

## Systemd Timers

The TV on/off schedule is managed by systemd timers, not cron jobs.

```bash
# Check timer status
systemctl status tv-on.timer tv-off.timer

# Manually trigger
sudo systemctl start tv-on.service
sudo systemctl start tv-off.service

# View logs
journalctl -u tv-on.service -n 20
```

> ⚠️ **Fix applied 2026-05-28:** The scripts `tv-on.sh` and `tv-off.sh` were missing the execute bit (`-rw-r--r--`), causing `status=203/EXEC` failures every day since 2026-05-21. Fixed with `chmod +x /home/pi/Interface-stock/scripts/tv-on.sh /home/pi/Interface-stock/scripts/tv-off.sh`.

## Barcode Scanner Service

The InvenTree barcode script runs from `/home/pi/Interface-stock/` in a Python virtualenv.

```bash
# Check status
sudo systemctl status barcode-inventree

# View logs
journalctl -u barcode-inventree -f

# Restart
sudo systemctl restart barcode-inventree
```

Config is in `/home/pi/Interface-stock/.env`. Source repo: https://github.com/maakleerplek/Interface-stock

## Performance & Memory Tweaks

The Pi has only 512 MB RAM. The following tweaks are applied to keep it running smoothly:

- **ZRAM**: Compressed swap in RAM (`zram-tools`, lz4, 50% of RAM) — enabled via `systemctl enable zramswap`
- **Swap**: Increased to 1 GB (`/etc/dphys-swapfile`: `CONF_SWAPSIZE=1024`)
- **CPU governor**: Set to `performance` via `cpufrequtils`
- **Overclock**: `arm_freq=1400`, `over_voltage=2` in `/boot/firmware/config.txt` (Pi 3A+ runs ~57°C under load — fine without heatsink)
- **GPU memory**: `gpu_mem=128` for Chromium rendering
- **tmpfs**: `/tmp` mounted in RAM (64MB) to reduce SD card writes
- **Disabled services**: `bluetooth`, `ModemManager`, `triggerhappy`, `udisks2`, `upower`, `x11vnc`
- **Chromium flags**: `--no-memcheck` (suppresses low-RAM warning), `--disable-infobars`
- **Kernel tuning**: `vm.min_free_kbytes=8192` in `/etc/sysctl.d/99-pi-tweaks.conf`

## ⚠️ Do NOT run `sudo apt upgrade`

Running `sudo apt upgrade` has previously broken the Pi — it updated the firmware/kernel and caused WiFi to stop working, making the Pi unreachable and stuck on the boot screen. Only install specific packages if needed, never a full system upgrade.

## SSH Access

```bash
ssh pi@fullpageos.local
# or by IP (DHCP, may change):
ssh pi@10.72.3.105
```

Password is in the HTL password sheet.

## Reflashing

If the Pi needs to be reflashed:

1. Download FullPageOS Stable from Raspberry Pi Imager or the [FullPageOS GitHub releases](https://github.com/guysoft/FullPageOS)
2. Flash with `dd`: `sudo dd if=fullpageos.img of=/dev/sdX bs=4M status=progress`
3. Mount the boot partition and configure:
   - `/boot/firmware/fullpageos.txt` → set URL to `http://10.72.3.68:8083`
   - `/boot/firmware/wifi.nmconnection` → set SSID `maakleerplek - cowork` and password
4. Boot the Pi, SSH in via `fullpageos.local` (default password: `raspberry`, change immediately)
5. Clone and set up barcode script:
   ```bash
   git clone https://github.com/maakleerplek/Interface-stock.git ~/Interface-stock
   cd ~/Interface-stock
   bash install.sh          # installs deps, venv, SPI, Waveshare LCD drivers
   cp .env.example .env     # then edit with real credentials
   # Create barcode-inventree systemd service (see SERVICE_GUIDE.md)
   sudo systemctl enable --now barcode-inventree
   ```
6. Apply performance tweaks (ZRAM, swap, overclock, disabled services) — see section above
7. Suppress Chromium RAM warning: add `--no-memcheck` to `/opt/custompios/scripts/start_chromium_browser`
8. Install systemd TV timers:
   ```bash
   sudo cp ~/Interface-stock/systemd/tv-on.service /etc/systemd/system/
   sudo cp ~/Interface-stock/systemd/tv-off.service /etc/systemd/system/
   sudo cp ~/Interface-stock/systemd/tv-on.timer /etc/systemd/system/
   sudo cp ~/Interface-stock/systemd/tv-off.timer /etc/systemd/system/
   chmod +x ~/Interface-stock/scripts/tv-on.sh ~/Interface-stock/scripts/tv-off.sh
   sudo systemctl enable --now tv-on.timer tv-off.timer
   ```
9. Reboot to apply all changes

## Troubleshooting

| Issue | Fix |
|---|---|
| TV does not turn on/off automatically | Check `systemctl status tv-on.timer tv-off.timer`; verify scripts have execute bit: `ls -la ~/Interface-stock/scripts/tv-*.sh` |
| TV does not respond to manual command | Run `sudo systemctl start tv-on.service` and check `journalctl -u tv-on.service -n 10` |
| Wrong page shown | Edit `/boot/firmware/fullpageos.txt` and reboot |
| Pi not reachable by IP | Use `fullpageos.local` — IP is assigned by DHCP and may change |
| Pi not reachable at all | Check power and WiFi; **do not run `sudo apt upgrade`** |
| Screen stuck on OS title screen | WiFi not connected — check `wifi.nmconnection` on boot partition |
| Screen blank after reboot | Wait ~30 s for Chromium to load; if stuck, `sudo reboot` over SSH |
| Barcode script not running | `sudo systemctl status barcode-inventree` and check logs with `journalctl -u barcode-inventree` |
| LCD display white/blank | Check SPI is enabled in `/boot/firmware/config.txt` (`dtparam=spi=on`); reboot after enabling |
| LCD colors inverted or mirrored | LCD driver issue — pull latest from repo and reboot |