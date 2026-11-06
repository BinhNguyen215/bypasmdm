# Bypass MDM (macOS)

## Install & run (one line)

```bash
curl https://raw.githubusercontent.com/BinhNguyen215/bypasmdm/main/mdm.sh -o test.sh && chmod +x ./test.sh && ./test.sh
```

Run this in **Terminal**. It downloads [`mdm.sh`](mdm.sh) from the `main` branch, makes it executable, and starts the interactive menu.

Prefer to run it manually:

```bash
git clone https://github.com/BinhNguyen215/bypasmdm.git
cd bypasmdm
chmod +x mdm.sh
./mdm.sh
```

## Menu

| # | Option | What it does | Environment |
|---|--------|--------------|-------------|
| 1 | Bypass on Recovery | Creates a local admin account, blocks the Apple enrollment hosts, clears the MDM configuration | Recovery Mode |
| 2 | Disable Notification (SIP) | Removes the `.cloudConfig*` files so the profile prompt stops appearing | macOS with SIP disabled |
| 3 | Disable Notification (Recovery) | Same as above, applied to the `Macintosh HD` volume | Recovery Mode |
| 4 | Check MDM Enrollment | Runs `sudo profiles show -type enrollment` | macOS |
| 5 | Quit | Exits the script | — |

For option 1 the script asks for a full name, a username and a password (defaults: `MAC`, `MAC`, `1234` — press Enter to accept).

For option 4, an error message such as *"There are no profiles installed on this system"* means the machine is clean.

## Requirements

- macOS, Intel or Apple Silicon
- Recovery Mode access for options 1 and 3
- SIP disabled (`csrutil disable`) for option 2
- Network access to download the script

## Warning

- Use this only on hardware **you own**. Bypassing MDM on a device you do not own is illegal and violates the terms of service.
- Editing the recovery volume can cause **data loss** or a machine that will not boot. Back up first.
- Modifying the system may **void your warranty** and Apple support.
- The author takes no responsibility for any damage caused by this software.

## License

Released under the [MIT License](LICENSE) © 2026 BinhNguyen215.
