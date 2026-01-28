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
"✅ GUT";
let customerName := "Max Mustermann";
let orderTotal := sum(select Orders[Amount]);

"❌ SCHLECHT";
let x := "Max Mustermann";
let t := sum(select Orders[Amount]);
```

### this-Kontext: Immer in Variable speichern
**WICHTIG**: Um this-Kontext-Probleme zu vermeiden, speichere `this` zu Beginn in einer Variable:

```ninox
"Best Practice: this in Variable speichern";
let my := this;
"Danach überall 'my' statt 'this' verwenden";
for item in my.Relation do
  "Verarbeitung";
end
```

**Grund**: `this` kann in bestimmten Kontexten (Schleifen, verschachtelte Funktionen) Probleme verursachen. `let my := this;` speichert den Kontext zuverlässig.

Siehe auch: `rules/common-mistakes.md` - Fehler 13

---

## Kommentare

### WICHTIG: Kommentar-Syntax in Ninox

**In Ninox funktionieren Kommentare NICHT mit `//` oder `/* */`!**

Kommentare werden als String-Statements geschrieben:

```ninox
let code := 1;
"Dies ist ein Kommentar!";
let mehrCode := 2;
"Mehrzeilige Kommentare";
"müssen als separate";
"String-Statements geschrieben werden";
```

### Wann kommentieren
- Komplexe Logik erklären
- Undokumentierte Features kennzeichnen
- Wichtige Entscheidungen dokumentieren

### Format
```ninox
"Einzeiliger Kommentar";

"Mehrzeilige Kommentare";
"müssen als separate";
"String-Statements geschrieben werden";

"⚠️ Nicht in offizieller Dokumentation, aber funktioniert";
let records := select Table[Condition];
```

### Beispiel
```ninox
let my := this;
"Berechnet den Bestand aus Lagerbuchungen";
"⚠️ Nicht in offizieller Dokumentation, aber funktioniert: Relation[Filter]";
first(my.Produkt.Lagerbuchungen[Lager = my.'von Quell-Lager']).'Bestand in Basiseinheit in diesem Lager'
```

---

## Funktionen

### Eigene Funktionen
- Verwende aussagekräftige Funktionsnamen
- Dokumentiere Parameter und Rückgabewerte
- Halte Funktionen fokussiert

### Beispiel
```ninox
"Berechnet den Gesamtpreis inklusive Steuer";
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
  "Verarbeitung";
else
  "Fehlerbehandlung";
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
"Berechnet Gesamtsumme aller offenen Bestellungen";
function calculateOpenOrdersTotal() do
  let openOrders := select Orders where Status = "Open";
  sum(openOrders[Amount])
end

"Hauptlogik";
do as transaction
  let total := calculateOpenOrdersTotal();
  if total > 1000 then
    "Verarbeitung";
  end
end
```

### Schlechter Code-Stil
```ninox
"Keine Kommentare, schlechte Namen, keine Performance-Optimierung";
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
