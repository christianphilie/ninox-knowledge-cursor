# Relationen und for-Schleifen in Ninox

## Übersicht

Dieses Dokument erklärt den korrekten Umgang mit Relationen und for-Schleifen in Ninox-Skripten.

**Quelle**: https://forum.ninox.de/category/docs

---

## Was sind Relationen?

Relationen sind verknüpfte Tabellen in Ninox. Wenn eine Tabelle `Rechnungen` eine Relation `'Rechnung Positionen'` hat, dann zeigt diese Relation automatisch nur die Positionen, die zu der aktuellen Rechnung gehören.

**Wichtig**: Beziehungsfelder (Relationen) sind **keine Tabellen** und können nicht direkt in `select`-Statements verwendet werden. Verwende stattdessen den Namen der zugrundeliegenden Tabelle.

**Beispiel**:
- ❌ FALSCH: `select 'Pos Produkte /Leistungen' where ...` (Beziehungsfeld)
- ✅ RICHTIG: `select 'Pos Produkte' where ...` (Tabelle)

---

## For-Schleifen mit Relationen

### ✅ RICHTIG: Direkte Iteration über Relationen

```ninox
"Relation ist bereits kontextbezogen gefiltert";
"WICHTIG: this in Variable speichern, um Kontext-Probleme zu vermeiden";
let my := this;
for i in 'Rechnung Positionen' do
  "'Rechnung Positionen' zeigt automatisch nur Positionen von 'my'";
  "Code";
end
```

**Grund**: 
- Relationen sind bereits durch den Kontext gefiltert. Wenn du `my.'Rechnung Positionen'` verwendest, zeigt es nur die Positionen der aktuellen Rechnung.
- **Wichtig**: `let my := this;` speichert den Kontext zuverlässig und vermeidet Probleme mit `this` in Schleifen oder komplexeren Operationen. Siehe auch `rules/common-mistakes.md` - Fehler 13.

---

## For-Schleifen mit Select-Statements

### ✅ RICHTIG: Select vor der Schleife

```ninox
"Erst select, dann iterieren";
let positions := select 'Rechnung Positionen' where Rechnungen = myID order by Pos;
for i in positions do
  "Code";
end
```

**Grund**: `select` erstellt eine gefilterte und sortierte Sammlung, über die dann iteriert werden kann.

---

## ❌ FALSCH: Where-Klausel direkt in for-Schleife

```ninox
"Funktioniert NICHT in Ninox";
for i in select 'Rechnung Positionen' where Rechnungen = myID order by Pos do
  "Code";
end
```

**Grund**: `for`-Schleifen können nicht direkt mit `select ... where` kombiniert werden. Die Syntax `for ... in select ... where ...` wird nicht unterstützt.

---

## Wann Relationen verwenden?

### Relationen verwenden, wenn:
- Du über alle verknüpften Datensätze eines aktuellen Records iterieren willst
- Die Filterung automatisch durch den Kontext erfolgt
- Du keine zusätzliche Sortierung benötigst

**Beispiel**:
```ninox
let my := this;
for position in 'Rechnung Positionen' do
  "Verarbeitung aller Positionen dieser Rechnung";
end
```

---

## Wann Select verwenden?

### Select verwenden, wenn:
- Du zusätzliche Filterung benötigst (nicht nur Kontext-Filterung)
- Du Sortierung benötigst (`order by`)
- Du Limitierung benötigst (`limit`)
- Du über Datensätze aus verschiedenen Kontexten iterieren willst

**Beispiel**:
```ninox
"Alle Positionen einer bestimmten Rechnung, sortiert";
let positions := select 'Rechnung Positionen' where Rechnungen = myID order by 'Pos Nr';
for i in positions do
  "Verarbeitung";
end
```

---

## Beziehungsfelder vs. Tabellen in select

### ❌ FALSCH: Beziehungsfeld in select verwenden
```ninox
"Beziehungsfeld kann nicht direkt in select verwendet werden";
let artikelPositionen := select 'Pos Produkte /Leistungen' where Servicebericht = thisServicebericht;
```

**Problem**: `'Pos Produkte /Leistungen'` ist ein Beziehungsfeld (Relation), keine Tabelle. Beziehungsfelder zeigen nur auf Datensätze in anderen Tabellen und können nicht direkt in `select` verwendet werden.

### ✅ RICHTIG: Tabelle verwenden
```ninox
"Verwende die zugrundeliegende Tabelle";
let artikelPositionen := select 'Pos Produkte' where Servicebericht = thisServicebericht;
```

**Grund**: 
- `select` benötigt den Namen der tatsächlichen Tabelle
- Die Tabelle enthält die Datensätze, das Beziehungsfeld zeigt nur darauf
- Mit `where` kann dann nach dem verknüpften Datensatz gefiltert werden

**Wann welches verwenden**:
- **Beziehungsfeld**: Direkt in `for`-Schleifen: `for pos in 'Pos Produkte /Leistungen' do`
- **Tabelle**: In `select`-Statements: `select 'Pos Produkte' where Servicebericht = ...`

---

## Häufige Fehler

### Fehler 1: Where in for-Schleife
```ninox
"❌ FALSCH";
for i in select Table where Condition do
end
```

```ninox
"✅ RICHTIG";
let filtered := select Table where Condition;
for i in filtered do
end
```

### Fehler 2: Relation mit where kombinieren
```ninox
"❌ FALSCH - Relationen haben keinen where-Parameter";
for i in 'Rechnung Positionen' where Bedingung do
end
```

```ninox
"✅ RICHTIG - Erst select mit where, dann iterieren";
let filtered := select 'Rechnung Positionen' where Bedingung;
for i in filtered do
end
```

### Fehler 3: Beziehungsfeld statt Tabelle in select
```ninox
"❌ FALSCH - Beziehungsfeld kann nicht in select verwendet werden";
let positions := select 'Pos Produkte /Leistungen' where Servicebericht = my;
```

```ninox
"✅ RICHTIG - Verwende die Tabelle";
let positions := select 'Pos Produkte' where Servicebericht = my;
```

---

## Best Practices

1. **Bei Relationen**: Direkt über die Relation iterieren
   ```ninox
   for item in Relation do
   ```

2. **Bei Select**: Erst select, dann iterieren
   ```ninox
   let collection := select Table where Condition;
   for item in collection do
   ```

3. **Performance**: Bei großen Datensätzen `limit` verwenden
   ```ninox
   let collection := select Table where Condition limit 100;
   for item in collection do
   ```

---

## Zusammenfassung

| Situation | Syntax |
|-----------|--------|
| Relation im aktuellen Kontext | `for i in 'Relation' do` |
| Gefilterte Datensätze | `let filtered := select Table where Condition; for i in filtered do` |
| Sortierte Datensätze | `let sorted := select Table order by Field; for i in sorted do` |
| Limitierte Datensätze | `let limited := select Table limit 10; for i in limited do` |
| **Wichtig**: Beziehungsfeld in select | `select Table where ...` (nicht `select 'Beziehungsfeld'`) |

**Wichtig**: `for ... in select ... where ...` funktioniert **NICHT** in Ninox!

---

**Quellen**:
- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Common Mistakes: `rules/common-mistakes.md`
