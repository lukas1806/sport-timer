# Sport Timer

Ein einfacher Tabata-Timer als statische Webseite.

Live-Seite:

https://lukas1806.github.io/sport-timer/

## Was gebaut wurde

Dieses Projekt enthaelt eine einzelne `index.html`, in der HTML, CSS und JavaScript direkt zusammenliegen. Es gibt keine externen Libraries, keinen Build-Prozess und keine weiteren Abhaengigkeiten.

Die App ist fuer die Nutzung auf dem iPhone in Safari gedacht und funktioniert auch als normale Webseite auf Desktop-Browsern.

## Funktionen

- Tabata-Timer mit Sport- und Pausenphase
- Standard-Sportzeit: 40 Sekunden
- Standard-Pausenzeit: 20 Sekunden
- Sportzeit und Pausenzeit per Plus/Minus einstellbar
- Mindestwert: 5 Sekunden
- Start, Stopp und Reset
- Start setzt nach Stopp an der aktuellen Zeit fort
- Reset setzt die Runde auf 0 und springt zur Sportphase zurueck
- Automatischer Wechsel zwischen Sport und Pause
- Nach jeder Sportphase wird die Rundenzahl um 1 erhoeht
- Klare optische Unterscheidung zwischen Sport und Pause
- Grosse verbleibende Zeit
- Zeiten koennen nur geaendert werden, wenn der Timer nicht laeuft
- Timer-Logik basiert auf `setInterval`

## iPhone- und Safari-Anpassungen

Die `index.html` enthaelt Meta-Tags fuer mobile Nutzung:

- `viewport`
- `theme-color`
- `mobile-web-app-capable`
- `apple-mobile-web-app-capable`
- `apple-mobile-web-app-title`
- `apple-mobile-web-app-status-bar-style`

Ausserdem nutzt die App die Screen Wake Lock API, wenn sie im Browser verfuegbar ist:

- Beim Start wird versucht, den Bildschirm wachzuhalten.
- Bei Stopp und Reset wird der Wake Lock freigegeben.
- Nach Rueckkehr in den sichtbaren Tab wird Wake Lock erneut angefordert, falls der Timer laeuft.
- Wenn Wake Lock nicht verfuegbar oder blockiert ist, funktioniert der Timer trotzdem normal weiter.
- Eine kleine Statusanzeige zeigt an, ob Bildschirm-Wachhalten aktiv, verfuegbar, blockiert oder nicht verfuegbar ist.

## Dateien

- `index.html`: komplette Timer-App
- `.gitignore`: ignoriert lokale macOS-Dateien wie `.DS_Store`
- `README.md`: diese Projektdokumentation
- `GITHUB_PAGES.md`: Dokumentation zur GitHub- und GitHub-Pages-Einrichtung

## Lokales Testen

Die Datei kann direkt im Browser geoeffnet werden. Fuer einen realistischeren Test als Webseite kann im Projektordner ein lokaler Server gestartet werden:

```sh
python3 -m http.server 8000
```

Danach ist die lokale Version erreichbar unter:

```text
http://127.0.0.1:8000/
```

## Spaetere Aenderungen

Wenn spaeter etwas am Timer geaendert wird:

1. `index.html` bearbeiten
2. In GitHub Desktop die Aenderungen ansehen
3. Commit erstellen
4. Push zu GitHub ausfuehren
5. GitHub Pages aktualisiert die Live-Seite automatisch nach kurzer Zeit
