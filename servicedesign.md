Service-Design für Werkstattauftrag
======


### Einleitung
Diese Dokumentation wurde im Rahmen des Moduls 157 erarbeitet und zeigt alle Schritte auf, die es braucht um die LB2-Kriterien zu erfüllen.

### Inhaltsverzeichnis

[01 - Autoren, Versionierung](#01---Autoren,-Versionierung)

[02 - Funktion](#Funktion) 
 
[03 - Benötigte Hard- und Software](#03---benötigte-hard--und-software)
   
[04 - Installationsanleitung](#04---Installationsanleitung)

[05 - Testing](*05---Testing)

[06 - Übergabe an den Betrieb](#06---übergabe-an-den-betrieb)
 
[07 - Quellen](#07---Quellen)


  
___

01 - Autoren, Versionierung
======

### Autoren, Versionierung des Dokumentes 

| Autoren      | Datum    | Version  |                                
| -------------|----------|----------|
| David Malic  | 30.10.19 |   0.1    |
| David Malic  | 31.10.19 |   0.2    |
| David Malic  | 04.11.19 |   0.3    |
| David Malic, Gian-Luca Dal Pian  | 07.11.19 |   1.0   |    
___

02 - Funktion 
======

### Funktion des Services

Es wird ein Raspberry Pi der Version 3 mit der aktuellsten Version von Linux Debian installiert. Das Ziel ist es, den Raspberry Pi so zu programmieren, damit er als Funktionsfähiger Accesspoint eingesetzt werden kann.
Sobald der Raspberry Pi aufgesetzt ist, muss er konfiguriert werden. Zuerst wird das Betriebssystem auf den aktuellsten Stand gebracht. Dann nehmen wir uns die Netzwerkkonfiguration vor. Nach diesen Arbeitsschritten werden wir den Raspberry Pi als einen Accesspoint umkonfigurieren, mit Hilfe der Installationsanleitung. 

| Tätigkeit | Zeit |
|----------------------|--------|
| Raspberry Pi aufsetzen | 45min |
| Updates installieren | 30min |
| Netzwerkkonfiguration | 30min | 
| Konfiguration | 1.5h |
___

03 - Benötigte Hard- und Software
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


### Entscheidungsmatrix
![software](https://user-images.githubusercontent.com/47855918/67899501-b2676c80-fb62-11e9-94a1-779f72806b2e.png)

___

04 - Installationsanleitung
======

### Schritt 1
Als erstes wird der Raspberry Pi auf den neusten stand gebracht und die Access-Point Software installiert.
```
sudo apt-get update
sudo apt-get upgrade

sudo apt-get install hostapd bridge-utils
```

Schritt 2:
Nun wird die Konfigurations Datei des Access-Points angepasst. Dazu welchseln wir in das verzeichniss: 
sudo nano /etc/hostapd/hostapd.conf

Jetzt fügen wir folgende Konfigurations-Datei ein und passen in der Zeile 1 die SSID und in der Zeile 2 das Passwort an.
ssid=RaspberryAP
wpa_passphrase=WLANPASSWORT

driver=nl80211
country_code=DE
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

Schritt 3:

Aus Sicherheitsgründen wird die Berechtigung der Konfigurations-Datei so angepasst, das sie nur vom Owner gelesen und verändert werden kann.

sudo chmod 600 /etc/hostapd/hostapd.conf

Schritt 4:

Nun wird die Konfigurations-Datei des Netzwerkes bearbeitet, dazu wechseln wir ins folgende Verzeichniss:

sudo nano /etc/network/interfaces

Jetzt passen wir die Konfigurations-Datei folgendermassen an:

# WLAN
auto wlan0
allow-hotplug wlan0
iface wlan0 inet manual
wireless-power off

# Netzwerkbrücke
auto br0
iface br0 inet dhcp
bridge_ports eth0 wlan0 # build bridge
bridge_fd 0 # no forwarding delay
bridge_stp off # disable Spanning Tree Protocol

Schritt 5:

Zu gutter Letzt richten wir noch eine automatischen Start des AccessPoint ein, dazu wechseln wir ins folgende Verzeichniss: 

sudo nano /etc/default/hostapd

Und fügen folgende Textsequenz ein:

RUN_DAEMON=yes
DAEMON_CONF="/etc/hostapd/hostapd.conf"





___

05 - Testing
======

### Testprotokoll  

| Beschreibung     | Status |                               
| -------------|----------|
| Der Raspberry Pi ist pingbar  | :heavy_check_mark: |        
| Den Raspberry Pi ist als Access Point in der Wlan-Leiste sichtbar  | :heavy_check_mark: |		     
| Verbindung herstellen mit dem Rasperry Pi Access Point ist möglich  | :heavy_check_mark: |                                      
| Durch den Raspberry Pi Access Point ist eine Internetverbindung vorhanden| :heavy_check_mark: |
| Der zweite Rasperry Pi Access Point erfüllt die oben aufgelisteten Punkte | :heavy_check_mark: |
___

06 - Übergabe an den Betrieb
======

### Seperates Dokument (Übergabeprotokoll)



___

07 - Quellen
======

https://www.libe.net/raspberry-als-accesspoint

https://www.craftsmany.net/raspberry-pi-3-wifi-hotspot-access-point-erstellen/

https://developer-blog.net/raspberry-pi-als-wlan-access-point-einrichten/

https://www.randombrick.de/raspberry-pi-als-wlan-access-point-nutzen/

https://www.security-blog.eu/raspberry-pi-als-accesspoint-einrichten/

___
 
