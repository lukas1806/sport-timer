# Sport Timer

Mobile, statische Trainings-App für GitHub Pages – ohne Build-Prozess und ohne Abhängigkeiten. Die komplette Anwendung befindet sich in [`index.html`](index.html): HTML, CSS, Workout-Konfiguration und JavaScript.

## Aktueller Funktionsumfang

- **Stoppuhr:** frei laufende Stoppuhr mit Start, Stopp, Fortsetzen und Neustart.
- **Tabata:** frei einstellbarer Sport-/Pausen-Timer mit Start, Stopp und Reset.
- **Workout:** Auswahl geführter Workouts. Das erste Workout ist **Morning 100** (16:20 Minuten): vier Aufwärmübungen, fünf Runden und drei Abschlussübungen.
- **Steuerung:** Pause/Fortsetzen hält die Restzeit an; Beenden kehrt zur Workout-Auswahl zurück; Neustart beginnt das Workout bei 0.
- **Darstellung:** aktuelle Übung, Runde, Countdown, Gesamtfortschritt und die *nächste echte Übung*. Wechselzeiten und Pausen werden in der Vorschau bewusst übersprungen.
- **Gerätefunktionen:** Sprachansagen und Signaltöne können ein-/ausgeschaltet werden und werden im Local Storage gespeichert. Wake Lock hält den Bildschirm – falls vom Browser unterstützt – während des Trainings wach.

Die Restzeit wird aus echten Zeitstempeln berechnet, nicht durch bloßes Herunterzählen. Dadurch bleibt der Timer nach einem kurzen Wechsel in den Hintergrund korrekt.

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

Die Workout-Phasen stehen im JavaScript-Block in `index.html` im Array `workout`. Eine Phase wird mit dem Helfer `phase(...)` beschrieben:

```js
phase("Name der Übung", 30, "work", { round: 1, reps: 12 })
```

Verwende dabei diese Typen:

- `warm` für Aufwärmübungen
- `work` für Belastungsübungen innerhalb einer Runde
- `transition` für stumme Wechselzeiten
- `rest` für Pausen
- `cooldown` für Abschlussübungen

Für ein vollständig neues, auswählbares Workout muss die Anwendung von der einzelnen Variablen `workout` auf eine Workout-Liste mit einer aktiven Auswahl erweitert werden. Dabei dürfen die generischen Funktionen für `isExercise`, `nextRealExercise`, `enterPhase` und `tickRun` nicht durch workout-spezifische Sonderlogik ersetzt werden: Sie sorgen dafür, dass die Regeln aus der Tabelle für alle Workouts einheitlich angewendet werden.

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
