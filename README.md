# Seifenkisten-Rechner

Ein Browser-Tool zur physikalischen Auslegung von Rennseifenkisten: Schwerpunkt, Luftwiderstand (cW-Wert) und Fahrzeit-Simulation auf einer beliebigen Strecke — alles live, ohne Installation.

**[→ Demo öffnen](#)** *(Link einfügen, sobald via GitHub Pages gehostet)*

---

## Warum

Beim Bau einer Rennseifenkiste (z. B. für ein IG-Seifenkisten-Derby-Rennen) stellen sich früh Fragen wie:

- Lohnt sich eine stromlinienförmige CF-Nase gegenüber einem einfachen Holzbrett?
- Ist mehr Ballast (bis zum Reglement-Maximum) tatsächlich schneller?
- Wo sollte der Schwerpunkt liegen — und was bedeutet das für die Fahrzeit auf einer konkreten Strecke?

Dieses Tool beantwortet solche Fragen mit einem einfachen physikalischen Modell, das man live mit eigenen Zahlen durchspielen kann, statt es nur überschlagsmässig im Kopf zu rechnen.

## Funktionen

- **Schwerpunkt-Rechner** — Gewicht und Position einzelner Bauteile (Kiste, Fahrer, Ballast, Achsen) eingeben, Gesamtschwerpunkt und Gewichtsverteilung vorne/hinten werden live berechnet.
- **cW-Wert-Baukasten** — Luftwiderstand wird aus einzelnen Bauteilen (Fahrer, Nase, Räder, Achsen) mit jeweils eigenem cW-Wert und Fläche zusammengesetzt (additive Drag-Area-Methode), statt einen einzigen Gesamt-cW zu schätzen.
- **Streckenprofil** — Länge, Gefälle, Rollwiderstand (Presets für verschiedene Beläge), Windbedingungen, Temperatur und Höhe über Meer (für die Luftdichte).
- **Fahrzeit-Simulation** — numerische Integration (Euler-Verfahren) über die Kräfte Hangabtrieb, Rollwiderstand und Luftwiderstand, ergibt Fahrzeit, Endgeschwindigkeit und ein Geschwindigkeits-Distanz-Diagramm.

## Physikalisches Modell

Grundgleichung entlang der Fahrtrichtung:

```
F_netto = m·g·sin(θ) − Crr·m·g·cos(θ) − 0.5·ρ·CdA·v²
a = F_netto / m
```

mit:

| Symbol | Bedeutung |
|---|---|
| `m` | Gesamtmasse (Kiste + Fahrer + Ballast) |
| `g` | Erdbeschleunigung (9.81 m/s²) |
| `θ` | Hangwinkel der Strecke |
| `Crr` | Rollwiderstandskoeffizient |
| `ρ` | Luftdichte (aus Temperatur + Höhe) |
| `CdA` | Widerstandsfläche = Σ (cW-Wert × Fläche) aller Bauteile |
| `v` | Momentangeschwindigkeit |

Die Simulation integriert diese Gleichung in kleinen Zeitschritten (Δt = 0.02 s) über die gesamte Streckenlänge.

## Nutzung

Einfach `seifenkisten-rechner.html` im Browser öffnen — keine Installation, kein Build-Schritt, keine externen Abhängigkeiten. Alle vier Tabs sind live miteinander verknüpft: Änderungen an Gewicht oder cW-Wert wirken sich sofort auf die Simulation in Tab 4 aus.

## Roadmap / offene Punkte

- [ ] Echte cW-Werte-Tabelle aus Windkanal- oder Coast-down-Messungen statt Schätzwerten
- [ ] Variables Höhenprofil statt konstantem mittlerem Gefälle (reale Rampen sind oft am Start steiler)
- [ ] Coast-down-Kalibrierungsmodus: aus einem realen Ausrollversuch (Distanz bis Stillstand aus bekannter Anfangsgeschwindigkeit) automatisch Crr und CdA zurückrechnen
- [ ] Export/Import von Fahrzeug-Konfigurationen als JSON

Beiträge und Pull Requests willkommen.

## Haftungsausschluss

Alle berechneten Werte sind Näherungen eines vereinfachten physikalischen Modells. Für sicherheitsrelevante Entscheidungen (Bremsen, Achsen, Lenkung, Überrollbügel) gelten ausschliesslich die Vorgaben des jeweiligen Reglements (z. B. IG Seifenkisten Derby Schweiz / SSK) — dieses Tool ersetzt keine technische Abnahme.

## Lizenz

MIT — siehe [LICENSE](LICENSE)
