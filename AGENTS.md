# Hinweise für zukünftige Änderungen

Dieses Repository enthält eine statische mobile Workout-App in `index.html`. Es gibt absichtlich keinen Paketmanager, Build-Schritt oder ein Framework. Änderungen sollen die schlanke, GitHub-Pages-taugliche Struktur beibehalten.

## Nicht verändern ohne ausdrücklichen Wunsch

- Die Tabs **Stoppuhr**, **Tabata** und **Workout** bleiben erhalten.
- Workout-Steuerung: **Pause** hält an, **Fortsetzen** läuft mit der korrekten Restzeit weiter, **Beenden** führt zur Workout-Auswahl zurück, **Neustart** beginnt bei 0.
- Der Timer muss weiterhin aus Zeitstempeln (`Date.now()`) berechnet werden, damit Hintergrundwechsel keine Zeit verfälschen.
- Die Karte „Nächste Übung“ darf nur Phasen mit `warm`, `work` oder `cooldown` nennen, niemals `transition` oder `rest`.

## Einheitliche Audio-Regeln für jedes Workout

Die Funktionen `isExercise`, `enterPhase` und `tickRun` implementieren diese Regeln zentral. Sie müssen bei neuen Workouts unverändert weiter gelten:

1. Bei einer echten Übung (`warm`, `work`, `cooldown`) spricht die App ausschließlich den Namen der Übung.
2. Es gibt keine Ansagen für Dauer, Wiederholungen, Runden, Halbzeit, Wechsel, Pausen, „Noch zehn Sekunden“, Countdown-Zahlen oder Workout-Ende.
3. Wechselzeiten (`transition`) sind sprachlos.
4. In der Mitte jeder echten Übung ertönt genau ein kurzer Ton. Bei 30 Sekunden also nach 15 Sekunden, bei 20 Sekunden nach 10 Sekunden.
5. Nur bei echten Übungen ertönen einzelne Töne bei 3, 2 und 1 Sekunden Restzeit. Pausen und Wechselzeiten bekommen weder Halbzeit- noch Countdown-Töne.
6. Die Ton-Markierungen `midpointPlayed` und `countdownTones` werden bei jeder neuen Phase zurückgesetzt. Nicht entfernen: Sie verhindern, dass Töne in späteren Runden oder bei einem unregelmäßigen Timer-Takt fehlen.

## Neue Workouts ergänzen

Die aktuelle Konfiguration `workout` ist ein einzelnes Array im JavaScript von `index.html`. Wenn ein zweites auswählbares Workout ergänzt wird, diese Konfiguration in eine Liste von Workout-Objekten überführen und das gewählte Objekt als aktives Workout verwenden. Die Ablauf- und Audio-Logik darf dabei nicht dupliziert werden.

Jede Phase wird über `phase(name, seconds, type, options)` definiert. Erlaubte Typen:

- `warm`: Aufwärmübung
- `work`: Belastungsübung
- `transition`: Wechselzeit
- `rest`: Pause
- `cooldown`: Abschlussübung

Für neue Workouts immer Kachel, Detailansicht, Phasenkonfiguration, Gesamtdauer und Abschlusswerte ergänzen. Danach lokal testen: Reihenfolge, echte Restzeit nach Pause, Neustart, Beenden, Halbzeitton, 3-2-1-Töne und „Nächste Übung“-Vorschau.
