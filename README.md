![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of shame (2020-04-08)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
46.165.230.5|tor-exit.dhalgren.org|11
89.234.157.254|marylou.nos-oignons.net|10
185.220.100.253|tor-exit-2.zbau.f3netze.de|10
178.165.72.177|178-165-72-177-kh.maxnet.ua|10
77.247.181.165|politkovskaja.torservers.net|10
195.206.105.217|zrh-exit.privateinternetaccess.com|10
171.25.193.78|tor-exit4-readme.dfri.se|9
185.107.47.171|tor-exit.r2.darknet.dev|9
18.27.197.252|wholesomeserver.media.mit.edu|9
46.165.245.154|-|9
185.220.100.252|tor-exit-1.zbau.f3netze.de|9
185.220.100.255|tor-exit-4.zbau.f3netze.de|9
185.165.168.229|-|9
185.220.101.28|-|9
185.220.101.21|-|9
77.247.181.162|chomsky.torservers.net|9
77.247.181.163|lumumba.torservers.net|9
167.88.7.134|the-windy-onion.tor-exits.alec.ninja|9
171.25.193.25|tor-exit5-readme.dfri.se|9
144.217.255.89|ns542132.ip-144-217-255.net|9
51.75.144.43|ns3129517.ip-51-75-144.eu|9
62.102.148.68|-|9
185.220.101.16|-|9
51.15.111.139|139-111-15-51.rev.cloud.scaleway.com|8
94.102.49.82|no-reverse-dns-configured.com|8
185.220.101.1|-|8
199.87.154.255|tor.les.net|8
69.158.207.141|-|8
162.247.72.199|jaffer.tor-exit.calyxinstitute.org|8
185.220.100.254|tor-exit-3.zbau.f3netze.de|8
185.107.70.202|tor-exit.r3.darknet.dev|8
192.42.116.16|tor-exit.hartvoorinternetvrijheid.nl|8
185.220.102.8|-|8
185.220.101.136|-|8
162.247.74.27|turing.tor-exit.calyxinstitute.org|8
185.213.155.172|-|8
171.25.193.20|tor-exit0-readme.dfri.se|8
176.10.99.200|accessnow.org|8
114.67.74.50|-|8
185.129.62.62|tor01.zencurity.dk|8
94.102.63.27|no-reverse-dns-configured.com|8
185.220.100.242|tor-exit-15.zbau.f3netze.de|8
185.220.100.243|tor-exit-16.zbau.f3netze.de|8
185.220.100.241|tor-exit-14.zbau.f3netze.de|8
185.220.101.32|-|8
51.15.43.205|tor4thepeople3.torexitnode.net|8
213.74.176.36|host-213-74-176-36.superonline.net|8
185.220.100.240|tor-exit-13.zbau.f3netze.de|8
