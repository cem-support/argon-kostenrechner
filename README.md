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

| | bis 30.11.2026 | ab 01.12.2026 |
| --- | --- | --- |
| Input | $2 / 1 Mio. Tokens | $4 / 1 Mio. Tokens |
| Output (inkl. Thinking) | $10 / 1 Mio. Tokens | $20 / 1 Mio. Tokens |
| Gecachter Input | 95 % Rabatt | 95 % Rabatt |

Die Sätze stammen aus Sekundärquellen ([VentureBeat][vb], [Lindy][lindy],
[LiteLLM][ll]) und sind **nicht von Google bestätigt**. Vor einer
Kostenentscheidung auf Googles offizieller Preisseite prüfen.

Nicht enthalten: die Speicherkosten des Kontext-Caches (pro Token und Stunde),
abweichende Reseller-Tarife und Steuern.

[vb]: https://venturebeat.com/technology/google-makes-gemini-4-argon-broadly-available-with-limited-time-low-api-pricing-of-2-10-per-1m-token
[lindy]: https://www.lindy.ai/blog/gemini-4-argon
[ll]: https://models.litellm.ai/models/gemini-4-argon

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
