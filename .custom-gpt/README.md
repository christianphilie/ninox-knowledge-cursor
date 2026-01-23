# Ninox Custom GPT für ChatGPT

Dieser Ordner enthält alle benötigten Dateien und Konfigurationen, um ein Custom GPT für ChatGPT zu erstellen, das analog zur Ninox AI Knowledge Base funktioniert.

## 📋 Voraussetzungen

- **ChatGPT Plus oder Enterprise** erforderlich (Custom GPTs sind nicht im kostenlosen Plan verfügbar)
- Alle Dateien aus diesem Ordner bereit haben

## 📁 Struktur

### Konfigurationsdateien (für ChatGPT Custom GPT Setup)

1. **`01_name.txt`** - Vorschläge für den Namen des Custom GPT
2. **`02_beschreibung.txt`** - Vorschläge für die Kurzbeschreibung (1-2 Sätze)
3. **`03_hinweise.txt`** - Langer Hinweistext (System-Prompt) für das Custom GPT
4. **`04_gespraechsaufhaenger.txt`** - Beispielanfragen als Gesprächsaufhänger (Buttons)

### Wissen-Dateien (für Upload in ChatGPT)

Diese Dateien sollten in das "Wissen"-Feld des Custom GPT hochgeladen werden:

- `wissen-01-strikte-regeln.md` - Die wichtigsten Regeln für Ninox-Scripting
- `wissen-02-function-whitelist.md` - Dokumentierte Funktionen (Whitelist)
- `wissen-03-forbidden-patterns.md` - Verbotene Patterns und häufige Fehler
- `wissen-04-undocumented-features.md` - Undokumentierte aber funktionierende Features
- `wissen-05-performance.md` - Performance-Optimierungen
- `wissen-06-style-guide.md` - Coding-Standards und Best Practices
- `wissen-07-common-mistakes.md` - Häufige Fehler und wie man sie vermeidet
- `wissen-08-scripting-functions.md` - Scripting-Funktionen Dokumentation
- `wissen-09-database-tables.md` - Datenbank- und Tabellen-Konzepte
- `wissen-10-automation-api.md` - Automatisierung und API-Integration

## 🚀 Schritt-für-Schritt Anleitung

### Schritt 1: Custom GPT erstellen

1. Gehe zu [chat.openai.com](https://chat.openai.com)
2. Klicke links auf "Explore GPTs" oder "Entdecke GPTs"
3. Klicke auf "Create a GPT" oder "GPT erstellen"
4. Wähle den Tab **"Configure"** (nicht "Create")

### Schritt 2: Name festlegen

1. Im Feld **"Name"**:
   - Öffne `01_name.txt`
   - Wähle einen Namen aus (z.B. "Ninox Expert Assistent")
   - Oder verwende deinen eigenen Namen

**Empfehlung**: "Ninox Expert Assistent" oder "Ninox Knowledge Base Helper"

### Schritt 3: Beschreibung eingeben

1. Im Feld **"Description"** (Beschreibung):
   - Öffne `02_beschreibung.txt`
   - Wähle eine Beschreibung aus
   - Oder verwende deine eigene (1-2 Sätze)

**Empfehlung**: "Experte für Ninox-Datenbanken, Scripting und Automatisierung. Hilft bei Formeln, Skripten, Performance-Optimierung und Best Practices."

### Schritt 4: Hinweise (Instructions) einfügen

1. Im großen Textfeld **"Instructions"** (Hinweise):
   - Öffne `03_hinweise.txt`
   - Kopiere den **gesamten Inhalt**
   - Füge ihn in das Feld ein

**Wichtig**: Dies ist der System-Prompt, der das Verhalten des GPT steuert. Kopiere alles!

### Schritt 5: Gesprächsaufhänger hinzufügen

1. Im Bereich **"Conversation starters"** (Gesprächsaufhänger):
   - Öffne `04_gespraechsaufhaenger.txt`
   - Kopiere die Zeilen einzeln
   - Jede Zeile wird zu einem Button
   - Füge mindestens 3-4 hinzu

**Beispiel-Buttons**:
- "Wie schreibe ich eine Formel, die alle offenen Bestellungen summiert?"
- "Wie verbessere ich die Performance meiner Ninox-Datenbank?"
- "Wie richte ich eine Automatisierung mit Trigger ein?"

### Schritt 6: Wissen hochladen

1. Im Bereich **"Knowledge"** (Wissen):
   - Klicke auf "Upload files" oder "Dateien hochladen"
   - Lade **ALLE** `wissen-*.md` Dateien hoch (alle 10 Dateien)
   - Du kannst alle auf einmal hochladen (Multi-Select)

**Hinweis**: 
- ChatGPT unterstützt bis zu 20 Dateien - wir haben 10, passt perfekt!
- Markdown-Dateien werden optimal verarbeitet

### Schritt 7: Speichern und Testen

1. Klicke oben rechts auf **"Save"** (Speichern)
2. Wähle, ob das GPT:
   - **Nur für dich** (Only me)
   - **Für Personen mit Link** (Anyone with a link)
   - **Öffentlich** (Public) - nicht empfohlen, da es deine Knowledge Base enthält

3. **Teste das GPT**:
   - Stelle eine Testfrage: "Wie summiere ich alle Bestellungen?"
   - Prüfe, ob die Antwort dokumentationskonform ist
   - Teste verschiedene Szenarien

## ✅ Checkliste

- [ ] Name eingetragen
- [ ] Beschreibung eingetragen
- [ ] Hinweise (Instructions) eingefügt
- [ ] Mindestens 3-4 Gesprächsaufhänger hinzugefügt
- [ ] Alle 10 Wissen-Dateien hochgeladen
- [ ] GPT gespeichert
- [ ] Testfragen gestellt und Antworten geprüft

## 🎯 Erwartetes Verhalten

Nach der Einrichtung sollte das Custom GPT:

✅ **Nur dokumentierte Funktionen verwenden**  
✅ **Undokumentierte Features kennzeichnen**  
✅ **Keine erfundenen Funktionen verwenden**  
✅ **Performance-Optimierungen beachten**  
✅ **Quellenangaben hinzufügen**  
✅ **Code-Beispiele mit Kommentaren liefern**

## 🔧 Anpassungen

### Hinweise anpassen

Wenn du die Hinweise anpassen möchtest:
1. Bearbeite `03_hinweise.txt`
2. Kopiere den neuen Inhalt
3. Gehe zu deinem Custom GPT → "Edit" → "Configure"
4. Ersetze die Instructions
5. Speichern

### Wissen aktualisieren

Wenn sich die Knowledge Base ändert:
1. Aktualisiere die entsprechenden `wissen-*.md` Dateien
2. Gehe zu deinem Custom GPT → "Edit" → "Configure"
3. Im Bereich "Knowledge":
   - Entferne die alte Datei (falls nötig)
   - Lade die aktualisierte Datei hoch
4. Speichern

## 🐛 Fehlerbehebung

### GPT verwendet erfundene Funktionen
- Prüfe, ob alle Wissen-Dateien hochgeladen wurden
- Prüfe die Instructions (Hinweise) - sind sie vollständig?
- Stelle explizit klar: "Verwende nur dokumentierte Funktionen"

### GPT antwortet nicht auf Ninox-Fragen
- Prüfe die Beschreibung - ist sie klar?
- Füge mehr Gesprächsaufhänger hinzu
- Teste mit expliziten Fragen

### Antworten sind zu allgemein
- Erweitere die Instructions mit mehr Details
- Füge spezifische Beispiele hinzu
- Stelle präzisere Fragen

## 📝 Technische Details

### Dateiformate

ChatGPT Custom GPTs unterstützen folgende Dateiformate für Knowledge:
- ✅ **Markdown (.md)** - Empfohlen für unsere Zwecke
- ✅ **Text (.txt)**
- ✅ **PDF (.pdf)**
- ✅ **Word (.docx)**
- ✅ **CSV/Excel (.csv, .xlsx)**

Wir verwenden **Markdown**, da es:
- Gut strukturiert ist
- Code-Beispiele enthält
- Von ChatGPT gut verstanden wird
- Einfach zu aktualisieren ist

### Limits

- **Maximal 20 Dateien** pro Custom GPT
- **Maximal 512 MB** pro Datei
- **Maximal 2 Millionen Tokens** pro Textdatei
- Unsere Dateien sind deutlich kleiner als diese Limits

## 📚 Quellen

- [ChatGPT Custom GPTs Dokumentation](https://platform.openai.com/docs/guides/gpt)
- Offizielle Ninox-Dokumentation: https://forum.ninox.de/category/docs
- Ninox Tutorials: https://ninox.com/de/tutorials
- Community Forum: https://forum.ninox.de

---

**Erstellt für**: Ninox Knowledge Base Custom GPT  
**Version**: 1.0  
**Datum**: 2025
