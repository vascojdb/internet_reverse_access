# Internet Reverse Access
A simple way to access your Raspberry Pi or Linux through the internet without messy steps!

## Why is it simple?
 - Works even if you are behind a NAT created by your internet provider
 - You do not need a public IP *(some providers make you pay for that)*
 - You do not need to setup any port forwarding on the router
 - Uses [serveo.net](http://serveo.net/) reverse access so its **free** and **no registration is required**
 - Will let you access your webserver *(port 80)* and SSH connection *(port 22)*. You can configure others if desired.

## How does it work?
You can read [here](http://serveo.net/#intro) all about how serveo.net works.  
Basically what this repository contains is a init.d script that runs on boot, starts an autossh session and establishes the connection to serveo.net with the name you desire.

## Requirements
You need to install autossh and git:
```
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install autossh git
```

## Installation
Installation is simple:  
First clone/download the repository:
```
$ git clone https://github.com/vascojdb/internet_reverse_access.git
$ cd internet_reverse_access
```

Then copy the script file to your init.d folder and change permitions to executable:
```
$ cp serveo /etc/init.d/serveo
$ chmod +x /etc/init.d/serveo
```

Now open the file with vim or nano and edit at your own will:
```
$ sudo nano /etc/init.d/serveo
```

You can edit the following lines, specially the **SUBDOMAIN_NAME**:
```
SUBDOMAIN_NAME="whateveryouwant"
WEB_LOCAL_PORT=80
WEB_INTERNET_PORT=80
SSH_LOCAL_PORT=22
SSH_INTERNET_PORT=22
```

After save the file and run the following to enable the script to be run on every boot:
```
$ sudo update-rc.d serveo defaults
```

Now test the script by running start/stop/restart
```
$ /etc/init.d/serveo start
Starting AutoSSh tunnel connection to serveo.net: http://whateveryouwant.serveo.net (Ports: WEB: 80, SSH: 22)
```

## WEB access
Open your browser and access the following website:
```
http://whateveryouwant.serveo.net
```

## SSH access
Open your favourite SSH terminal or browser *(puTTY, WinSCP)* and connect to the **SUBDOMAIN_NAME** *(which is also the host name)* on port 22 with your regular username.  
You will need to configure the SSH to access the device using a proxy or tunnel, which should be set to `serveo.net` on port `22`.  
For more information check [SSH forwarding](http://serveo.net/#intro)

## TCP access
You can also access any TCP port using this method, for this you need to take a look at [Generic TCP forwarding](http://serveo.net/#intro) and then modify the script file `/etc/init.d/serveo` according to your needs.

## Custom domain
If you do not want to use the <something>.serveo.net subdomain, you may set a domain of your own to look like <something>.com for example. To do this please follow the section [Custom Domain](http://serveo.net/#intro).


**CONGRATULATIONS** you will now be able to access your Raspberry Pi or Linux machine from the internet!
