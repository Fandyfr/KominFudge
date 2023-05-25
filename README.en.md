<p align="center"><img src="./assets/kominfudge-500x250.png" align="center"></p>
<p align="center">"Because Kominfo blocks, let's unblock!"</p>

<p align="center">
    <a href="README.md">Indonesia</a> | <b>English</b>
</p>

<p align="center"><sup>DISCLAIMER: Kominfudge is not responsible for any damages caused to your device, do with your own risk.</sup></p>

### Navigation
- [Top Choices](#top-choices)
- [Choosing less-strict ISP](#choosing-less-strict-isp)
  - [Effort level to unblock with DPI](#effort-level-to-unblock-with-dpi)
- [Choosing the right DNS](#choosing-the-right-dns)
  - [DNS Applications](#dns-applications)
  - [How to change DNS](#how-to-change-dns)
- [Applications to eliminate DPI](#applications-to-eliminate-dpi)
  - [Trick to bypass DPI without application](#trick-to-bypass-dpi-without-application)
  - [Trick to bypass DPI using router](#trick-to-bypass-dpi-using-router)
- [List of hosts file](#list-of-hosts-file)
  - [How to unblock using hosts file](#how-to-unblock-using-hosts-file)
- [Choosing secure VPN](#choosing-secure-vpn)
  - [VPN for Advanced Users](#vpn-for-advanced-users)
- [Tor Applications](#tor-applications)

This project would not exist without your [contributions](/kredit.md)  
*Oh, if you want to contribute, take a look [at this first](/CONTRIBUTING.md)*

## Top Choices[🔝](#navigation)

DNS: [1.1.1.1](https://1.1.1.1)  
Most intuitive DNS resolver and easy to use 

DPI: [PowerTunnel](https://github.com/krlvm/PowerTunnel)  
Intuitive and Open Source  

Filehost: [bebasid](https://bebasid.com)  
Host file with a lot of content 

VPN: [ProtonVPN](https://protonvpn.com)  
Free and secure

## Choosing less-STRICT ISP[🔝](#navigation)
ISP is your Internet provider, this list will helps you understand more about how Indonesian ISPs blocking[;](/sssssssssssssssssssssssssssssssssss.md)

### IP Transit 
<sup><b>To determine what Transit IP that our ISP is using, you can check on https://bgp.tools atau https://bgp.he.net</b></sup><br>

ISP that using these upstreams will not be able to change DNS in usual way due to port 53 redirection to each Transit IP provider DNS resolvers following the <a href="https://youtu.be/q1706yrzzws?t=18927">National DNS that unveiled during IDNOG 2022.</a><br>
| ASN | Name | Blocking using DNS | Note | Example of affected ISP |
| :---: | :---: | :---: | :---: | :---: |
| [AS4800](https://bgp.tools/as/4800) | PT Aplikanusa Lintasarta | [Transparent DNS (Port 53 redirected to server](assets/proofs/png/AS4800-1.png?raw=1) | [Lintasarta redirecting port 53 to their own server so other DNS server and individual ISP will not work if the ISP routing their server towards Lintasarta even if the DNS server is located in Indonesia](assets/proofs/png/AS4800-2.png?raw=1) | Netciti, CYB Media |

<sup style="text-align:center;">If your ISP does not comply with National DNS regulation but uses Transit IP as shown above, you will experience the same blocking and must use encrypted DNS.<br>Or you can use DNS that is not routed towards those Transit IPs if available</sup><br>

<b>If you are using ISP with these upstream, you must use VPN/GoodbyeDPI/Powertunnel</b>
| ASN | Name | Blocking using DPI | Note | Example of affected ISP |
| :---: | :---: | :---: | :---: | :---: |
| [AS4800](https://bgp.tools/as/4800) | PT Aplikanusa Lintasarta | Yes | | Netciti, Varion |
| [AS137366](https://bgp.tools/as/137366) | PT iForte Solusi Infotek | [Yes](assets/image.png?raw=1) | Does not blocking Vimeo. | MNC, Transvision, MTM Bali |
| [AS4761](https://bgp.tools/as/4761) | INDOSAT Internet Network Provider | [Yes](assets/proofs/png/AS23951-AS4761.png?raw=1) |  | Citranet, Nusanet |
| [AS58495](https://bgp.tools/as/58495) / [AS138840](https://bgp.tools/as/138840) | PT Parsaoran Global Datatrans (HSP-NET) | [Yes](assets/proofs/png/AS58495-HSP-IX.png?raw=1) | | Megavision, MNC Play |
| [AS17451](https://bgp.tools/as/17451) | BIZNET NETWORKS | Yes | | |
| [AS4787](https://bgp.tools/as/4787) | PT Cyberindo Aditama (CBN) | Yes | | |
| [AS138128](https://bgp.tools/as/138128) | PT Solnet Indonesia | [Yes](assets/proofs/png/AS138128-DPI-Proof.png?raw=1) | [Traceroute proof](assets/proofs/png/AS138128-DPI-Traceroute.png?raw=1) | | ProNET |
| [AS131219](https://bgp.tools/as/131219) | Indosat Singapore Pte Ltd | Yes | | |
| [AS9341](https://bgp.tools/as/9341) / [AS38757](https://bgp.tools/as/38757)  | PT. Indonesia Comnet Plus (ICONNET) | Yes | | |
| [AS55655](https://bgp.tools/as/55655) | PT Saranainsan Mudaselaras | Yes |  | MNC Play |
| [AS18351](https://bgp.tools/as/18351) | PT Media Akses Global Indo | Yes |  | |
| [AS18351](https://bgp.tools/as/18351) | DTPNET NAP | [Yes](https://media.discordapp.net/attachments/1109515185108046015/1109935886889656450/image.png?width=648&height=559) |  |  |
| [AS136106](https://bgp.tools/as/136106) | PT Mega Akses Persada (Fiberstar) | Yes |  | MyRepublic, Mayatama |

<sup style="text-align:center;">If your ISP does not use DPI but using those upstreams, you can use an anti DPI tool to bypass</sup><br>

<b>Internet Exchange using DPI middlebox</b>
| Name | Using DPI | Example of affected CDN | Note |
| :---: | :---: | :---: | :---: |
| BIX - Biznet Internet Exchange | Yes | [Cloudflare, and all CDNs that peered with BIX](assets/proofs/png/BIX.png?raw=1) | Even with GoodbyeDPI, Powertunnel, etc will not work because it is already blocked by Biznet from the Server side 

### Fiber ISP 
**Residential ISP**
| Name | Blocking using DNS | Blocking using DPI | Sending TCP RST to server | Note |
| :---: | :---: | :---: | :---: | :---: |
| Indihome | Yes (Out, Local) | Yes | Yes | Telkom's residential offering . Indihome DPI also sending TCP RST to server |
| CBN | Yes | Yes | No |
| Biznet Home | Yes (Out, Local) | Yes | Yes | Biznet DPI also sending TCP RST to server |
| MyRepublic | Yes (Out, Local) | Yes | No | MyRepublic DPI only blocking 18+ sites  |
| FirstMedia | Yes (Out, Local) | Yes | No |
| Megavision | Yes (Out, Local) | Yes/No (Depends on routing) | ? | Other name: StarNET. Affected with DPI from PT Parsaoran Global Datatrans upstream  |
| MNC | Yes | Yes/No (Depends on routing) | ? | Affected with DPI from iForte upstream  |
| Iconnet PLN | Yes | Yes | Yes | Iconnet DPI also sending TCP RST to server. Two-way DPI blocking |
| PT Netciti Persada | Yes | Yes/No (Depends on routing) | ? | Affected with National DNS and DPI from Lintasarta upstream |
| Oxygen | Yes (Out) | Yes | No | Other name: Moratelindo <br /> Blocking Google DoH andn DoT <br>Blocking alt-port DNS 5353 |
| Citranet | Yes | Yes/No (Depends on routing) | ? | DPI from Citranet upstream. If routed towards Indosat and some of their upstreams, it will be affected |
| Padi Net | Yes (Out, Local) | No | ? |
| Fiberstream | Yes (Out, Local) | No | ? | Residential ISP of G-MEDIA |
| Balifiber | Yes | No | ? |
| PT Media Cepat Indonesia | Yes (Out, Local) | No | ? |
| Melsa | Yes (Out, Local) | No | ? | Google DNS should be safe |

**Corporate ISP**
| Name | Blocking using DNS | Blocking using DPI | Sending TCP RST to server | Note |
| :---: | :---: | :---: | :---: | :---: |
| Astinet | Yes (DNS Injection) | Yes | ? | Telkom's corporate offering |
| Linknet | Yes | No | No | FirstMedia's corporate offering |
| Lintasarta | Yes (Out, Local) | Yes | Yes | Lintasarta DPI also sending TCP RST to server. Two-way DPI blocking |
| Metronet | Yes (Out) | Yes | Yes | aka Biznet Dedicated |
| PT Metrasat | Yes | Yes | ? |
| PT Pasifik Satelit Nusantara | Yes | No | ? |
| PT Artha Telekomindo | Yes | No | ? |
| PT Hawk Teknologi Solusi | Yes | No | ? |
| PT Jaringanku Sarana Nusantara | Yes (Out, Local) | No | ? | Other name: JSN |
| PT. Infotama Lintas Global | Yes (Out, Local) | No | ? |
| PT Remala Abadi | Yes | No | No | Other name: Tachyon |
| PT iForte Global internet | Yes | Yes | No | DPI does not blocking Vimeo |
| PT Cipta Informatika Cemeriang | Yes | No | ? |
| PT Lexa Net | Yes | No | ? | Other name: PT Lexa Global Akses |
| PT Media Sarana Data  | Yes (Out, Local) | No | ? | Other name: G-MEDIA |
| PT Artorius Telemetri Sentosa | Yes | No | ? |
| D-NET | Yes | No | ? | Other name: PT Core Mediatech <br />Only redirecting Google, Cloudflare, and Quad9 DNS |
| PT Sumber Koneksi Indotelematika | Yes | No | ? |
| ProNET | Yes | Yes/No (Depends on routing) | Yes | Other name: PT Trisari Data Indonesia<br />Several Public DNS resolvers like Cloudflare, Alibaba DNS, and several Indonesian DNS resolvers are blocked. Affected with TCP RST from Solnet upstream  |
| PT Media Jaringan Telekomunikasi | Yes | No | ? |
| PT Sekawan Global Komunika | Yes | No | ? |
| PT INFORMASI NUSANTARA TEKNOLOGI | Yes | No | ? |
| Orion Cyber Internet | Yes | No | ? | Popular DNS resolvers like Cloudflare, Google, Quad9, Level3, etc are redirected to ISP server |
| PT AGTI | Yes (Out, Local) | No | ? | Other name: PT. Arjuna Global Teknologi Indonesia |
| PT Parsaoran Global Datatrans | Yes | Yes | Yes (But weak) | Other name: HSP NET. Two-way DPI blocking |
| PT Fiber Networks Indonesia | Yes (Out, Local) | No | ? | Other name: FIBERNET |
| PT Power Telecom Indonesia | Yes | Yes | ? | DPI does not blocking Vimeo |
| PT Solnet Indonesia | Yes | Yes | Yes | Solnet DPI also sending TCP RST to server |

### Mobile ISP
| Name | Blocking using DNS | Blocking using DPI | Sending TCP RST to server |  Note |
| :---: | :---: | :---: | :---: | :---: |
| Telkomsel / By.U / KartuHalo | Yes (Out, Local) | Yes | Yes | Telkomsel DPI also sending TCP RST to server |
| XL / Axis / Live On | Yes (Out, Local) | Yes | Yes | XL DPI also sending TCP RST to server | 
| 3 | Yes | Yes | Yes | Tri DPI also sending TCP RST to server |
| Indosat | Yes | Yes | No |
| Smartfren | Yes (Out, Local) | Yes | No | Blocking Google DoH/DoT |

### Effort level to unblock with DPI
How much effort needed to unblock with DPI per-ISP

**THIS DATA IS NOT COMPLETE**
| Name | Effort
| :---: | :---: |
| Telkomsel / By.U / KartuHalo | High |
| XL / Axis / Live On | High |
| Biznet | High |
| Lintasarta | High |
| PT Parsaoran Global Datatrans | High |
| Iconnet | High |
| Indihome | Medium |
| Indosat | Medium |
| Moratel / Oxygen | Medium|
| 3 | Medium |
| CBN | Medium |
| Smartfren | Low |
| PT Solnet Indonesia | Low |
| FirstMedia | Low |
| MyRepublic | Low |
| PT Power Telecom Indonesia | Low |

<sup>Take this with a grain of salt, all ISPs will change their blocking method without notice</sup>


## Choosing the right DNS[🔝](#navigation)
DNS, a simple way for kominfo to block, but DNS can be [changed!](#how-to-change-dns)  
This is a list of DNS resolvers that can be used instead of blocking resolvers of Kominfo

| Name | Note | IPv4 | IPv4 2 | Alternative Port | IPv6 | IPv6 2 | DoH | DoT |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |  :---: |  :---: |
| Cloudflare DNS | - | `1.1.1.1` | `1.0.0.1` | - | `2606:4700:4700::1111` | `2606:4700:4700::1001` | `cloudflare-dns.com/dns-query`  | `1dot1dot1dot1.cloudflare-dns.com` |
| Cloudflare Secure DNS | Blocking malware | `1.1.1.2` | `1.0.0.2` | - | `2606:4700:4700::1112` | `2606:4700:4700::1002` | `security.cloudflare-dns.com/dns-query`  | `security.cloudflare-dns.com` |
| Cloudflare Family DNS | Blocking malware & adult sites | `1.1.1.3` | `1.0.0.3` | - | `2606:4700:4700::1113` | `2606:4700:4700::1003` | `family.cloudflare-dns.com/dns-query`  | `family.cloudflare-dns.com` |
| Google DNS | - | `8.8.8.8` | `8.8.4.4` | - | `2001:4860:4860::8888` | `2001:4860:4860::8844` | `dns.google/dns-query` | `dns.google` |
| OpenDNS | - | `208.67.222.222` | `208.67.220.220` | `5353, 443` | ` 2620:119:35::35` | `2620:119:53::53` | `doh.opendns.com/dns-query` | - |
| OpenDNS Familyshield | Blocking adult sites | `208.67.222.123` | `208.67.220.123` | `5353, 443` | - | - | `doh.familyshield.opendns.com/dns-query` | - |
| Quad9 Secured | Blocking malware | `9.9.9.9` | `149.112.112.112` | `9953` | `2620:fe::fe` | `2620:fe::9` | `dns.quad9.net/dns-query` | `tls://dns.quad9.net` | 
| Quad9 Secured with ECS | Blocking malware, supporting ECS | `9.9.9.11` | `149.112.112.11` | `9953` | `2620:fe::11` | `2620:fe::fe::11` | `dns11.quad9.net/dns-query` | `tls://dns11.quad9.net` |
| Quad9 Unsecured | Alternative DNS resolvers from Quad9 that does not block malware | `9.9.9.10` | `149.112.112.10` | `9953` | `2620:fe::10` | `2620:fe::fe:10` | `dns10.quad9.net/dns-query` | `tls://dns10.quad9.net` |
| Quad9 Unsecured ECS | Alternative DNS resolvers from Quad9 that does not block malware, supporting ECS | `9.9.9.12` | `149.112.112.12` | `9953` | `2620:fe::12` | `2620:fe::fe:12` | `dns12.quad9.net/dns-query` | `tls://dns12.quad9.net` |
| BebasDNS | Bebasid's own DNS resolver, blocking ad and malware | `47.254.192.66` | - | `1753` | `2001:470:36:b90:beba:5::1d` | - | `dns.bebasid.com/dns-query` | `dns.bebasid.com` |
| [AhaDNS](https://blitz-setup.ahadns.com) | - | ? | ? | ? | ? | ? | `blitz.ahadns.com` | ? |
| BlahDNS | - | `45.91.92.121`  | X | - | `2a0e:dc0:6:23::2` | X | `doh-ch.blahdns.com/dns-query` | `dot-ch.blahdns.com` |
| [RethinkDNS](https://rethinkdns.com/configure) | - | ? | ? | - | ? | ? | `basic.rethinkdns.com` | `max.rethinkdns.com` |
| NextDNS | - | `45.90.28.233` | `45.90.30.233` | `5353` | `2a07:a8c0::` | `2a07:a8c0::` | `dns.nextdns.io` | `dns.nextdns.io` |
| LibreDNS | - | `116.202.176.26` | X | - | X | X | `doh.libredns.gr/dns-query` | `dot.libredns.gr` |
| [ControlD](https://controld.com/free-dns) | - | `76.76.2.2` | `76.76.10.2` | - | `2606:1a40::2` | `2606:1a40:1::2` | `freedns.controld.com/p1` | `p1.freedns.controld.com`|
| AdGuard DNS | Blocking ad and malware | `94.140.14.14` | `94.140.15.15` | `5353` | `2a10:50c0::ad1:ff` | `2a10:50c0::ad2:ff` | `https://dns.adguard-dns.com/dns-query` | `dns.adguard-dns.com` |
| [DNSWarden](https://dnswarden.com/customfilter.html) | - | ? | ? | ? | ? | ? | ? | ? |

<sup>More comprehensive list can be seen at [Adguard KB](https://adguard-dns.io/kb/general/dns-providers/) and [Curl wiki](https://github.com/curl/curl/wiki/DNS-over-HTTPS). You can create your own DNS over HTTPS with [Cloudflare Workers](https://github.com/tina-hello/doh-cf-workers) or [with PHP](https://github.com/NotMikeDEV/DoH)</sup>

## DNS Applications[🔝](#navigation)
These DNS applications can help you in configuring DNS resolvers on your system

> ⚠ **ATTENTION** ⚠  
> If your ISP is also blocking using DPI also use [applications to eliminate DPI](#applications-to-eliminate-dpi)

1.[Nebulo](https://nebulo.app) [Android]  
Application to easily change DNS on Android

2.[DNSCloak](https://apps.apple.com/app/id1452162351) [iOS]  
Application to change DNS and configure dnscrypt on iOS

3.[DNSCrypt](https://dnscrypt.info) [Windows,macOS,Linux]  
Selfhost DNS that can do forwarding to DNSCrypt & DNS over HTTPS servers

4.[SimpleDNSCrypt](https://simplednscrypt.org) [Windows]  
An easy to use graphical DNSCrypt client

5.[DNS Profile Creator](https://dns.notjakob.com/tool.html) [Browser]  
Easily create mobileconfig Apple

6.[YogaDNS](https://yogadns.com) [Windows]  
DNS changer for Windows

7.[RethinkDNS](https://rethinkdns.com) [Android]  
Application to change DNS and ad blocker

8.[Intra](https://getintra.org) [Android]  
Application to change DNS on Android

9.[AdGuard Home](https://github.com/AdguardTeam/AdGuardHome) [Windows, macOS, Linux]  
Selfhost DNS with integrated adblock, encrypted upstream and downstream

10.[Stubby](https://github.com/getdnsapi/stubby) [Windows, macOS, Linux]  
Selfhost DNS that can do forwarding to DNS over TLS server

11.[InviZible](https://github.com/Gedsh/InviZible) [Android]  
An Android application for DNS and Tor

## How to change DNS[🔝](#navigation)
Now, you have got the List, so how to use it?

### On Android
1.Settings>Other Wireless Connections>Private DNS  
2.Type the [DNS hostname](#choosing-the-right-dns) and tap Save

### On iOS

1.Settings>Wi-Fi>*wifi*  
2.Tap (i) icon  
3.Ganti IP Adress jadi Static Change the IP Address into Static and type the [DNS hostname](#choosing-the-right-dns) on the DNS column

### On Windows
#### Windows 10 and earlier 
1. Control Panel>Network and Internet>Network and Sharing Center>Connections>Properties  
2. Click Internet Protocol Version 4 (TCP/IPv4) twice  
3. Change from "Obtain DNS server address automatically" to "Use the following DNS server addresses"  
4. Type the [DNS hostname](#choosing-the-right-dns) on the DNS column and click OK

#### Windows 11
1. Open Settings on Windows 11, Go to Network & Internet and click Properties    
2. On the DNS server assignment section, click Edit button  
3. Change from Automatic to Manual  
4. On Preferred DNS, type 1.1.1.1/8.8.8.8/9.9.9.9 and on Alternate type 1.0.0.1/8.8.4.4/149.112.112.112
5. On Preferred and Alternate DNS Encryption, choose Encrypted only (DNS-over-HTTPS) option 
6. Click Save

### On macOS
1. System Preferences>Network>Wi-Fi>Advanced>DNS  
2. Click “+” button and type the [DNS hostname](#choosing-the-right-dns) on the DNS column, click OK and Apply

### On Linux
1. Open Terminal  
2. Type the command `nano /etc/resolv.conf` to edit `/etc/resolv.conf`  
3. Ubah isi file menjadi seperti berikut Change the file content into something like this (replace `<dns hostname>` into one of the DNS hostname [listed here](#choosing-the-right-dns))
```
nameserver <dns hostname>
nameserver <dns hostname>
```
Note: Some components that installed on Linux distribution (like NetworkManager) may change the content of `/etc/resolv.conf` without notice, to prevent this you can type `chattr +i /etc/resolv.conf` after editing the file. If you want to change the content of `/etc/resolv.conf` again, you can type `chattr -i /etc/resolv.conf`

### On Chromium-based browser
1.Settings>Privacy and Security  
2.Type the [DNS hostname](#choosing-the-right-dns) on the DNS column

### On Firefox
1.Settings>Network Settings  
2.Type the [DNS hostname](#choosing-the-right-dns) on the DNS column

#### *How to determine if the DNS is properly configured*  
Go to [DNSLeakTest](https://dnsleaktest.com) or [BrowserLeaks](https://browserleaks.com/dns) for testing
If the ISP DNS being shown instead of one you have already set, you can download [DNSCrypt](https://dnscrypt.info) or [SimpleDNSCrypt](https://simplednscrypt.org)

## Applications to eliminate DPI[🔝](#navigation)
Now, many [ISPs](#choosing-less-strict-isp) are using Deep Packet Inspection as blocking method, but you can eliminate the DPI with these applications

> ⚠ **ATTENTION** ⚠  
> Do not forget to change [DNS](#dns-applications) first or using [Hosts file](#list-of-hosts-file) if your [ISP](#choosing-less-strict-isp) is also using DNS for blocking

> ℹ️ **Info**  
> We also providing config for application and ISP in [this folder](/dpi-circumvention-config)


1.[GoodbyeDPI](https://github.com/ValdikSS/GoodbyeDPI) [Windows]  
CLI application to eliminate DPI

2.[GreenTunnel](https://github.com/SadeghHayeri/GreenTunnel) [Windows,macOS,Linux]  
GUI application to eliminate DPI

3.[PowerTunnel](https://github.com/krlvm/PowerTunnel) [Windows,macOS,Linux,[Android](https://github.com/krlvm/PowerTunnel-Android)]  
GUI application to eliminate DPI (2)

4.[SNI-Mask](https://github.com/macronut/SNI-Mask) [Windows]  
Proxy to eliminate DPI

5.[Accesser](https://github.com/URenko/Accesser) [Windows,macOS,Linux]  
*???*

6.[GhosTCP](https://github.com/macronut/ghostcp) [Windows]  
Securing TCP connection

7.[sniffjoke](https://github.com/vecna/sniffjoke) [Linux]  
Securing wiretap/sniff/IDS

8.[SpoofDPI](https://github.com/xvzc/SpoofDPI) [macOS,Linux]  
Spoofing your DPI

9.[Zapret](https://github.com/bol-van/zapret/blob/master/docs/readme.eng.md) [Linux, FreeBSD]  
DPI Circumvention Tool

10.[DPITunnel](https://github.com/zhenyolka/DPITunnel-cli) [Linux,[Android](https://github.com/zhenyolka/DPITunnel-android)]  
CLI application for Linux

11.[Geneva](https://github.com/kkevsterrr/geneva) [Linux]  
AI-powered DPI Circumvention Tool 

### Trick to bypass DPI without application[🔝](#navigation)

#### On Linux
*Drop TCP RST and lamanlabuh*
Run command `sudo iptables -I INPUT -p tcp --tcp-flags ALL RST,ACK -j DROP` and `sudo iptables -A INPUT -p tcp -m string --string "Location: http://lamanlabuh.aduankonten.id/" --algo bm -j DROP` or `sudo firewall-cmd --direct --add-rule ipv4 filter INPUT 0 -p tcp --tcp-flags ALL RST,ACK -j DROP` (for Linux distribution that using firewalld, like Fedora and OpenSUSE) in terminal\
Tetapi perintah diatas tidak akan bekerja apabila But those commands will not work if ISP is also sending TCP RST to server (List of ISP can be seen in Sending TCP RST to server column on above table)

### Trick to bypass DPI using router[🔝](#navigation)

#### OpenWRT
Follow this tutorial https://github.com/bebasid/bebasit/blob/master/docs/openwrt-tutorial.en.md

### MikroTik
Follow this tutorial https://github.com/bebasid/bebasit/blob/master/docs/mikrotik-tutorial.en.md

## List of hosts file[🔝](#navigation)
If you have a big brain and prefer to use hosts file, here the list

| List | Alternative |
| :---: | :---: |
| [bebasid](https://raw.githubusercontent.com/bebasid/bebasid/master/releases/hosts) |
| [mul14](https://gist.githubusercontent.com/mul14/eb05e88fcec5bb195cbb/raw/611c0693c460fc5bd7037c6d9d43fa6c0ce4fd7c/hosts) |
| [tumblr](https://gist.github.com/mul14/eb05e88fcec5bb195cbb?permalink_comment_id=2556197#gistcomment-2556197) |
| [Netflix](https://gist.github.com/mul14/eb05e88fcec5bb195cbb?permalink_comment_id=3235083#gistcomment-3235083) | [2](https://gist.github.com/mul14/eb05e88fcec5bb195cbb?permalink_comment_id=3324456#gistcomment-3324456) |
| [nhentai](https://gist.github.com/mul14/eb05e88fcec5bb195cbb?permalink_comment_id=3324461#gistcomment-3324461) |
| [Binance](https://gist.github.com/mul14/eb05e88fcec5bb195cbb?permalink_comment_id=3727848#gistcomment-3727848) |
| [Reddit](https://gist.github.com/mul14/eb05e88fcec5bb195cbb?permalink_comment_id=3878656#gistcomment-3878656) |
| [Steam](https://gist.github.com/mul14/eb05e88fcec5bb195cbb?permalink_comment_id=4250815#gistcomment-4250815) | [2](https://pastebin.com/auhuXvAD) |

## How to unblock using hosts file[🔝](#navigation)
So, you have the file... now what?

### On Windows
1.Copy the text inside the hosts file that you have chosen before
2.Open File Explorer and go to `C:\Windows\System32\drivers\etc`  
3.Paste text to "hosts" file

### On Android

#### ROOT:
1.Copy the text inside the hosts file that you have chosen before  
2.Open File Explorer and go to `/system/etc`  
3.Paste text to "hosts" file

#### NON-ROOT:
1.Copy the text inside the hosts file that you have chosen before 
2.Create the file and paste the text inside that file
3.Install [Virtual Hosts](https://github.com/x-falcon/Virtual-Hosts) or [Host Go](https://play.google.com/store/apps/details?id=dns.hosts.server.change)  
4.Tap "Select Host File"/"Import HOSTS file" and choose the file that you have created before

## Choosing secure VPN[🔝](#navigation)
Ah VPN, the easiest way to bypass the block if any of above methods do not work, *But* do not download insecure and untrustworthy VPN!
Take a look at this list of secure VPN that you can use instead of untrustworthy VPN

| Name | Positive | Negative | Server |
| :---: | :---: | :---: | :---: |
| [Mullvad](https://mullvad.net/) | A secure paid VPN | Paid | 867 |
| [ProtonVPN](https://protonvpn.com) | A "secure" "free" VPN | Lack of Split-tunneling on free plan and [this](https://arstechnica.com/information-technology/2021/09/privacy-focused-protonmail-provided-a-users-ip-address-to-authorities) | 100 |
| [Windscribe](https://windscribe.com) | Split-tunneling and many features | 15GB per month and [this](https://arstechnica.com/gadgets/2021/07/vpn-servers-seized-by-ukrainian-authorities-werent-encrypted) | 15 |
| [ExpressVPN](https://expressvpn.com) | Fast | Not that secure and paid | 148 |
| [Psiphon](https://psiphon.ca) | Open Source | ? | ? |
| [OVPN](https://ovpn.com) | **Secure** | Paid | 102 |

### VPN for Advanced Users[🔝](#navigation)
VPN in this section needs configuration, if you just want a Out of the box VPN, please ignore this

| Name | Description |
| :---: | :---: |
| [OpenVPN](https://openvpn.net) | VPN system that implements techniques to create secure point-to-point or site-to-site connections |
| [Wireguard](https://wireguard.com) | Similar to OpenVPN |
| [Softether](https://softether.org) | Similar to OpenVPN(?) |

## Tor Applications[🔝](#navigation)
And, this is the most extreme part, using Tor

1.[Tor Browser](https://www.torproject.org) [Windows,macOS,Linux,Android]  
Official browser of Tor Project

2.[Orbot](https://guardianproject.info/apps/org.torproject.android) [Android]  
Proxy with Tor  

3.[Onion Browser](https://onionbrowser.com) [iOS]  
Tor browser for iOS

4.[InviZible](https://github.com/Gedsh/InviZible) [Android]  
Android application for DNS and Tor

<p align="center">Share this project</p>
<div id="sosial">
 <p align="center">
  <a href="https://twitter.com/intent/tweet?text=https%3A//github.com/bebasid/KominFudge%20%23BlokirKominfo%20%23BlokirGakPakeMikir"><img src="https://img.shields.io/badge/Twitter-blue?style=flat&logo=twitter&logoColor=white"/></a>
  <a href="https://www.facebook.com/sharer/sharer.php?u=https%3A//github.com/bebasid/KominFudge"><img src="https://img.shields.io/badge/Facebook-1877F2?style=flat&logo=facebook&logoColor=white"/></a>
  </p>
  <p align="center"><a href="https://github.com/bebasid/KominFudge#readme">KominFudge</a> is licensed under <a href="https://github.com/bebasid/KominFudge/blob/main/LICENSE">CC-BY-SA-4.0</a>.</p>
</div>