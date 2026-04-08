# Auszahlungslogik

## Überblick

Jeden Monat führt Legalhero einen Auszahlungsprozess durch, um Partner-Anwälte für abgeschlossene Mandate zu bezahlen. Die Auszahlung wird als SEPA-Datei erstellt und an die Bank gesendet.

## Wie die Auszahlung berechnet wird

Die Auszahlung wird pro **Rechtsgebiet** berechnet. Die Gesamtauszahlung eines Anwalts ist die Summe aller Rechnungsbeträge über alle seine Rechtsgebiete hinweg.

### Anteilsverteilung nach Rechtsgebiet

Die Aufteilung zwischen Legalhero und dem Partner-Anwalt variiert je nach Rechtsgebiet:

- **Arbeitsrecht**: 50/50-Aufteilung
- **Vertragsrecht**: 70% Anwalt / 30% Legalhero

Bei gemischten Rechtsgebieten mit Gutschriften können komplexe Berechnungssituationen entstehen.

## BaaS-Rechnungen und die 50%-Schwelle

BaaS-Rechnungen werden erst erstellt, wenn **mindestens 50% des Rechnungsbetrags** eingegangen sind. Dies war eine bewusste Entscheidung von Anfang an.

- Zahlungen unter 50% werden **nicht ausgezahlt** und erscheinen im Tab **„Nicht in nächster Auszahlung"**.
- Das System weiß automatisch, welcher Betrag ausgezahlt werden muss, unter Berücksichtigung dieser 50%-Regel.

### Problemfall: Teilzahlung + Stornierung

**Szenario:**
1. Eine 800€-Rechnung wird mit 350€ teilbezahlt (unter 50%) → keine BaaS-Rechnung wird erstellt.
2. Die Rechnung wird auf 350€ storniert → sie ist nun vollständig bezahlt, aber die BaaS-Rechnung fehlt.

**Lösung (in Arbeit):** Der BaaS-Job soll so angepasst werden, dass er auch bei Stornierungen automatisch läuft.

## Technische Details der Auszahlungsberechnung

### Schlüsselbegriffe

| Begriff | Bedeutung |
|---|---|
| **Received New** | Neu erhaltener Betrag in diesem Monat |
| **Received Total** | Gesamtbetrag, der von der Rechnung bisher erhalten wurde |
| **Our Share Net** | Legalheros Netto-Anteil an der Rechnung |
| **Our Fees Net** | Legalheros Netto-Gebühren |
| **BaaS Discount** | Entspricht einer Gutschrift – entsteht, wenn zu viel BaaS abgerechnet wurde |

### Losing Amount

- **Formel:** `Losing Amount = Our Share Net − Our Fees Net`
- Wird nur berechnet, wenn `Our Fees Net < Our Share Net`

### Datenstruktur in der Auszahlungsansicht

| Farbe | Bedeutung |
|---|---|
| Grün | Erhaltener Betrag (Received) |
| Rot | Unsere Gebühren (Our Fees) |
| Orange | Auszahlung an den Partner |

Der verbleibende Betrag für Legalhero wird **nicht separat überwiesen**, sondern bleibt schlicht übrig.

**Durchgestrichene Einträge:** BaaS-Rechnungen, die bereits in einem Vormonat berücksichtigt wurden, werden durchgestrichen. Sie werden nur einmal in der Auszahlung berücksichtigt.

## Negative Rechnungen (Gutschriften)

Es kann vorkommen, dass eine Abschlagsrechnung in einem Fall höher ist als die Schlussrechnung. In diesem Fall:

1. Eine **negative Rechnung (Gutschrift)** wird für die Differenz erstellt.
2. Eine **Buchhaltungsaufgabe** wird für das Finance-Team erstellt.
3. Die Buchhaltung zahlt die Differenz an die Versicherung (RSV) zurück und **hakt die Aufgabe ab**.
4. Sobald die Aufgabe abgehakt ist, wird die negative Rechnung in den **nächsten Auszahlungszyklus** einbezogen.

## Bekannte Probleme & Fixes

### Fix: Negativitätsprüfung auf Gesamtebene (Sprint 33 — OS-3133)

**Problem:** Die Auszahlungsvalidierung prüfte die Negativität zuvor auf **Rechtsgebiets-Ebene**. Wenn eine einzelne negative Rechnung der einzige Eintrag in einem Rechtsgebiet war (z.B. nur eine Gutschrift in „Arbeitsrecht"), war das Gesamtergebnis für dieses Feld negativ — was die gesamte SEPA-Datei-Generierung zum Scheitern brachte und die vollständige monatliche Auszahlung blockierte.

**Fix:** Die Negativitätsprüfung wurde auf die **Gesamtauszahlungsebene** verschoben. Solange der Gesamtauszahlungsbetrag eines Anwalts (Summe über alle Rechtsgebiete) nicht negativ ist, wird die Auszahlung durchgeführt. Nur ein negatives Gesamtergebnis blockiert die SEPA-Generierung.

### Offenes Problem: Berechnungsfehler bei Gutschriften

**Problem (entdeckt: 07.04.2026):** Das System zeigt einen „Losing Amount", obwohl bei Gutschriften keine Verluste entstehen sollten. Jan hat bereits eine Liste von Anwälten geschickt, bei denen tatsächlich Verluste entstanden sind.

**Erwartetes Verhalten:** Bei Gutschriften sollte einfach weniger gutgeschrieben werden, anstatt dass Legalhero Verluste macht.

**Status:** Wird untersucht.

### Offenes Problem: BaaS-Job bei Stornierungen

**Problem:** Der BaaS-Job läuft aktuell nicht automatisch bei Stornierungen. Dadurch können Fälle entstehen, in denen eine stornierte Rechnung vollständig bezahlt ist, aber keine BaaS-Rechnung existiert.

**Lösung:** Amir und das Team haben bereits eine Lösung entwickelt — der BaaS-Job soll auch bei Stornierungen automatisch laufen.

## Offene Themen (nicht detailliert besprochen)

- **OPOS** — Offene Posten, Klärung ausstehend
- **E-Rechnungen** — Anforderungen/Umsetzung offen
- **Rechnungskorrektur im Rechnungs-Tab** — noch nicht besprochen
