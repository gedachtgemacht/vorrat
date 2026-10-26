# vorrat.

Behalte im Blick, was im Kühlschrank und im Vorratsschrank bald abläuft. Offline, ohne Konto, ohne Server. Alles bleibt auf deinem Handy.

<p align="center">
  <img src="bilder/1-liste.png" width="240" alt="">
  <img src="bilder/2-statistik.png" width="240" alt="">
  <img src="bilder/3-detail.png" width="240" alt="">
</p>

## Warum

In fast jedem Haushalt landen Lebensmittel im Müll, weil man vergisst, was wann abläuft. vorrat. macht das sichtbar: Produkt rein, Datum rein, fertig. Die App zeigt, was zuerst dran ist, und erinnert dich rechtzeitig. Keine KI, keine Werbung, kein Tracking.

## Funktionen

- **Schnell hinzufügen**: Barcode scannen oder Namen tippen, Ort wählen, Datum über Schnellwahl (+3 Tage bis +1 Jahr) oder Zifferneingabe (`251226` wird 25.12.2026, `2512` wird der nächste 25.12.).
- **MHD und Verbrauchsdatum** werden unterschieden. Abgelaufenes Verbrauchsdatum ist rot markiert („nicht mehr essen“), abgelaufenes MHD gelb („prüfen: sehen, riechen, schmecken“).
- **Barcode-Scanner** mit der Rückkamera. Nutzt den eingebauten `BarcodeDetector` (Chrome auf Android) und sonst eine eingebettete Bibliothek (iPhone, Safari, Firefox). EAN-13, EAN-8, UPC-A, UPC-E, Prüfziffer wird immer geprüft. Alternativ Foto vom Barcode wählen oder Nummer eintippen.
- **Produktgedächtnis**: Ein Barcode oder Name, den du schon mal hattest, füllt Name, Ort, Art und typische Haltbarkeit vor.
- **Geöffnet am**: Mit der Haltbarkeit nach dem Öffnen (z. B. Milch 3 Tage) gilt automatisch das frühere Datum.
- **Liste** gruppiert nach Abgelaufen, Heute und morgen, Diese Woche, Später. Filter nach Ort, Suche, Menge, Foto, Notiz.
- **Verbraucht oder Weggeworfen** mit Rückgängig. Daraus entsteht die **Statistik**: Rettungsquote für den Monat und gesamt, Balken der letzten 6 Monate, die am häufigsten weggeworfenen Produkte.
- **Erinnerungen**: lokale Benachrichtigung beim Öffnen (höchstens einmal am Tag) und Kalender-Export (.ics) aller Ablaufdaten der nächsten 60 Tage mit Alarm einen Tag vorher um 9 Uhr.
- **Export**: Vorrat und Verlauf als CSV (deutsches Excel), Sicherung als JSON inklusive Fotos, wieder einlesbar.
- Hell und dunkel, offline nutzbar nach dem ersten Aufruf.

## Datenschutz

Alle Daten liegen in IndexedDB im Browser auf deinem Gerät. Es gibt keinen Server und kein Konto.

Einzige Ausnahme, abschaltbar unter **Mehr, Einstellungen**: Beim Scannen eines unbekannten Barcodes fragt vorrat. [Open Food Facts](https://world.openfoodfacts.org) nach dem Produktnamen. Dabei wird nur die Barcode-Nummer gesendet, keine anderen Daten. Ohne Netz oder bei Zeitüberschreitung (4 Sekunden) tippst du den Namen einfach selbst.

## Installation

1. Den Ordner `vorrat/` auf einen beliebigen statischen Webhost legen (eigener Server, GitHub Pages, Netlify). Es gibt keinen Build-Schritt und keine Abhängigkeiten.
2. Die Adresse im Handybrowser öffnen.
3. Im Browsermenü **Zum Startbildschirm hinzufügen** wählen. Danach startet vorrat. wie eine App und läuft offline.

Die Kamera und Benachrichtigungen funktionieren nur über **HTTPS** (oder `localhost`). Auf dem iPhone gibt es Benachrichtigungen nur, wenn vorrat. auf dem Startbildschirm liegt. Ohne Kamera kannst du ein Foto vom Barcode wählen oder die Nummer eintippen.

Lokal testen:

```
cd vorrat
python3 -m http.server 8000
```

Dann `http://localhost:8000` öffnen.

## Technik

Eine einzelne `index.html` mit eingebetteten Schriften, Styles und Skripten, dazu Manifest, Service Worker und Icons. Keine CDNs, keine externen Abhängigkeiten zur Laufzeit.

Barcode-Fallback: eine Teilmenge von [ZXing for JS](https://github.com/zxing-js/library) (`@zxing/library` 0.23.0, nur die EAN/UPC-Leser), mit esbuild gebündelt und direkt eingebettet, rund 61 KB. Lizenz: Apache License 2.0, Copyright ZXing authors.

## Lizenz

GNU Affero General Public License v3.0 (AGPL-3.0), siehe `LICENSE`.

Ein Projekt von **gedacht.gemacht.**
