# Arbeitsumgebung

**WICHTIG**: Dieser Ordner ist der Standard-Speicherort für ALLE neuen Dateien.

Erstelle hier deine aktuellen Ninox-Skripte. Cursor nutzt automatisch die Knowledge Base aus `../rules/` und `../docs/`.

## Datei-Erstellung

- **ALLE neuen Dateien** werden hier im `workspace/` Ordner angelegt
- Cursor ist so konfiguriert, dass neue Inhalte automatisch hier erstellt werden
- Bestehende Ordner wie `examples/` oder `docs/` enthalten nur Referenzmaterial

## Dateinamen-Konvention

**Dateiendung**: `.ninox`

**Beispiele**:
- `bestellungen-abfragen.ninox`
- `kunden-export.ninox`
- `rechnungen-generieren.ninox`

**Hinweis**: Es gibt keine offizielle Dateiendung für Ninox-Skripte. `.ninox` wird hier verwendet, damit Cursor die Performance-Regeln automatisch anwendet (siehe `.cursor/rules/ninox-performance.mdc`).

**Beispiel-Workflow**: Erstelle `workspace/mein-script.ninox` → Stelle Fragen → Cursor nutzt automatisch die Regeln.
