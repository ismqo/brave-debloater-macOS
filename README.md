# brave-debloater-macOS — Repository Explanation

## Overview

[`ismqo/brave-debloater-macOS`](https://github.com/ismqo/brave-debloater-macOS) is a small macOS-focused repository for applying managed Brave Browser policies. Its goal is to “debloat” Brave by disabling or controlling optional Brave features such as AI chat, Rewards, Wallet, VPN, Tor, telemetry-related features, News, Talk, Speedreader, Playlist, autofill, password manager, translation, and DNS-over-HTTPS settings.

The repository currently contains three files:

| File | Purpose |
|---|---|
| `README.md` | Basic manual installation instructions. |
| `com.brave.Browser.plist` | A Brave managed-policy preference file intended for `/Library/Managed Preferences/`. |
| `brave.mobileconfig` | A macOS configuration profile version of the same idea, intended to make the policy more persistent. |

## What the repo is trying to do

Brave supports enterprise-style managed policies. On macOS, these can be applied either through a managed preferences `.plist` file or through a `.mobileconfig` configuration profile. Once installed, Brave reads the configured policy keys and applies the values as managed browser settings.

This repo uses that mechanism to disable or set Brave features without modifying the Brave app itself.

## Main policies included

The README and policy files reference these settings:

| Policy key | Intended effect |
|---|---|
| `BraveAIChatEnabled` | Disables Brave AI / Leo chat when set to `false`. |
| `BraveRewardsDisabled` | Disables Brave Rewards. |
| `BraveWalletDisabled` | Disables Brave Wallet. |
| `BraveVPNDisabled` | Disables Brave VPN. |
| `TorDisabled` | Disables Tor/private-window-with-Tor functionality. |
| `BraveP3AEnabled` | Disables Brave P3A metrics when set to `false`. |
| `BraveStatsPingEnabled` | Disables stats ping when set to `false`. |
| `BraveWebDiscoveryEnabled` | Disables Brave Web Discovery when set to `false`. |
| `BraveNewsDisabled` | Disables Brave News. |
| `BraveTalkDisabled` | Disables Brave Talk. |
| `BraveSpeedreaderEnabled` | Disables Speedreader when set to `false`. |
| `BraveWaybackMachineEnabled` | Disables Wayback Machine integration when set to `false`. |
| `BravePlaylistEnabled` | Disables Playlist when set to `false`. |
| `SyncDisabled` | In the README example this appears as `false`, meaning Sync is not disabled. |
| `PasswordManagerEnabled` | Disables the browser password manager when set to `false`. |
| `AutofillAddressEnabled` | Disables address autofill when set to `false`. |
| `AutofillCreditCardEnabled` | Disables credit-card autofill when set to `false`. |
| `TranslateEnabled` | Disables translation when set to `false`. |
| `DnsOverHttpsMode` | Sets DNS-over-HTTPS mode. The README uses `secure`. |
| `DnsOverHttpsTemplates` | Sets the DoH provider URL. The README uses AdGuard DNS: `https://dns.adguard-dns.com/dns-query`. |

## How installation works

### Option 1: Managed preferences plist

The README suggests creating this file:

```bash
sudo nano /Library/Managed\ Preferences/com.brave.Browser.plist
```

Then the Brave policy configuration is added to that file. After saving it, Brave is restarted:

```bash
killall "Brave Browser"
open -a "Brave Browser"
```

This approach writes directly to macOS managed preferences for Brave’s bundle identifier, `com.brave.Browser`.

### Option 2: macOS configuration profile

The README says the `.mobileconfig` approach is the most reliable/persistent option. A configuration profile can be installed through:

```text
System Settings -> Privacy & Security -> Profiles
```

The repo’s `brave.mobileconfig` file is meant to package the Brave policy settings into a macOS profile using a `com.apple.ManagedClient.preferences` payload.

## Important caveats

1. **The raw files in the repo appear flattened/minified.**  
   The GitHub-rendered README shows a complete XML-style plist example, but the raw `com.brave.Browser.plist` and `brave.mobileconfig` files currently appear as single-line text with policy names and values rather than fully structured XML plist/profile content. Before relying on them, open and validate the files locally.

2. **A valid `.plist` or `.mobileconfig` must be proper XML plist format.**  
   macOS configuration profiles and plist files need valid Apple plist structure. A plain list of keys is not enough.

3. **Some policies are intentionally restrictive.**  
   This configuration disables password manager, address autofill, credit-card autofill, and translation. That may be desirable for a hardened setup, but it can also remove convenience features.

4. **Sync is not disabled in the README example.**  
   `SyncDisabled` is set to `false`, so Brave Sync remains allowed.

5. **Verify in Brave after installation.**  
   Open Brave and visit:

```text
brave://policy
```

This page shows which managed policies Brave has detected and whether they are valid.

## Suggested improved README structure

A clearer README could be organized like this:

```markdown
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
```

## Recommended next improvements for the repo

- Add a proper XML-formatted `com.brave.Browser.plist` file.
- Add a proper XML-formatted `brave.mobileconfig` file with real payload UUIDs and organization values.
- Add a “Verify installation” section using `brave://policy`.
- Add an “Uninstall / rollback” section.
- Document which settings are privacy-related, UI-cleanup-related, or convenience-disabling.
- Consider leaving password manager/autofill policies optional, since some users may want debloating without disabling credential storage.

## One-sentence summary

This repo is a macOS Brave Browser managed-policy setup that attempts to remove optional Brave features and enforce a cleaner, more privacy-oriented configuration, but the raw policy files should be validated and likely reformatted before use.
