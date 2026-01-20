# Häufige Fehler in Ninox-Skripten

## Übersicht

Diese Liste beschreibt häufige Fehler und wie man sie vermeidet.

---

## Fehler 1: Select ohne Where

### ❌ FALSCH
```ninox
let allOrders := select Orders;
let openOrders := allOrders[Status = "Open"];
```

### ✅ RICHTIG
```ninox
let openOrders := select Orders where Status = "Open";
```

**Grund**: `where` filtert bereits bei der Selektion, was bessere Performance bedeutet.

---

## Fehler 2: Select in Schleife

### ❌ FALSCH
```ninox
for customer in select Customers do
  let orders := select Orders where Customer = customer;
  // Verarbeitung
end
```

### ✅ RICHTIG
```ninox
let allOrders := select Orders;
for customer in select Customers do
  let orders := allOrders[Customer = customer];
  // Verarbeitung
end
```

**Grund**: Jeder `select` ist ein Datenbankzugriff. Mehrfache Zugriffe vermeiden.

---

## Fehler 3: Keine Transaction bei mehreren Schreiboperationen

### ❌ FALSCH
```ninox
record1.field := value1;
record2.field := value2;
record3.field := value3;
```

### ✅ RICHTIG
```ninox
do as transaction
  record1.field := value1;
  record2.field := value2;
  record3.field := value3;
end
```

**Grund**: Transaction Blocks reduzieren die Anzahl der Datenbankzugriffe.

---

## Fehler 4: Loop statt Aggregatfunktion

### ❌ FALSCH
```ninox
let total := 0;
for order in select Orders do
  total := total + order.Amount;
end
```

### ✅ RICHTIG
```ninox
let total := sum(select Orders[Amount]);
```

**Grund**: Aggregatfunktionen sind optimiert und schneller.

---

## Fehler 5: Erfundene Funktionen verwenden

### ❌ FALSCH
```ninox
// Diese Funktionen existieren NICHT in Ninox
let filtered := orders.filter(o => o.Status = "Open");
let mapped := orders.map(o => o.Amount);
let joined := array.join(orders, ",");
```

### ✅ RICHTIG
```ninox
// Verwende dokumentierte Funktionen
let filtered := select Orders where Status = "Open";
let amounts := filtered[Amount];
let joined := concat(amounts);
```

**Grund**: Nur dokumentierte Funktionen verwenden. Siehe `rules/forbidden-patterns.md`

---

## Fehler 6: Falsche Syntax aus anderen Sprachen

### ❌ FALSCH
```ninox
// JavaScript-Syntax - funktioniert NICHT
for (let i = 0; i < length; i++) {
  // Code
}

// Python-Syntax - funktioniert NICHT
for item in array:
  // Code
```

### ✅ RICHTIG
```ninox
// Ninox-Syntax
for item in collection do
  // Code
end
```

**Grund**: Ninox hat eigene Syntax. Siehe `rules/forbidden-patterns.md`

---

## Fehler 7: Undokumentierte Features ohne Kennzeichnung

### ❌ FALSCH
```ninox
// Undokumentiertes Feature ohne Kennzeichnung
let records := select Table[Condition];
```

### ✅ RICHTIG
```ninox
// ⚠️ Nicht in offizieller Dokumentation, aber funktioniert
let records := select Table[Condition];
```

**Grund**: Undokumentierte Features müssen gekennzeichnet werden. Siehe `rules/undocumented-features.md`

---

## Fehler 8: Keine Validierung

### ❌ FALSCH
```ninox
let result := amount / divisor; // Kann Division durch Null verursachen
```

### ✅ RICHTIG
```ninox
if divisor != 0 then
  let result := amount / divisor;
else
  // Fehlerbehandlung
end
```

**Grund**: Immer Eingaben validieren.

---

## Fehler 9: Alle Datensätze laden statt Limit

### ❌ FALSCH
```ninox
let recentOrders := select Orders order by Date desc;
```

### ✅ RICHTIG
```ninox
let recentOrders := select Orders order by Date desc limit 10;
```

**Grund**: Bei großen Datensätzen nur benötigte Daten laden.

---

## Fehler 10: Verschachtelte Selects

### ❌ FALSCH
```ninox
let customers := select Customers;
for customer in customers do
  let orders := select Orders where Customer = customer;
  for order in orders do
    let items := select OrderItems where Order = order;
  end
end
```

### ✅ RICHTIG
```ninox
let allOrders := select Orders;
let allItems := select OrderItems;
for customer in select Customers do
  let orders := allOrders[Customer = customer];
  for order in orders do
    let items := allItems[Order = order];
  end
end
```

**Grund**: Vermeide verschachtelte Selects für bessere Performance.

---

## Checkliste zur Fehlervermeidung

Vor jedem Skript prüfen:

- [ ] Verwende `select ... where` statt nachträglicher Filterung
- [ ] Vermeide `select` in Schleifen
- [ ] Verwende `do as transaction` bei mehreren Schreiboperationen
- [ ] Verwende Aggregatfunktionen statt Loops
- [ ] Verwende nur dokumentierte Funktionen
- [ ] Kennzeichne undokumentierte Features
- [ ] Validiere Eingaben
- [ ] Verwende `limit` bei großen Datensätzen
- [ ] Vermeide verschachtelte Selects

---

**Quellen**:
- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Performance-Regeln: `rules/performance-rules.md`
- Forbidden Patterns: `rules/forbidden-patterns.md`
