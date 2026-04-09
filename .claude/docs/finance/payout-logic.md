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
1. Eine 100€-Rechnung wird mit 30€ teilbezahlt (unter 50%) → keine BaaS-Rechnung wird erstellt.
2. Die Rechnung wird um 70€ storniert → die verbleibenden 30€ sind nun vollständig bezahlt (über 50%), aber die BaaS-Rechnung fehlt.

**Lösung (in Arbeit):** Der BaaS-Job soll so angepasst werden, dass er auch bei Stornierungen automatisch läuft und die 50%-Schwelle prüft. Der Job ist intelligent genug, um die Bedingungen selbst zu prüfen.

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

### Payout-Logik bei mehreren BaaS-Rechnungen

Das System verwendet bei der Auszahlungsberechnung automatisch die **neueste BaaS-Rechnung** (höchste ID), da die Map nach ID sortiert und neuere Einträge ältere überschreiben. Das bedeutet: Selbst wenn Duplikate existieren, wird in der Auszahlung immer die korrekte (neueste) Rechnung herangezogen.

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

**Wichtig:** Seit 02.04.2026 ist die Service Invoice (BaaS-Rechnung) für negative B2B-Rechnungen optional. Ein Fall mit einer negativen Rechnung ohne BaaS-Rechnung blockiert die Auszahlung nicht mehr.

## Bekannte Probleme & Fixes

### Fix: Negativitätsprüfung auf Gesamtebene (Sprint 33 — OS-3133)

**Problem:** Die Auszahlungsvalidierung prüfte die Negativität zuvor auf **Rechtsgebiets-Ebene**. Wenn eine einzelne negative Rechnung der einzige Eintrag in einem Rechtsgebiet war (z.B. nur eine Gutschrift in „Arbeitsrecht"), war das Gesamtergebnis für dieses Feld negativ — was die gesamte SEPA-Datei-Generierung zum Scheitern brachte und die vollständige monatliche Auszahlung blockierte.

**Fix:** Die Negativitätsprüfung wurde auf die **Gesamtauszahlungsebene** verschoben. Solange der Gesamtauszahlungsbetrag eines Anwalts (Summe über alle Rechtsgebiete) nicht negativ ist, wird die Auszahlung durchgeführt. Nur ein negatives Gesamtergebnis blockiert die SEPA-Generierung.

### Fix: Auszahlung blockiert bei negativer Rechnung ohne BaaS-Rechnung (02.04.2026)

**Problem:** Wenn in einem Fall eine negative Rechnung (Gutschrift) vorlag und keine BaaS-Rechnung existierte, wurde die gesamte Auszahlung blockiert.

**Fix (02.04.2026):** Die Service Invoice (BaaS-Rechnung) ist nun für negative B2B-Rechnungen optional. Das Szenario ist valide und blockiert die Auszahlung nicht mehr.

### Fix: Doppelte BaaS-Rechnungen durch parallele Uploads (OS-3376 / OS-3377)

**Problem (entdeckt: 09.04.2026):** 525 Fälle aus März hatten doppelte BaaS-Rechnungen.

**Ursache:** Import- und Payment-Jobs liefen parallel und erstellten beide BaaS-Rechnungen. Ein Job hatte alle Partner Agency IDs, der andere keine — beide erstellten dennoch Rechnungen, weil die Prüfung fehlte.

**Auswirkungen:**
- In der Auszahlungsberechnung: nicht berücksichtigt ✓ (System nutzt automatisch die neueste Rechnung per ID-Sortierung)
- In der Payout Summary für Anwälte: nicht berücksichtigt ✓
- Im Rechnungsexport des Anwalts: **berücksichtigt** ✗
- Künstlich erhöhte interne Umsatzdarstellung ✗

**Implementierte präventive Fixes:**
1. **Distributed Lock auf den File-Upload** — verhindert parallele Uploads
2. **Distributed Lock auf den BaaS-Job selbst** — verhindert parallele Ausführung des Jobs
3. **Leerlistenprüfung** — Job wird nicht eingereiht, wenn keine `partner_agency_id` in der Liste vorhanden ist
4. **FE (OS-3377):** Upload-Button wird gesperrt und Upload-Status angezeigt, solange ein Upload läuft

**Offene Maßnahmen (Bereinigung der bestehenden Duplikate):**
1. Ältere Duplikate (niedrigere ID) löschen
2. Gelöschte Rechnungen für Finance dokumentieren (Invoice IDs + Case IDs)
3. Lawyer Invoice Export nach Cleanup verifizieren

### Offenes Problem: Berechnungsfehler bei Gutschriften — falscher „Losing Amount"

**Problem (entdeckt: 07.04.2026):** Das System zeigt einen „Losing Amount", obwohl bei Gutschriften keine Verluste entstehen sollten. Auffällig: Der Discount für den Anwalt ist deutlich höher als für Legalhero. Hinweis kam vom Finance-Team, das Diskrepanzen bei ausgezahlten Fällen bemerkt hat.

**Erwartetes Verhalten:** Bei Gutschriften sollte einfach weniger gutgeschrieben werden, anstatt dass Legalhero Verluste macht.

**Status:** Wird untersucht. Keine konkreten Beispiele vorliegen noch. Jan's Liste der betroffenen Anwälte ist Ausgangspunkt für die Root-Cause-Analyse.

### Offenes Problem: BaaS-Job läuft nicht bei Teilstornierungen

**Problem:** Bei Teilstornierungen wird der BaaS-Job nicht automatisch ausgeführt.

**Beispiel:** Rechnung 100€, Zahlung 30€ (unter 50% → kein BaaS), dann Stornierung von 70€ → verbleibende 30€ sind jetzt vollständig bezahlt (über 50%), aber keine BaaS-Rechnung wird erstellt.

**Lösung:** Amir und das Team haben eine Lösung entwickelt — der BaaS-Job soll auch bei Stornierungen getriggert werden und selbst prüfen, ob die 50%-Schwelle erreicht ist. Ticket steht noch aus.

### Offenes Problem: Lawyer Invoice Export — falsche Query-Logik

**Problem (entdeckt: 09.04.2026):** Der Rechnungsexport für Anwälte verwendet eine andere Query-Logik als die Auszahlungsberechnung:
- Export zieht Service Invoices direkt aus der Datenbank basierend auf der Legal Case ID
- Berücksichtigt Soft-Deletes nicht korrekt
- Ergebnis: Zahlen im Export stimmen nicht mit dem tatsächlichen Payout überein — Duplikate erscheinen im Export

**Erwartetes Verhalten:** Export und Payout-Berechnung sollten dieselbe Logik verwenden. Nach dem Löschen der Duplikate sollte sich das Problem teilweise von selbst lösen, aber die Query-Logik muss langfristig angeglichen werden.

**Status:** Offen, kein Ticket vorhanden.

### Offenes Problem: Soft-Deleted B2B Invoices

**Problem:** Eine Liste von B2B-Rechnungen liegt vor, die fälschlicherweise soft-deleted wurden. Diese müssen für den nächsten Auszahlungszyklus wiederhergestellt (undeleted) werden.

**Status:** Liste liegt vor. Koordination zwischen Jan und dem Team erforderlich. Aktion ausstehend.

### Offenes Problem: E-Rechnungen — Zugferd-Format

**Problem:** Ein Anwalt (Magintan) hat gemeldet, dass das E-Rechnungsformat (Zugferd) falsch sei.

**Aktuelle Erkenntnis:** Das XML wird bereits validiert und scheint korrekt zu sein. Ein Online-Validator zeigt grün.

**Nächste Schritte:** Konkrete Beispiele von fehlerhaften PDFs werden benötigt, um die Ursache weiter einzugrenzen.

## Offene Themen (nicht detailliert besprochen)

- **OPOS** — Offene Posten, Klärung ausstehend
- **Rechnungskorrektur im Rechnungs-Tab** — noch nicht besprochen
