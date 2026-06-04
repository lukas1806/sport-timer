# GitHub Pages Einrichtung

Diese Datei dokumentiert, wie dieses Projekt auf GitHub und GitHub Pages veroeffentlicht wurde.

## Repository

Lokaler Projektordner:

```text
/Users/lukasoswald/Documents/Projects/sport-timer
```

GitHub-Repository:

```text
https://github.com/lukas1806/sport-timer
```

Live-Webseite:

```text
https://lukas1806.github.io/sport-timer/
```

## Warum ein eigenes Repository?

Es gab bereits ein anderes GitHub-Projekt namens `dinner-diary`. Dieses Projekt sollte davon nicht betroffen sein.

Deshalb wurde fuer den Tabata-Timer ein eigenes Repository namens `sport-timer` verwendet. Git arbeitet ordnerbezogen: Solange in GitHub Desktop oben links `sport-timer` als aktuelles Repository ausgewaehlt ist, werden keine Aenderungen am anderen Repository `dinner-diary` gemacht.

## Was eingerichtet wurde

1. Der vorhandene Projektordner `sport-timer` wurde genutzt.
2. Die bestehende `index.html` wurde zur fertigen Timer-App erweitert.
3. Im Ordner wurde ein eigenes lokales Git-Repository initialisiert.
4. Das lokale Repository wurde in GitHub Desktop als bestehendes Repository hinzugefuegt.
5. Das Repository wurde unter dem Namen `sport-timer` zu GitHub veroeffentlicht.
6. GitHub Pages wurde in den Repository-Settings aktiviert.

## GitHub Pages Einstellungen

In GitHub wurden diese Einstellungen gesetzt:

- Bereich: `Settings` -> `Pages`
- Source: `Deploy from a branch`
- Branch: `main`
- Folder: `/(root)`
- HTTPS: aktiviert

Diese Einstellung ist richtig, weil die Datei `index.html` direkt im Hauptordner des Repositories liegt.

## Wann ist die Webseite erreichbar?

Die Webseite bleibt erreichbar, solange:

- der GitHub-Account `lukas1806` existiert
- das Repository `sport-timer` existiert
- GitHub Pages fuer dieses Repository aktiviert bleibt
- die Datei `index.html` im Branch `main` im Hauptordner liegt

Die Seite verschwindet normalerweise nicht automatisch. Sie waere nur nicht mehr erreichbar, wenn zum Beispiel das Repository geloescht, umbenannt, privat gestellt, GitHub Pages deaktiviert oder die `index.html` entfernt beziehungsweise fehlerhaft geaendert wird.

## Aenderungen veroeffentlichen

Wenn spaeter eine Aenderung an der Webseite gemacht wird:

1. In GitHub Desktop sicherstellen, dass oben links `sport-timer` ausgewaehlt ist.
2. Dateien bearbeiten, meistens `index.html`.
3. In GitHub Desktop eine Commit-Nachricht eintragen.
4. Auf `Commit to main` klicken.
5. Auf `Push origin` klicken.
6. Einige Sekunden bis Minuten warten, bis GitHub Pages aktualisiert ist.

Danach ist die neue Version wieder unter dieser URL erreichbar:

```text
https://lukas1806.github.io/sport-timer/
```

## iPhone-Test

Auf dem iPhone in Safari oeffnen:

```text
https://lukas1806.github.io/sport-timer/
```

Danach pruefen:

- Start startet den Timer.
- Stopp pausiert den Timer.
- Start nach Stopp setzt fort.
- Reset setzt Runde auf 0.
- Sport- und Pausenphase wechseln automatisch.
- Plus/Minus sind waehrend des laufenden Timers deaktiviert.
- Die Statusanzeige fuer Bildschirm-Wachhalten erscheint.

Optional kann die Seite in Safari ueber Teilen -> `Zum Home-Bildschirm` als App-Symbol auf dem iPhone abgelegt werden.
