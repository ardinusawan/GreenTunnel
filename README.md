# Green Tunnel

GreenTunnel is an local proxy server that tries to bypass DPI (Deep Packet Inspection) systems found in many ISPs (Internet Service Providers) which block access to certain websites.

### How to use
##### Graphical user interface (GUI)
You can simply choose the suitable installation for your OS in the [releases](http://google.com "releases") section.

##### Command-line interface (CLI)
The easiest way to install GreenTunnel is using [npm](https://www.npmjs.org/ "npm"):
```
$ npm install --global green-tunnel
```
then you can run it useing `gt` or `green-tunnel` commands.

```
GreenTunnel bypass DPI (Deep Packet Inspection) systems found in many ISPs.

  Usage:

    green-tunnel [arguments]
	gt [arguments]

  Flags:
    -h, --help          show usage information
    -v, --version       print the current version
    -S, --save          update package.json dependencies
    -D, --save-dev      update package.json devDependencies
    -O, --save-optional update package.json optionalDependencies
    -r, --registry      use a custom registry
                        (default: http://registry.npmjs.org/)
    -b, --build         execute lifecycle scripts upon completion
                        (e.g. postinstall)

  README:  https://github.com/alexanderGugel/ied
  ISSUES:  https://github.com/alexanderGugel/ied/issues
```

### Tested on
- MacOS Mojava 10.14 with node 8 and npm 6
- Ubuntu 18.04 with node 8 and npm 6
- Windows 10 with node 8 and npm 6


### FAQ
**How does it work?**
###### DNS
When you enter a URL in a Web browser, the first thing the Web browser does is to ask a DNS (Domain Name System) server, at a known numeric address, to look up the domain name referenced in the URL and supply the corresponding IP address.
If the DNS server is configured to block access, it consults a blacklist of banned domain names. When a browser requests the IP address for one of these domain names, the DNS server gives a wrong answer or no answer at all.
GreenTunnel use [DNS over HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "doh (DNS over HTTPS)") and [DNS over TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "DNS over TLS") to get real IP address and bypass DNS Spoofing.


###### HTTP
There are gaps in providers in DPI.  They happen from what the DPI rules write for ordinary user programs, omitting all possible cases that are permissible by standards.  This is done for simplicity and speed.
Some DPIs cannot recognize the http request if it is divided into TCP segments.  For example, a request of the form

```
GET / HTTP/1.0`
Host: www.youtube.com
...
```
we send it in 2 parts: first comes `GET / HTTP/1.0 \n Host: www.you` and second sends as `tube.com \n ...`. in this example ISP can not found blocked word **youtube** in packets and bypass it!


###### HTTTPS
Server Name Indication (SNI) is an extension to TLS (Transport Layer Security) that indicates the actual destination hostname a client is attempting to access over HTTPS. For this Web Filter feature, SNI hostname information is used for blocking access to specific sites over HTTPS. For example, if the administrator chooses to block the hostname **youtube** using this feature, all Website access attempts over HTTPS that contain **youtube** like **www.youtube.com** in the SNI would be blocked. However access to the same hostname over HTTP would not be blocked by this feature. GreenTunnel tries to split first **CLIENT-HELLO** packet to small chunks and ISPs can't parse packet and found SNI field so bypass traffic!

### Development notes
GreenTunnel is an open-source app and I really appreciate other developers adding new features and/or helping fix bugs. If you want to contribute to GreenTunnel, you can fork this repository, make the changes and create a pull request.

However, please make sure you follow a few rules listed below to ensure that your changes get merged into the main repo. The rules listed below are enforced to make sure the changes made are well-documented and can be easily kept track of.

- ⇄ Pull requests and ★ Stars are always welcome.
- For bugs and feature requests, please create an issue.
- Make sure your pull request has a informative title. You should use prefixes like ADD:, FIX:, etc at the start of the title which describe the changes followed by a one-line description of the changes. Example: ADD: Added a new feature to GreenTunnel
- Commits in your fork should be informative, as well. Make sure you don't combine too many changes into a single commit.

### TODO List
- [ ] enable/disable proxy on windows
- [ ] HTTPHandler
- [ ] add CLI arguments
- [ ] catch all exceptions

### License
Licensed under the MIT license. See [LICENSE](https://github.com/SadeghHayeri/GreenTunnel/blob/master/LICENSE "LICENSE").

