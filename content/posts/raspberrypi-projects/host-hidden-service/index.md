---
title: 'Host Hidden Service on the RaspberryPi'
date: 2024-04-29T13:00:50+02:00
---


## How to install

```bash
sudo apt install tor
```

## Configure

```bash
sudo nano /etc/tor/torrc
```


Look for this section


```conf
############### This section is just for location-hidden services ###

## Once you have configured a hidden service, you can look at the
## contents of the file ".../hidden_service/hostname" for the address
## to tell people.
##
## HiddenServicePort x y:z says to redirect requests on port x to the
## address y:z.

#HiddenServiceDir /var/lib/tor/hidden_service/
#HiddenServicePort 80 127.0.0.1:80
```

* Now uncomment the following lines
    * `HiddenServiceDir /var/lib/tor/hidden_service/`

    * `HiddenServicePort 80 127.0.0.1:PORT`

## Host hidden service

* Start a example node
    * Start a example node project with npx 
        * `sudo apt-get install npm`
        * `sudo apt-get install nodejs`
        * `sudo npm install --global serve`
        * `npm i npx` 
        * `npx serve -l 5000`
*  With express
    * Create an express-project
    * Set the port to the port set in the config-file
        * Start the server with for example: `node server.js`

* Change the port in torrc
    * `sudo nano /etc/tor/torrc`
        * Change: `HiddenServicePort 80 127.0.0.1:PORT` to `HiddenServicePort 80 127.0.0.1:5000`

* Get the domain:

```bash
sudo cat /var/lib/tor/hidden_service/hostname
```

## Troubleshooting: 
* Check if tor is running:

```bash
sudo service tor status
```

* Stop tor:

```bash
sudo service tor stop
```

* Start tor:

```bash
sudo service tor start
```

* Restart tor:

```sh
sudo service tor restart
```