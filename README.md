# Brave Debloater for macOS

Managed Brave Browser policy files for disabling optional Brave features on macOS.

## Features

- Disable Brave AI / Leo
- Disable Rewards, Wallet, VPN, Tor
- Disable Brave telemetry-related features
- Disable Brave News, Talk, Speedreader, Wayback Machine, Playlist
- Disable password manager, autofill, and translation
- Enforce DNS-over-HTTPS with AdGuard DNS
- Leave Brave Sync enabled

## Files

- `com.brave.Browser.plist`: managed preferences policy file
- `brave.mobileconfig`: macOS configuration profile

## Installation

### Recommended: configuration profile

1. Download `brave.mobileconfig`.
2. Open System Settings.
3. Go to Privacy & Security -> Profiles.
4. Install the profile.
5. Restart Brave.
6. Visit `brave://policy` to confirm the policies are active.

### Manual plist method

1. Create `/Library/Managed Preferences/com.brave.Browser.plist`.
2. Paste the policy plist XML.
3. Restart Brave.
4. Confirm in `brave://policy`.

## Removal

- Remove the installed profile from System Settings, or
- Delete the managed preferences plist, then restart Brave.

## Notes

These policies are managed browser settings. They do not modify the Brave app binary.
