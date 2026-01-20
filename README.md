# Ninox Knowledge Base für Cursor

> **Wichtig**: Diese Knowledge Base ist speziell für **Cursor** entwickelt, um sicherzustellen, dass generierte Ninox-Skripte dokumentationskonform sind und nur existierende Funktionen verwenden.

## 📌 Was ist Cursor?

**[Cursor](https://cursor.sh)** ist ein AI-gestützter Code-Editor, der mit LLMs wie Composer 1 arbeitet. Cursor lädt automatisch Project Rules aus `.cursor/rules/*.mdc` Dateien, um konsistente und dokumentationskonforme Code-Generierung zu gewährleisten.

## 🎯 Zweck

Diese Knowledge Base hilft Cursor (z.B. mit Composer 1) dabei, korrekte Ninox-Skripte zu generieren:

- ✅ Nur dokumentierte Ninox-Funktionen verwenden
- ✅ Keine erfundenen Funktionen aus anderen Programmiersprachen übernehmen
- ✅ Undokumentierte aber funktionierende Features korrekt kennzeichnen
- ✅ Performance-optimierte Skripte generieren

**Warum ist das wichtig?** LLMs neigen dazu, Funktionen zu erfinden oder aus anderen Sprachen zu übernehmen. Diese Knowledge Base verhindert das durch strikte Regeln und eine Function-Whitelist.

## 🚀 Schnellstart

### Voraussetzungen

- **[Cursor](https://cursor.sh)** installiert und eingerichtet

### Schritte

1. **Ordner in Cursor öffnen**: Öffne diesen Ordner in Cursor
2. **Automatisch aktiv**: `.cursor/rules/*.mdc` werden automatisch geladen
3. **Skripte erstellen**: Erstelle Ninox-Skripte im `workspace/` Ordner
4. **Fertig**: Stelle Fragen zu Ninox - Cursor nutzt automatisch die Knowledge Base

## 📁 Struktur

- `docs/` - Dokumentation (Scripting, Datenbanken, Automatisierung)
- `examples/` - Beispiele und Patterns
- `rules/` - Regeln (Function-Whitelist, Forbidden Patterns, Performance)
- `.cursor/rules/*.mdc` - **Cursor Project Rules** (automatisch geladen)
- `workspace/` - Hier erstellst du deine aktuellen Ninox-Skripte

## 📋 Wichtigste Regeln

### Drei Kategorien von Funktionen:

1. **✅ Dokumentiert** - Bevorzugt verwenden
2. **⚠️ Undokumentiert aber funktionierend** - Mit Kennzeichnung verwenden
3. **❌ Nicht existierend** - ABSOLUT VERBOTEN

**Prinzip**: Bevorzuge dokumentierte Lösungen, aber wenn etwas funktioniert (auch wenn nicht dokumentiert), kann es verwendet werden - mit entsprechender Kennzeichnung.

## 🔍 Validierungsprozess

Jedes generierte Ninox-Skript muss:

1. Bevorzugt Funktionen aus der Whitelist verwenden (`rules/function-whitelist.md`)
2. Keine Patterns aus `rules/forbidden-patterns.md` enthalten
3. Quellenangaben zu forum.ninox.de für dokumentierte Features enthalten
4. Undokumentierte Features explizit kennzeichnen: `⚠️ Nicht in offizieller Dokumentation, aber funktioniert`

## 📖 Quellen

- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Ninox Tutorials: https://ninox.com/de/tutorials
- Community Forum: https://forum.ninox.de

## ⚖️ Lizenz

Creative Commons Attribution 4.0 International (CC-BY 4.0) - siehe [LICENSE](LICENSE) für Details.

**Hinweis**: Ninox ist eine Marke von Ninox Software GmbH. Diese Knowledge Base ist nicht offiziell von Ninox unterstützt.

## ⚠️ Disclaimer

- Diese Knowledge Base ist **nicht** die offizielle Ninox-Dokumentation
- Undokumentierte Features können sich ändern oder entfernt werden
- Immer die offizielle Dokumentation bevorzugen
