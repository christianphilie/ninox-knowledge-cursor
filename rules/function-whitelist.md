# Function Whitelist - Dokumentierte Ninox-Funktionen

Diese Liste enthält alle **dokumentierten** Ninox-Funktionen, die sicher verwendet werden können. Diese Funktionen sind bevorzugt zu verwenden.

## Quellen

- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Ninox Tutorials: https://ninox.com/de/tutorials
- Community Forum: https://forum.ninox.de

---

## Grundlegende Syntax

### Variablen und Zuweisungen
- `let variable := value` - Variable definieren
- `variable := value` - Variable zuweisen

**Quelle**: https://ninox.com/de/tutorials/basic-scripting

### Bedingte Logik
- `if condition then ... else ... end` - Bedingte Ausführung
- `switch value do case ... end` - Mehrfachauswahl

**Quelle**: https://ninox.com/de/tutorials/if-then-else-statement

### Schleifen
- `while condition do ... end` - While-Schleife
- `for item in collection do ... end` - For-Schleife über Sammlung
- `repeat ... until condition` - Repeat-Until-Schleife

**Quelle**: Ninox Tutorials

---

## Datenbank-Operationen

### Select-Anweisungen
- `select Table` - Alle Datensätze aus Tabelle
- `select Table where condition` - Gefilterte Datensätze
- `select Table order by field` - Sortierte Datensätze
- `select Table limit number` - Begrenzte Anzahl

**Quelle**: https://ninox.com/de/tutorials/advanced-tutorial-2

### Datensatz-Operationen
- `create Table` - Neuen Datensatz erstellen
- `record.field := value` - Feld setzen
- `record.field` - Feld lesen
- `delete record` - Datensatz löschen

**Quelle**: Ninox Dokumentation

---

## Aggregatfunktionen

### Mathematische Funktionen
- `sum(collection)` - Summe berechnen
- `count(collection)` - Anzahl zählen
- `average(collection)` - Durchschnitt berechnen
- `min(collection)` - Minimum finden
- `max(collection)` - Maximum finden

**Quelle**: Ninox Dokumentation

### Datensatz-Funktionen
- `first(collection)` - Ersten Datensatz
- `last(collection)` - Letzten Datensatz

**Quelle**: Ninox Dokumentation

---

## String-Funktionen

- `concat(string1, string2, ...)` - Strings zusammenfügen
- `contains(text, search)` - Enthält Text
- `startsWith(text, prefix)` - Beginnt mit
- `endsWith(text, suffix)` - Endet mit
- `length(text)` - Länge des Textes
- `upper(text)` - Großbuchstaben
- `lower(text)` - Kleinbuchstaben
- `trim(text)` - Leerzeichen entfernen (falls dokumentiert)

**Quelle**: Ninox Dokumentation - Funktionen

---

## Datum- und Zeit-Funktionen

- `today()` - Heutiges Datum
- `now()` - Aktueller Zeitpunkt
- `date(year, month, day)` - Datum erstellen
- `time(hour, minute, second)` - Zeit erstellen
- `datetime(date, time)` - Datum und Zeit kombinieren
- `year(date)` - Jahr extrahieren
- `month(date)` - Monat extrahieren
- `day(date)` - Tag extrahieren
- `weekday(date)` - Wochentag
- `week(date)` - Kalenderwoche
- `quarter(date)` - Quartal

**Quelle**: Ninox Dokumentation - Funktionen

---

## Mathematische Funktionen

- `abs(number)` - Absolutwert
- `round(number)` - Runden
- `floor(number)` - Abrunden
- `ceil(number)` - Aufrunden
- `sqrt(number)` - Quadratwurzel
- `pow(base, exponent)` - Potenz

**Quelle**: Ninox Dokumentation - Funktionen

---

## Logische Funktionen

- `and(condition1, condition2)` - Logisches UND
- `or(condition1, condition2)` - Logisches ODER
- `not(condition)` - Logische Negation

**Quelle**: Ninox Dokumentation

---

## Performance-Optimierungen

### Transaction Blocks
- `do as transaction ... end` - Transaktionsblock für mehrere Schreiboperationen

**Quelle**: https://forum.ninox.de (Performance-Dokumentation)

### Server Execution
- `do as server ... end` - Ausführung auf Server-Seite

**Quelle**: Ninox Dokumentation

### Deferred Execution
- `do as deferred ... end` - Verzögerte Ausführung

**Quelle**: Ninox Dokumentation

---

## Eigene Funktionen

### Funktion definieren
- `function name(params) do ... end` - Eigene Funktion erstellen

**Parameter-Typen**:
- `text`
- `number`
- `boolean`
- `date`
- `time`
- `datetime`
- Tabellen-Typen

**Quelle**: https://forum.ninox.com/t/x2yz1t2/create-your-own-functions

---

## HTTP-Operationen

- `http(url, options)` - HTTP-Request ausführen

**Quelle**: Ninox API-Dokumentation

---

## Feld-Zugriff

- `record.field` - Feld lesen
- `record.field := value` - Feld setzen
- `record.relationField` - Relation-Feld
- `record.relationField.field` - Feld in Relation

**Quelle**: Ninox Dokumentation

---

## Datentypen

- `text` - Text
- `number` - Zahl
- `boolean` - Wahrheitswert
- `date` - Datum
- `time` - Zeit
- `datetime` - Datum und Zeit
- Tabellen-Typen (Referenzen)

**Quelle**: Ninox Dokumentation

---

## Wichtige Hinweise

1. **Diese Liste ist nicht vollständig** - Sie wird kontinuierlich erweitert
2. **Immer Quellenangabe** - Bei Verwendung einer Funktion die Quelle angeben
3. **Bei Unsicherheit** - In der offiziellen Dokumentation nachschlagen
4. **Bevorzugt verwenden** - Diese Funktionen sind dokumentiert und sicher

## Erweiterung

Wenn du eine neue dokumentierte Funktion findest:
1. Füge sie zu dieser Liste hinzu
2. Gib die Quelle an (URL zur Dokumentation)
3. Füge ein kurzes Beispiel hinzu

---

**Letzte Aktualisierung**: Initiale Erstellung basierend auf offizieller Dokumentation
