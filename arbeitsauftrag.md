Arbeitsauftrag für Werkstattauftrag 
======

### Einleitung
Diese Dokumentation wurde im Rahmen des Moduls 157 erarbeitet und zeigt alle Schritte auf, die es braucht um die LB2-Kriterien zu erfüllen.

### Inhaltsverzeichnis

[01 - Autoren, Versionierung](#01---Autoren,-Versionierung)

[02 - Einführung](#02---Einführung)
 
[03 - Materialliste](#03---Materialliste)
   
[04 - Installationsanleitung](#04---installationsanleitung)

[05 - Qualitätskontrolle](#05---Qualitätskontrolle)

[06 - Error-Handling](#06---Error-Handling)
 
  
___

01 - Autoren, Versionierung
======

| Autoren      | Datum    | Version  |                                
| -------------|----------|----------|
| David Malic  | 30.10.19 |    0.1   |
| David Malic  | 31.10.19 |    0.2   |
| David Malic  | 04.11.19 |    0.3   |
___

02 - Einführung
======

Es wird ein Raspberry Pi der Version 3 mit der aktuellsten Version von Linux Debian installiert. Das Ziel ist es, den Raspberry Pi so zu programmieren, damit er als Funktionsfähiger Accesspoint eingesetzt werden kann.
Sobald der Raspberry Pi aufgesetzt ist, muss er konfiguriert werden. Zuerst wird das Betriebssystem auf den aktuellsten Stand gebracht. Dann nehmen wir uns die Netzwerkkonfiguration vor. Nach diesen Arbeitsschritten werden wir den Raspberry Pi als einen Accesspoint umkonfigurieren, mit Hilfe der Installationsanleitung. 

| Tätigkeit | Zeit |
|----------------------|--------|
| Raspberry Pi aufsetzen | 45min |
| Updates installieren | 30min |
| Netzwerkkonfiguration | 30min | 
| Konfiguration | 1.5h |
	

___

03 - Materialliste
======

### Hardware
- Raspberry Pi 3 (vorherige Modelle sind nicht kompatibel)
- Micro USB Netzteil
- Micro SD Karte (mind. 4GB)
- Netzwerk- und Internetverbindung
- Zwei LAN Kabel
- Monitor, Maus und Tastatur

### Software
Hostapd  
Noobs OS

#### Entscheidungsmatrix
![software](https://user-images.githubusercontent.com/47855918/67899501-b2676c80-fb62-11e9-94a1-779f72806b2e.png)
___

04 - Installationsanleitung
======

### Schritt 1
Damit wir mit einen Accesspoint auf einem Raspberry installieren kann benöntigt man die Software Hostapd und bridge-utils. 

### Schritt 2
Sobald die Software installiert ist werden wir eine Konfigdatei namens hostapd.conf anlegen unter sudo nano /etc/hostapd/

### Schritt 3 
Nun muss die Konfig-Datei überschrieben werden. Folgende Konfiguration muss eingesezt werden, und die SSID und das Passwort geändert werden: 
``` bash
ssid=RaspberryAP
wpa_passphrase=WLANPASSWORT

driver=nl80211
country_code=CH
ieee80211d=1
hw_mode=g
beacon_int=100
channel=9
ieee80211n=1
ht_capab=[SHORT-GI-20][DSSS_CCK-40]
interface=wlan0
ap_isolate=1
bss_load_update_period=60
disassoc_low_ack=1
preamble=1
wmm_enabled=1
ignore_broadcast_ssid=0
uapsd_advertisement_enabled=1
auth_algs=1
wpa=2
wpa_pairwise=CCMP
bridge=br0
wpa_key_mgmt=WPA-PSK
okc=0
disable_pmksa_caching=1
macaddr_acl=0
```

### Schritt 4
Aus Sicherheitsgründen setzen wir die Berechtigung so, das nur der Owner berechtigung auf Lesen und verändern hat.

### Schritt 5
Nun wird die Netzwerkkonfiguration festgelegt. Unter Interfaces wird nun die WLAN konfiguraion vorgenommen:
##### WLAN
``` bash
auto wlan0
allow-hotplug wlan0
iface wlan0 inet manual
wireless-power off
```
##### Netzwerkbrücke
```
auto br0
iface br0 inet dhcp
bridge_ports eth0 wlan0 # build bridge
bridge_fd 0 # no forwarding delay
bridge_stp off # disable Spanning Tree Protocol
```

### Schritt 6
Richten sie den Raspberry Pi so ein, dass er den AccessPoint automatisch startet.

Nachdem wir uns über Putty verbunden haben, sollten zuerst mal alle vorhanden Updates installiert werden:  
```bash
sudo apt-get update
sudo apt-get upgrade
```
___

05 - Qualitätskotrolle
======

Die Funktionalität, der Raspberry Pi Installation kann so getestet werden, indem man auf einem anderen WLAN fähigem Gerät  in der Nähe des Raspberry Pi’s, das WLAN-Netzwerk gesucht wird und verbunden wird.

### Commands für Überprüfung
``` bash
iw dev wlan0 info  
iw dev wlan0 get power_save
```
___

06 - Error-Handling
======

hostapd kann auch mit folgendem Befehl gestartet werden. Im Terminal werden dabei Informationen zum Start, bzw. zu den verbundenen Geräten angezeigt: 
```
sudo hostapd -dd /etc/hostapd/hostapd.conf
```
___
