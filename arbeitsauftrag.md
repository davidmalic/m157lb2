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
___

02 - Einführung
======


___

03 - Materialliste
======

### Hardware
-   Raspberry Pi 3 (vorherige Modelle sind nicht kompatibel)
-   Micro USB Netzteil 
-   Micro SD Karte 
-   Netzwerk- und Internetverbindung

### Software

###### Entscheidungsmatrix

___

04 - Installationsanleitung
======

### Schritt 1

### Schritt 2
___

05 - Qualitätskotrolle
======

### Commands für Überprüfung
iw dev wlan0 info
iw dev wlan0 get power_save
___

06 - Error-Handling
======

### Wie haben wir die Fehler korriegiert, wie sind wir vorgegangen
sudo hostapd -dd /etc/hostapd/hostapd.conf
___
