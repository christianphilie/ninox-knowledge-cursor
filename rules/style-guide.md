# Ninox Scripting - Style Guide

## Übersicht

Dieser Style Guide beschreibt Coding-Standards und Best Practices für Ninox-Skripte.

---

## Code-Formatierung

### Einrückung
Verwende konsistente Einrückung (z.B. 2 Leerzeichen oder Tabs).

### Zeilenlänge
Halte Zeilen übersichtlich. Bei langen Zeilen umbrechen.

### Leerzeilen
Verwende Leerzeilen zur Gruppierung logisch zusammengehöriger Code-Blöcke.

---

## Variablen-Namen

### Benennung
- Verwende aussagekräftige Namen
- Verwende camelCase für Variablen
- Verwende klare, beschreibende Namen

### Beispiele
```ninox
// ✅ GUT
let customerName := "Max Mustermann";
let orderTotal := sum(select Orders[Amount]);

// ❌ SCHLECHT
let x := "Max Mustermann";
let t := sum(select Orders[Amount]);
```

---

## Kommentare

### Wann kommentieren
- Komplexe Logik erklären
- Undokumentierte Features kennzeichnen
- Wichtige Entscheidungen dokumentieren

### Format
```ninox
// Einzeiliger Kommentar

/*
 Mehrzeiliger Kommentar
 für komplexere Erklärungen
 */

// ⚠️ Nicht in offizieller Dokumentation, aber funktioniert
let records := select Table[Condition];
```

---

## Funktionen

### Eigene Funktionen
- Verwende aussagekräftige Funktionsnamen
- Dokumentiere Parameter und Rückgabewerte
- Halte Funktionen fokussiert

### Beispiel
```ninox
// Berechnet den Gesamtpreis inklusive Steuer
function calculateTotal(amount, taxRate) do
  amount + (amount * taxRate)
end
```

---

## Fehlerbehandlung

### Validierung
Validiere Eingaben bevor du sie verwendest.

```ninox
if amount > 0 then
  // Verarbeitung
else
  // Fehlerbehandlung
end
```

---

## Performance

### Best Practices
- Verwende `select ... where` statt nachträglicher Filterung
- Verwende `do as transaction` bei mehreren Schreiboperationen
- Vermeide `select` in Schleifen
- Verwende Aggregatfunktionen statt Loops

Siehe auch: `rules/performance-rules.md`

---

## Dokumentationskonformität

### Regeln
1. Bevorzuge dokumentierte Funktionen
2. Kennzeichne undokumentierte Features
3. Verwende keine erfundenen Funktionen

Siehe auch: `rules/strict-rules.md`

---

## Beispiele

### Guter Code-Stil
```ninox
// Berechnet Gesamtsumme aller offenen Bestellungen
function calculateOpenOrdersTotal() do
  let openOrders := select Orders where Status = "Open";
  sum(openOrders[Amount])
end

// Hauptlogik
do as transaction
  let total := calculateOpenOrdersTotal();
  if total > 1000 then
    // Verarbeitung
  end
end
```

### Schlechter Code-Stil
```ninox
// Keine Kommentare, schlechte Namen, keine Performance-Optimierung
let o := select Orders;
let t := 0;
for x in o do
  if x.Status = "Open" then
    t := t + x.Amount;
  end
end
```

---

## Checkliste

Vor jedem Skript prüfen:

- [ ] Aussagekräftige Variablennamen
- [ ] Kommentare bei komplexer Logik
- [ ] Performance-Optimierungen beachtet
- [ ] Dokumentationskonformität geprüft
- [ ] Code formatiert und lesbar

---

**Quellen**:
- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Best Practices: https://forum.ninox.de
