# TP1 : Premiers pas Docker

## I. Init

### 1. Installation de Docker

### 2. Vérifier que Docker est bien là

### 3. sudo c pa bo

**🌞 Ajouter votre utilisateur au groupe docker**

    [l3z@localhost ~]$ sudo usermod -aG docker l3z

### 4. Un premier conteneur en vif

**🌞 Lancer un conteneur NGINX**

    [l3z@localhost ~]$ docker run -d -p 9999:80 nginx
    Unable to find image 'nginx:latest' locally
    latest: Pulling from library/nginx
    7cf63256a31a: Pull complete 
    bf9acace214a: Pull complete 
    513c3649bb14: Pull complete 
    d014f92d532d: Pull complete 
    9dd21ad5a4a6: Pull complete 
    943ea0f0c2e4: Pull complete 
    103f50cb3e9f: Pull complete 
    Digest: sha256:9d6b58feebd2dbd3c56ab5853333d627cc6e281011cfd6050fa4bcf2072c9496
    Status: Downloaded newer image for nginx:latest
    c4538debb036705aadf8641e4180f1356ec16c47edf04bd080e857d7a8e0831c
    
**🌞 Visitons**

**vérifier que le conteneur est actif avec une commande qui liste les conteneurs en cours de fonctionnement**
    CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                     NAMES
    c4538debb036   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:9999->80/tcp, [::]:9999->80/tcp   stoic_hamilton
**afficher les logs du conteneur**
    [l3z@localhost ~]$ docker logs c4538debb036
    /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
    /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
    10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
    10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
    /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
    /docker-entrypoint.sh: Configuration complete; ready for start up
    2025/03/04 09:45:03 [notice] 1#1: using the "epoll" event method
    2025/03/04 09:45:03 [notice] 1#1: nginx/1.27.4
    2025/03/04 09:45:03 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14) 
    2025/03/04 09:45:03 [notice] 1#1: OS: Linux 5.14.0-503.14.1.el9_5.x86_64
    2025/03/04 09:45:03 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1073741816:1073741816
    2025/03/04 09:45:03 [notice] 1#1: start worker processes
    2025/03/04 09:45:03 [notice] 1#1: start worker process 30
    2025/03/04 09:45:03 [notice] 1#1: start worker process 31
    2025/03/04 09:45:03 [notice] 1#1: start worker process 32

**afficher toutes les informations relatives au conteneur avec une commande docker inspect**
    [l3z@localhost ~]$ docker inspect c4538debb036
    [
        {
            "Id": "c4538debb036705aadf8641e4180f1356ec16c47edf04bd080e857d7a8e0831c",
            "Created": "2025-03-04T09:45:03.268468777Z",
            "Path": "/docker-entrypoint.sh",
            "Args": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "State": {
                "Status": "running",
                "Running": true,
                "Paused": false,
                "Restarting": false,
                "OOMKilled": false,
                "Dead": false,
                "Pid": 30659,
                "ExitCode": 0,
                "Error": "",
                "StartedAt": "2025-03-04T09:45:03.509045238Z",
                "FinishedAt": "0001-01-01T00:00:00Z"
            },
            "Image": "sha256:b52e0b094bc0e26c9eddc9e4ab7a64ce0033c3360d8b7ad4ff4132c4e03e8f7b",
            "ResolvConfPath": "/var/lib/docker/containers/c4538debb036705aadf8641e4180f1356ec16c47edf04bd080e857d7a8e0831c/resolv.conf",
            "HostnamePath": "/var/lib/docker/containers/c4538debb036705aadf8641e4180f1356ec16c47edf04bd080e857d7a8e0831c/hostname",
            "HostsPath": "/var/lib/docker/containers/c4538debb036705aadf8641e4180f1356ec16c47edf04bd080e857d7a8e0831c/hosts",
            "LogPath": "/var/lib/docker/containers/c4538debb036705aadf8641e4180f1356ec16c47edf04bd080e857d7a8e0831c/c4538debb036705aadf8641e4180f1356ec16c47edf04bd080e857d7a8e0831c-json.log",
            "Name": "/stoic_hamilton",
            "RestartCount": 0,
            "Driver": "overlay2",
            "Platform": "linux",
            "MountLabel": "",
            "ProcessLabel": "",
            "AppArmorProfile": "",
            "ExecIDs": null,
            "HostConfig": {
                "Binds": null,
                "ContainerIDFile": "",
                "LogConfig": {
                    "Type": "json-file",
                    "Config": {}
                },
                "NetworkMode": "bridge",
                "PortBindings": {
                    "80/tcp": [
                        {
                            "HostIp": "",
                            "HostPort": "9999"
                        }
                    ]
                },
                "RestartPolicy": {
                    "Name": "no",
                    "MaximumRetryCount": 0
                },
                "AutoRemove": false,
                "VolumeDriver": "",
                "VolumesFrom": null,
                "ConsoleSize": [
                    40,
                    94
                ],
                "CapAdd": null,
                "CapDrop": null,
                "CgroupnsMode": "private",
                "Dns": [],
                "DnsOptions": [],
                "DnsSearch": [],
                "ExtraHosts": null,
                "GroupAdd": null,
                "IpcMode": "private",
                "Cgroup": "",
                "Links": null,
                "OomScoreAdj": 0,
                "PidMode": "",
                "Privileged": false,
                "PublishAllPorts": false,
                "ReadonlyRootfs": false,
                "SecurityOpt": null,
                "UTSMode": "",
                "UsernsMode": "",
                "ShmSize": 67108864,
                "Runtime": "runc",
                "Isolation": "",
                "CpuShares": 0,
                "Memory": 0,
                "NanoCpus": 0,
                "CgroupParent": "",
                "BlkioWeight": 0,
                "BlkioWeightDevice": [],
                "BlkioDeviceReadBps": [],
                "BlkioDeviceWriteBps": [],
                "BlkioDeviceReadIOps": [],
                "BlkioDeviceWriteIOps": [],
                "CpuPeriod": 0,
                "CpuQuota": 0,
                "CpuRealtimePeriod": 0,
                "CpuRealtimeRuntime": 0,
                "CpusetCpus": "",
                "CpusetMems": "",
                "Devices": [],
                "DeviceCgroupRules": null,
                "DeviceRequests": null,
                "MemoryReservation": 0,
                "MemorySwap": 0,
                "MemorySwappiness": null,
                "OomKillDisable": null,
                "PidsLimit": null,
                "Ulimits": [],
                "CpuCount": 0,
                "CpuPercent": 0,
                "IOMaximumIOps": 0,
                "IOMaximumBandwidth": 0,
                "MaskedPaths": [
                    "/proc/asound",
                    "/proc/acpi",
                    "/proc/kcore",
                    "/proc/keys",
                    "/proc/latency_stats",
                    "/proc/timer_list",
                    "/proc/timer_stats",
                    "/proc/sched_debug",
                    "/proc/scsi",
                    "/sys/firmware",
                    "/sys/devices/virtual/powercap"
                ],
                "ReadonlyPaths": [
                    "/proc/bus",
                    "/proc/fs",
                    "/proc/irq",
                    "/proc/sys",
                    "/proc/sysrq-trigger"
                ]
            },
            "GraphDriver": {
                "Data": {
                    "ID": "c4538debb036705aadf8641e4180f1356ec16c47edf04bd080e857d7a8e0831c",
                    "LowerDir": "/var/lib/docker/overlay2/4a1afee8ef1def0a57b426991263099dc1066980f72ecfe0c7474ab3d0875488-init/diff:/var/lib/docker/overlay2/40a03b5c55a39ceef7805c376da6d4dfbb2ab2fc14c4e0525dd7a66943284470/diff:/var/lib/docker/overlay2/bb37f200c9a302e2748f5a86bdce4092c22d409d9b0b2ab478e96368aa66bd43/diff:/var/lib/docker/overlay2/ecaaa8dcfa766f8f1b6cf2610c301bb886493ab84ec6b79252830753630e5f44/diff:/var/lib/docker/overlay2/3bb96e09429d20e6eb55bc31b21bf7abd6f576cf6f23faba10ffc2c70079317d/diff:/var/lib/docker/overlay2/427067e031bc0d72c7efb9218e4eb4a06ef7bfb6d70e363e8653c4d6c716580f/diff:/var/lib/docker/overlay2/4fe4757fbb7be2c5b492621920de977749737994efe05aeaa1f58d052f3965c1/diff:/var/lib/docker/overlay2/7942fb0242c052fb7d10345354f6ff9925e9dbf561869d03e42c19f6ceaaae50/diff",
                    "MergedDir": "/var/lib/docker/overlay2/4a1afee8ef1def0a57b426991263099dc1066980f72ecfe0c7474ab3d0875488/merged",
                    "UpperDir": "/var/lib/docker/overlay2/4a1afee8ef1def0a57b426991263099dc1066980f72ecfe0c7474ab3d0875488/diff",
                    "WorkDir": "/var/lib/docker/overlay2/4a1afee8ef1def0a57b426991263099dc1066980f72ecfe0c7474ab3d0875488/work"
                },
                "Name": "overlay2"
            },
            "Mounts": [],
            "Config": {
                "Hostname": "c4538debb036",
                "Domainname": "",
                "User": "",
                "AttachStdin": false,
                "AttachStdout": false,
                "AttachStderr": false,
                "ExposedPorts": {
                    "80/tcp": {}
                },
                "Tty": false,
                "OpenStdin": false,
                "StdinOnce": false,
                "Env": [
                    "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                    "NGINX_VERSION=1.27.4",
                    "NJS_VERSION=0.8.9",
                    "NJS_RELEASE=1~bookworm",
                    "PKG_RELEASE=1~bookworm",
                    "DYNPKG_RELEASE=1~bookworm"
                ],
                "Cmd": [
                    "nginx",
                    "-g",
                    "daemon off;"
                ],
                "Image": "nginx",
                "Volumes": null,
                "WorkingDir": "",
                "Entrypoint": [
                    "/docker-entrypoint.sh"
                ],
                "OnBuild": null,
                "Labels": {
                    "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
                },
                "StopSignal": "SIGQUIT"
            },
            "NetworkSettings": {
                "Bridge": "",
                "SandboxID": "d1829085613ff78e7f4b99d58c98ffe79f9adc4fc6bc9ec9d701bdb66b039de2",
                "SandboxKey": "/var/run/docker/netns/d1829085613f",
                "Ports": {
                    "80/tcp": [
                        {
                            "HostIp": "0.0.0.0",
                            "HostPort": "9999"
                        },
                        {
                            "HostIp": "::",
                            "HostPort": "9999"
                        }
                    ]
                },
                "HairpinMode": false,
                "LinkLocalIPv6Address": "",
                "LinkLocalIPv6PrefixLen": 0,
                "SecondaryIPAddresses": null,
                "SecondaryIPv6Addresses": null,
                "EndpointID": "688e423fdac01960d9adec69b042e0762d6c6917563697f09a2c065500f1ca26",
                "Gateway": "172.17.0.1",
                "GlobalIPv6Address": "",
                "GlobalIPv6PrefixLen": 0,
                "IPAddress": "172.17.0.2",
                "IPPrefixLen": 16,
                "IPv6Gateway": "",
                "MacAddress": "b2:f4:f1:1b:f9:b5",
                "Networks": {
                    "bridge": {
                        "IPAMConfig": null,
                        "Links": null,
                        "Aliases": null,
                        "MacAddress": "b2:f4:f1:1b:f9:b5",
                        "DriverOpts": null,
                        "GwPriority": 0,
                        "NetworkID": "a20b92073cec726fe18e22fd66695cf21bb4e13adf4e406f87f3cae8d5c3b3fd",
                        "EndpointID": "688e423fdac01960d9adec69b042e0762d6c6917563697f09a2c065500f1ca26",
                        "Gateway": "172.17.0.1",
                        "IPAddress": "172.17.0.2",
                        "IPPrefixLen": 16,
                        "IPv6Gateway": "",
                        "GlobalIPv6Address": "",
                        "GlobalIPv6PrefixLen": 0,
                        "DNSNames": null
                    }
                }
            }
        }
    ]

**afficher le port en écoute sur la VM avec un sudo ss -lnpt**
    [l3z@localhost ~]$ sudo ss -lnpt | grep docker
    [sudo] password for l3z: 
    LISTEN 0      4096         0.0.0.0:9999      0.0.0.0:*    users:(("docker-proxy",pid=30684,fd=7))
    LISTEN 0      4096            [::]:9999         [::]:*    users:(("docker-proxy",pid=30690,fd=7))

**ouvrir le port 9999/tcp (vu dans le ss au dessus normalement) dans le firewall de la VM**
    [l3z@localhost ~]$ sudo iptables -A INPUT -p TCP --dport 9999 -j ACCEPT

**depuis le navigateur de votre PC, visiter le site web sur http://IP_VM:9999**[l3z@localhost ~]$ curl http://192.168.56.101:9999
    <!DOCTYPE html>
    <html>
    <head>
    <title>Welcome to nginx!</title>
    <style>
    html { color-scheme: light dark; }
    body { width: 35em; margin: 0 auto;
    font-family: Tahoma, Verdana, Arial, sans-serif; }
    </style>
    </head>
    <body>
    <h1>Welcome to nginx!</h1>
    <p>If you see this page, the nginx web server is successfully installed and
    working. Further configuration is required.</p>

    <p>For online documentation and support please refer to
    <a href="http://nginx.org/">nginx.org</a>.<br/>
    Commercial support is available at
    <a href="http://nginx.com/">nginx.com</a>.</p>

    <p><em>Thank you for using nginx.</em></p>
    </body>
    </html>
### 5. Un deuxième conteneur en vif

**🌞 Lance un conteneur Python, avec un shell**

    [l3z@localhost ~]$ docker run -it python bash
    Unable to find image 'python:latest' locally
    latest: Pulling from library/python
    155ad54a8b28: Pull complete 
    8031108f3cda: Pull complete 
    1d281e50d3e4: Pull complete 
    447713e77b4f: Pull complete 
    21754c21aa78: Pull complete 
    854e2aed8deb: Pull complete 
    5e9ad5aa09b4: Pull complete 
    Digest: sha256:385ccb8304f6330738a6d9e6fa0bd7608e006da7e15bc52b33b0398e1ba4a15b
    Status: Downloaded newer image for python:latest

**🌞 Installe des libs Python**

    root@b7e2729ed021:/# pip install aiohttp
    Collecting aiohttp
    Downloading aiohttp-3.11.13-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.7 kB)
    Collecting aiohappyeyeballs>=2.3.0 (from aiohttp)
    Downloading aiohappyeyeballs-2.4.8-py3-none-any.whl.metadata (5.9 kB)
    Collecting aiosignal>=1.1.2 (from aiohttp)
    Downloading aiosignal-1.3.2-py2.py3-none-any.whl.metadata (3.8 kB)
    Collecting attrs>=17.3.0 (from aiohttp)
    Downloading attrs-25.1.0-py3-none-any.whl.metadata (10 kB)
    Collecting frozenlist>=1.1.1 (from aiohttp)
    Downloading frozenlist-1.5.0-cp313-cp313-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (13 kB)
    Collecting multidict<7.0,>=4.5 (from aiohttp)
    Downloading multidict-6.1.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.0 kB)
    Collecting propcache>=0.2.0 (from aiohttp)
    Downloading propcache-0.3.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (10 kB)
    Collecting yarl<2.0,>=1.17.0 (from aiohttp)
    Downloading yarl-1.18.3-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (69 kB)
    Collecting idna>=2.0 (from yarl<2.0,>=1.17.0->aiohttp)
    Downloading idna-3.10-py3-none-any.whl.metadata (10 kB)
    Downloading aiohttp-3.11.13-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.7 MB)
    ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.7/1.7 MB 28.9 MB/s eta 0:00:00
    Downloading aiohappyeyeballs-2.4.8-py3-none-any.whl (15 kB)
    Downloading aiosignal-1.3.2-py2.py3-none-any.whl (7.6 kB)
    Downloading attrs-25.1.0-py3-none-any.whl (63 kB)
    Downloading frozenlist-1.5.0-cp313-cp313-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (267 kB)
    Downloading multidict-6.1.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (131 kB)
    Downloading propcache-0.3.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (227 kB)
    Downloading yarl-1.18.3-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (339 kB)
    Downloading idna-3.10-py3-none-any.whl (70 kB)
    Installing collected packages: propcache, multidict, idna, frozenlist, attrs, aiohappyeyeballs, yarl, aiosignal, aiohttp
    Successfully installed aiohappyeyeballs-2.4.8 aiohttp-3.11.13 aiosignal-1.3.2 attrs-25.1.0 frozenlist-1.5.0 idna-3.10 multidict-6.1.0 propcache-0.3.0 yarl-1.18.3
    WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable.It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.

    [notice] A new release of pip is available: 24.3.1 -> 25.0.1
    [notice] To update, run: pip install --upgrade pip


    root@b7e2729ed021:/# pip install aioconsole
    Collecting aioconsole
    Downloading aioconsole-0.8.1-py3-none-any.whl.metadata (46 kB)
    Downloading aioconsole-0.8.1-py3-none-any.whl (43 kB)
    Installing collected packages: aioconsole
    Successfully installed aioconsole-0.8.1
    WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable.It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.

    [notice] A new release of pip is available: 24.3.1 -> 25.0.1
    [notice] To update, run: pip install --upgrade pip

    root@b7e2729ed021:/# python
    Python 3.13.2 (main, Feb 25 2025, 05:25:21) [GCC 12.2.0] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import aiohttp
    >>> 

## II. Images

### 1. Images publiques

**🌞 Récupérez des images**

   [l3z@localhost ~]$ docker image ls
    REPOSITORY           TAG       IMAGE ID       CREATED         SIZE
    linuxserver/wikijs   latest    df2a4c7bfb67   10 days ago     482MB
    wordpress            latest    458dad822ff7   2 weeks ago     701MB
    nginx                latest    b52e0b094bc0   3 weeks ago     192MB
    python               3.13      36d17f72f4f3   3 weeks ago     1.02GB
    python               latest    36d17f72f4f3   3 weeks ago     1.02GB
    hello-world          latest    74cc54e27dc4   5 weeks ago     10.1kB
    python               3.11      78553a4d82cb   3 months ago    1.01GB
    mysql                5.7       5107333e08a8   14 months ago   501MB

**🌞 Lancez un conteneur à partir de l'image Python**

    [l3z@localhost ~]$ docker run -it python:3.11 bash
    Unable to find image 'python:3.11' locally
    3.11: Pulling from library/python
    155ad54a8b28: Already exists 
    8031108f3cda: Already exists 
    1d281e50d3e4: Already exists 
    447713e77b4f: Already exists 
    441749a24fb5: Pull complete 
    ae604eab20d6: Pull complete 
    672d84e58157: Pull complete 
    Digest: sha256:68a8863d0625f42d47e0684f33ca02f19d6094ef859a8af237aaf645195ed477
    Status: Downloaded newer image for python:3.11
    root@204f049a7cda:/#

### 2. Construire une image

**🌞 Ecrire un Dockerfile pour une image qui héberge une application Python**

    [l3z@localhost ~]$ cat Dockerfile 
    FROM debian 
    RUN apt update 
    RUN apt install -y python3
    RUN pip install emoji
    COPY app.py
    ENTRYPOINT ["python3", "app.py"]

**🌞 Build l'image**
    [l3z@localhost python_app_build]$ docker build . -t python_app:version_de_ouf
    [+] Building 10.7s (10/10) FINISHED                                            docker:default
    => [internal] load build definition from Dockerfile                                     0.0s
    => => transferring dockerfile: 228B                                                     0.0s
    => [internal] load metadata for docker.io/library/python:3.9                            2.3s
    => [internal] load .dockerignore                                                        0.0s
    => => transferring context: 2B                                                          0.0s
    => [1/5] FROM docker.io/library/python:3.9@sha256:5ea663a1c6ba266fdcac5949d1d2ea364ce3  2.5s
    => => resolve docker.io/library/python:3.9@sha256:5ea663a1c6ba266fdcac5949d1d2ea364ce3  0.0s
    => => sha256:9f98746e2033b7c45b22bf0b4f3bed6edee1b9a100c215c346e607458 6.17kB / 6.17kB  0.0s
    => => sha256:93bee3686f319cf7bd4fcc659256d85121430628478ba3d026b5a9696 6.16MB / 6.16MB  0.5s
    => => sha256:95b7226c62e1a4719940920ae7fffd1ea4915befd3139d7020b84da 19.85MB / 19.85MB  0.8s
    => => sha256:521cad6ddc5302ec0b1d426cdf6df64316fd18ddf3cb0924d24daee81b661 250B / 250B  0.5s
    => => sha256:5ea663a1c6ba266fdcac5949d1d2ea364ce30a2da92a3df95bb3c01 10.35kB / 10.35kB  0.0s
    => => sha256:8bc030886625d9be09abc0be226220146fb470fd7aa0c2ae05ea52b0f 2.32kB / 2.32kB  0.0s
    => => extracting sha256:93bee3686f319cf7bd4fcc659256d85121430628478ba3d026b5a96967b35c  0.5s
    => => extracting sha256:95b7226c62e1a4719940920ae7fffd1ea4915befd3139d7020b84da24182ff  1.2s
    => => extracting sha256:521cad6ddc5302ec0b1d426cdf6df64316fd18ddf3cb0924d24daee81b6615  0.0s
    => [internal] load build context                                                        0.0s
    => => transferring context: 86B                                                         0.0s
    => [2/5] RUN apt update                                                                 2.6s
    => [3/5] RUN apt install -y python3                                                     0.8s
    => [4/5] RUN pip3 install emoji                                                         2.3s 
    => [5/5] COPY app.py .                                                                  0.0s 
    => exporting to image                                                                   0.1s 
    => => exporting layers                                                                  0.1s 
    => => writing image sha256:52fd776e17e3ff7905b9a939d030e63577d8890182dc1386fe26a2efc82  0.0s 
    => => naming to docker.io/library/python_app:version_de_ouf

**🌞 Lancer l'image**
        [l3z@localhost python_app_build]$ docker run python_app:version_de_ouf                        
        Cet exemple d'application est vraiment naze 👎

## III. Docker compose

**🌞 Créez un fichier docker-compose.yml**

    [l3z@localhost compose_test]$ cat docker-compose.yml 
    version: "3"

    services:
    conteneur_nul:
        image: debian
        entrypoint: sleep 9999
    conteneur_flopesque:
        image: debian
        entrypoint: sleep 9999

**🌞 Lancez les deux conteneurs avec docker compose**

    [l3z@localhost compose_test]$ docker compose up -d
    WARN[0000] /home/l3z/compose_test/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
    [+] Running 3/3
    ✔ conteneur_flopesque Pulled                                                            4.1s 
    ✔ conteneur_nul Pulled                                                                  3.6s 
    ✔ 155ad54a8b28 Already exists                                                         0.0s 
    [+] Running 3/3
    ✔ Network compose_test_default                  Creat...                                0.3s 
    ✔ Container compose_test-conteneur_flopesque-1  Started                                 0.3s 
    ✔ Container compose_test-conteneur_nul-1        Started                                 0.3s 

**🌞 Vérifier que les deux conteneurs tournent**

    [l3z@localhost compose_test]$ docker compose ps
    WARN[0000] /home/l3z/compose_test/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
    NAME                                 IMAGE     COMMAND        SERVICE               CREATED              STATUS              PORTS
    compose_test-conteneur_flopesque-1   debian    "sleep 9999"   conteneur_flopesque   About a minute ago   Up About a minute   
    compose_test-conteneur_nul-1         debian    "sleep 9999"   conteneur_nul         About a minute ago   Up About a minute 

**🌞 Pop un shell dans le conteneur conteneur_nul**

    [l3z@localhost compose_test]$ docker compose exec conteneur_nul bash
    WARN[0000] /home/l3z/compose_test/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
    root@e348701ee843:/# 


