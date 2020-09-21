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
- atacante (kalilinux/rolling)
- zombie (vulnerable windows 7)

![lab-image](lab-topology.png)

Para iniciar el laboratorio, ejecutamos comando:

```
lab-idle-scan-zombie/$ vagrant up
Bringing machine 'victima' up with 'virtualbox' provider...
Bringing machine 'atacante' up with 'virtualbox' provider...
Bringing machine 'zombie' up with 'virtualbox' provider...
==> victima: Importing base box 'debian/jessie64'...
==> victima: Matching MAC address for NAT networking...
==> victima: Checking if box 'debian/jessie64' version '8.11.1' is up to date...
==> victima: Setting the name of the VM: iddle-scan_victima_1600653761197_36353
==> victima: Clearing any previously set network interfaces...
==> victima: Preparing network interfaces based on configuration...
    victima: Adapter 1: nat
==> victima: Forwarding ports...
    victima: 22 (guest) => 2222 (host) (adapter 1)
==> victima: Running 'pre-boot' VM customizations...
==> victima: Booting VM...
==> victima: Waiting for machine to boot. This may take a few minutes...
    victima: SSH address: 127.0.0.1:2222
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
==> atacante: Importing base box 'kalilinux/rolling'...
==> atacante: Matching MAC address for NAT networking...
==> atacante: Checking if box 'kalilinux/rolling' version '2020.3.0' is up to date...
==> atacante: Setting the name of the VM: iddle-scan_atacante_1600653973125_18411
==> atacante: Fixed port collision for 22 => 2222. Now on port 2200.
==> atacante: Clearing any previously set network interfaces...
==> atacante: Preparing network interfaces based on configuration...
    atacante: Adapter 1: nat
==> atacante: Forwarding ports...
    atacante: 22 (guest) => 2200 (host) (adapter 1)
==> atacante: Running 'pre-boot' VM customizations...
==> atacante: Booting VM...
==> atacante: Waiting for machine to boot. This may take a few minutes...
    atacante: SSH address: 127.0.0.1:2200
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

Se va a lanzar una GUI que corresponde al Windows Zombie como así también del Kali Linux del atacante.

	La box de Windows tiene algunos inconvenientes que no permiten configurar todo de forma automática, como por ejemplo no tener instaladas las guest tools.

Por lo tanto, lo primero que se debe hacer:

Es cambiar manualmente la interface de red de virtualbox (de la VM que ejecuto) para que forme parte de una red "Host-Only" y anexada a la interfaz "vboxnet0". (Es un workaround, no lo ideal)

Luego en segundo lugar hay deshabilitar el firewall.

	Desde la GUI es necesario desactivar el Firewall de Windows para que funcione el laboratorio.

Lo tecero que deberá hacer es tomar nota de las IP que tomo cada uno de los nodos.

Ambas tareas la realizará conectandose a cada una de las VMs

* Para conectarse al zombie, lo hará mediente la GUI (ingresa sin credenciales).
* La VM atacante tiene instalada una GUI y puede conectarse mediante ella con usuario vagrant y contraseña vagrant.
* Para conectarse tanto a la VM victima lo podrá hacer ejecutando: `vagrant ssh victima` desde la consola ubicandose en el espacio de trabajo. Este método es válido también para atacante en tal caso ingresará `vagrant ssh atacante` 

Entonces,

```
$ vagrant ssh atacante
Linux kali 5.7.0-kali1-amd64 #1 SMP Debian 5.7.6-1kali2 (2020-07-01) x86_64

The programs included with the Kali GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Kali GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Sun Sep 20 22:32:51 2020 from 10.0.2.2

vagrant@kali:~$ ifconfig eth1
eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.28.128.10  netmask 255.255.255.0  broadcast 172.28.128.255
        ether 08:00:27:e4:ca:8f  txqueuelen 1000  (Ethernet)
        RX packets 26  bytes 6938 (6.7 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 17  bytes 2676 (2.6 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vagrant@kali:~$ exit
logout
Connection to 127.0.0.1 closed.

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

* Automatizar windows (deshabilitar firewall y instalar guest-tools)

* Hacer un lab que las VMs esten en distintas LAN. La victima podría incluso no incluirse como parte del laboratorio de Vagrant o bien ser opcional.

* Algun otro fix durante la marcha.
