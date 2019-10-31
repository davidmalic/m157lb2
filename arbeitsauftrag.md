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
-   Raspberry Pi 3 (vorherige Modelle sind nicht kompatibel)
-   Micro USB Netzteil 
-   Micro SD Karte 
-   Netzwerk- und Internetverbindung

### Software
Hostapd

###### Entscheidungsmatrix
![software](https://user-images.githubusercontent.com/47855918/67899501-b2676c80-fb62-11e9-94a1-779f72806b2e.png)
___

04 - Installationsanleitung
======

### Schritt 1

Nachdem wir uns über Putty verbunden haben, sollten zuerst mal alle vorhanden Updates installiert werden:  
sudo apt-get update
sudo apt-get upgrade
### Schritt 2
___

05 - Qualitätskotrolle
======

Die Funktionalität, der Raspberry Pi Installation kann so getestet werden, indem man auf einem anderen WLAN fähigem Gerät  in der Nähe des Raspberry Pi’s, das WLAN-Netzwerk gesucht wird und verbunden wird.

### Commands für Überprüfung
iw dev wlan0 info  
iw dev wlan0 get power_save
___

06 - Error-Handling
======

hostapd kann auch mit folgendem Befehl gestartet werden. Im Terminal werden dabei Informationen zum Start, bzw. zu den verbundenen Geräten angezeigt:  
sudo hostapd -dd /etc/hostapd/hostapd.conf
___
