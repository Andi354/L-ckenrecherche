# Nischensuche Frontier AI (TIM-156)

Auftrag: Linear TIM-156, Abschnitt "Forschungsauftrag". Skala fest: Score = Lücke × Nachfrage × Machbarkeit (je 0–5).
Fortsetzen: Auftrag lesen, dann diese Datei, dann die letzten Zeilen von `log.tsv`.

## Stand (wird überschrieben)
- Start der Recherche: 2026-11-13 18:50 UTC. Budget 2–4 h, also weiche Frist 22:50 UTC.
- Runde: 4 läuft (Tiefenprüfung K23+K24, Kurzprüfung K22). Runde 3 abgeschlossen.
- Top-Kandidaten nach Runde 3: K19b 60, K13b 45, K01b 36 (dann K08b 32, K16 30). Top 3 hat sich gegenüber Runde 2 geändert, also noch nicht stabil.
- Nächster Schritt: Runde 4 auswerten; wenn Top 3 stabil: Zweitbewerter (Top 5 blind), Prüfer, Bericht.

## Lehren (nur anhängen)
- L1 (K01, K02): Reines Verhaltens-Messen von Regelbefolgung bei Coding-Agenten ist 2026 dicht besetzt, etwa eine neue Arbeit pro Monat (Gamage, McMillan, SKILL-USE, SkillClash, Sun et al.). Die Kurzprüfung mit einer Suche hat das nicht gesehen: "nichts Direktes gefunden" in der Kurzprüfung ist kein Beleg für eine Lücke. Ähnliche Ideen (reine Messung auf Achse 3) niedriger einstufen.
- L2: Abruf-Limit 100 WebFetch pro Stunde über alle Agenten. Tiefenprüfungen nacheinander oder knapp halten.

- L3 (K08, K13): Labs betreiben Monitore für "overeager"-Verhalten schon im Produkt. Offen sind nur enge Schnitte mit prüfbarer Ground Truth. Nachfrage für "benigne Regelverstöße" ist nirgends wörtlich belegt, nur abgeleitet: Nachfrage dort höchstens 4, eher 3.
- L4 (K13): Claude- und OpenAI-APIs liefern kein rohes Reasoning. Alles, was CoT braucht, geht sauber nur mit offenen Reasoning-Modellen. Tims eigene Logs taugen dafür nicht.
- L5 (K13): "Vergessen" gegen "bewusst übergangen" ist die Unterscheidung, an der Verhaltens-Messungen scheitern. Genau dort helfen Interna (Probes). Das hebt Ideen auf der Brücke Achse 2 x 3 x 5.
- L6 (Runde 2): Das Abruf-Limit (100 pro Stunde, nur WebFetch, kein direkter Netzzugang) war nach den ersten Tiefenprüfungen erschöpft. Runde 2 beruht bei K13b/K15/K16 großteils auf Titeln. Diese Scores sind vorläufig, bis die Pflichtlektüre gelesen ist: 2608.02089, 2607.07405, 2608.12323, 2608.09867, 2608.12321, 2604.28031, ICML "Decomposing Smooth Agentic Inference Scaling", claude-md-doctor.
- L7 (K15): Probes für verbotene Aktionen in offenen Tool-Agenten gibt es seit Oktober 2026 (The Agent Knew). Zwei Arbeiten widersprechen sich dabei: Fomin et al. (Probes lesen die Situation, nicht die Aktion) gegen Fayyazi et al. (AUROC 0,94). Ein Widerspruch zwischen zwei frischen Arbeiten ist eine konkrete Lücke.
- L8 (Runde 3): CAPE-Bench (206.697 Episoden, 4 offene Modelle, Reasoning je Zug, Verstoß-Labels, CC-BY-4.0, Code offen) ist ein öffentlicher Hebel: Projekte darauf brauchen keine eigene Datenerzeugung. Das hebt die Machbarkeit aller Kandidaten, die darauf aufsetzen, auf 5.
- L9 (Runde 3): "Vergessen" ist als Ursache von Regelverstößen widerlegt (2604.28031, 2608.12321). Der Engpass liegt im Routing von Wissen zu Handlung. Mechanistische Fragen sollten dort ansetzen.
- L10 (Runde 3): Probe-Monitoring bei Agenten bewegt sich im Wochentakt (drei Arbeiten in vier Wochen). Was dort liegt, hat hohes Überhol-Risiko, braucht aber wenig Aufwand.
- Korrektur: K18 steht im Log mit Nachfrage 2 (Score 24). Im Thread-Update nach Runde 2 stand fälschlich 36.

## Ideen-Backlog
Runde 4:
- K23 | 2x3 | Wo scheitert das Routing von Regelwissen zur Handlung? Activation Patching / Attribution auf CAPE-Bench-Entscheidungszügen (Gemma oder gpt-oss): überträgt 2608.12321 von pragmatischem Schließen auf Tool-Agenten | L | hoch (wegen L9, L8) | Runde 3; ersetzt K04
- K24 | 5x2 | Was bleibt dem Monitor, wenn Reasoning zusammengefasst oder verborgen ist? Auf CAPE-Bench: Text-Monitor auf roher CoT, auf Zusammenfassung, nur auf Aktionen, gegen Probe. Gewinnt die Probe ihren Vorteil zurück, sobald die CoT wie in Produktions-APIs fehlt? | M | hoch (wegen L8, L4) | Zusammenführung K13b+K16+K19b
- K22 | 3 | Wirkt eine aufgeschriebene Regel? Natürliches Experiment in Tims Logs | M | mittel | noch ohne Kurzprüfung
Runde 3:
- K19 | 2x5 | Lesen Probes für verbotene Aktionen die Situation oder die Absicht? Widerspruch Fomin et al. gegen "The Agent Knew" auflösen: Replikation auf gpt-oss-20b mit Kontrollen (gleiche Situation, andere Aktion) → nutzt Interp-Werkzeug, eine GPU | M | hoch (wegen L7) | Tiefenprüfung K15
- K22 | 3 | Wirkt eine aufgeschriebene Regel? Natürliches Experiment in Tims eigenen Logs: Wiederholungsrate eines Fehlers vor und nach dem Eintrag in CLAUDE.md/Skill | M | mittel | eigene Daten
- Pflichtlektüre aus L6 (entscheidet über K13b, K16, K15, K14, K08b).
Runde 2:
- K15 | 2x3x5 | Vergessen oder übergangen? Bei Regelverstößen offener Reasoning-Agenten 2x2 aus roher CoT (Regel erwähnt ja/nein) und Probe (Regel intern dekodierbar ja/nein) → trennt stilles Übergehen von Vergessen, nutzt Tims Interp-Werkzeug | L | hoch (wegen L5) | eigene Idee aus K03+K13b
- K16 | 5 | Was verliert ein Monitor durch zusammengefasstes statt rohes Reasoning? Offene Modelle mit roher CoT, Summarizer dazwischen, Monitor-Recall vorher/nachher | M | hoch (SHUSHCAST-Beobachtung bei Claude) | Tiefenprüfung K08
- K18 | 4x3 | Dunkelziffer: Regelverstöße in echten Sitzungen, die kein Nutzer-Pushback sichtbar macht (Tang et al. schließen sie aus) | M | mittel | Tiefenprüfung K08
- K04, K14, K08b: aus Runde 1 offen, Tiefenprüfung bzw. Abruf ungeprüfter Treffer in Runde 2.
Runde 1:
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
