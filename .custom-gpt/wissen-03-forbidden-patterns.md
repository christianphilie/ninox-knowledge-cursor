# Verbotene Patterns - Häufige LLM-Fehler

Diese Liste enthält Funktionen, Syntax und Patterns, die **NICHT** in Ninox existieren, aber häufig von LLMs erfunden werden.

## ❌ ABSOLUT VERBOTEN

### JavaScript/Python-Funktionen, die nicht existieren

#### Array-Methoden
- ❌ `array.map()` - Existiert nicht
- ❌ `array.filter()` - Existiert nicht (verwende `select ... where` oder `[]`-Filter)
- ❌ `array.forEach()` - Existiert nicht (verwende `for ... in ... do`)
- ❌ `array.reduce()` - Existiert nicht
- ❌ `array.find()` - Existiert nicht (verwende `select ... where` mit `first()`)
- ❌ `array.includes()` - Existiert nicht
- ❌ `array.indexOf()` - Existiert nicht

**Korrekte Alternative**: Verwende `select ... where` oder Schleifen mit `for ... in ... do`

#### String-Methoden
- ❌ `string.split()` - Existiert nicht
- ❌ `string.join()` - Existiert nicht
- ❌ `string.replace()` - Existiert nicht
- ❌ `string.substring()` - Existiert nicht
- ❌ `string.trim()` - Existiert nicht

**Korrekte Alternative**: Verwende dokumentierte String-Funktionen (siehe Function-Whitelist)

#### Objekt/Record-Methoden
- ❌ `Object.keys()` - Existiert nicht
- ❌ `Object.values()` - Existiert nicht
- ❌ `Object.entries()` - Existiert nicht

**Korrekte Alternative**: Direkter Zugriff auf Felder über Punkt-Notation

### Syntax aus anderen Sprachen

#### Try-Catch
- ❌ `try ... catch ... finally` - Existiert nicht in Ninox

**Korrekte Alternative**: Fehlerbehandlung über `if`-Bedingungen und Validierung

#### For-Schleifen
- ❌ `for (let i = 0; i < length; i++)` - JavaScript-Syntax, existiert nicht
- ❌ `for item in array:` - Python-Syntax, existiert nicht

**Korrekte Alternative**: `for ... in ... do` (Ninox-Syntax)

#### Arrow Functions
- ❌ `() => {}` - JavaScript-Syntax, existiert nicht

**Korrekte Alternative**: Funktionen mit `function name() do ... end`

#### Template Literals
- ❌ `` `String ${variable}` `` - JavaScript-Syntax, existiert nicht

**Korrekte Alternative**: String-Konkatenation mit `+` oder `concat()`

### Erfundene Ninox-Funktionen

- ❌ `find()` - Existiert nicht (verwende `select ... where` mit `first()`)
- ❌ `search()` - Existiert nicht
- ❌ `filter()` - Existiert nicht (verwende `select ... where`)
- ❌ `sort()` - Existiert nicht direkt (verwende `select ... order by`)
- ❌ `unique()` - Existiert nicht
- ❌ `groupBy()` - Existiert nicht direkt

**Korrekte Alternative**: Verwende `select` mit entsprechenden Klauseln

### Reguläre Ausdrücke

- ❌ Reguläre Ausdrücke wie `/pattern/` - Nicht direkt unterstützt
- ❌ `match()`, `test()` - Existieren nicht

**Korrekte Alternative**: Verwende String-Funktionen wie `contains()`, `startsWith()`, `endsWith()`

### JSON-Manipulation

- ❌ `JSON.parse()` - Existiert nicht direkt
- ❌ `JSON.stringify()` - Existiert nicht direkt

**Korrekte Alternative**: Ninox hat eigene Datentypen, direkter Zugriff auf Felder

### Asynchrone Funktionen

- ❌ `async/await` - Existiert nicht
- ❌ `Promise` - Existiert nicht
- ❌ `.then()`, `.catch()` - Existieren nicht

**Korrekte Alternative**: Ninox-Skripte laufen synchron

## Häufige Fehlerquellen

### 1. Annahme von JavaScript-Ähnlichkeit
**Problem**: LLMs nehmen an, dass Ninox wie JavaScript funktioniert
**Lösung**: Immer in Function-Whitelist nachschauen

### 2. Annahme von SQL-Ähnlichkeit
**Problem**: LLMs verwenden SQL-Syntax, die nicht existiert
**Lösung**: Ninox hat eigene Syntax, siehe Dokumentation

### 3. Erfinden von "praktischen" Funktionen
**Problem**: LLMs erfinden Funktionen, die "sinnvoll" erscheinen
**Lösung**: Nur dokumentierte Funktionen verwenden

## Validierung

Vor jedem Skript prüfen:
1. Enthält das Skript Funktionen aus dieser Liste? → ENTFERNEN
2. Gibt es eine dokumentierte Alternative? → VERWENDEN
3. Ist etwas unsicher? → Als "nicht bestätigt" markieren

## Quellen

- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Function Whitelist: Siehe wissen-02-function-whitelist.md
