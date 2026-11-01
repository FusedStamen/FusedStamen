# FusedStamen
RF hobbyist. Wardriver, builder, passive collector.  
Active contributor to WiGLE (username: FusedStamen), [OPwngrid](https://opwngrid.xyz), and community mapping platforms.

<a href="https://wigle.net"><img border="0" src="https://wigle.net/bi/Xud1ssIMdXsvSExZczmaAw.png"></a>

I build wardriving hardware, measure antennas properly, and write the tools I wish already existed. Most of what's here started as a fix for my own setup and got shared because other people had the same problem.

---

## Projects

- **[PACKET_HOG](https://github.com/FusedStamen/PACKET_HOG)** - 10-node ESP32-C5 carrier board for wardriving. Modular, designed in KiCad, and available to buy.
- **[StamenScan](https://github.com/FusedStamen/StamenScan)** - passive surveillance infrastructure detection for the WiFi Pineapple Pager.
- **[antenna-database](https://github.com/FusedStamen/antenna-database)** - 130+ WiFi, LoRa, ADS-B, GPS and LTE antennas measured with a LiteVNA 64 under a written, versioned methodology. Three tiers: VNA bench testing, fixed-location field testing with a Biscuit Ultra, and open-field range comparison. Verdicts are based on worst in-band SWR, not SWR at resonance. Outside contributors are credited in the repo.
- **[antenna-database-v2](https://github.com/FusedStamen/antenna-database-v2)** - a ground-up rebuild where every entry has a verified purchase source, a manufacturer SKU and a direct link, so you can buy exactly what was tested. Every unit is tested individually, and thresholds are tuned for passive-receive wardriving rather than transmit.
- **[ads-b](https://github.com/FusedStamen/ads-b)** - ADS-B archive logger. A single stdlib-only Python script that polls a dump1090-fa, readsb or tar1090 feed and builds a daily archive of every unique aircraft seen. Runs on Windows and Linux, with setup docs for Task Scheduler and systemd.
- **[AWUS036ACM_Setup](https://github.com/FusedStamen/AWUS036ACM_Setup)** - sets up the Alfa AWUS036ACM (MT7612U) in monitor mode on the WiFi Pineapple Pager with configurable channel hopping that keeps running after the payload exits, so other payloads can use it immediately.

---

## Tools
- [`wigle_sort`](https://github.com/FusedStamen/Wigle) - Merge, deduplicate, and split WiGLE CSV exports by region
- [`wigle_sort_v2`](https://github.com/FusedStamen/Wigle) - Extended version with 46-country + US state-level splitting, channel analysis, and structured output
- [`wigle_sort_v3`](https://github.com/FusedStamen/Wigle) - v2 plus a small-state bounding box fix (Rhode Island, DC, etc. now match correctly instead of being swallowed by larger neighbors)
- [`wigle_channel_compare`](https://github.com/FusedStamen/Wigle) - Side-by-side channel distribution comparison between two scan datasets, for A/B testing scan configurations
- [`beacon_spam_detector`](https://github.com/FusedStamen/Wigle) and beacon spam contamination analysis - find and measure beacon-spam noise in wardriving logs

---

## Contributions to other people's projects

**WatchDogsGo (LOCOSP)**
- **[wdg_wifi_bridge.py](https://github.com/FusedStamen/WatchDogsGo)** - lets the game run on uConsole AIO v1 hardware without an ESP32, using the host's own WiFi (via `iw`) and Bluetooth (via `bleak`) adapters by emulating the projectZero serial protocol. Listed by name under Community contributions in the upstream README.
- **[Fork](https://github.com/FusedStamen/WatchDogsGo)** - compatibility fixes for hardware that doesn't match the reference setup, including AC1200-based builds.

**WDGoWars Pineapple Pager payload (LOCOSP)**
- **[GPS scanner rewrite](https://github.com/FusedStamen/pineapple_pager_wdgwars/commit/88b61faa14338dfa244fb9d17df28c4cc814b12b)** - replaced the raw serial GPS reader with a gpsd socket client (146 lines added, 251 removed in `scanners/gps.py`).

**Hak5 WiFi Pineapple Pager payload library**
- **Jelly Sentinel fixes** - diagnosed and fixed six false-positive and parsing problems in another author's recon payload, found by running it on my own Pager, and submitted them as PR #325. The original author thanked me for the contribution; the PR was closed without merging.
  - Router credential check: replaced "HTTP 200/302 means success" with vendor-specific login verification (TP-Link, ASUS, Netgear, MikroTik, plus a generic fallback)
  - PMF check: stopped flagging WPA3 networks and scoped the check to the connected AP instead of every AP in range
  - DNS rebinding test: replaced a domain that can never resolve with real external domains, so the test can actually fire
  - AP count: scoped to the current scan instead of the cumulative recon database (it was reporting 85,000+)
  - OUI vendor lookup: fixed blank vendor names caused by a leading newline in `whoismac` output
  - Device classification: stopped labeling EasyMesh nodes and range extenders as routers just because of a networking-vendor OUI

---

## WiGLE Stats (last updated 30Aug2026)

- **Total unique records:** 10,055,869
- **Input CSVs processed:** 1,484
- **Countries covered:** 8
- **US states covered:** 42

### Type Breakdown

| Type | Count |
|---|---:|
| BLE | 6,177,566 |
| WIFI | 2,769,859 |
| BT | 1,082,536 |
| LTE | 19,742 |
| GSM | 5,404 |
| WCDMA | 762 |

### Top 15 Countries

| Country | Records |
|---|---:|
| usa | 9,451,779 |
| netherlands | 259,370 |
| mexico | 155,833 |
| india | 153,381 |
| uk | 22,012 |
| other | 10,997 |
| canada | 2,407 |

---

## Hardware
- Packet_Hog
- uConsole CM4
- An egregious amount of ESP32s
- T-Dongle C5
- Hak5 WiFi Pineapple Pager
- C5 Wardriver (ESP32-C5)
- Signal Sleuth (dual ESP32-WROOM-32U + BW16)
- RayHunter (Orbic - T-Mobile / Verizon / AT&T)
- ESP32 Marauder Mini / V7 / V8
- Pwnagotchi fleet
- muzi works R1 Neo
- Flipper Zero
- LiteVNA 64
- AirGradient + EnviroPi air quality monitors
- GL.iNet GL-MT3000
- Bambu Lab P1S

---

## Disclaimer

Everything here is shared for education, research and personal use. These are my personal projects, not affiliated with or endorsed by any employer.

- **Authorized use only.** Use these tools, scripts and designs only on networks, devices and radio spectrum you own or have explicit written permission to test.
- **Passive collection.** Wardriving and ADS-B logging here record signals that devices broadcast openly. Don't use collected data to track, identify or harass anyone.
- **Active features.** Some projects, mostly forks of other people's work such as WatchDogsGo and the Pineapple Pager payloads, include active security-testing features. Check your local laws before using them.
- **Your responsibility.** Laws on computer access, interception and radio use differ by country and state. Following them is on you.
- **Hardware.** Board designs and cases are provided as-is. Review them yourself before building, especially anything involving batteries or power.
- **Antenna data.** Measurements describe the specific units I tested using the documented methodology. Your results may differ.
- **No warranty.** Everything is provided "as is", without warranty of any kind. I'm not liable for damage, data loss or misuse.
- **Trademarks.** WiGLE, Hak5, Flipper, Alfa and other names belong to their owners. No affiliation is implied.

---

## Links
- 🌐 [fusedstamen.com](https://fusedstamen.com)
- 📡 WiGLE username: FusedStamen
- 💬 [Join my Discord server](https://discord.gg/CbHqnBnq3J)
- ✉️ [Message me on Discord](https://discord.com/users/407585179494907924) (username: FusedStamen)
- ✉️ Antenna test requests and submissions: antennas@fusedstamen.com
- 🎮 [Twitch: FusedStamen](https://twitch.tv/fusedstamen)
- 📺 [YouTube: @fusedstamen](https://www.youtube.com/@fusedstamen)
