# Sport Timer

Mobile, statische Trainings-App für GitHub Pages – ohne Build-Prozess und ohne Abhängigkeiten. Die komplette Anwendung befindet sich in [`index.html`](index.html): HTML, CSS, Workout-Konfiguration und JavaScript.

## Aktueller Funktionsumfang

- **Stoppuhr:** frei laufende Stoppuhr mit Start, Stopp, Fortsetzen und Neustart.
- **Tabata:** frei einstellbarer Sport-/Pausen-Timer mit Start, Stopp und Reset.
- **Workout:** Auswahl geführter Workouts. Enthalten sind **Morning 100** (16:20 Minuten), **300** (rundenbasiert), **Chinesische Morgenroutine** (8 Minuten) sowie **AMRAP 24 + 12 Kettlebell** (20 Minuten).
- **Steuerung:** Pause/Fortsetzen hält die Restzeit an; Beenden kehrt zur Workout-Auswahl zurück; Neustart beginnt das Workout bei 0.
- **Darstellung:** aktuelle Übung, Runde, Countdown, Gesamtfortschritt und die *nächste echte Übung*. Wechselzeiten und Pausen werden in der Vorschau bewusst übersprungen.
- **Gerätefunktionen:** Sprachansagen und Signaltöne können ein-/ausgeschaltet werden und werden im Local Storage gespeichert. Wake Lock hält den Bildschirm – falls vom Browser unterstützt – während des Trainings wach.

Die Restzeit wird aus echten Zeitstempeln berechnet, nicht durch bloßes Herunterzählen. Dadurch bleibt der Timer nach einem kurzen Wechsel in den Hintergrund korrekt.

## Workout „300“

Das Workout 300 besteht aus zehn Runden mit jeweils 10 Liegestützen, 10 Squats und 10 Sit-Ups. Es misst die Zeit bis zum Abschluss; es gibt keine vorgegebenen Übungszeiten und keine Audiohinweise.

- Der große Button **„+1 Runde geschafft“** zählt die aktuelle Runde hoch.
- Mit **−** kann eine versehentlich gezählte Runde während des laufenden Workouts wieder abgezogen werden.
- Nach der zehnten Runde wird das Workout automatisch beendet.
- **Fertig** beendet ein Workout vorzeitig; eine solche Zeit wird nicht als Rekord gewertet.
- Der persönliche Rekord wird im Local Storage gespeichert. Der anfängliche Rekord beträgt 9:23. Nach einer vollständigen, schnelleren Zeit fragt die App ausdrücklich, ob sie als neuer Rekord gespeichert werden soll.
- Die drei lokalen Übungsillustrationen liegen unter `assets/`.

## Chinesische Morgenroutine

Die chinesische Morgenroutine besteht aus acht direkt aufeinanderfolgenden Ein-Minuten-Übungen: Lymphatic Hops, Body Waves, Alternate Arm Swings, Trunk Twists, Chest Opener, Golf Swings, Marches with Knee Slaps und Body Taps. Es gibt keine Übergangs- oder Pausenphase. Die mitgelieferte Übungen-Übersicht liegt als lokales, für den dunklen Hintergrund hell dargestelltes Bild unter `assets/chinese-morning-routine.png`.

## AMRAP 24 + 12 Kettlebell

Dieses Workout läuft 20 Minuten rückwärts. Pro Runde werden 6 Kettlebell Swings, 6 Squats, 6 Kettlebell Overhead Presses, 6 Push-Ups und 12 Lunges erledigt; danach beginnt die Reihenfolge wieder von vorn. Die fünf Übungskacheln bleiben während des Trainings sichtbar.

- **+1** und **−** zählen abgeschlossene Runden während der laufenden Zeit und korrigieren Fehlklicks.
- Nach Ablauf der 20 Minuten oder über **Fertig** erscheint die absolvierte Rundenzahl.
- Der anfängliche Rekord beträgt 13 Runden. Nur bei mehr Runden wird angeboten, den Rekord nach ausdrücklicher Bestätigung lokal zu speichern.
- Das AMRAP ist rundenbasiert und löst keine Sprach- oder Countdown-Signale aus.

## Feste Regeln für geführte Workouts

Diese Regeln gelten für Morning 100 und müssen für jedes weitere geführte Workout beibehalten werden:

| Situation | Verhalten |
| --- | --- |
| Start einer echten Übung | Ein kurzer Signalton; die Sprachausgabe nennt **nur den Übungsnamen**. Keine Wiederholungszahl, Dauer, Rundenansage oder „Los“. |
| Wechselzeit | Keine Sprachausgabe. |
| Pause | Keine Sprachausgabe und kein Halbzeit- oder 3-2-1-Signal. |
| Halbzeit einer echten Übung | Ein kurzer Signalton exakt bei der Hälfte der Dauer, z. B. bei 15 Sekunden Restzeit in einer 30-Sekunden-Übung und bei 10 Sekunden Restzeit in einer 20-Sekunden-Übung. |
| Letzte drei Sekunden einer echten Übung | Je ein Signalton bei 3, 2 und 1 Sekunden Restzeit; keine gesprochenen Zahlen. |
| Workout-Ende | Abschlussansicht ohne zusätzliche Sprachausgabe. |

Als „echte Übung“ gelten die Phasentypen `warm`, `work` und `cooldown`. Die Typen `transition` und `rest` sind davon ausdrücklich ausgenommen. Die Logik verwendet pro Übung gespeicherte Ton-Markierungen, damit die Halbzeit- sowie 3-2-1-Töne auch bei gelegentlichen verzögerten Browser-Takten und in späteren Runden nicht ausfallen.

## Weiteres Workout hinzufügen

Die Phasen für Morning 100 und die chinesische Morgenroutine stehen im JavaScript-Block in `index.html`. Für den Ablauf wird die jeweils ausgewählte Konfiguration als aktives Array `workout` gesetzt. Eine Phase wird mit dem Helfer `phase(...)` beschrieben:

```js
phase("Name der Übung", 30, "work", { round: 1, reps: 12 })
```

Verwende dabei diese Typen:

- `warm` für Aufwärmübungen
- `work` für Belastungsübungen innerhalb einer Runde
- `transition` für stumme Wechselzeiten
- `rest` für Pausen
- `cooldown` für Abschlussübungen

Für ein neues geführtes Workout eine eigene Phasen-Konfiguration anlegen und sie beim Start als aktives `workout` setzen. Die generischen Funktionen für `isExercise`, `nextRealExercise`, `enterPhase` und `tickRun` dürfen dabei nicht durch workout-spezifische Sonderlogik ersetzt werden: Sie sorgen dafür, dass die Regeln aus der Tabelle für alle Workouts einheitlich angewendet werden.

Bei rundenbasierten Workouts wie **300** (For Time) oder **AMRAP 24 + 12 Kettlebell** ist dagegen eine separate, Zeit- und Rundenzähler-basierte Ansicht sinnvoll. Diese dürfen keine der geführten Audio-Regeln auslösen. For-Time-Rekorde werden nur bei erreichter Zielrundenzahl angeboten; AMRAP-Rekorde nur bei einer höheren Rundenzahl und stets erst nach ausdrücklicher Bestätigung gespeichert.

Für jedes neue Workout außerdem:

1. Eine Kachel in der Workout-Auswahl und eine passende Detailansicht mit Dauer, Runden und Zusammenfassung ergänzen.
2. Alle Phasen inklusive Wechselzeiten und Pausen in der richtigen Reihenfolge konfigurieren.
3. Dauer als Summe aller Phasen berechnen und in der Kachel anzeigen.
4. Prüfen, dass die „Nächste Übung“-Karte niemals `transition` oder `rest` ausgibt.
5. Start, Pause/Fortsetzen, Beenden, Neustart, Halbzeitton sowie die drei Countdown-Töne testen.

Details für KI- oder Entwickler-Änderungen stehen zusätzlich in [`AGENTS.md`](AGENTS.md).

## Lokal testen

```sh
python3 -m http.server 8000
```

Dann `http://127.0.0.1:8000/` öffnen. Für Sprachansagen, Signaltöne und Bildschirm-Wachhalten ist ein Test auf einem echten Smartphone-Browser empfehlenswert.
