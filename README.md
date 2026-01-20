# Ninox Knowledge Base

Diese Knowledge Base dient als strukturierte Wissenssammlung für Ninox-Scripting, um sicherzustellen, dass alle generierten Skripte dokumentationskonform sind und nur existierende Funktionen verwenden.

## Struktur

### 📚 Dokumentation (`docs/`)
- `scripting/` - Scripting-Dokumentation (Funktionen, Syntax, Performance)
- `database/` - Datenbank-Konzepte (Tabellen, Beziehungen, Felder)
- `automation/` - Automatisierung (Workflows, Funktionen, API)

### 📝 Beispiele (`examples/`)
- `good-practices/` - Korrekte, dokumentationskonforme Skripte
- `patterns/` - Häufige Muster und Lösungen
- `undocumented-examples/` - Beispiele mit undokumentierten aber funktionierenden Features

### 📋 Regeln (`rules/`)
- `strict-rules.md` - **KRITISCH**: Regeln zur Dokumentationskonformität
- `function-whitelist.md` - Liste aller dokumentierten Ninox-Funktionen
- `undocumented-features.md` - Undokumentiert aber funktionierend
- `forbidden-patterns.md` - Häufige LLM-Fehler: erfundene Funktionen/Syntax
- `style-guide.md` - Coding-Standards und Best Practices
- `performance-rules.md` - Performance-Optimierungen
- `common-mistakes.md` - Häufige Fehler und wie man sie vermeidet

### ⚙️ Konfiguration (`ninox-config/`)
- `system-prompt.md` - System-Prompt für Ninox-Anfragen
- `references.md` - Liste wichtiger Dokumentations-URLs

## Wichtigste Regeln

### Drei Kategorien von Funktionen:

1. **Dokumentierte Funktionen** - Bevorzugt verwenden, Standard-Ansatz
2. **Undokumentiert aber funktionierend** - Kann verwendet werden, aber mit entsprechender Kennzeichnung/Warnung
3. **Nicht existierende Funktionen** - ABSOLUT VERBOTEN: Nichts erfinden oder aus anderen Programmiersprachen übernehmen

### Prinzip

Bevorzuge dokumentierte Lösungen, aber wenn etwas funktioniert (auch wenn nicht dokumentiert), kann es verwendet werden - mit entsprechender Kennzeichnung.

## Nutzung

Bei jeder Ninox-Anfrage:

1. **OBLIGATORISCH**: Zuerst Prüfung der Function-Whitelist - bevorzuge dokumentierte Funktionen
2. Prüfung der "undocumented-features.md" - wenn undokumentiert aber funktionierend, mit Kennzeichnung verwenden
3. Automatische Suche in der Knowledge Base
4. Verweis auf relevante Dokumentationsstellen (mit URL) für dokumentierte Features
5. Anwendung der Regeln (strict-rules.md)
6. Prüfung gegen "forbidden-patterns.md" - keine erfundenen Funktionen/Syntax
7. Nutzung von Beispielen als Referenz
8. **Bei undokumentierten Features**: Explizit kennzeichnen mit Kommentar wie "⚠️ Nicht in offizieller Dokumentation, aber funktioniert"

## Validierungsprozess

Jedes generierte Ninox-Skript muss:

1. Bevorzugt Funktionen aus der Whitelist verwenden (dokumentiert)
2. Undokumentierte aber funktionierende Features aus "undocumented-features.md" mit entsprechender Kennzeichnung verwenden
3. Keine Patterns aus "forbidden-patterns.md" enthalten (erfundene Funktionen)
4. Quellenangaben zu forum.ninox.de für dokumentierte Features enthalten
5. Bei undokumentierten Features explizit kennzeichnen: "⚠️ Nicht in offizieller Dokumentation, aber funktioniert"

## Erweiterung

Die Knowledge Base kann kontinuierlich erweitert werden:
- Wenn neue Dokumentation verfügbar ist
- Wenn du weitere Beispiele hinzufügst
- Wenn neue undokumentierte aber funktionierende Features entdeckt werden

## Quellen

- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Ninox Tutorials: https://ninox.com/de/tutorials
- Community Forum: https://forum.ninox.de
