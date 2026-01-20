# Ninox Scripting - Performance-Optimierung

## Übersicht

Diese Dokumentation beschreibt Best Practices für Performance-Optimierung in Ninox-Skripten.

**Quelle**: https://forum.ninox.de/category/docs

---

## Wichtigste Regeln

### 1. Select-Optimierung

#### ✅ BEVORZUGT: Select mit Where
```ninox
// Gut: Filtert bereits bei der Selektion (serverseitig)
select Orders where Status = "Open"
```

#### ⚠️ VERMEIDEN: Select ohne Where, dann Filterung
```ninox
// Schlecht: Holt alle Datensätze, dann Filterung (clientseitig)
let orders := select Orders;
let filtered := orders[Status = "Open"];
```

**Grund**: `where` filtert bereits bei der Selektion, was weniger Datenverkehr und bessere Performance bedeutet.

**Quelle**: https://forum.ninox.de/t/h7yxvgh

---

### 2. Transaction Blocks

#### ✅ BEVORZUGT: Mehrere Operationen in Transaction
```ninox
do as transaction
  record1.field := value1;
  record2.field := value2;
  record3.field := value3;
end
```

#### ❌ VERMEIDEN: Einzelne Operationen
```ninox
// Schlecht: Jede Operation einzeln
record1.field := value1;
record2.field := value2;
record3.field := value3;
```

**Grund**: Transaction Blocks reduzieren die Anzahl der Datenbankzugriffe.

**Quelle**: https://forum.ninox.de (Performance-Dokumentation)

---

### 3. Vermeide verschachtelte Selects

#### ❌ VERMEIDEN: Select in Schleife
```ninox
// Schlecht: Select in jeder Iteration
for customer in select Customers do
  let orders := select Orders where Customer = customer;
  // Verarbeitung
end
```

#### ✅ BEVORZUGT: Select einmalig, dann Verarbeitung
```ninox
// Gut: Select einmalig, dann Verarbeitung
let allOrders := select Orders;
for customer in select Customers do
  let orders := allOrders[Customer = customer];
  // Verarbeitung
end
```

**Grund**: Jeder `select` ist ein Datenbankzugriff. Mehrfache Zugriffe vermeiden.

---

### 4. Aggregatfunktionen statt Loops

#### ❌ VERMEIDEN: Summe in Loop berechnen
```ninox
// Schlecht: Loop für Summe
let total := 0;
for order in select Orders do
  total := total + order.Amount;
end
```

#### ✅ BEVORZUGT: Aggregatfunktion verwenden
```ninox
// Gut: Aggregatfunktion
let total := sum(select Orders[Amount]);
```

**Grund**: Aggregatfunktionen sind optimiert und schneller.

---

### 5. Limit bei großen Datensätzen

#### ✅ BEVORZUGT: Limit verwenden
```ninox
// Gut: Nur benötigte Datensätze laden
select Orders order by Date desc limit 10
```

#### ❌ VERMEIDEN: Alle Datensätze laden
```ninox
// Schlecht: Alle Datensätze laden
select Orders order by Date desc
```

---

## Performance-Block-Typen

### do as transaction
**Verwendung**: Bei mehreren Schreiboperationen
```ninox
do as transaction
  // Mehrere Schreiboperationen
end
```

### do as server
**Verwendung**: Code auf Server-Seite ausführen
```ninox
do as server
  // Server-seitige Ausführung
end
```

### do as deferred
**Verwendung**: Verzögerte Ausführung
```ninox
do as deferred
  // Verzögerte Ausführung
end
```

**Quelle**: Ninox Dokumentation

---

## Checkliste für Performance

Vor jedem Skript prüfen:

- [ ] Verwende `select ... where` statt nachträglicher Filterung
- [ ] Verwende `do as transaction` bei mehreren Schreiboperationen
- [ ] Vermeide `select` in Schleifen
- [ ] Verwende Aggregatfunktionen statt Loops
- [ ] Verwende `limit` bei großen Datensätzen
- [ ] Vermeide verschachtelte `select`-Anweisungen

---

## Häufige Performance-Fehler

### Fehler 1: Select in Loop
```ninox
// ❌ SCHLECHT
for customer in select Customers do
  let orders := select Orders where Customer = customer;
end
```

### Fehler 2: Keine Transaction bei mehreren Schreiboperationen
```ninox
// ❌ SCHLECHT
record1.field := value1;
record2.field := value2;
record3.field := value3;
```

### Fehler 3: Nachträgliche Filterung statt Where
```ninox
// ❌ SCHLECHT
let allOrders := select Orders;
let filtered := allOrders[Status = "Open"];
```

---

**Quellen**:
- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Performance-Diskussionen: https://forum.ninox.de
