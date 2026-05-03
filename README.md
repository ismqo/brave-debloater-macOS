# brave-debloater

Why Debloat Brave

Even though Brave emphasizes privacy, there are valid reasons to reduce its feature set:

    Lower background resource usage
    Improve startup performance
    Reduce interface clutter
    Minimize telemetry
    Achieve a minimal Chromium-like experience

Using macOS Policy Configuration

Brave supports managed policies on macOS through a configuration file.

Policy File Location

/Library/Managed Preferences/com.brave.Browser.plist

Step 1: Create the Policy File

Run the following command:

sudo nano /Library/Managed\ Preferences/com.brave.Browser.plist

Step 2: Add Debloat Configuration

Below is the equivalent macOS plist configuration based on your JSON:

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" 
"http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>

    <key>BraveAIChatEnabled</key>
    <false/>
    <key>BraveRewardsDisabled</key>
    <true/>
    <key>BraveWalletDisabled</key>
    <true/>
    <key>BraveVPNDisabled</key>
    <true/>
    <key>TorDisabled</key>
    <true/>
    <key>BraveP3AEnabled</key>
    <false/>
    <key>BraveStatsPingEnabled</key>
    <false/>
    <key>BraveWebDiscoveryEnabled</key>
    <false/>
    <key>BraveNewsDisabled</key>
    <true/>
    <key>BraveTalkDisabled</key>
    <true/>
    <key>BraveSpeedreaderEnabled</key>
    <false/>
    <key>BraveWaybackMachineEnabled</key>
    <false/>
    <key>BravePlaylistEnabled</key>
    <false/>

    <key>SyncDisabled</key>
    <false/>
    <key>PasswordManagerEnabled</key>
    <false/>
    <key>AutofillAddressEnabled</key>
    <false/>
    <key>AutofillCreditCardEnabled</key>
    <false/>
    <key>TranslateEnabled</key>
    <false/>

    <key>DnsOverHttpsMode</key>
    <string>secure</string>
    <key>DnsOverHttpsTemplates</key>
    <string>https://dns.adguard-dns.com/dns-query</string>

</dict>
</plist>

Step 3: Apply Changes

Restart Brave completely:

killall "Brave Browser"
open -a "Brave Browser"

Step 4: Verify Policies

Open the following URL in Brave:

brave://policy

You should see all configured policies listed and active.
What Each Setting Does

    Rewards, Wallet, VPN, and Tor are disabled to remove additional services not required for standard browsing
    Telemetry features such as P3A and StatsPing are disabled to reduce data collection
    AI chat is disabled to remove built-in assistant functionality
    News, Talk, and Playlist features are disabled to reduce interface clutter
    Autofill and password manager are disabled for users relying on external tools
    DNS over HTTPS is enabled using AdGuard to improve privacy and block trackers at the network level

Things to Keep in Mind

    Some interface elements may still be visible but non-functional
    Policies persist across browser updates
    Managed policies override user-configured settings

Optional Enhancements

You can further optimize your setup with:

Disable background mode:

defaults write com.brave.Browser BackgroundModeEnabled -bool false

Additional options include using a hosts file for blocking or installing a content blocker extension if needed.
