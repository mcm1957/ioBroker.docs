---
translatedFrom: en
translatedWarning: Wenn Sie dieses Dokument bearbeiten möchten, löschen Sie bitte das Feld "translationsFrom". Andernfalls wird dieses Dokument automatisch erneut übersetzt
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/de/adapterref/iobroker.places/README.md
title: ioBroker.places
hash: IZ3xVAwrX/8hKuFdFHuCG8pIYwTjGTZIoShTd11M/vo=
---
![Logo](../../../en/adapterref/iobroker.places/admin/places.png)

![Anzahl der Installationen](http://iobroker.live/badges/places-stable.svg)
![NPM-Version](http://img.shields.io/npm/v/iobroker.places.svg)
![Downloads](https://img.shields.io/npm/dm/iobroker.places.svg)

# IoBroker.places
![Testen und freigeben](https://github.com/iobroker-community-adapters/ioBroker.places/workflows/Test%20and%20Release/badge.svg) [![Übersetzungsstatus](https://weblate.iobroker.net/widgets/adapters/-/places/svg-badge.svg)](https://weblate.iobroker.net/engage/adapters/?utm_source=widget)

**Dieser Adapter verwendet Sentry-Bibliotheken, um Ausnahmen und Codefehler automatisch an die Entwickler zu melden.** Weitere Details und Informationen zum Deaktivieren der Fehlerberichterstattung finden Sie unter [Sentry-Plugin-Dokumentation](https://github.com/ioBroker/plugin-sentry#plugin-sentry)! Sentry Reporting wird ab js-controller 3.0 verwendet.

## Beschreibung
Dies ist ein ioBroker-Adapter zur Verarbeitung von Standortinformationen, die mindestens einen Benutzer, eine Geo-Position und einen Zeitstempel enthalten sollten.
Der Adapter analysiert, ob sich die Standortinformationen in einem Umkreis um die Standortkonfiguration von ioBroker oder optional an anderen Orten befinden.

## Aufbau
Es gibt nur einen obligatorischen Konfigurationswert: den Radius (Meter), der verwendet wird, um den aktuellen Standort eines Benutzers zu identifizieren.
Der Standort von ioBroker wird verwendet, um Benutzer zu identifizieren, die "zu Hause" sind, andere Orte können als Teil der Konfiguration hinzugefügt werden.

* **Radius** (_mandatory_) sollte der Radius in Metern sein, der verwendet wird, um zu überprüfen, ob sich der Benutzer an einem bestimmten Ort befindet (zu Hause oder benutzerdefiniert).
* **Name for home** kann verwendet werden, um einen benutzerdefinierten Namen für den Heimatort festzulegen.
* **Google Maps-API-Schlüssel** wird zum Aktivieren der Geocodierung verwendet. Ein fehlender API-Schlüssel wird von einer konfigurierten Vis-Map-Instanz (falls verfügbar) abgerufen, wenn die Konfigurationsseite geöffnet wurde.
* **Google Maps Geocoding** kann aktiviert werden, um eine echte Adresse und eine Höhe für eine angegebene Geoposition zu erhalten.
* **Orte** ist eine flexible Liste mit benutzerdefinierten Orten, bei denen jeder Ort gültige Werte für Name, Breitengrad und Längengrad haben sollte.
* **Benutzer** ist eine flexible Liste mit Benutzerzuordnungen.

## Verwendungszweck
Um die Standortaktualisierung zu verarbeiten, senden Sie einfach eine Nachricht mit der folgenden Syntax:

```
// send a message to all instances of places adapter
sendTo('locations', {
        user:       "Name of person",
        latitude:   50.9576191,
        longitude:  6.8272409,
        timestamp:  1520932471
});

// send a message to a specific instance of places adapter adapter
sendTo('locations.0', {
        user:       "Name of person",
        latitude:   50.9576191,
        longitude:  6.8272409,
        timestamp:  1520932471
});

// send a message to a specific instance and define a callback
sendTo('locations.0', {
        user:       "Name of person",
        latitude:   50.9576191,
        longitude:  6.8272409,
        timestamp:  1520932471
}, function (res) { log(JSON.stringify(res)); });
```

## Struktur für zurückgegebene Nachrichten
Der folgende Block zeigt, wie Antwortnachrichten aussehen. Für jeden Wert hat der ioBroker-Objektbaum einen entsprechenden Zustand.

```
{
    "user":         "Name of person",       // name of person (may have been replaced by user mapping)
    "latitude":     50.9576191,
    "longitude":    6.8272409,
    "timestamp":    1520932471000,
    "date":         "2018-03-13 10:14:31",  // date extracted from timestamp
    "atHome":       false,                  // true if inside the configured radius around ioBroker
    "homeDistance": 104898,                 // distance in meters between position and ioBroker
    "name":         "",                     // name of place found within the configuration
    "address":      "",                     // readable address (if geocoding is active)
    "elevation":    "",                     // elevation in meters (if geocoding is active)
}
```

## Beispiel: OwnTracks + ioBroker.iot + ioBroker.places
### 1. Konfigurieren Sie iobroker.iot
Fügen Sie einen benutzerdefinierten Dienst **xyz** unter **Weiße Liste für Dienste** hinzu.

### 2. Konfigurieren Sie die mobilen Apps von OwnTracks
Ändern Sie den Modus auf **HTTP Private** und verwenden Sie die folgende Adresse als **Host** : https://iobroker.pro/service/custom_xyz/<user-app-key>

### 3. Konfigurieren Sie iobroker.places
Auf der Registerkarte Integration müssen Sie die Instanz des Cloud-Adapters und **xyz** als Dienst auswählen. Der Adapter hört auf eingehende Anforderungen für den Dienst und startet die Verarbeitung.

## Beispiel: Telegramm + ioBroker.telegram + ioBroker.places
### 1. Konfigurieren Sie iobroker.telegram
Aktivieren Sie die Option zum **Speichern von Rohanforderungen**.

### 2. Skript erstellen (ioBroker.javascript)
Erstellen Sie ein kurzes Skript mit einem Abonnement für die Rohanfrage, z. von **telegram.0.communicate.requestRaw**, und senden Sie ein neues Anforderungsobjekt an iobroker.places (oder eine Instanz davon):

```
on({id: "telegram.0.communicate.requestRaw", change: "ne"}, function (obj) {
    var data = JSON.parse(obj.newState.val);
    if (data.from && data.location) {
        sendTo('places.0', {
            user: data.from.first_name,
            latitude: data.location.latitude,
            longitude: data.location.longitude,
            timestamp: data.date
        }, function (res) { log('places analyzed telegram position as: ' + JSON.stringify(res)); });
    }
});
```

## Credits
Die Implementierung basiert teilweise auf dschaedls [ioBroker.geofency](https://github.com/ioBroker/ioBroker.geofency)-Adapter. Das Logo wurde von [Free Icons PNG](http://www.freeiconspng.com/images/maps-icon) und wurde modifiziert, um einen transparenten Hintergrund zu haben.

## Changelog
### 1.1.0 (2022-03-25)
* (Basgo) Correctly set ack flag
* (Apollon77) Add Sentry for crash reporting

### 1.0.0 (2020-08-16)
* (bluefox) Updated packages
* (bluefox) Refactoring

### 0.7.0 (2019-01-12)
* (BasGo) Added compact mode, replaced integration of iobroker.cloud with iobroker.iot

### 0.6.2 (2018-12-06)
* (bluefox) Error with blockly was fixed

### 0.6.1
* (BasGo) Added handling for invalid route details

### 0.6.0
* (BasGo) Changed implementation to use promises
* (BasGo) Added route details for driving home

### 0.5.1
* (BasGo) Extended help texts

### 0.5.0
* (BasGo) Added optional subscription for cloud adapter

### 0.4.2
* (BasGo) UI fixes

### 0.4.1
* (BasGo) Configuration dialog extended

### 0.4.0
* (BasGo) Google Maps can be used for configuration
* (BasGo) Geocoding can be activated

### 0.3.0
* (BasGo) Added user mappings

### 0.2.3
* (BasGo) Optimized state handling
* (BasGo) Added option to clear array

### 0.2.2
* (BasGo) Added check for newer entries

### 0.2.1
* (BasGo) Extended configuration

### 0.2.0
* (BasGo) Materialized admin page

### 0.1.1
* (BasGo) Fixed some smaller issues

### 0.1.0
* (BasGo) Initial release

## License

This adapter is licensed under the [MIT License](../blob/master/LICENSE) which is part of this repository.

Copyright (c) 2018-2022 BasGo <basgo@gmx.de>