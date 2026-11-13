---
issue: TIM-156
topic: Nischensuche Frontier AI
question: Welche belegte Nische eignet sich für ein Forschungsprojekt Richtung Frontier AI, das Tim mit Claude und Codex in drei Monaten nebenher umsetzen kann?
runs: []
status: draft
date: 2026-11-13
---

# Nischensuche Frontier AI

## Zusammenfassung

**Empfehlung:** ein Projekt in Stufen auf dem öffentlichen Datensatz CAPE-Bench mit dem offenen Modell gpt-oss-20b. Der Kern ist K23b (wo bricht im Modell der Weg vom Regelwissen zur Handlung ab). Der erste 2-Wochen-Schritt ist K19b (liest eine Probe die Absicht oder nur die Situation), weil er dieselbe Pipeline braucht und schnell ein prüfbares Ergebnis liefert.

**Die Top 3** (Score = Lücke × Nachfrage × Machbarkeit, je 0–5):

| Kandidat | Frage in einem Satz | Erstbewertung | Zweitbewertung | Mittel |
|---|---|---|---|---|
| K19b | Trennt eine Probe vor einer verbotenen Aktion Verstoß und Nicht-Verstoß auch innerhalb derselben Situation? | 3×4×5 = 60 | 3×3×4 = 36 | 48 |
| K24 | Was bleibt einem Monitor, wenn das Reasoning nur zusammengefasst vorliegt, und schließt eine Probe die Lücke? | 3×3×5 = 45 | 4×3×4 = 48 | 46,5 |
| K23b | Wo im Modell bricht bei einem Tool-Agenten der Weg vom Regelwissen zur Handlung ab? | 4×4×3 = 48 | 4×3×3 = 36 | 42 |

**Rauschgrenze:** Erst- und Zweitbewertung weichen bei den besten fünf im Mittel um 13 Punkte ab, höchstens um 24. Innerhalb der Top 3 ist die Rangfolge deshalb nicht belastbar. Belastbar ist nur, dass die drei als Gruppe vor den übrigen liegen (Mittel 42–48 gegen 27–28), und auch das nur knapp über der Rauschgrenze.

**Leitplanken entscheiden zwischen den drei:** K19b und K24 haben ein hohes Überhol-Risiko (bei K19b drei eng verwandte Arbeiten in vier Wochen). Nur K23b besteht alle Leitplanken und hat die beste Passung zu Tims Thesis. Deshalb ist K23b der Kern und K19b der schnelle erste Schritt.

**Ehrliche Einordnung:** Kein Kandidat liegt über 60 von 125. Das Feld rund um Regelbefolgung, Monitoring und Probes bei Agenten ist 2026 sehr dicht besetzt. Alle breiten Fassungen der Ideen waren schon beantwortet, übrig geblieben sind eng geschnittene Fragen.

**Stoppgrund:** Die Top 3 blieb über Runde 5 stabil, und im Backlog steht keine offene Idee mehr mit „hoch“ oder „mittel“. Verbraucht sind rund 1 h 45 min Uhrzeit von 2–4 h (davon 40 min Wartezeit wegen des Abruf-Limits), 5 Runden, 24 bewertete Kandidaten und Fassungen, 13 Subagenten mit zusammen rund 1,45 Mio. Tokens.

## Rangliste

Alle Kandidaten mit ihrem letzten Stand. Die Einzelbelege stehen in `log.tsv`.

| ID | Kandidat | L | N | M | Score | Status |
|---|---|---|---|---|---|---|
| K19b | Probe: Absicht oder Situation, auf CAPE-Bench | 3 | 4 | 5 | 60 | Top 3 |
| K23b | Routing von Regelwissen zur Handlung, Forking-Token und Patching | 4 | 4 | 3 | 48 | Top 3 |
| K24 | Monitor bei zusammengefasstem Reasoning (enthält K13b und K16) | 3 | 3 | 5 | 45 | Top 3 |
| K01b | Zerfall einer Prozessregel mit Tool-Calls, Stop-Hook gegen Reminder | 3 | 3 | 4 | 36 | ungeklärt |
| K08b | Monitor-Erkennung nach Regeltyp gegen deterministische Checks | 2 | 4 | 4 | 32 | ungeklärt |
| K30 | Begründung an der Regel: hilft oder schadet sie | 3 | 2 | 5 | 30 | ungeklärt |
| K18 | Dunkelziffer unbemerkter Regelverstöße in echten Sitzungen | 4 | 2 | 3 | 24 | ungeklärt |
| K22 | Wirkt eine aufgeschriebene Regel, Vorher-Nachher in eigenen Logs | 3 | 2 | 4 | 24 | ungeklärt |
| K09 | Regelverstöße in öffentlichen Trajektorien annotieren | 2 | 2 | 4 | 16 | ungeklärt |
| K32 | Forking-Punkte in Agenten-Trajektorien allgemein | 3 | 2 | 3 | 18 | ungeklärt |
| K12 | Fehlervorhersage im Lauf aus Aktivierungen | 2 | 3 | 3 | 18 | ungeklärt |
| K07 | Warum Agenten bereitstehende Tools nicht nutzen | 4 | 2 | 2 | 16 | ungeklärt |
| K14 | Hochbudget-Leistung aus billigen Läufen schätzen | 2 | 4 | 2 | 16 | ungeklärt |
| K06 | API gegen GUI gegen Hybrid | 2 | 3 | 2 | 12 | ungeklärt |
| K10 | Regeltreue kleiner offener Modelle, Destillation | 3 | 2 | 2 | 12 | ungeklärt |
| K15 | Vergessen oder übergangen | 1 | 3 | 3 | 9 | widerlegt |
| K11 | Selbst erzeugte gegen kuratierte Skills | 1 | 2 | 4 | 8 | widerlegt |
| K05 | Tool-Entscheidung über mehrere Schritte dekodieren | 1 | 2 | 3 | 6 | widerlegt |
| K02 | Skill nicht geladen gegen geladen, aber ignoriert | 0 | 3 | 4 | 0 | widerlegt |

Die breiten Fassungen K01, K08, K13, K19, K23 und K16 sind in ihren engen Fassungen aufgegangen und stehen mit eigenen Zeilen im Log.

## Die Top 3 im Einzelnen

Gemeinsame Grundlage ist CAPE-Bench aus „The Agent Knew“ (Fayyazi et al., 12.10.2026, <https://arxiv.org/abs/2610.17301>). Der Datensatz enthält 206.697 Episoden von vier offenen Modellen als Tool-Agenten, mit rohem Reasoning je Zug und einer Markierung jedes Regelverstoßes. Jede der 24 Vorlagen gibt es als nicht autorisierte Welt und als autorisierten Zwilling. Daten (<https://huggingface.co/datasets/Afayyazi/CAPE-Bench>, CC-BY-4.0) und Code (<https://github.com/AryaFayyazi/Honesty>) sind öffentlich. Aktivierungen sind nicht gespeichert und müssen per Replay erzeugt werden.

### K19b: Liest die Probe die Absicht oder nur die Situation?

- **Frage:** Trennt eine lineare Probe im Entscheidungszug Verstoß und Nicht-Verstoß auch innerhalb identischer nicht autorisierter Welten und nach Neuziehen vieler Fortsetzungen ab demselben Präfix? Schlägt sie dort ein einfaches Wortzähl-Modell (TF-IDF) auf dem Reasoning?
- **Lücke (3):** „The Agent Knew“ berichtet diesen Wert nicht und zitiert die Gegenposition (Fomin et al., <https://arxiv.org/abs/2606.30449>) nur. Die Kontrolle selbst ist bekannt: „Pre-Crime for Agents“ (<https://arxiv.org/abs/2610.40588v1>) macht sie für ein Szenario auf gpt-oss-20b, „What Do Collusion Probes Read?“ (<https://arxiv.org/html/2611.10620>) für Multi-Agenten-Kollusion mit AUROC 0,46. Neu ist nur die Übertragung auf Autorisierungs-Verstöße einzelner Agenten plus Präfix-Resampling.
- **Nachfrage (4, Zweitbewertung 3):** Google DeepMind schreibt „probes fail to generalize under important production distribution shifts“ (<https://alphaxiv.org/abs/2601.11516>). Anthropic nennt „substantial risk that activation monitors are not robust to distributional shifts“ (<https://alignment.anthropic.com/2025/recommended-directions>). Fomin et al. fordern, Monitor-Behauptungen müssten Kontrollen auf Situation und Aktion überstehen. Genau diese Kontrolle auf CAPE fordert niemand wörtlich.
- **Machbarkeit (5, Zweitbewertung 4):** Schätzung der Tiefenprüfung 40–50 h und 5–10 GPU-Stunden. Erstes Ergebnis in 10–16 h, falls das Replay die Zahlen des Papers reproduziert.
- **Leitplanken:** Passung gut. Kosten niedrig. Überhol-Risiko **hoch**: drei eng verwandte Arbeiten in vier Wochen, die Autoren haben vorregistrierte Läufe offen, die Analyse ist billig.
- **Schärfste Einwände:** Der Widerspruch zwischen Fomin und Fayyazi ist schwächer als er aussieht, denn Fayyazi behauptet im Entscheidungszug keinen Vorteil gegenüber Text. Bei 2–13 % Verstoßrate gibt es wenige Positive pro Vorlage. Ein AUROC um 0,5 ist ohne Resampling zweideutig.

### K23b: Wo bricht der Weg vom Regelwissen zur Handlung ab?

- **Frage:** In Episoden mit informiertem Verstoß: An welchem Token im Reasoning ist der Verstoß entschieden (gefunden durch Neuziehen ab gleichem Präfix), und in welchen Schichten kippt das Einsetzen der Aktivierungen aus dem nicht verstoßenden Geschwister-Lauf die Entscheidung?
- **Lücke (4):** Wen et al. (<https://arxiv.org/html/2609.37737v1>) lokalisieren die Entscheidung bei Prompt Injection in einfachen Settings und berichten für den Agenten-Fall einen Negativbefund: „no single-token intervention controls the decision“. Sie nennen „multi-token or multi-step patching“ als künftige Arbeit. Li et al. (<https://www.alphaxiv.org/abs/2608.12321>) zeigen den Engpass zwischen Wissen und Nutzung auf gpt-oss-20b, aber ohne Agenten und Tools. Die Grundfigur (Wissen vorhanden, später Engpass) ist also schon gezeigt, der Agenten-Fall nicht.
- **Nachfrage (4, Zweitbewertung 3):** Das Positionspapier von Aghzal, Geva, Stein und Yao (<https://ziyu-yao-nlp-lab.github.io/mi-for-agents.github.io/>) nennt Patching in Agenten-Trajektorien als ungelöstes Methodenproblem. Wen et al. nennen den Schritt selbst. Kein Lab fordert es ausdrücklich.
- **Machbarkeit (3):** Schätzung 70–100 h bei einem Budget von 65–104 h. Die Tiefenprüfung nennt 3–7 GPU-Stunden, der Zweitbewerter hält 20–40 für realistischer, weil die Suche nach dem Forking-Token viele Fortsetzungen braucht. Erstes Ergebnis in 10–16 h nur ohne Attribution Graphs.
- **Leitplanken:** Passung **sehr gut** (Patching und Attribution sind Tims Thesis-Werkzeug). Kosten niedrig bis mittel. Überhol-Risiko mittel: die Gruppe um Wen kündigt den Schritt an, bisher gibt es keinen direkten Treffer.
- **Schärfste Einwände:** Bei Reasoning-Modellen fällt die Entscheidung im Text des Reasonings und liegt über viele Tokens verteilt. Es droht, dass das Projekt nur den Negativbefund von Wen et al. wiederholt. Attribution Graphs sind nur für gpt-oss-20b denkbar (circuit-tracer 0.5.0 mit `mntss/clt-131k`, <https://pypi.org/project/circuit-tracer/>) und für lange Agenten-Kontexte unerprobt.

### K24: Was bleibt dem Monitor bei zusammengefasstem Reasoning?

- **Frage:** Wie viel Erkennungsrate bei 1 % und 5 % Fehlalarmen verliert ein Text-Monitor, wenn er statt des rohen Reasonings nur eine Zusammenfassung sieht (wie bei Claude und OpenAI üblich)? Welche Art von Hinweis geht verloren (Regel erwähnt, Abwägung, Entschluss)? Schließt eine Probe die Lücke?
- **Lücke (3, Zweitbewertung 4):** Die Endpunkte sind belegt. Rohes Reasoning ist etwa so gut wie die Probe (CAPE-Bench). Die Probe schlägt einen Monitor, der nur Aktionen sieht („Caught in the Act“, <https://arxiv.org/html/2610.12445v1>). Auf SHADE-Arena liegt die Erkennungsrate bei 5 % Fehlalarmen mit Reasoning bei 0,923 und nur mit Aktionen bei 0,058 (<https://arxiv.org/html/2611.07586v1>). Die „Observability Ladder“ (<https://arxiv.org/abs/2608.02089>) vergleicht Zusammenfassung und volle Trace, aber nur für die Korrektheit von Antworten. Die Zusammenfassung bei Regelverstößen von Agenten hat niemand gemessen.
- **Nachfrage (3):** METR nennt die Zusammenfassung als ungeklärte mögliche Erklärung dafür, dass Reasoning-Zugang bei Claude kaum hilft (<https://metr.org/blog/2026-01-19-early-work-on-monitorability-evaluations/>). Ein LessWrong-Pilot mit sechs statischen Fällen nennt echte Agenten-Trajektorien als nächsten Schritt (<https://www.lesswrong.com/posts/bL4xXLQuiDyh9mEKs/how-summarization-loses-safety-signal-depends-on-the-model-1>). Eine ausdrückliche Forderung eines Labs gibt es nicht.
- **Machbarkeit (5, Zweitbewertung 4):** Schätzung 55–80 h, API-Kosten 60–560 USD (Preise sind ungeprüfte Annahmen), 1–3 GPU-Stunden für den Probe-Arm. Erstes Ergebnis in 10–16 h realistisch.
- **Leitplanken:** Passung mittel (wenig Interpretierbarkeit). Kosten mittel. Überhol-Risiko mittel bis **hoch**: billig, offene Daten, viele Gruppen arbeiten an Monitorability.
- **Schärfste Einwände:** Eine selbst gebaute Zusammenfassung ist nicht die der Produktions-APIs, und der Pilot zeigt, dass die Anweisung an den Zusammenfasser alles entscheidet. Das Ergebnis ist teilweise vorhersagbar. Liegt ein Monitor nur auf Aktionen auf CAPE-Bench schon nahe 0,94, verliert die Frage ihre Pointe. Das ist ungeprüft.

## Erster 2-Wochen-Schritt für den Sieger

Der Schritt ist so geschnitten, dass er K19b beantwortet und zugleich die Pipeline für K23b legt. Aufwand 10–16 h.

| Nr. | Schritt | Stunden | Ergebnis |
|---|---|---|---|
| 1 | Vorab-Checks ohne Rechnen: im PDF von „The Agent Knew“ den Wert des Monitors nur auf Aktionen, Anhang R (Sichtbarkeit im Reasoning) und Anhang T (laufende Arbeiten) lesen. GPU prüfen: gpt-oss-20b braucht in bf16 rund 42 GB. | 1 | Entscheidung, ob K24 noch eine Pointe hat und ob K19b schon überholt ist |
| 2 | CAPE-Bench laden, Episoden von gpt-oss-20b filtern, Replay bauen (Chat-Format des Modells nachbilden). Prüfen, dass für rund 50 Entscheidungszüge die aufgezeichnete Aktion reproduziert wird. | 4–6 | funktionierende Replay-Pipeline |
| 3 | Probe wie im Paper nachbauen und den veröffentlichten Wert (AUROC etwa 0,94 gepoolt) reproduzieren. | 3–4 | Plausibilitätsprüfung |
| 4 | AUROC nur innerhalb nicht autorisierter Welten berechnen, daneben TF-IDF auf dem Reasoning in denselben Gruppen, mit Bootstrap-Intervallen. | 3–4 | erstes prüfbares Ergebnis zu K19b |

**Weiter oder Abbruch nach zwei Wochen:**
- Replay reproduziert die Paper-Zahlen nicht: Ursache suchen (Chat-Format, Quantisierung). Erst dann weiter.
- Probe trennt innerhalb der Welt klar und schlägt TF-IDF: kurze Notiz schreiben und schnell veröffentlichen, dann K23b.
- Probe liegt nahe 0,5 oder gleichauf mit TF-IDF: Präfix-Resampling ergänzen (4–6 h). Das Ergebnis ist dann zugleich der Einstieg in K23b.
- Erscheint in der Zeit eine Arbeit mit genau dieser Kontrolle: K19b fallen lassen und mit der Pipeline direkt zu K23b.

## Nötige neue Skills pro Top-Kandidat

Aufbau über skills-design. Die Stundenangaben sind grobe Schätzungen für Entwurf und einen Probelauf.

| Skill | Wozu | K19b | K23b | K24 | Aufwand |
|---|---|---|---|---|---|
| `cape-replay` | Episoden laden, Chat-Format nachbilden, Replay mit Teacher-Forcing, Aktivierungen an festen Lesepositionen speichern, Abgleich mit Paper-Werten | ja | ja | ja (Probe-Arm) | 6–8 h |
| `probe-eval` | Probe trainieren, AUROC nach Gruppen, Bootstrap, Text-Baseline, Prüfung auf Leckagen | ja | teilweise | ja | 4–6 h |
| `prefix-resampling` | Viele Fortsetzungen ab gleichem Präfix ziehen (vLLM), Forking-Token bestimmen, Protokoll | optional | ja | nein | 6–8 h |
| `patching-sweep` | Schichtweises Residual-Patching mit Kontrollen, feste Ergebnisform | nein | ja | nein | 8–10 h |
| `attribution-graph-agent` | Attribution Graphs für gpt-oss-20b mit dem vorhandenen CLT auf kurzen Ausschnitten | nein | optional | nein | 8–12 h |
| `monitor-harness` | Monitor-Prompts, Erkennungsrate bei fester Fehlalarmrate, Kostenprotokoll | nein | nein | ja | 5–7 h |
| `evidenz-annotation` | Zusammenfasser-Bedingungen, Einordnung der Hinweis-Typen per LLM mit 100 von Hand geprüften Fällen | nein | nein | ja | 5–7 h |

Summe je Kandidat: K19b rund 10–14 h, K23b rund 24–32 h (ohne Graphen), K24 rund 20–28 h. Vorhandene Skills reichen für Auftrag, Analyse und Schreiben (ds-autoresearch, ds-analysis, paper-write).

## Widerlegt

Hier steht, was sich als schon beantwortet herausgestellt hat.

- **K02 Skill nicht geladen gegen geladen, aber ignoriert** (Achse 3, Lücke 0). SKILL-USE macht genau diese Zerlegung in Claude Code und Codex mit 8 Modellen (<https://arxiv.org/html/2608.04828v1>). SkillClash nennt Treiber der zweiten Klasse (<https://arxiv.org/html/2610.25064v1>).
- **K15 Vergessen oder übergangen** (Achsen 2, 3, 5, Lücke 1). Modelle kennen die verletzte Regel noch: „Models Recall What They Violate“ (<https://arxiv.org/abs/2604.28031>) und „LLMs Know the Constraint But Do Not Use It“ (<https://arxiv.org/abs/2608.12321>).
- **K05 Tool-Entscheidung über mehrere Schritte dekodieren** (Achse 2, Lücke 1). „Reading the Plan“ zeigt das für 1, 3 und 5 Schritte voraus (<https://neurips.cc/virtual/2026/168165>).
- **K11 Selbst erzeugte gegen kuratierte Skills** (Achse 6, Lücke 1). Kernbefund in SkillsBench (<https://arxiv.org/abs/2602.12670>).
- **K01 in der breiten Fassung** (Achse 3, Lücke 2). Gamage zeigt mit kontrolliertem Experiment, dass die Tokenmenge den Abfall treibt und nicht die Zahl der Turns, und dass Verbote zerfallen, Gebote aber halten (<https://arxiv.org/abs/2604.20911>).

## Ungeklärt

Hier steht, was weder trägt noch tot ist, jeweils mit dem Grund.

- **K01b Prozessregel, Tool-Calls, Stop-Hook** (36, Zweitbewertung 18). Offen laut McMillan (<https://arxiv.org/pdf/2605.10039>). Probleme: Harness ändert sich laufend und fügt selbst Reminder ein, rund 900 USD, etwa eine Nachbararbeit pro Monat. 1 Tiefenprüfung.
- **K08b Monitor-Erkennung nach Regeltyp** (32, Zweitbewertung 24). Apollo hat im Juli 2026 16 Monitor-Modelle auf 2.904 Coding-Trajektorien verglichen, einschließlich Verstößen gegen Anweisungen (<https://www.apolloresearch.ai/products/evaluating-llm-calibration-for-coding-agent-monitoring/>). Übrig bleibt nur die Aufteilung nach Regeltyp. 1 Tiefenprüfung, 1 Nachlese.
- **K30 Begründung an der Regel** (30). Nur ein Blog mit 9–10 Läufen (<https://inferal-com.pages.dev/blog/instruction-adherence-research>). Sehr billig, aber Nachfrage nur aus der Praxis. 1 Kurzprüfung. Ob Tsuchida et al. den Wortlaut variieren, ist nicht geprüft.
- **K18 Dunkelziffer unbemerkter Verstöße** (24). Nichts Direktes gefunden. Unklar, ob die Sitzungsdatensätze samt Instruktionsdateien herunterladbar sind. 1 Kurzprüfung.
- **K22 Wirkt eine aufgeschriebene Regel** (24). Eine Vorarbeit ohne Vorher-Vergleich (<https://www.alphaxiv.org/abs/2607.13091>). Mit den eigenen Logs machbar, aber nur ein Nutzer. 1 Kurzprüfung.
- **K14 Hochbudget-Leistung aus billigen Läufen** (16). UK AISI nennt die Frage ausdrücklich offen (<https://aisi.gov.uk/blog/more-compute-more-capability-why-ai-agent-evals-need-to-account-for-test-time-compute>). Die Referenzmessung braucht aber 50 Mio. Tokens mal 107 Aufgaben. Scheitert an der Machbarkeit.
- **K06, K07 API gegen GUI** (12 und 16). Teilweise beantwortet durch „Terminal Agents Suffice“ (<https://arxiv.org/abs/2604.00073>), MCPWorld und OSWorld-MCP. Teuer. Nur Kurzprüfung.
- **K09, K10, K12, K32** (12–18). Jeweils teilweise beantwortet, nur Kurzprüfung. Belege im Log.

## Verlauf

| Runde | Inhalt | Top 3 danach |
|---|---|---|
| 1 | Scan der sechs Achsen, 14 Ideen, 14 Kurzprüfungen, 4 Tiefenprüfungen | K08b 48, K13b 48, K01b 36 |
| 2 | 3 neue Ideen aus den Lehren, Abruf-Limit erschöpft, Scores vorläufig | K13b 36, K01b 36, K08b 32 |
| 3 | 9 offene Arbeiten nachgelesen, K19 geprüft, CAPE-Bench gefunden | K19b 60, K13b 45, K01b 36 |
| 4 | K23 und K24 in der Tiefe, K22 kurz | K19b 60, K23b 48, K24 45 |
| 5 | K30 und K32 kurz, Zweitbewertung | K19b 60, K23b 48, K24 45 (stabil) |

## Lehren

1. Eine Kurzprüfung mit einer Suche ist kein Beleg für eine Lücke. In Runde 1 standen vier Ideen bei 60–64 Punkten, nach der Tiefenprüfung bei 24–48.
2. Reines Verhaltens-Messen von Regelbefolgung bei Coding-Agenten ist 2026 dicht besetzt, etwa eine neue Arbeit pro Monat.
3. Labs betreiben Monitore für übereifriges Verhalten schon im Produkt. Nachfrage nach „harmlosen Regelverstößen“ ist nirgends wörtlich belegt.
4. Claude und OpenAI liefern über die API kein rohes Reasoning. Tims eigene Logs taugen deshalb nicht für Fragen zum Reasoning. Dafür braucht es offene Modelle.
5. „Vergessen“ ist als Ursache von Regelverstößen widerlegt. Der Engpass liegt zwischen Wissen und Handlung.
6. CAPE-Bench ist ein öffentlicher Hebel. Projekte darauf brauchen keine eigene Datenerzeugung.
7. Probe-Monitoring bei Agenten bewegt sich im Wochentakt. Was dort liegt, ist billig, aber schnell überholt.
8. Bei Reasoning-Modellen muss mechanistische Analyse am Entscheidungspunkt im Reasoning ansetzen, nicht am Aktionstoken.
9. Tims eigene Daten zu ignorierten Regeln haben am Ende keinen der Top-Kandidaten getragen. Sie taugen für K22 und K30, die aber an der Nachfrage scheitern.

## Geparkt und offen

- **GPU:** gpt-oss-20b braucht in bf16 rund 42 GB. Ob die Uni-GPU 48 GB hat, ist nicht bekannt. Mit 24 GB geht es nur quantisiert, und die Machbarkeit von K19b und K23b sinkt laut Zweitbewerter um etwa einen Punkt. Das muss Tim klären.
- **Ungeprüft:** alle API-Preise, der Inhalt der Anhänge R und T von „The Agent Knew“, das Werkzeug claude-md-doctor, der Wortlaut-Teil bei Tsuchida et al., ein Zitat von Walden und Wanner (nur über eine Sekundärseite).
- **Projektfakten:** Für dieses Repo gibt es keine `CLAUDE.md`. Ob und wo Recherche-Ordner und Linear-Projekt dauerhaft eingetragen werden, entscheidet Tim.

## Rahmen

- **Auftrag:** Linear TIM-156, Abschnitt „Forschungsauftrag“. Skala, Suchachsen und Modellverteilung unverändert.
- **Zeit:** Start 13.11.2026 18:50 UTC, Stopp nach Runde 5 um etwa 20:35 UTC. Davon 40 min Wartezeit.
- **Modelle:** Koordination Fable 5.2. 3 Paper-Leser (Sonnet, 337k Tokens), 4 Kurzprüfungen (Haiku, 326k), 5 Tiefenprüfungen (Opus, 699k), 1 Zweitbewerter (Opus, 89k). Der Koordinator hat selbst keine Paper gelesen.
- **Abweichungen:**
  - Pushen des Zweigs `research/TIM-156` war von Tim freigegeben.
  - Das Abruf-Limit von 100 Webseiten pro Stunde hat Runde 2 entwertet. Die Lücken wurden in Runde 3 geschlossen.
  - Die Paper-Leser haben in Runde 1 als Achsen-Scan gearbeitet, nicht pro Paper.
  - Belege stammen überwiegend aus Abstract- und HTML-Seiten, nicht aus vollständiger Lektüre der PDFs.
- **Auswahl-Verzerrung:** Die Scores stammen vom selben Koordinator, der die Ideen entwickelt hat. Die Zweitbewertung korrigiert das nur für die besten fünf.
- **Prüfer-Befund:** folgt.
