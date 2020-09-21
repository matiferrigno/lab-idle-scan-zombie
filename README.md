# Lab Idle Scan - Zombie (alfa)

### Seguridad y Privacidad en Redes 

Last update: 21-sep-2020

Status: Alfa

**Requisitos:**

* VirtualBox (https://www.virtualbox.org/wiki/Downloads)
* Vagrant (https://www.vagrantup.com/downloads)

## Clonar el espacio de trabajo

```
$ git clone git@github.com:matiferrigno/lab-idle-scan-zombie.git
$ cd lab-idle-scan-zombie/
lab-idle-scan-zombie/$
```

## Up & Running

El laboratorio consta de tres maquinas virtuales, con los tres roles necesarios:

- victima (debian/jessie64)
- atacante (debian/jessie64)
- zombie (vulnerable windows 7)

![lab-image](lab-topology.png)

Para iniciar el laboratorio, ejecutamos comando:

```
lab-idle-scan-zombie/$ vagrant up
Bringing machine 'victima' up with 'virtualbox' provider...
Bringing machine 'atacante' up with 'virtualbox' provider...
Bringing machine 'zombie' up with 'virtualbox' provider...
==> atacante: Importing base box 'debian/jessie64'...
==> atacante: Matching MAC address for NAT networking...
==> atacante: Checking if box 'debian/jessie64' version '8.11.1' is up to date...
==> atacante: Setting the name of the VM: iddle-scan_atacante_1600716979020_77980
==> atacante: Clearing any previously set network interfaces...
==> atacante: Preparing network interfaces based on configuration...
    atacante: Adapter 1: nat
    atacante: Adapter 2: hostonly
==> atacante: Forwarding ports...
    atacante: 22 (guest) => 2222 (host) (adapter 1)
==> atacante: Running 'pre-boot' VM customizations...
==> atacante: Booting VM...
==> atacante: Waiting for machine to boot. This may take a few minutes...
    atacante: SSH address: 127.0.0.1:2222
    atacante: SSH username: vagrant
    atacante: SSH auth method: private key
    atacante: 
    atacante: Vagrant insecure key detected. Vagrant will automatically replace
    atacante: this with a newly generated keypair for better security.
    atacante: 
    atacante: Inserting generated public key within guest...
    atacante: Removing insecure key from the guest if it's present...
    atacante: Key inserted! Disconnecting and reconnecting using new SSH key...
==> atacante: Machine booted and ready!
==> atacante: Checking for guest additions in VM...
    atacante: No guest additions were detected on the base box for this VM! Guest
    atacante: additions are required for forwarded ports, shared folders, host only
    atacante: networking, and more. If SSH fails on this machine, please install
    atacante: the guest additions and repackage the box to continue.
    atacante: 
    atacante: This is not an error message; everything may continue to work properly,
    atacante: in which case you may ignore this message.
==> atacante: Configuring and enabling network interfaces...
==> atacante: Running provisioner: shell...
    atacante: Running: inline script
    atacante: 
    atacante: WARNING: apt does not have a stable CLI interface yet. Use with caution in scripts.
    atacante: Get:1 http://security.debian.org jessie/updates InRelease [44.9 kB]
    atacante: Ign http://httpredir.debian.org jessie InRelease
    atacante: Get:2 http://httpredir.debian.org jessie Release.gpg [1,652 B]
    atacante: Get:3 http://httpredir.debian.org jessie Release [77.3 kB]
    atacante: Get:4 http://security.debian.org jessie/updates/main Sources [366 kB]
    atacante: Hit http://httpredir.debian.org jessie/main Sources
    atacante: Hit http://httpredir.debian.org jessie/main amd64 Packages
    atacante: Get:5 http://security.debian.org jessie/updates/main amd64 Packages [781 kB]
    atacante: Fetched 1,271 kB in 2s (600 kB/s)
    atacante: Reading package lists...
    atacante: Building dependency tree...
    atacante: Reading state information...
    atacante: 76 packages can be upgraded. Run 'apt list --upgradable' to see them.
    atacante: WARNING: 
    atacante: apt
    atacante:  
    atacante: does not have a stable CLI interface yet. 
    atacante: Use with caution in scripts.
    atacante: Reading package lists...
    atacante: Building dependency tree...
    atacante: Reading state information...
    atacante: The following extra packages will be installed:
    atacante:   libpcap0.8 libtcl8.6
    atacante: Suggested packages:
    atacante:   tcl8.6
    atacante: The following NEW packages will be installed:
    atacante:   hping3 libpcap0.8 libtcl8.6 tcpdump
    atacante: 0 upgraded, 4 newly installed, 0 to remove and 76 not upgraded.
    atacante: Need to get 1,608 kB of archives.
    atacante: After this operation, 5,717 kB of additional disk space will be used.
    atacante: Get:1 http://httpredir.debian.org/debian/ jessie/main libtcl8.6 amd64 8.6.2+dfsg-2 [978 kB]
    atacante: Get:2 http://security.debian.org/ jessie/updates/main libpcap0.8 amd64 1.6.2-2+deb8u1 [134 kB]
    atacante: Get:3 http://security.debian.org/ jessie/updates/main tcpdump amd64 4.9.3-1~deb8u1 [391 kB]
    atacante: Get:4 http://httpredir.debian.org/debian/ jessie/main hping3 amd64 3.a2.ds2-7 [105 kB]
    atacante: dpkg-preconfigure: unable to re-open stdin: No such file or directory
    atacante: Fetched 1,608 kB in 1s (1,436 kB/s)
    atacante: Selecting previously unselected package libpcap0.8:amd64.
    atacante: (Reading database ... 
    atacante: (Reading database ... 5%
    atacante: (Reading database ... 10%
    atacante: (Reading database ... 15%
    atacante: (Reading database ... 20%
    atacante: (Reading database ... 25%
    atacante: (Reading database ... 30%
    atacante: (Reading database ... 35%
    atacante: (Reading database ... 40%
    atacante: (Reading database ... 45%
    atacante: (Reading database ... 50%
    atacante: (Reading database ... 55%
    atacante: (Reading database ... 60%
    atacante: (Reading database ... 65%
    atacante: (Reading database ... 70%
    atacante: (Reading database ... 75%
    atacante: (Reading database ... 80%
    atacante: (Reading database ... 85%
    atacante: (Reading database ... 90%
    atacante: (Reading database ... 95%
    atacante: (Reading database ... 100%
    atacante: (Reading database ... 
    atacante: 32922 files and directories currently installed.)
    atacante: Preparing to unpack .../libpcap0.8_1.6.2-2+deb8u1_amd64.deb ...
    atacante: Unpacking libpcap0.8:amd64 (1.6.2-2+deb8u1) ...
    atacante: Selecting previously unselected package libtcl8.6:amd64.
    atacante: Preparing to unpack .../libtcl8.6_8.6.2+dfsg-2_amd64.deb ...
    atacante: Unpacking libtcl8.6:amd64 (8.6.2+dfsg-2) ...
    atacante: Selecting previously unselected package tcpdump.
    atacante: Preparing to unpack .../tcpdump_4.9.3-1~deb8u1_amd64.deb ...
    atacante: Unpacking tcpdump (4.9.3-1~deb8u1) ...
    atacante: Selecting previously unselected package hping3.
    atacante: Preparing to unpack .../hping3_3.a2.ds2-7_amd64.deb ...
    atacante: Unpacking hping3 (3.a2.ds2-7) ...
    atacante: Processing triggers for man-db (2.7.0.2-5) ...
    atacante: Setting up libpcap0.8:amd64 (1.6.2-2+deb8u1) ...
    atacante: Setting up libtcl8.6:amd64 (8.6.2+dfsg-2) ...
    atacante: Setting up tcpdump (4.9.3-1~deb8u1) ...
    atacante: Setting up hping3 (3.a2.ds2-7) ...
    atacante: Processing triggers for libc-bin (2.19-18+deb8u10) ...
==> victima: Importing base box 'debian/jessie64'...
==> victima: Matching MAC address for NAT networking...
==> victima: Checking if box 'debian/jessie64' version '8.11.1' is up to date...
==> victima: Setting the name of the VM: iddle-scan_victima_1600717038019_90926
==> victima: Fixed port collision for 22 => 2222. Now on port 2200.
==> victima: Clearing any previously set network interfaces...
==> victima: Preparing network interfaces based on configuration...
    victima: Adapter 1: nat
    victima: Adapter 2: hostonly
==> victima: Forwarding ports...
    victima: 22 (guest) => 2200 (host) (adapter 1)
==> victima: Running 'pre-boot' VM customizations...
==> victima: Booting VM...
==> victima: Waiting for machine to boot. This may take a few minutes...
    victima: SSH address: 127.0.0.1:2200
    victima: SSH username: vagrant
    victima: SSH auth method: private key
    victima: 
    victima: Vagrant insecure key detected. Vagrant will automatically replace
    victima: this with a newly generated keypair for better security.
    victima: 
    victima: Inserting generated public key within guest...
    victima: Removing insecure key from the guest if it's present...
    victima: Key inserted! Disconnecting and reconnecting using new SSH key...
==> victima: Machine booted and ready!
==> victima: Checking for guest additions in VM...
    victima: No guest additions were detected on the base box for this VM! Guest
    victima: additions are required for forwarded ports, shared folders, host only
    victima: networking, and more. If SSH fails on this machine, please install
    victima: the guest additions and repackage the box to continue.
    victima: 
    victima: This is not an error message; everything may continue to work properly,
    victima: in which case you may ignore this message.
==> victima: Configuring and enabling network interfaces...
==> victima: Running provisioner: shell...
    victima: Running: inline script
    victima: 
    victima: WARNING: apt does not have a stable CLI interface yet. Use with caution in scripts.
    victima: Get:1 http://security.debian.org jessie/updates InRelease [44.9 kB]
    victima: Get:2 http://security.debian.org jessie/updates/main Sources [366 kB]
    victima: Ign http://httpredir.debian.org jessie InRelease
    victima: Get:3 http://security.debian.org jessie/updates/main amd64 Packages [781 kB]
    victima: Get:4 http://httpredir.debian.org jessie Release.gpg [1,652 B]
    victima: Get:5 http://httpredir.debian.org jessie Release [77.3 kB]
    victima: Hit http://httpredir.debian.org jessie/main Sources
    victima: Hit http://httpredir.debian.org jessie/main amd64 Packages
    victima: Fetched 1,271 kB in 3s (389 kB/s)
    victima: Reading package lists...
    victima: Building dependency tree...
    victima: Reading state information...
    victima: 76 packages can be upgraded. Run 'apt list --upgradable' to see them.
    victima: WARNING: 
    victima: apt
    victima:  
    victima: does not have a stable CLI interface yet. 
    victima: Use with caution in scripts.
    victima: Reading package lists...
    victima: Building dependency tree...
    victima: Reading state information...
    victima: The following extra packages will be installed:
    victima:   libpcap0.8 libtcl8.6
    victima: Suggested packages:
    victima:   tcl8.6
    victima: The following NEW packages will be installed:
    victima:   hping3 libpcap0.8 libtcl8.6 tcpdump
    victima: 0 upgraded, 4 newly installed, 0 to remove and 76 not upgraded.
    victima: Need to get 1,608 kB of archives.
    victima: After this operation, 5,717 kB of additional disk space will be used.
    victima: Get:1 http://httpredir.debian.org/debian/ jessie/main libtcl8.6 amd64 8.6.2+dfsg-2 [978 kB]
    victima: Get:2 http://security.debian.org/ jessie/updates/main libpcap0.8 amd64 1.6.2-2+deb8u1 [134 kB]
    victima: Get:3 http://security.debian.org/ jessie/updates/main tcpdump amd64 4.9.3-1~deb8u1 [391 kB]
    victima: Get:4 http://httpredir.debian.org/debian/ jessie/main hping3 amd64 3.a2.ds2-7 [105 kB]
    victima: dpkg-preconfigure: unable to re-open stdin: No such file or directory
    victima: Fetched 1,608 kB in 0s (3,831 kB/s)
    victima: Selecting previously unselected package libpcap0.8:amd64.
    victima: (Reading database ... 
(Reading database ... 65%abase ... 5%
    victima: (Reading database ... 70%
    victima: (Reading database ... 75%
    victima: (Reading database ... 80%
    victima: (Reading database ... 85%
    victima: (Reading database ... 90%
    victima: (Reading database ... 95%
(Reading database ... 32922 files and directories currently installed.)
    victima: Preparing to unpack .../libpcap0.8_1.6.2-2+deb8u1_amd64.deb ...
    victima: Unpacking libpcap0.8:amd64 (1.6.2-2+deb8u1) ...
    victima: Selecting previously unselected package libtcl8.6:amd64.
    victima: Preparing to unpack .../libtcl8.6_8.6.2+dfsg-2_amd64.deb ...
    victima: Unpacking libtcl8.6:amd64 (8.6.2+dfsg-2) ...
    victima: Selecting previously unselected package tcpdump.
    victima: Preparing to unpack .../tcpdump_4.9.3-1~deb8u1_amd64.deb ...
    victima: Unpacking tcpdump (4.9.3-1~deb8u1) ...
    victima: Selecting previously unselected package hping3.
    victima: Preparing to unpack .../hping3_3.a2.ds2-7_amd64.deb ...
    victima: Unpacking hping3 (3.a2.ds2-7) ...
    victima: Processing triggers for man-db (2.7.0.2-5) ...
    victima: Setting up libpcap0.8:amd64 (1.6.2-2+deb8u1) ...
    victima: Setting up libtcl8.6:amd64 (8.6.2+dfsg-2) ...
    victima: Setting up tcpdump (4.9.3-1~deb8u1) ...
    victima: Setting up hping3 (3.a2.ds2-7) ...
    victima: Processing triggers for libc-bin (2.19-18+deb8u10) ...
==> atacante: Machine 'atacante' has a post `vagrant up` message. This is a message
==> atacante: from the creator of the Vagrantfile, and not from Vagrant itself:
==> atacante: 
==> atacante: Vanilla Debian box. See https://app.vagrantup.com/debian for help and bug reports
==> victima: Machine 'victima' has a post `vagrant up` message. This is a message
==> victima: from the creator of the Vagrantfile, and not from Vagrant itself:
==> victima: 
==> victima: Vanilla Debian box. See https://app.vagrantup.com/debian for help and bug reports
==> zombie: Importing base box 'matthewjberger/win7-64-en'...
==> zombie: Matching MAC address for NAT networking...
==> zombie: Checking if box 'matthewjberger/win7-64-en' version '1.0.0' is up to date...
==> zombie: Setting the name of the VM: iddle-scan_zombie_1600654223981_5494
==> zombie: Fixed port collision for 22 => 2222. Now on port 2201.
==> zombie: Clearing any previously set network interfaces...
==> zombie: Preparing network interfaces based on configuration...
    zombie: Adapter 1: nat
==> zombie: Forwarding ports...
    zombie: 22 (guest) => 2201 (host) (adapter 1)
==> zombie: Running 'pre-boot' VM customizations...
==> zombie: Booting VM...
==> zombie: Waiting for machine to boot. This may take a few minutes...
    zombie: SSH address: 127.0.0.1:2201
    zombie: SSH username: vagrant
    zombie: SSH auth method: private key
==> zombie: Machine booted and ready!
==> zombie: Checking for guest additions in VM...
    zombie: The guest additions on this VM do not match the installed version of
    zombie: VirtualBox! In most cases this is fine, but in rare cases it can
    zombie: prevent things such as shared folders from working properly. If you see
    zombie: shared folder errors, please make sure the guest additions within the
    zombie: virtual machine match the version of VirtualBox you have installed on
    zombie: your host and reload your VM.
    zombie: 
    zombie: Guest Additions Version: 4.3.12
    zombie: VirtualBox Version: 6.1

==> victima: Machine 'victima' has a post `vagrant up` message. This is a message
==> victima: from the creator of the Vagrantfile, and not from Vagrant itself:
==> victima: 
==> victima: Vanilla Debian box. See https://app.vagrantup.com/debian for help and bug reports
```

Vagrant creará automáticamente las VMs en Virtualbox.

Se va a lanzar una GUI que corresponde al Windows Zombie.

> La box de Windows tiene algunos inconvenientes que no permiten configurar todo de forma automática, como por ejemplo no tener instaladas las guest tools.

Por lo tanto, lo primero que se debe hacer:

Es cambiar manualmente la interface de red de virtualbox (de la VM que ejecuto) para que forme parte de una red "Host-Only" y anexada a la interfaz "vboxnet0". (Es un workaround, no lo ideal)

Luego en segundo lugar hay deshabilitar el firewall.

> Desde la GUI es necesario desactivar el Firewall de Windows para que funcione el laboratorio.

Lo tecero que deberá hacer es tomar nota de las IP que tomo cada uno de los nodos.

Ambas tareas la realizará conectandose a cada una de las VMs

* Para conectarse al zombie, lo hará mediente la GUI (ingresa sin credenciales).
* Para conectarse tanto a la VM victima lo podrá hacer ejecutando: `vagrant ssh victima` desde la consola ubicandose en el espacio de trabajo. Este método es válido también para atacante en tal caso ingresará `vagrant ssh atacante`.

Entonces,

```
$ vagrant ssh atacante

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Mon Sep 21 19:40:25 2020 from 10.0.2.2
vagrant@jessie:~$ sudo su
root@jessie:/home/vagrant# ifconfig eth1
eth1      Link encap:Ethernet  HWaddr 08:00:27:e4:0e:d9  
          inet addr:172.28.128.10  Bcast:172.28.128.255  Mask:255.255.255.0
          inet6 addr: fe80::a00:27ff:fee4:ed9/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:17 errors:0 dropped:0 overruns:0 frame:0
          TX packets:10 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:5120 (5.0 KiB)  TX bytes:1332 (1.3 KiB)

root@jessie:/home/vagrant# 
```

```
$ vagrant ssh victima

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.

vagrant@jessie:~$ sudo ifconfig eth1
eth1      Link encap:Ethernet  HWaddr 08:00:27:aa:d4:c5  
          inet addr:172.28.128.8  Bcast:172.28.128.255  Mask:255.255.255.0
          inet6 addr: fe80::a00:27ff:feaa:d4c5/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:45 errors:0 dropped:0 overruns:0 frame:0
          TX packets:14 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:12269 (11.9 KiB)  TX bytes:2136 (2.0 KiB)

vagrant@jessie:~$  exit
```

En mi caso:

* victima: 172.28.128.8 (obtenida por shell)
* atacante: 172.28.128.10 (obtenida por shell)
* zombie: 172.28.128.4 (obtenida por GUI)

Las IPs pueden cambiar dependiendo de la configuración de VirtualBox y de la asignación del servidor DHCP.

## Ejercicios 

1. Utilizando la VM atacante (172.28.128.10) y sin dejar rastros en victima (172.28.128.8) indique sí el puerto tcp/22 y tcp/23 se encuentran abiertos o cerrados. 

[![asciicast](https://asciinema.org/a/360831.svg)](https://asciinema.org/a/360831)



## Destroy

```
lab-idle-scan-zombie/$ vagrant destroy --force
==> atacante: Destroying VM and associated drives...
==> victima:Destroying VM and associated drives...
==> zombie: Destroying VM and associated drives...
```

## TODO

* Automatizar la creación de vboxnet0 si no está creada.

* Automatizar windows (deshabilitar firewall y instalar guest-tools).

* Hacer un lab que las VMs esten en distintas LAN. La victima podría incluso no incluirse como parte del laboratorio de Vagrant o bien ser opcional.

* Agregar más ejercicios.

* Algun otro fix durante la marcha.
