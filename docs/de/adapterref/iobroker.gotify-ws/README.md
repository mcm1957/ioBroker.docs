---
translatedFrom: en
translatedWarning: Wenn Sie dieses Dokument bearbeiten möchten, löschen Sie bitte das Feld "translationsFrom". Andernfalls wird dieses Dokument automatisch erneut übersetzt
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/de/adapterref/iobroker.gotify-ws/README.md
title: ioBroker.gotify-ws
hash: 7ZfcQLE4vzTByHNxXthzOoL0iaydL0n0MW1hS0f3g14=
---
![Logo](../../../en/adapterref/iobroker.gotify-ws/admin/gotify-ws.png)

![Anzahl der Installationen](http://iobroker.live/badges/gotify-ws-stable.svg)
![NPM-Version](http://img.shields.io/npm/v/iobroker.gotify-ws.svg)
![Downloads](https://img.shields.io/npm/dm/iobroker.gotify-ws.svg)
![Bekannte Schwachstellen](https://snyk.io/test/github/simatec/ioBroker.gotify-ws/badge.svg)
![Lizenz](https://img.shields.io/github/license/simatec/ioBroker.gotify-ws?style=flat)
![Spenden](https://img.shields.io/badge/paypal-donate%20|%20spenden-blue.svg)
![](https://img.shields.io/static/v1?label=Sponsor&message=%E2%9D%A4&logo=GitHub&color=%23fe8e86)

# IoBroker.gotify-ws
![Testen und Freigeben](https://github.com/simatec/ioBroker.gotify-ws/workflows/Test%20and%20Release/badge.svg)

Dieser Adapter verwendet den Dienst `Sentry.io`, um mir als Entwickler automatisch Ausnahmen und Codefehler sowie neue Geräteschemata zu melden. Weitere Details siehe unten!

---

## Adapterentwicklung unterstützen
**Wenn Ihnen ioBroker.gotify-ws gefällt, denken Sie bitte über eine Spende nach:**

[![paypal](https://www.paypalobjects.com/en_US/DK/i/btn/btn_donateCC_LG.gif)](https://paypal.me/mk1676)

---

## Gotify-ws-Adapter für ioBroker
Gotify-WS ist ein Adapter, der eine WebSocket-Verbindung zu einem Gotify-Server aufbaut und somit alle Nachrichten vom Server empfangen und verarbeiten kann.

Hintergrund war für mich eine fehlende Anbindung an alle gängigen Systeme.
Beispielsweise gibt es keine richtige App für IOS.

Da Gotify jedoch immer beliebter wird und mittlerweile auch in vielen Systemen wie beispielsweise Proxmox als Benachrichtigungsdienst Einzug gehalten hat, brauchte ich eine Lösung.

Hier kommt Gotify-WS ins Spiel.
Gotify-WS empfängt Nachrichten und leitet diese an einen von ioBroker unterstützten Benachrichtigungsdienst weiter. So können Nachrichten beispielsweise an Telegram weitergeleitet werden.

Spotify-WS unterstützt derzeit die folgenden Benachrichtigungsdienste

* E-Mail
* Matrix
* Benachrichtigungs-Manager
* Schwächling
* Zwietracht
* Signal
* Telegram
* WhatsApp

---

## Adapterkonfiguration
Die Konfiguration des Adapters ist sehr einfach.

Du erstellst einen neuen Client auf deinem Gotify-Server und kopierst den generierten Token des Clients.
Diesen trägst du in die Gotify-WS-Adapterkonfiguration ein.
Gotify-WS benötigt außerdem die IP-Adresse bzw. Domain und den Port des Gotify-Servers.

Dadurch wird eine Verbindung hergestellt und der Adapter kann alle eingehenden Nachrichten vom Gotify-Server empfangen.

Zur Weiterleitung können Sie anschließend einen Benachrichtigungsdienst Ihrer Wahl konfigurieren.

--- <!-- ### **IN ARBEIT** -->

## Changelog
### **WORK IN PROGRESS**
* (simatec) Fix Adapter Check
* (simatec) Dependencies updated

### 0.1.5 (2024-07-22)
* (simatec) small fix

### 0.1.4 (2024-07-19)
* (simatec) Dependencies updated

### 0.1.3 (2024-07-17)
* (simatec) Fix Test & Release
* (simatec) Fix Timeout

### 0.1.2 (2024-06-26)
* (simatec) Fix io-package
* (simatec) Notification-Manager added

### 0.1.1 (2024-06-19)
* (simatec) Fix Branch

### 0.1.0 (2024-06-19)
* (simatec) First Release

### 0.0.1 (2024-03-15)
* (simatec) initial release

---

## License

MIT License

Copyright (c) 2024 simatec

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.