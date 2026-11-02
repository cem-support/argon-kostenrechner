# Argon API-Kostenrechner

**Live: https://argon-kostenrechner.netlify.app**

Rechner für die Token-Kosten von Gemini 4 Argon über die API, im Vergleich zur
Abo-Pauschale. Die beiden Preisstufen — bis 30.11.2026 und ab 01.12.2026, wenn
sich der Satz verdoppelt — stehen nebeneinander.

Eine einzelne HTML-Datei, kein Build-Schritt, keine Abhängigkeiten außer der
Schriftart von Google Fonts. Alle Berechnungen laufen im Browser; es werden
keine Daten übertragen und keine Cookies gesetzt.

## Nutzungsprofile

Sechs vorgerechnete Profile, jeweils mit Anfragen pro Monat, Input- und
Output-Tokens je Anfrage und gecachtem Input-Anteil. Alle Werte sind frei
überschreibbar.

| Profil | jetzt | ab 01.12.2026 |
| --- | --- | --- |
| Chat-Assistent, täglich | $11,34 | $22,68 |
| Power-User, viel Kontext | $45,36 | $90,72 |
| Meeting-Pipeline | $1,79 | $3,57 |
| Dokumentenanalyse | $1,94 | $3,88 |
| Agent mit Wissensbasis | $13,28 | $26,55 |
| Workflow in Endlosschleife | $180,00 | $360,00 |

## Preisgrundlage

Standard-Tier, USD je 1 Mio. Tokens:

| | bis 30.11.2026 | ab 01.12.2026 |
| --- | --- | --- |
| Input | $2,00 | $4,00 |
| Output (inkl. Thinking-Tokens) | $10,00 | $20,00 |
| Gecachter Input | $0,10 | $0,20 |

Geprüft am 03.11.2026 gegen [Googles offizielle Preisseite][g].

Argon ist im kostenlosen Kontingent **nicht** enthalten. Caching läuft nur
implizit — explizites Caching unterstützt das Modell nicht, dafür weist Google
für Argon auch keine Cache-Speicherkosten aus.

Dieselbe Arbeit in anderen Tiers:

| Tier | bis 30.11.2026 | ab 01.12.2026 |
| --- | --- | --- |
| Batch / Flex | $1 / $5 | $2 / $10 |
| Standard | $2 / $10 | $4 / $20 |
| Priority | $3,60 / $18 | $7,20 / $36 |

Nicht enthalten: abweichende Reseller-Tarife, Grounding-Anfragen und Steuern.
Die Vertex-AI-Preisseite war beim Abgleich nicht abrufbar; ob die Sätze dort
identisch sind, ist offen.

[g]: https://aistudio.google.com/docs/pricing

## Lokal öffnen

```bash
start index.html
```

Kein Server nötig — die Datei läuft direkt im Browser.

## Deployment

Netlify veröffentlicht das Wurzelverzeichnis ohne Build-Schritt; die
Konfiguration steht in `netlify.toml`.

Die Site wurde per CLI angelegt (`argon-kostenrechner`, Team AIX2 Advisory)
und wird per CLI aktualisiert:

```bash
npx netlify-cli deploy --prod --dir .
```

Ein Push auf GitHub löst **kein** Deployment aus. Wer das will, verbindet das
Repo einmalig in Netlify unter *Project configuration → Build & deploy →
Link repository*; danach deployt jeder Push auf `main` automatisch.

## Preise aktualisieren

Die Preisstufen stehen als `REGIMES` am Anfang des `<script>`-Blocks in
`index.html`, die Profile direkt darunter als `PRESETS`. Der Rabatt auf
gecachten Input ist in der Funktion `calc` als Faktor `0.05` hinterlegt.

## Lizenz

[MIT](LICENSE) — Weiterverwendung und Anpassung erlaubt, Haftung
ausgeschlossen. Die Preisangaben sind unverbindlich und ersetzen keine
Kalkulation auf Basis von Googles offizieller Preisliste.
