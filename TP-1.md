# TP1 : Premiers pas Docker

## 0. Setup

## I. Init

### 1. Installation de Docker**
#
### 2. Vérifier que Docker est bien là**
#
### 3. sudo c pa bo**

**🌞 Ajouter votre utilisateur au groupe docker**
    

    [ibra@vbox ~]$ su -
    Password:
    Last login: Wed Dec 11 10:56:52 CET 2024 on tty1
    [root@vbox ~]# usermod -aG docker ibra
    [root@vbox ~]# logout

### 4. Un premier conteneur en vif

**🌞 Lancer un conteneur NGINX**

    [ibra@vbox ~]$ docker run -d -p 8888:80 nginx
    e319ae450f622c38f7790c95dc764e3160d94510381fef01ff3a16638a91162d

**🌞 Visitons**

**vérifier que le conteneur est actif avec une commande qui liste les conteneurs en cours de fonctionnement**
        [ibra@vbox ~]$ docker ps
        CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS
                            NAMES
        e319ae450f62   nginx     "/docker-entrypoint.…"   43 seconds ago   Up 42 seconds   0.0.0.0:8888->80/tcp, [::]:8888->80/tcp   stoic_lederberg

**afficher toutes les informations relatives au conteneur avec une commande docker inspect**

        [ibra@vbox ~]$ docker inspect e319ae450f62
    [
        {
            "Id": "e319ae450f622c38f7790c95dc764e3160d94510381fef01ff3a16638a91162d",
            "Created": "2024-12-11T10:21:39.719014635Z",
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

**afficher le port en écoute sur la VM avec un sudo ss -lnpt**

    [ibra@vbox ~]$ sudo ss -lnpt
    State  Recv-Q Send-Q  Local Address:Port   Peer Address:Port Process
    LISTEN 0      4096          0.0.0.0:8888        0.0.0.0:*     users:(("docker-proxy",pid=50371,fd=4))

**ouvrir le port 9999/tcp (vu dans le ss au dessus normalement) dans le firewall de la VM**

    [ibra@vbox ~]$ sudo systemctl start firewalld
    [ibra@vbox ~]$ sudo firewall-cmd --permanent --add-port=8888/tcp
    success
    [ibra@vbox ~]$ sudo firewall-cmd --reload
    success
    [ibra@vbox ~]$ sudo firewall-cmd --list-ports
    8888/tcp

**depuis le navigateur de votre PC, visiter le site web sur http://IP_VM:8888**


#


**🌞 On va ajouter un site Web au conteneur NGINX**

    [ibra@vbox ~]$ cd nginx/
    [ibra@vbox nginx]$ nano index.html
    [ibra@vbox nginx]$ cat index.html
    <h1>MEOOOW</h1>
    [ibra@vbox nginx]$ nano site_nul.conf
    [ibra@vbox nginx]$ cat site_nul.conf
    server {
        listen        8080;

        location / {
            root /var/www/html;
        }
    }
    [ibra@vbox nginx]$

    [ibra@vbox nginx]$ docker run -d -p 9999:8080 -v /home/ibra/nginx/index.html:/var/www/html/index.html
    -v /home/ibra/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf nginx
    38ecf87631e17ce260eaa2159b724f603564d25a7ad3bd771d6c8799f4f51896

**🌞 Visitons**

### 5. Un deuxième conteneur en vif

**🌞 Lance un conteneur Python, avec un shell**

    [ibra@vbox nginx]$ docker run -it python bash
    Unable to find image 'python:latest' locally
    latest: Pulling from library/python
    fdf894e782a2: Pull complete
    5bd71677db44: Pull complete
    551df7f94f9c: Pull complete
    ce82e98d553d: Pull complete
    5f0e19c475d6: Pull complete
    abab87fa45d0: Pull complete
    2ac2596c631f: Pull complete
    Digest: sha256:220d07595f288567bbf07883576f6591dad77d824dce74f0c73850e129fa1f46
    Status: Downloaded newer image for python:latest
    root@8e80d6aa9ba1:/#

**🌞 Installe des libs Python**

    root@8e80d6aa9ba1:/# pip install aiohttp
    root@8e80d6aa9ba1:/# pip install aioconsole
    
    root@8e80d6aa9ba1:/# python3
    Python 3.13.1 (main, Dec  4 2024, 20:40:27) [GCC 12.2.0] on linux
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import aiohttp
    >>>