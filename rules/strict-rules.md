# Strikte Regeln für Ninox-Scripting

## KRITISCH: Dokumentationskonformität mit Nuancen

**WICHTIGSTE REGEL**: Ninox-Skript ist sehr eingeschränkt. Es gibt drei Kategorien von Funktionen und Features:

### 1. Dokumentierte Funktionen ✅
**Status**: Bevorzugt verwenden, Standard-Ansatz

- Alle Funktionen, die in der offiziellen Ninox-Dokumentation stehen
- Funktionen aus offiziellen Tutorials (ninox.com/tutorials)
- Funktionen, die in der offiziellen Dokumentation auf forum.ninox.de beschrieben sind
- Quellenangabe erforderlich: Immer URL zur Dokumentation angeben

**Beispiele**:
- `select ... where ...` - Dokumentiert in Ninox Tutorials
- `sum()`, `count()`, `first()`, `last()` - Dokumentierte Aggregatfunktionen
- `if ... then ... else` - Dokumentierte bedingte Logik
- `do as transaction ... end` - Dokumentierte Performance-Optimierung

### 2. Undokumentiert aber funktionierend ⚠️
**Status**: Kann verwendet werden, aber mit entsprechender Kennzeichnung/Warnung

- Features, die nicht in der offiziellen Dokumentation stehen, aber nachweislich funktionieren
- Muss durch mindestens zwei unabhängige Quellen oder offizielle Community-Beispiele bestätigt sein
- **OBLIGATORISCHE KENNZEICHNUNG**: Immer mit Kommentar markieren: `⚠️ Nicht in offizieller Dokumentation, aber funktioniert`
- Bei Verwendung: Explizit darauf hinweisen, dass es nicht dokumentiert ist

**Beispiele**:
- `select Tabelle[ Bedingung ]` - Eckige Klammern als Filter (funktioniert, aber Performance-Unterschied zu `where`)
- Kombinationen von Features, die nicht explizit dokumentiert sind, aber funktionieren

### 3. Nicht existierende Funktionen ❌
**Status**: ABSOLUT VERBOTEN

- Nichts erfinden oder aus anderen Programmiersprachen übernehmen
- Keine Funktionen verwenden, die nicht existieren
- Keine Syntax verwenden, die nicht in Ninox unterstützt wird
- Wenn unsicher: Immer dokumentierte Alternative verwenden oder explizit warnen

**Häufige Fehler**:
- Funktionen aus JavaScript/Python/etc. übernehmen (z.B. `Array.map()`, `String.split()`)
- Erfundene Funktionen (z.B. `find()`, `filter()` als separate Funktionen)
- Syntax aus anderen Sprachen (z.B. `for ... in ...`, `try ... catch`)

## Prinzip

**Bevorzuge dokumentierte Lösungen**, aber wenn etwas funktioniert (auch wenn nicht dokumentiert), kann es verwendet werden - **mit entsprechender Kennzeichnung**.

## Validierungsprozess

Vor jedem generierten Ninox-Skript:

1. ✅ Prüfe Function-Whitelist - bevorzuge dokumentierte Funktionen
2. ⚠️ Prüfe undocumented-features.md - wenn verwendet, kennzeichnen
3. ❌ Prüfe forbidden-patterns.md - keine erfundenen Funktionen/Syntax
4. 📚 Quellenangaben für dokumentierte Features hinzufügen
5. ⚠️ Undokumentierte Features explizit kennzeichnen

## Bei Unsicherheit

Wenn du dir nicht sicher bist, ob eine Funktion existiert:

1. **Zuerst**: In function-whitelist.md nachschauen
2. **Dann**: In undocumented-features.md nachschauen
3. **Dann**: In forbidden-patterns.md nachschauen
4. **Wenn nicht gefunden**: Als "nicht bestätigt" markieren und dokumentierte Alternative verwenden
5. **Niemals**: Etwas erfinden oder aus anderen Sprachen übernehmen

## Quellen

- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Ninox Tutorials: https://ninox.com/de/tutorials
- Community Forum: https://forum.ninox.de
