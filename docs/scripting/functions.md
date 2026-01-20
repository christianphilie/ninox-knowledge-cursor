# Ninox Scripting - Funktionen

## Übersicht

Diese Dokumentation beschreibt die dokumentierten Funktionen in Ninox-Scripting.

**Quelle**: https://forum.ninox.de/category/docs

---

## Grundlegende Syntax

### Variablen
```ninox
let variable := value;
variable := newValue;
```

**Quelle**: https://ninox.com/de/tutorials/basic-scripting

### Bedingte Logik
```ninox
if condition then
  // Code
else
  // Code
end
```

**Quelle**: https://ninox.com/de/tutorials/if-then-else-statement

### Schleifen
```ninox
while condition do
  // Code
end

for item in collection do
  // Code
end
```

**Quelle**: Ninox Tutorials

---

## Datenbank-Operationen

### Select-Anweisungen

#### Basis-Select
```ninox
select Table
```

#### Select mit Where
```ninox
select Table where condition
```

**Performance-Hinweis**: `where` filtert bereits bei der Selektion (serverseitig), daher bevorzugt verwenden.

**Quelle**: https://ninox.com/de/tutorials/advanced-tutorial-2

#### Select mit Order By
```ninox
select Table order by field
select Table order by field desc
```

#### Select mit Limit
```ninox
select Table limit 10
```

---

## Aggregatfunktionen

### Mathematische Funktionen
- `sum(collection)` - Summe aller Werte
- `count(collection)` - Anzahl der Datensätze
- `average(collection)` - Durchschnittswert
- `min(collection)` - Minimum
- `max(collection)` - Maximum

**Beispiel**:
```ninox
let total := sum(select Orders[Amount]);
let count := count(select Orders);
```

**Quelle**: Ninox Dokumentation - Funktionen

### Datensatz-Funktionen
- `first(collection)` - Erster Datensatz
- `last(collection)` - Letzter Datensatz

**Beispiel**:
```ninox
let firstOrder := first(select Orders order by Date);
```

---

## String-Funktionen

- `concat(string1, string2, ...)` - Strings zusammenfügen
- `contains(text, search)` - Prüft ob Text enthalten ist
- `startsWith(text, prefix)` - Prüft ob Text mit Präfix beginnt
- `endsWith(text, suffix)` - Prüft ob Text mit Suffix endet
- `length(text)` - Länge des Textes
- `upper(text)` - In Großbuchstaben umwandeln
- `lower(text)` - In Kleinbuchstaben umwandeln

**Beispiel**:
```ninox
let fullName := concat(firstName, " ", lastName);
if contains(email, "@") then
  // Email ist gültig
end
```

**Quelle**: Ninox Dokumentation - Funktionen

---

## Datum- und Zeit-Funktionen

### Aktuelle Werte
- `today()` - Heutiges Datum
- `now()` - Aktueller Zeitpunkt

### Datum erstellen
- `date(year, month, day)` - Datum erstellen
- `time(hour, minute, second)` - Zeit erstellen
- `datetime(date, time)` - Datum und Zeit kombinieren

### Datum extrahieren
- `year(date)` - Jahr
- `month(date)` - Monat
- `day(date)` - Tag
- `weekday(date)` - Wochentag
- `week(date)` - Kalenderwoche
- `quarter(date)` - Quartal

**Beispiel**:
```ninox
let today := today();
let currentYear := year(today);
let currentQuarter := quarter(today);
```

**Quelle**: Ninox Dokumentation - Funktionen

---

## Mathematische Funktionen

- `abs(number)` - Absolutwert
- `round(number)` - Runden
- `floor(number)` - Abrunden
- `ceil(number)` - Aufrunden
- `sqrt(number)` - Quadratwurzel
- `pow(base, exponent)` - Potenz

**Beispiel**:
```ninox
let rounded := round(3.7); // 4
let absolute := abs(-5); // 5
```

**Quelle**: Ninox Dokumentation - Funktionen

---

## Logische Funktionen

- `and(condition1, condition2)` - Logisches UND
- `or(condition1, condition2)` - Logisches ODER
- `not(condition)` - Logische Negation

**Beispiel**:
```ninox
if and(age >= 18, hasLicense) then
  // Kann Auto fahren
end
```

**Quelle**: Ninox Dokumentation

---

## Eigene Funktionen

### Funktion definieren
```ninox
function calculateTotal(amount, tax) do
  amount + (amount * tax)
end
```

### Parameter-Typen
- `text`
- `number`
- `boolean`
- `date`
- `time`
- `datetime`
- Tabellen-Typen

**Quelle**: https://forum.ninox.com/t/x2yz1t2/create-your-own-functions

---

## Performance-Optimierungen

### Transaction Blocks
```ninox
do as transaction
  // Mehrere Schreiboperationen
  record1.field := value1;
  record2.field := value2;
end
```

**Verwendung**: Bei mehreren Schreiboperationen für bessere Performance.

**Quelle**: https://forum.ninox.de (Performance-Dokumentation)

### Server Execution
```ninox
do as server
  // Code der auf Server ausgeführt wird
end
```

**Quelle**: Ninox Dokumentation

### Deferred Execution
```ninox
do as deferred
  // Code der verzögert ausgeführt wird
end
```

**Quelle**: Ninox Dokumentation

---

## Wichtige Hinweise

1. **Performance**: Bevorzuge `select ... where` statt `select` mit nachträglicher Filterung
2. **Transaktionen**: Verwende `do as transaction` bei mehreren Schreiboperationen
3. **Quellenangabe**: Immer Quelle angeben bei Verwendung einer Funktion

---

**Quellen**:
- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Ninox Tutorials: https://ninox.com/de/tutorials
