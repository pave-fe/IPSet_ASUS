# Skynet - Asus Firewall Addition
Lightweight firewall addition for ARM/HND based ASUS Routers using IPSet as seen on [SmallNetBuilder](https://www.snbforums.com/threads/skynet-asus-firewall-addition-dynamic-malware-country-manual-ip-blocking.16798/)

Skynet is the first comprehensive IP banning and security tool exclusively for Asus Devices.

The goal of this tool is to enhance the firmware's built in functionality such as the SPI Firewall, Brute Force Detection and AiProtect while adding easy to use tools for users to implement custom firewall rules they desire. Skynet has a range of feature from banning single IPs, domains, entire countries or pulling predefined malware lists from reputable providers. It is the one stop shop for router security and the first line of defense in your home network.


## Donate

Want to help support Skynet future development? All donations are appreciated.

[Donate With PayPal](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=BPN4LTRZKDTML)


## Usage

Skynet provides both a user interactive menu, and command line interface for those who prefer it.

To open the menu its as simple as;

```sh /jffs/scripts/firewall```

[![Skynet GUI](https://i.imgur.com/KRHYq3e.png "Skynet GUI")](https://i.imgur.com/KRHYq3e.png "Skynet GUI")

To use the CLI, execute the following;

```sh /jffs/scripts/firewall *commandhere*```

    "unban"        # <-- Remove Entry From Blacklist (IP/Range/Domain/Country/Malware/Nomanual/All)
    "ban"          # <-- Adds Entry To Blacklist (IP/Range/Domain/Country)
    "banmalware"   # <-- Bans Various Malicious Domains/IPs
    "whitelist"    # <-- Add Entry To Whitelist (IP/Range/Domain/VPN/Remove/Refresh/List)
    "import"       # <-- Bans All IPs From URL/Local File
    "deport"       # <-- Unbans All IPs From URL/Local File
    "save"         # <-- Save Blacklists To skynet.ipset
    "restart"      # <-- Restart Skynet
    "disable"      # <-- Temporarily Disable Skynet
    "update"       # <-- Update Script To Latest Version (check github for changes)
    "debug"	       # <-- Debug Features
    "stats"        # <-- Show/Search Stats Of Banned IPs (Requires debugging enabled)
    "install"      # <-- Install Script (Or Change Boot Args)
    "uninstall     # <-- Uninstall All Traces Of Script


## Installation

In your favorite SSH Client;

```sh
/usr/sbin/curl --retry 3 "https://raw.githubusercontent.com/Adamm00/IPSet_ASUS/master/firewall.sh" -o "/jffs/scripts/firewall" && chmod +x /jffs/scripts/firewall && sh /jffs/scripts/firewall install
```

## Help

```
Here Are Some Example Unban Commands;
( sh /jffs/scripts/firewall unban ip 8.8.8.8 ) This Unbans The IP Specified
( sh /jffs/scripts/firewall unban range 8.8.8.8/24 ) This Unbans the CIDR Block Specified
( sh /jffs/scripts/firewall unban domain google.com ) This Unbans the URL Specified
( sh /jffs/scripts/firewall unban comment "Apples" ) This Unbans Entries With The Comment Apples
( sh /jffs/scripts/firewall unban country ) This Unbans Entries Added By The "Ban Country" Feature
( sh /jffs/scripts/firewall unban malware ) This Unbans Entries Added By The "Ban Malware" Feature
( sh /jffs/scripts/firewall unban nomanual ) This Unbans Everything But Manual Bans
( sh /jffs/scripts/firewall unban all ) This Unbans All Entries From Both Blacklists

Here Are Some Example Ban Commands;
( sh /jffs/scripts/firewall ban ip 8.8.8.8 "Apples" ) This Bans The IP Specified With The Comment Apples
( sh /jffs/scripts/firewall ban range 8.8.8.8/24 "Apples" ) This Bans the CIDR Block Specified With The Comment Apples
( sh /jffs/scripts/firewall ban domain google.com ) This Bans the URL Specified
( sh /jffs/scripts/firewall ban country "pk cn sa" ) This Bans The Known IPs For The Specified Countries (Accepts Single/Multiple Inputs If Quoted) http://www.ipdeny.com/ipblocks/data/countries/

Here Are Some Example Banmalware Commands;
( sh /jffs/scripts/firewall banmalware ) This Bans IPs From The Predefined Filter List
( sh /jffs/scripts/firewall banmalware google.com/filter.list ) This Uses The Fitler List From The Specified URL
( sh /jffs/scripts/firewall banmalware reset ) This Will Reset Skynet Back To The Default Filter URL
( sh /jffs/scripts/firewall banmalware exclude "list1.ipset|list2.ipset" ) This Will Exclude Lists Matching The Names "list1.ipset list2.ipset" From The Current Filter (Quotes And Pipes Are Nessessary For Seperating Multiple Entries!)
( sh /jffs/scripts/firewall banmalware exclude reset ) This Will Reset The Exclusion List

Here Are Some Example Whitelist Commands;
( sh /jffs/scripts/firewall whitelist ip 8.8.8.8 "Apples" ) This Whitelists The IP Specified With The Comment Apples
( sh /jffs/scripts/firewall whitelist range 8.8.8.8/24 "Apples" ) This Whitelists The Range Specified With The Comment Apples
( sh /jffs/scripts/firewall whitelist domain google.com) This Whitelists the URL Specified
( sh /jffs/scripts/firewall whitelist vpn) Refresh VPN Whitelist
( sh /jffs/scripts/firewall whitelist remove all) This Removes All Non-Default Entries
( sh /jffs/scripts/firewall whitelist remove entry 8.8.8.8) This Removes IP/Range Specified
( sh /jffs/scripts/firewall whitelist remove comment "Apples" ) This Removes Entries With The Comment Apples
( sh /jffs/scripts/firewall whitelist refresh ) Regenerate Shared Whitelist Files
( sh /jffs/scripts/firewall whitelist list ips|domains|imported ) List Whitelist Entries Based On Category (Leave Blank For All)

Here Are Some Example Import Commands;
( sh /jffs/scripts/firewall import blacklist file.txt "Apples" ) This Bans All IPs From URL/Local File With The Comment Apples
( sh /jffs/scripts/firewall import whitelist file.txt "Apples" ) This Whitelists All IPs From URL/Local File With The Comment Apples

Here Are Some Example Deport Commands;
( sh /jffs/scripts/firewall deport blacklist file.txt ) This Unbans All IPs From URL/Local File
( sh /jffs/scripts/firewall deport whitelist file.txt ) This Unwhitelists All IPs From URL/Local File

Here Are Some Example Update Commands;
( sh /jffs/scripts/firewall update ) Standard Update Check - If Nothing Detected Exit
( sh /jffs/scripts/firewall update check ) Check For Updates Only - Wont Update If Detected
( sh /jffs/scripts/firewall update -f ) Force Update Even If No Changes Detected

Here Are Some Example Debug Commands;
( sh /jffs/scripts/firewall debug disable ) Disable Raw Debugging
( sh /jffs/scripts/firewall debug watch ) Show Debug Entries As They Appear
( sh /jffs/scripts/firewall debug info ) Print Useful Debug Info
( sh /jffs/scripts/firewall debug clean ) Cleanup Syslog Entries
( sh /jffs/scripts/firewall debug swap install|uninstall ) Install/Uninstall SWAP File
( sh /jffs/scripts/firewall debug backup ) Backup Skynet Files To Skynets Install Directory With The Name "Skynet-Backup.tar.gz"
( sh /jffs/scripts/firewall debug restore ) Restore Backup Files From Skynets Install Directory With The Name "Skynet-Backup.tar.gz"
( sh /jffs/scripts/firewall debug unbanprivate enable|disable ) Enable/Disable Unban_PrivateIP Function
( sh /jffs/scripts/firewall debug loginvalid enable|disable ) Enable/Disable Invalid Packet Logging
( sh /jffs/scripts/firewall debug banaiprotect enable|disable ) Enable/Disable Banning IP's Flagged By AiProtect
( sh /jffs/scripts/firewall debug securemode enable|disable ) Enable/Disable Insecure Settings Being Applied In WebUI

Here Are Some Example Stats Commands;
( sh /jffs/scripts/firewall stats ) Compile Stats With Default Top10 Output
( sh /jffs/scripts/firewall stats 20 ) Compile Stats With Customizable Top20 Output
( sh /jffs/scripts/firewall stats tcp ) Compile Stats Showing Only TCP Entries
( sh /jffs/scripts/firewall stats tcp 20 ) Compile Stats Showing Only TCP Entries With Customizable Top20 Output
( sh /jffs/scripts/firewall stats search port 23 ) Search All Debug Data For Entries On Port 23
( sh /jffs/scripts/firewall stats search port 23 20 ) Search All Debug Data For Entries On Port 23 With Customizable Top20 Output
( sh /jffs/scripts/firewall stats search ip 8.8.8.8 ) Search All Debug Data For Entries On 8.8.8.8
( sh /jffs/scripts/firewall stats search ip 8.8.8.8 20 ) Search All Debug Data For Entries On 8.8.8.8 With Customizable Top20 Output
( sh /jffs/scripts/firewall stats search malware 8.8.8.8 ) Search Malwarelists For Specified IP
( sh /jffs/scripts/firewall stats search manualbans ) Search For All Manual Bans
( sh /jffs/scripts/firewall stats search device 192.168.1.134 ) Search For All Outbound Entries From Local Device 192.168.1.134
( sh /jffs/scripts/firewall stats search device reports ) Search Previous Hourly Report History
( sh /jffs/scripts/firewall stats remove ip 8.8.8.8 ) Remove Log Entries Containing IP 8.8.8.8
( sh /jffs/scripts/firewall stats remove port 23 ) Remove Log Entries Containing Port 23
( sh /jffs/scripts/firewall stats reset ) Reset All Collected Debug Data
```


### About

```Skynet gained self-awareness after it had spread into millions of computer servers all across the world; realizing the extent of its abilities, its creators tried to deactivate it. In the interest of self-preservation, Skynet concluded that all of humanity would attempt to destroy it and impede its capability in safeguarding the world. Its operations are almost exclusively performed by servers, mobile devices, drones, military satellites, war-machines, androids and cyborgs (usually a terminator), and other computer systems. As a programming directive, Skynet's manifestation is that of an overarching, global, artificial intelligence hierarchy (AI takeover), which seeks to exterminate the human race in order to fulfill the mandates of its original coding. (▀̿Ĺ̯▀̿ ̿)```
