---
name: release-notes
description: Erstelle Release Notes auf Deutsch, gruppiert nach Epics, basierend auf Jira-Tickets aus einem Sprint oder einer Slack-Nachricht.
---

# Release Notes erstellen

Erstelle Release Notes auf Deutsch, gruppiert nach Epics.

$ARGUMENTS

## Argumente

- **Slack-Nachricht** (optional): Slack-Nachricht mit Jira-Ticket-Nummern (z.B. OS-123)
- **Sprint-Nummer** (erforderlich): Sprint-Nummer (z.B. 30)
- **Sprint-Startdatum** (erforderlich): Startdatum des Sprints (z.B. 17.02.)
- **Sprint-Enddatum** (erforderlich): Enddatum des Sprints (z.B. 27.02.)
- **Projekt** (optional): Jira-Projekt-Key. Standard: OS.

## Ablauf

### Tickets ermitteln

**Variante A – Slack-Nachricht vorhanden:** Alle Jira-Ticket-Keys aus der Nachricht extrahieren.

**Variante B – Keine Slack-Nachricht:** Per JQL alle Tickets im angegebenen Sprint und Projekt abrufen, die den Status "Prod Review" oder "Done" haben:
```
project = {Projekt} AND sprint = {Sprint-Nummer} AND status IN ("Prod Review", "Done")
```

### Tickets aus Jira laden

Für jedes Ticket per Jira MCP abrufen: Key, Summary, Description, Epic. Tickets ohne Epic unter "Sonstiges" einordnen.

### Release Notes schreiben

Alle Texte auf **Deutsch**. Sprache: einfach, verständlich, für Stakeholder (PM, Design, Leadership). Pro Ticket 1-2 Sätze zum User-Impact, keine technischen Details.

Datei erstellen unter `.claude/product/releases/{sprint-enddatum}.md`:

```markdown
# Neuerungen in CaseForce {Sprint-Startdatum} - {Sprint-Enddatum}

**Sprint:** {Nummer}

## Zusammenfassung

{2-3 Sätze zum Fokus des Sprints}

## Änderungen nach Epic

### {Epic-Name}

- **{TICKET-KEY}**: {1-2 Sätze Beschreibung}

### Sonstiges

- **{TICKET-KEY}**: {1-2 Sätze Beschreibung}
```

### Notion-Seite erstellen

Seite in der Notion Release Notes Datenbank anlegen:
- **Datenbank-URL**: https://www.notion.so/25a5e8cace39809580e5e99da1c7bd11?v=25a5e8cace39806e8727000c0c660a07
- **Titel**: `Neuerungen in CaseForce {Sprint-Startdatum} - {Sprint-Enddatum}`
- **Date-Property**: Heutiges Datum (currentDate)
- **Inhalt**: Gleicher Inhalt wie die lokale `.md`-Datei

### Bestätigung

Ausgabe am Ende:
1. Lokaler Dateipfad als Link
2. Anzahl verarbeiteter Tickets
3. Notion-Link (falls erstellt) oder Hinweis auf manuelles Einfügen
