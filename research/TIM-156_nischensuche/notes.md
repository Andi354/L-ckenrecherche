# Nischensuche Frontier AI (TIM-156)

Auftrag: Linear TIM-156, Abschnitt "Forschungsauftrag". Skala fest: Score = Lücke × Nachfrage × Machbarkeit (je 0–5).
Fortsetzen: Auftrag lesen, dann diese Datei, dann die letzten Zeilen von `log.tsv`.

## Stand (wird überschrieben)
- Start der Recherche: 2026-11-13 18:50 UTC. Budget 2–4 h, also weiche Frist 22:50 UTC.
- Runde: 1. Scans der sechs Achsen fertig, 14 Ideen im Backlog, Kurzprüfung (Haiku) läuft.
- Top-Kandidaten: noch keine.
- Nächster Schritt: Kurzprüfung auswerten, vorläufige Scores, Tiefenprüfung (Opus) der Besten.

## Lehren (nur anhängen)
- L1 (K01, K02): Reines Verhaltens-Messen von Regelbefolgung bei Coding-Agenten ist 2026 dicht besetzt, etwa eine neue Arbeit pro Monat (Gamage, McMillan, SKILL-USE, SkillClash, Sun et al.). Die Kurzprüfung mit einer Suche hat das nicht gesehen: "nichts Direktes gefunden" in der Kurzprüfung ist kein Beleg für eine Lücke. Ähnliche Ideen (reine Messung auf Achse 3) niedriger einstufen.
- L2: Abruf-Limit 100 WebFetch pro Stunde über alle Agenten. Tiefenprüfungen nacheinander oder knapp halten.

## Ideen-Backlog
Kritikzeilen Runde 1 (ID | Achse | Idee → Mechanismus | Größe | Rating | Quelle):
- K01 | 3 | Warum Regelbefolgung in Coding-Agenten in der Sitzung abfällt: Kontextlänge gegen Zahl der Tool-Calls gegen Regeltyp trennen, Wiedereinblenden als kausaler Test → McMillan nennt Mechanismus offen, Tim hat Daten | M | hoch | Scan A3 (2605.10039)
- K02 | 3 | Skill-Fehler zerlegen: nicht geladen gegen geladen aber ignoriert → OCTOBENCH nennt Skills als Engpass ohne Erklärung | M | hoch | Scan A3 (2601.10343)
- K03 | 2×3 | Probe "Regel noch zugänglich" in kleinem offenem Coding-Agenten über Mehrschritt-Trajektorie, sagt sie die Verletzung vorher → überträgt "When Attention Closes" auf Agenten | L | hoch | Scan A2/A3 (2605.12922)
- K04 | 2 | Attribution Graph auf stilisiertem Kontext Regel plus Tool-Wahl: welcher Pfad überstimmt die Regel → nutzt Tims Thesis-Werkzeug | L | mittel | Scan A2
- K05 | 2 | Probes für Tool-Entscheidung über mehrere Schritte statt Einzelschritt | M | mittel | Scan A2 (2604.01202)
- K06 | 1 | API gegen GUI gegen Hybrid auf denselben Aufgaben, mehrere Frontier-Modelle, pass^k und Kosten | L | mittel | Scan A1 (MCPWorld, OSWorld-MCP)
- K07 | 1×2 | Warum Agenten bereitstehende Tools nicht nutzen (Aufrufrate 11–36 % in OSWorld-MCP) | M | mittel | Scan A1
- K08 | 5×3 | Schwache Monitore für nicht böswillige Regelverstöße in Alltags-Coding-Sitzungen statt Sabotage | M | hoch | Scan A5
- K09 | 4×3 | Regelverstöße als Annotationsschicht auf öffentlichen Trajektorien (SWE-chat), Vorhersage aus dem Verlauf | M | mittel | Scan A4
- K10 | 6×3 | Regelbefolgung kleiner offener Modelle mit Skills messen (Compliance statt Aufgabenerfolg), Destillation regelkonformer Trajektorien | L | mittel | Scan A6
- K11 | 6 | Selbst erzeugte gegen kuratierte Skills bei kleinen Modellen | M | mittel | Scan A6 (SkillsBench)
- K12 | 4×5 | Fehlervorhersage im Lauf aus Aktivierungen kleiner offener Agenten | L | mittel | Scan A4 (CatchBench)
- K13 | 5×3 | Kündigt das sichtbare Reasoning den Regelverstoß an (verbalisiert gegen still)? CoT-Monitorability für Regelverstöße | M | hoch | Scan A5 (2512.18311)
- K14 | 1 | Hochbudget-Leistung aus billigen Läufen schätzen (offene Frage UK AISI) | M | mittel | Scan A1 (AISI-Blog)

## Änderungen im Original (nur anhängen)
- Keine. Das Repo war leer; der Zweig `research/TIM-156` ist der einzige Zweig.
