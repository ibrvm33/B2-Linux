# TP3 Sécu : Linux Hardening
## Setup
## Guides CIS

**🌞 Suivre un guide CIS**

    ✅

## Conf SSH

**🌞 Chiffrement fort côté serveur**

## 4. DoT

**🌞 Configurer la machine pour qu'elle fasse du DoT**

    l3z@l3z:~$ cat /etc/systemd/resolved.conf 
    #  This file is part of systemd.
    #
    #  systemd is free software; you can redistribute it and/or modify it under the
    #  terms of the GNU Lesser General Public License as published by the Free
    #  Software Foundation; either version 2.1 of the License, or (at your option)
    #  any later version.
    #
    # Entries in this file show the compile time defaults. Local configuration
    # should be created by either modifying this file (or a copy of it placed in
    # /etc/ if the original file is shipped in /usr/), or by creating "drop-ins" in
    # the /etc/systemd/resolved.conf.d/ directory. The latter is generally
    # recommended. Defaults can be restored by simply deleting the main
    # configuration file and all drop-ins located in /etc/.
    #
    # Use 'systemd-analyze cat-config systemd/resolved.conf' to display the full config.
    #
    # See resolved.conf(5) for details.

    [Resolve]
    # Some examples of DNS servers which may be used for DNS= and FallbackDNS=:
    # Cloudflare: 1.1.1.1#cloudflare-dns.com 1.0.0.1#cloudflare-dns.com 2606:4700:4700::1111#cloudflare-dns.com 2606:4700:4700::1001#cloudflare-dns.com
    # Google:     8.8.8.8#dns.google 8.8.4.4#dns.google 2001:4860:4860::8888#dns.google 2001:4860:4860::8844#dns.google
    # Quad9:      9.9.9.9#dns.quad9.net 149.112.112.112#dns.quad9.net 2620:fe::fe#dns.quad9.net 2620:fe::9#dns.quad9.net
    #DNS=
    #FallbackDNS=
    #Domains=
    #DNSSEC=no
    #DNSOverTLS=no
    #MulticastDNS=no
    #LLMNR=no
    #Cache=no-negative
    #CacheFromLocalhost=no
    #DNSStubListener=yes
    #DNSStubListenerExtra=
    #ReadEtcHosts=yes
    #ResolveUnicastSingleLabel=no
    #StaleRetentionSec=0

**🌞 Prouvez que les requêtes DNS effectuées par la machine...**

        l3z@l3z:~$ dig ynov.com

        ; <<>> DiG 9.18.30-0ubuntu0.24.04.2-Ubuntu <<>> ynov.com
        ;; global options: +cmd
        ;; Got answer:
        ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 9673
        ;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

        ;; OPT PSEUDOSECTION:
        ; EDNS: version: 0, flags:; udp: 65494
        ;; QUESTION SECTION:
        ;ynov.com.			IN	A

        ;; ANSWER SECTION:
        ynov.com.		300	IN	A	104.26.10.233
        ynov.com.		300	IN	A	104.26.11.233
        ynov.com.		300	IN	A	172.67.74.226

        ;; Query time: 52 msec
        ;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
        ;; WHEN: Fri Mar 07 10:10:06 CET 2025
        ;; MSG SIZE  rcvd: 85

