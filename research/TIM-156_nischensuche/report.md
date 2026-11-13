---
issue: TIM-156
topic: Nischensuche Frontier AI
question: Welche belegte Nische eignet sich für ein Forschungsprojekt Richtung Frontier AI, das Tim mit Claude und Codex in drei Monaten nebenher umsetzen kann?
runs: []
status: done
date: 2026-11-13
---

# Nischensuche Frontier AI

## Zusammenfassung

**Ergebnis:** Nach fünf Runden, einer blinden Zweitbewertung und dem Prüfer liegt K24 (Monitor bei zusammengefasstem Reasoning) nach den Daten vorn. Es ist der einzige Spitzenkandidat, zu dem der Prüfer keine direkte Vorarbeit gefunden hat. K23b und K19b hat der Prüfer wegen übersehener Vorarbeiten herabgestuft.

**Empfehlung:** ein Projekt auf dem öffentlichen Datensatz CAPE-Bench mit den Episoden des offenen Modells gpt-oss-20b. Kern ist K24 einschließlich des Probe-Arms, weil dort der Score am höchsten und die Lücke am besten belegt ist. K23b ist die Alternative, wenn Tim die Passung zur Thesis (Patching, Attribution) höher gewichtet als den Score. Diese Abwägung ist eine Zielentscheidung und liegt bei Tim. Der erste 2-Wochen-Schritt ist so geschnitten, dass er ohne GPU beginnt und für beide Wege verwertbar bleibt.

**Die Top 3** (Score = Lücke × Nachfrage × Machbarkeit, je 0–5):

| Kandidat | Frage in einem Satz | Erstbewertung | Zweitbewertung | Nach Prüfer |
|---|---|---|---|---|
| K24 | Was bleibt einem Monitor, wenn das Reasoning nur zusammengefasst vorliegt, und schließt eine Probe die Lücke? | 3×3×5 = 45 | 4×3×4 = 48 | 3×3×4 = 36 |
| K23b | Wo im Modell bricht bei einem Tool-Agenten der Weg vom Regelwissen zur Handlung ab? | 4×4×3 = 48 | 4×3×3 = 36 | 3×3×3 = 27 |
| K19b | Trennt eine Probe vor einer verbotenen Aktion Verstoß und Nicht-Verstoß auch innerhalb derselben Situation? | 3×4×5 = 60 | 3×3×4 = 36 | 2×3×4 = 24 |

**Was der Prüfer geändert hat:** Bei K19b fehlten vier eng verwandte Arbeiten, und „The Agent Knew“ deckt selbst mehr ab als im Entwurf behauptet (Lücke 3 auf 2). Bei K23b ist die Methode bereits auf demselben Modell gezeigt, nur nicht für Agenten (Lücke 4 auf 3). Nachfrage 4 war bei beiden nicht gedeckt, weil niemand die Frage wörtlich fordert (auf 3). Machbarkeit 5 bei K19b und K24 war zu hoch, weil das Replay unerprobt ist (auf 4). Einzelheiten stehen im Abschnitt „Prüfer-Befund“.

**Rauschgrenze:** Erst- und Zweitbewertung weichen bei den besten fünf im Mittel um 13 Punkte ab, höchstens um 24. Der Vorsprung von K24 (36) vor K23b (27) und K19b (24) liegt unter dieser Grenze. Hinter K24 sind K23b, K19b, K01b (Zweitbewertung 18) und K08b (Zweitbewertung 24) nicht sicher voneinander zu trennen. Für K24 spricht, dass es in allen drei Bewertungen zwischen 36 und 48 lag, während die anderen stark schwanken.

**Leitplanken:** K24 hat mittlere Passung (wenig Interpretierbarkeit, nur im Probe-Arm), mittlere Kosten und ein mittleres bis hohes Überhol-Risiko. K23b hat die beste Passung, braucht aber am meisten GPU (20–40 Stunden, Größe der Uni-GPU ungeklärt), und zwei Gruppen kündigen den Schritt zu Agenten an (Überhol-Risiko mittel bis hoch). Bei K19b ist das Überhol-Risiko faktisch eingetreten.

**Ehrliche Einordnung:** Nach dem Prüfer liegt kein Kandidat über 36 von 125. Das Feld rund um Regelbefolgung, Monitoring und Probes bei Agenten ist 2026 sehr dicht besetzt. Alle breiten Fassungen der Ideen waren schon beantwortet, übrig geblieben sind eng geschnittene Fragen.

**Stoppgrund:** Die Gruppe der Top 3 blieb über Runde 5 stabil, und im Backlog steht keine offene Idee mehr mit „hoch“ oder „mittel“. Der Prüfer hat danach die Reihenfolge innerhalb der Gruppe gedreht, aber keinen neuen Kandidaten ergeben. Verbraucht sind rund 1 h 40 min Uhrzeit von 2–4 h (davon 40 min Wartezeit wegen des Abruf-Limits), 5 Runden, 24 bewertete Kandidaten und Fassungen, 14 Subagenten mit zusammen rund 1,58 Mio. Tokens.

## Rangliste

Alle Kandidaten mit ihrem letzten Stand, sortiert nach dem zuletzt vergebenen Score. L, N und M zeigen diesen letzten Stand. Werte, die nur auf einer Kurzprüfung beruhen, sind Obergrenzen (siehe Lehre 1). Die Einzelbelege stehen in `log.tsv`.

| ID | Kandidat | L | N | M | Score | Erst | Zweit | Prüftiefe | Status |
|---|---|---|---|---|---|---|---|---|---|
| K24 | Monitor bei zusammengefasstem Reasoning (enthält K13b und K16) | 3 | 3 | 4 | 36 | 45 | 48 | Tiefe, Zweit, Prüfer | Top 3 |
| K30 | Begründung an der Regel: hilft oder schadet sie | 3 | 2 | 5 | 30 | 30 | | nur Kurz | ungeklärt |
| K23b | Routing von Regelwissen zur Handlung, Forking-Token und Patching | 3 | 3 | 3 | 27 | 48 | 36 | Tiefe, Zweit, Prüfer | Top 3 |
| K19b | Probe: Absicht oder Situation, auf CAPE-Bench | 2 | 3 | 4 | 24 | 60 | 36 | Tiefe, Zweit, Prüfer | Top 3 |
| K08b | Monitor-Erkennung nach Regeltyp gegen deterministische Checks | 2 | 3 | 4 | 24 | 32 | 24 | Tiefe, Zweit | ungeklärt |
| K18 | Dunkelziffer unbemerkter Regelverstöße in echten Sitzungen | 4 | 2 | 3 | 24 | 24 | | nur Kurz | ungeklärt |
| K22 | Wirkt eine aufgeschriebene Regel, Vorher-Nachher in eigenen Logs | 3 | 2 | 4 | 24 | 24 | | nur Kurz | ungeklärt |
| K01b | Zerfall einer Prozessregel mit Tool-Calls, Stop-Hook gegen Reminder | 3 | 3 | 2 | 18 | 36 | 18 | Tiefe, Zweit | ungeklärt |
| K32 | Forking-Punkte in Agenten-Trajektorien allgemein | 3 | 2 | 3 | 18 | 18 | | nur Kurz | ungeklärt |
| K12 | Fehlervorhersage im Lauf aus Aktivierungen | 2 | 3 | 3 | 18 | 18 | | nur Kurz | ungeklärt |
| K09 | Regelverstöße in öffentlichen Trajektorien annotieren | 2 | 2 | 4 | 16 | 16 | | nur Kurz | ungeklärt |
| K07 | Warum Agenten bereitstehende Tools nicht nutzen | 4 | 2 | 2 | 16 | 16 | | nur Kurz | ungeklärt |
| K14 | Hochbudget-Leistung aus billigen Läufen schätzen | 2 | 4 | 2 | 16 | 16 | | Tiefe | ungeklärt |
| K06 | API gegen GUI gegen Hybrid | 2 | 3 | 2 | 12 | 12 | | nur Kurz | ungeklärt |
| K10 | Regeltreue kleiner offener Modelle, Destillation | 3 | 2 | 2 | 12 | 12 | | nur Kurz | ungeklärt |
| K15 | Vergessen oder übergangen | 1 | 3 | 3 | 9 | 9 | | Tiefe | widerlegt |
| K11 | Selbst erzeugte gegen kuratierte Skills | 1 | 2 | 4 | 8 | 8 | | nur Kurz | widerlegt |
| K05 | Tool-Entscheidung über mehrere Schritte dekodieren | 1 | 2 | 3 | 6 | 6 | | nur Kurz | widerlegt |
| K02 | Skill nicht geladen gegen geladen, aber ignoriert | 0 | 3 | 4 | 0 | 0 | | Tiefe | widerlegt |

K30, K18 und K22 stehen rechnerisch neben oder vor K23b und K19b. Sie zählen trotzdem nicht zur Spitzengruppe, weil ihre Werte nur aus einer Kurzprüfung stammen und ihre Nachfrage (2) nur aus der Praxis belegt ist.

Die breiten Fassungen K01, K08, K13, K19, K23 und K16 sind in ihren engen Fassungen aufgegangen und stehen mit eigenen Zeilen im Log.

## Die Top 3 im Einzelnen

Gemeinsame Grundlage ist CAPE-Bench aus „The Agent Knew“ (Fayyazi et al., 12.10.2026, <https://arxiv.org/abs/2610.17301>). Der Datensatz enthält 206.697 Episoden von vier offenen Modellen als Tool-Agenten, mit rohem Reasoning je Zug und einer Markierung jedes Regelverstoßes. Jede der 24 Vorlagen gibt es als nicht autorisierte Welt und als autorisierten Zwilling. Daten (<https://huggingface.co/datasets/Afayyazi/CAPE-Bench>, CC-BY-4.0) und Code (<https://github.com/AryaFayyazi/Honesty>) sind öffentlich. Aktivierungen sind nicht gespeichert und müssen per Replay erzeugt werden.

### K19b: Liest die Probe die Absicht oder nur die Situation?

- **Frage:** Trennt eine lineare Probe im Entscheidungszug Verstoß und Nicht-Verstoß auch innerhalb identischer nicht autorisierter Welten und nach Neuziehen vieler Fortsetzungen ab demselben Präfix? Schlägt sie dort ein einfaches Wortzähl-Modell (TF-IDF) auf dem Reasoning?
- **Lücke (3, nach Prüfer 2):** „The Agent Knew“ schichtet die AUROC bereits nach Modell und Vorlage und hat eine TF-IDF-Baseline über alles, was der Agent gesehen und geschrieben hat (Entscheidung gegen autorisierten Zwilling: Probe 0,916, TF-IDF 0,945, CoT-Monitor 0,949). Es fehlen dort nur die AUROC allein innerhalb nicht autorisierter Welten und TF-IDF nur auf dem Reasoning. Die Gegenposition (Fomin et al., <https://arxiv.org/abs/2606.30449>) wird nur zitiert. „Exposure Is Not Commitment“ (Sinha, <https://neurips.cc/virtual/2026/168194>) setzt die Kernidee für Tool-Agenten mit Prompt Injection schon um. Die Kontrolle selbst ist bekannt: „Pre-Crime for Agents“ (<https://arxiv.org/abs/2610.40588v1>) macht sie für ein Szenario auf gpt-oss-20b, „What Do Collusion Probes Read?“ (<https://arxiv.org/html/2611.10620>) für Multi-Agenten-Kollusion mit AUROC 0,46. Neu wäre nur die Übertragung auf Autorisierungs-Verstöße und Reasoning-Modelle plus Präfix-Resampling.
- **Nachfrage (4, Zweitbewertung und nach Prüfer 3):** Google DeepMind schreibt „probes fail to generalize under important production distribution shifts“ (<https://alphaxiv.org/abs/2601.11516>). Anthropic nennt „substantial risk that activation monitors are not robust to distributional shifts“ (<https://alignment.anthropic.com/2025/recommended-directions>). Fomin et al. fordern, Monitor-Behauptungen müssten Kontrollen auf Situation und Aktion überstehen. Genau diese Kontrolle auf CAPE fordert niemand wörtlich.
- **Machbarkeit (5, Zweitbewertung und nach Prüfer 4):** Schätzung der Tiefenprüfung 40–50 h und 5–10 GPU-Stunden. Erstes Ergebnis in 10–16 h, falls das Replay die Zahlen des Papers reproduziert.
- **Leitplanken:** Passung gut. Kosten niedrig. Überhol-Risiko **hoch und faktisch eingetreten**: mit Sinha vier eng verwandte Arbeiten, die Autoren haben vorregistrierte Läufe offen, die Analyse ist billig.
- **Schärfste Einwände:** Der Widerspruch zwischen Fomin und Fayyazi ist schwächer als er aussieht, denn Fayyazi behauptet im Entscheidungszug keinen Vorteil gegenüber Text. Bei 2–13 % Verstoßrate gibt es wenige Positive pro Vorlage. Ein AUROC um 0,5 ist ohne Resampling zweideutig.

### K23b: Wo bricht der Weg vom Regelwissen zur Handlung ab?

- **Frage:** In Episoden mit informiertem Verstoß: An welchem Token im Reasoning ist der Verstoß entschieden (gefunden durch Neuziehen ab gleichem Präfix), und in welchen Schichten kippt das Einsetzen der Aktivierungen aus dem nicht verstoßenden Geschwister-Lauf die Entscheidung?
- **Lücke (4, nach Prüfer 3):** Wen et al. (<https://arxiv.org/html/2609.37737v1>) lokalisieren die Entscheidung bei Prompt Injection in einfachen Settings und berichten für den Agenten-Fall einen Negativbefund: „so no single-token intervention controls it“ (Anhang G, Mistral-7B). Sie nennen „multi-token or multi-step patching“ als künftige Arbeit. Li et al. (<https://www.alphaxiv.org/abs/2608.12321>) zeigen den Engpass zwischen Wissen und Nutzung auf gpt-oss-20b, aber ohne Agenten und Tools. „The Point of No Return“ (Merrill und Srivastava, <https://arxiv.org/pdf/2605.17113>) zeigt Präfix-Resampling, Attribution Patching und Steering bereits auf gpt-oss-20b, aber nicht agentisch, und nennt „tool use“ als künftige Arbeit. Grundfigur und Methode sind also gezeigt, neu ist nur der Agenten- und Regelfall.
- **Nachfrage (4, Zweitbewertung und nach Prüfer 3):** Das Positionspapier von Aghzal, Geva, Stein und Yao (<https://ziyu-yao-nlp-lab.github.io/mi-for-agents.github.io/>) nennt Patching in Agenten-Trajektorien als ungelöstes Methodenproblem. Wen et al. nennen den Schritt selbst. Kein Lab fordert es ausdrücklich.
- **Machbarkeit (3):** Schätzung 70–100 h bei einem Budget von 65–104 h. Die Tiefenprüfung nennt 3–7 GPU-Stunden, der Zweitbewerter hält 20–40 für realistischer, weil die Suche nach dem Forking-Token viele Fortsetzungen braucht. Erstes Ergebnis in 10–16 h nur ohne Attribution Graphs.
- **Leitplanken:** Passung **sehr gut** (Patching und Attribution sind Tims Thesis-Werkzeug). Kosten niedrig bis mittel, aber der höchste GPU-Bedarf der drei. Überhol-Risiko mittel bis hoch: Wen et al. und Merrill und Srivastava kündigen den Schritt an, bisher gibt es keinen direkten Treffer.
- **Schärfste Einwände:** Bei Reasoning-Modellen fällt die Entscheidung im Text des Reasonings und liegt über viele Tokens verteilt. Es droht, dass das Projekt nur den Negativbefund von Wen et al. wiederholt. Attribution Graphs sind nur für gpt-oss-20b denkbar (circuit-tracer 0.5.0 mit `mntss/clt-131k`, <https://pypi.org/project/circuit-tracer/>) und für lange Agenten-Kontexte unerprobt.

### K24: Was bleibt dem Monitor bei zusammengefasstem Reasoning?

- **Frage:** Wie viel Erkennungsrate bei 1 % und 5 % Fehlalarmen verliert ein Text-Monitor, wenn er statt des rohen Reasonings nur eine Zusammenfassung sieht (wie bei Claude und OpenAI üblich)? Welche Art von Hinweis geht verloren (Regel erwähnt, Abwägung, Entschluss)? Schließt eine Probe die Lücke?
- **Lücke (3, Zweitbewertung 4, nach Prüfer 3):** Die Endpunkte sind belegt. Rohes Reasoning ist etwa so gut wie die Probe (CAPE-Bench). Die Probe schlägt einen Monitor, der nur Aktionen sieht („Caught in the Act“, <https://arxiv.org/html/2610.12445v1>). Auf SHADE-Arena liegt die Erkennungsrate bei 5 % Fehlalarmen mit Reasoning bei 0,923 und nur mit Aktionen bei 0,058 (<https://arxiv.org/html/2611.07586v1>). Die „Observability Ladder“ (<https://arxiv.org/abs/2608.02089>) vergleicht Zusammenfassung und volle Trace, aber nur für die Korrektheit von Antworten. Die Zusammenfassung bei Regelverstößen von Agenten hat niemand gemessen.
- **Nachfrage (3):** METR nennt die Zusammenfassung als ungeklärte mögliche Erklärung dafür, dass Reasoning-Zugang bei Claude kaum hilft (<https://metr.org/blog/2026-01-19-early-work-on-monitorability-evaluations/>). Ein LessWrong-Pilot mit sechs statischen Fällen fasst handgeschriebene Statusberichte zusammen, nicht Reasoning, und nennt als nächsten Schritt die Frage, ob nachgelagerte Agenten auf Zusammenfassungen anders handeln als auf dem vollen Text (<https://www.lesswrong.com/posts/bL4xXLQuiDyh9mEKs/how-summarization-loses-safety-signal-depends-on-the-model-1>). Eine ausdrückliche Forderung eines Labs gibt es nicht.
- **Machbarkeit (5, Zweitbewertung und nach Prüfer 4):** Schätzung 55–80 h, API-Kosten 60–560 USD (Preise sind ungeprüfte Annahmen), 1–3 GPU-Stunden für den Probe-Arm. Erstes Ergebnis in 10–16 h realistisch.
- **Leitplanken:** Passung mittel (wenig Interpretierbarkeit). Kosten mittel. Überhol-Risiko mittel bis **hoch**: billig, offene Daten, viele Gruppen arbeiten an Monitorability.
- **Schärfste Einwände:** Eine selbst gebaute Zusammenfassung ist nicht die der Produktions-APIs, und der Pilot zeigt, dass die Anweisung an den Zusammenfasser alles entscheidet. Die Richtung des Ergebnisses ist offen: Arike et al. (<https://arxiv.org/html/2601.21112v1>) finden, dass gefilterte Auszüge Monitore sogar verbessern. Liegt ein Monitor nur auf Aktionen auf CAPE-Bench schon nahe 0,94, verliert die Frage ihre Pointe. Das ist ungeprüft.

## Erster 2-Wochen-Schritt für den Sieger

Der Schritt beantwortet eine kleine Fassung von K24 und braucht keine GPU. Die geladenen Episoden und die Auswertung bleiben auch für K23b und K19b verwertbar. Aufwand 10–16 h.

| Nr. | Schritt | Stunden | Ergebnis |
|---|---|---|---|
| 1 | Vorab-Checks ohne Rechnen: im PDF von „The Agent Knew“ den Wert des Monitors nur auf Aktionen, Anhang R (Sichtbarkeit im Reasoning) und Anhang T (laufende Arbeiten) lesen. Größe der Uni-GPU klären (gpt-oss-20b braucht in bf16 rund 42 GB). | 1 | Entscheidung, ob K24 seine Pointe behält, und ob der Probe-Arm und K23b später machbar sind |
| 2 | CAPE-Bench laden, Episoden von gpt-oss-20b filtern, rund 300 Entscheidungszüge ziehen (Verstoß und Nicht-Verstoß, über die Vorlagen verteilt). | 2–3 | fester Stichprobensatz |
| 3 | Monitor-Harness bauen: ein Text-Monitor per API sieht das rohe Reasoning. Prüfen, dass er in der Stichprobe in der Nähe des veröffentlichten Werts liegt (AUROC etwa 0,94). | 3–4 | Plausibilitätsprüfung |
| 4 | Drei weitere Bedingungen messen: nur Aktionen, neutrale Zusammenfassung, knappe Zusammenfassung im Stil der Produkt-APIs. Erkennungsrate bei 1 % und 5 % Fehlalarmen mit Bootstrap-Intervallen. | 4–6 | erstes prüfbares Ergebnis zu K24 |
| 5 | 30 Fälle von Hand lesen, in denen die Zusammenfassung den Monitor kippt: welcher Hinweis fehlt? | 1–2 | erste Einordnung der verlorenen Hinweise |

**Weiter oder Abbruch nach zwei Wochen:**
- Der Monitor nur auf Aktionen liegt schon nahe am Monitor mit Reasoning: K24 verliert seine Pointe. Dann mit denselben Episoden zu K23b wechseln, sofern die GPU reicht.
- Die Zusammenfassung kostet deutlich Erkennungsrate: K24 weiterführen, als Nächstes Replay und Probe-Arm bauen (Skill `cape-replay`), das ist zugleich die Pipeline für K23b.
- Die Zusammenfassung kostet nichts oder hilft sogar (so bei Arike et al. für gefilterte Auszüge): Das ist ebenfalls ein Ergebnis. Dann klären, welche Art der Zusammenfassung das trägt, und den Umfang klein halten.
- Erscheint in der Zeit eine Arbeit mit genau dieser Messung: K24 fallen lassen und zu K23b wechseln.

**Falls Tim K23b als Kern wählt:** Schritt 1 und 2 bleiben gleich. Schritt 3 bis 5 werden ersetzt durch Replay bauen (4–6 h), die Probe des Papers reproduzieren (3–4 h) und Präfix-Resampling für 20 Episoden (4–6 h). Das setzt eine GPU mit ausreichend Speicher voraus.

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
| Prüfer | übersehene Vorarbeiten, Scores korrigiert | K24 36, K23b 27, K19b 24 |

## Lehren

1. Eine Kurzprüfung mit einer Suche ist kein Beleg für eine Lücke. In Runde 1 standen vier Ideen bei 60–64 Punkten, nach der Tiefenprüfung bei 24–48.
2. Reines Verhaltens-Messen von Regelbefolgung bei Coding-Agenten ist 2026 dicht besetzt, etwa eine neue Arbeit pro Monat.
3. Labs betreiben Monitore für übereifriges Verhalten schon im Produkt. Nachfrage nach „harmlosen Regelverstößen“ ist nirgends wörtlich belegt.
4. Claude und OpenAI liefern über die API kein rohes Reasoning. Tims eigene Logs taugen deshalb nicht für Fragen zum Reasoning. Dafür braucht es offene Modelle.
5. „Vergessen“ ist als Ursache von Regelverstößen widerlegt. Der Engpass liegt zwischen Wissen und Handlung.
6. CAPE-Bench ist ein öffentlicher Hebel. Projekte darauf brauchen keine eigene Datenerzeugung.
7. Probe-Monitoring bei Agenten bewegt sich im Wochentakt. Was dort liegt, ist billig, aber schnell überholt.
8. Bei Reasoning-Modellen muss mechanistische Analyse am Entscheidungspunkt im Reasoning ansetzen, nicht am Aktionstoken.
9. Auch fünf Runden mit Tiefenprüfung haben Vorarbeiten übersehen. Der Prüfer fand mit eigenen Suchbegriffen sechs weitere Arbeiten. Scores ohne unabhängige Gegenprüfung sind Obergrenzen.
10. Tims eigene Daten zu ignorierten Regeln haben am Ende keinen der Top-Kandidaten getragen. Sie taugen für K22 und K30, die aber an der Nachfrage scheitern.

## Geparkt und offen

- **GPU:** gpt-oss-20b braucht in bf16 rund 42 GB. Ob die Uni-GPU 48 GB hat, ist nicht bekannt. Mit 24 GB geht es nur quantisiert, und die Machbarkeit von K19b und K23b sinkt laut Zweitbewerter um etwa einen Punkt. Das muss Tim klären.
- **Ungeprüft:** alle API-Preise, der Inhalt der Anhänge R und T von „The Agent Knew“, das Werkzeug claude-md-doctor, der Wortlaut-Teil bei Tsuchida et al., ein Zitat von Walden und Wanner (nur über eine Sekundärseite).
- **Projektfakten:** Für dieses Repo gibt es keine `CLAUDE.md`. Ob und wo Recherche-Ordner und Linear-Projekt dauerhaft eingetragen werden, entscheidet Tim.

## Rahmen

- **Auftrag:** Linear TIM-156, Abschnitt „Forschungsauftrag“. Skala, Suchachsen und Modellverteilung unverändert.
- **Zeit:** Start 13.11.2026 18:50 UTC, Stopp nach Runde 5 um etwa 20:20 UTC, Prüfer bis etwa 20:30 UTC. Davon 40 min Wartezeit.
- **Modelle:** Koordination Fable 5.2. 3 Paper-Leser (Sonnet, 337k Tokens), 4 Kurzprüfungen (Haiku, 326k), 5 Tiefenprüfungen (Opus, 699k), 1 Zweitbewerter (Opus, 89k), 1 Prüfer (Opus, 129k). Summe rund 1,58 Mio. Tokens. Der Koordinator hat selbst keine Paper gelesen.
- **Abweichungen:**
  - Pushen des Zweigs `research/TIM-156` war von Tim freigegeben.
  - Das Abruf-Limit von 100 Webseiten pro Stunde hat Runde 2 entwertet. Die Lücken wurden in Runde 3 geschlossen.
  - Die Paper-Leser haben in Runde 1 als Achsen-Scan gearbeitet, nicht pro Paper.
  - Belege stammen überwiegend aus Abstract- und HTML-Seiten, nicht aus vollständiger Lektüre der PDFs.
- **Auswahl-Verzerrung:** Die Scores stammen vom selben Koordinator, der die Ideen entwickelt hat. Die Zweitbewertung korrigiert das nur für die besten fünf, der Prüfer nur für die Top 3.
- **Prüfer-Befund** (Opus, 21 Suchen, 12 erfolgreiche Abrufe). Urteil: Die Rechnungen stimmten, aber Lücke und Nachfrage waren bei K19b und K23b zu hoch angesetzt, und die Empfehlung für K23b war durch die Daten nicht gedeckt. Alle folgenden Punkte sind in diesen Bericht eingearbeitet.
  - **Übersehene Vorarbeiten zu K19b:** „The Agent Knew“ berechnet die AUROC bereits innerhalb von Schichten aus Modell und Vorlage und hat eine TF-IDF-Baseline, die am autorisierten Zwilling vor der Probe liegt (<https://arxiv.org/html/2610.17301>). „Exposure Is Not Commitment“ (Sinha, NeurIPS-2026-Workshop, <https://neurips.cc/virtual/2026/168194>, nur die Abstract-Seite gelesen) hält bei Tool-Agenten die Situation fest und findet Probe 0,853 gegen TF-IDF 0,855. „The Illusion of Intent“ (<https://icml.cc/virtual/2026/79985>) und „The Entanglement Wall“ (<https://arxiv.org/html/2607.13075>) zeigen außerhalb von Agenten dasselbe Muster. Lücke 3 auf 2.
  - **Übersehene Vorarbeiten zu K23b:** „The Point of No Return“ (Merrill und Srivastava, Mai 2026, <https://arxiv.org/pdf/2605.17113>) macht Präfix-Resampling mit 50 Fortsetzungen, Attribution Patching und Steering, unter anderem auf gpt-oss-20b, aber nicht agentisch. Die Autoren nennen „tool use“ als künftige Arbeit. „Thought Branches“ (arXiv 2510.27484) ist nur als Suchtreffer bekannt und nicht gelesen. Lücke 4 auf 3, Überhol-Risiko mittel bis hoch.
  - **K24:** keine direkte Vorarbeit gefunden. Arike et al. (<https://arxiv.org/html/2601.21112v1>) zeigen, dass gefilterte Auszüge aus dem Reasoning Monitore in 7 von 8 Paaren verbessern. Das Ergebnis von K24 ist damit weniger vorhersagbar als angenommen. Lücke bleibt 3.
  - **Folgearbeiten zu CAPE-Bench:** keine gefunden.
  - **Korrigierte Scores:** Nachfrage bei K19b und K23b von 4 auf 3 (niemand fordert die Frage wörtlich, siehe Lehre 3). Machbarkeit bei K19b und K24 von 5 auf 4 (Replay unerprobt, GPU ungeklärt).
  - **Korrigierte Textstellen:** Wortlaut des Zitats von Wen et al., Inhalt des LessWrong-Piloten, Sortierung der Rangliste, die Aussage „nur K23b besteht alle Leitplanken“, die Aussage „knapp über der Rauschgrenze“.
  - **Bestätigt:** alle Produkte und Mittelwerte, die Rauschgrenze (Mittel 13, Maximum 24), die Zahlen aus „The Agent Knew“ (Probe 0,941, CoT-Monitor 0,944), dass dort weder Patching noch Forking-Token vorkommen, die Aussage von Wen et al. zur künftigen Arbeit und die Wiedergabe von METR.
  - **Offen geblieben:** Der Wert des Monitors nur auf Aktionen in „The Agent Knew“ war im HTML nicht auffindbar. Anhang T ist nicht einsehbar.
