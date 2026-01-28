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
  "Verarbeitung";
end
```

### ✅ RICHTIG
```ninox
let allOrders := select Orders;
for customer in select Customers do
  let orders := allOrders[Customer = customer];
  "Verarbeitung";
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
"Diese Funktionen existieren NICHT in Ninox";
let filtered := orders.filter(o => o.Status = "Open");
let mapped := orders.map(o => o.Amount);
let joined := array.join(orders, ",");
```

### ✅ RICHTIG
```ninox
"Verwende dokumentierte Funktionen";
let filtered := select Orders where Status = "Open";
let amounts := filtered[Amount];
let joined := concat(amounts);
```

**Grund**: Nur dokumentierte Funktionen verwenden. Siehe `rules/forbidden-patterns.md`

---

## Fehler 6: Falsche Syntax aus anderen Sprachen

### ❌ FALSCH
```ninox
"JavaScript-Syntax - funktioniert NICHT";
for (let i = 0; i < length; i++) {
  "Code";
}

"Python-Syntax - funktioniert NICHT";
for item in array:
  "Code";
```

### ✅ RICHTIG
```ninox
"Ninox-Syntax";
for item in collection do
  "Code";
end
```

**Grund**: Ninox hat eigene Syntax. Siehe `rules/forbidden-patterns.md`

---

## Fehler 7: Undokumentierte Features ohne Kennzeichnung

### ❌ FALSCH
```ninox
"Undokumentiertes Feature ohne Kennzeichnung";
let records := select Table[Condition];
```

### ✅ RICHTIG
```ninox
"⚠️ Nicht in offizieller Dokumentation, aber funktioniert";
let records := select Table[Condition];
```

**Grund**: Undokumentierte Features müssen gekennzeichnet werden. Siehe `rules/undocumented-features.md`

---

## Fehler 8: Keine Validierung

### ❌ FALSCH
```ninox
let result := amount / divisor;
"Kann Division durch Null verursachen";
```

### ✅ RICHTIG
```ninox
if divisor != 0 then
  let result := amount / divisor;
else
  "Fehlerbehandlung";
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

## Fehler 11: Where-Klausel in for-Schleife mit Relationen

### ❌ FALSCH
```ninox
"Funktioniert NICHT: where-Klausel kann nicht direkt in for-Schleife verwendet werden";
for i in select 'Rechnung Positionen' where Rechnungen = myID order by Pos do
  "Code";
end
```

### ✅ RICHTIG
```ninox
"Bei Relationen direkt über die Relation iterieren";
"'Rechnung Positionen' ist bereits gefiltert durch den Kontext (this)";
for i in 'Rechnung Positionen' do
  "Code";
end

"Oder: Erst select, dann iterieren";
let positions := select 'Rechnung Positionen' where Rechnungen = myID order by Pos;
for i in positions do
  "Code";
end
```

**Grund**: `for`-Schleifen können nicht direkt mit `select ... where` kombiniert werden. Bei Relationen (wie `'Rechnung Positionen'`) wird direkt über die Relation iteriert, die bereits durch den Kontext gefiltert ist.

**Wichtig**: 
- Relationen sind bereits kontextbezogen gefiltert (z.B. `this.'Rechnung Positionen'` zeigt nur Positionen der aktuellen Rechnung)
- Bei `select`-Statements muss die Filterung explizit erfolgen
- `order by` kann nur in `select`-Statements verwendet werden, nicht direkt in `for`-Schleifen

---

## Fehler 12: Falsche Feldnamen durch Annahmen

### ❌ FALSCH
```ninox
"Annahme: Feld heißt 'Pos', aber tatsächlich heißt es 'Pos Nr'";
for i in 'Rechnung Positionen' do
  newPos.Pos := i.Pos;
  "Funktioniert nicht!";
end

"Annahme: Feld heißt 'Mengeneinheit', aber tatsächlich heißt es 'Einheit'";
newPos.Mengeneinheit := i.Mengeneinheit;
"Funktioniert nicht!";
```

### ✅ RICHTIG
```ninox
"Erst nachfragen oder prüfen, wie die Felder genau heißen";
"Dann korrekte Feldnamen verwenden";
for i in 'Rechnung Positionen' do
  newPos.'Pos Nr' := i.'Pos Nr';
  "Korrekter Feldname";
  newPos.Einheit := i.Einheit;
  "Korrekter Feldname";
end
```

**Grund**: Feldnamen können verschiedene Varianten haben. Häufige Varianten:
- Positionsnummern: `Pos`, `Pos Nr`, `Position`, `PosNr`
- Einheiten: `Einheit`, `Mengeneinheit`, `Mengeneinheit_alt`, `Unit`
- Datumsfelder: `Datum`, `Erstellungsdatum`, `'Datum Rechnung'`, `'Abrechnungsdatum von'`

**Wichtig**: Wenn Feldnamen nicht eindeutig sind, IMMER nachfragen statt raten! Siehe `rules/context-queries.md`

---

## Fehler 13: this-Kontext-Probleme vermeiden

### ❌ PROBLEMATISCH
```ninox
"this kann in bestimmten Kontexten Probleme verursachen";
for buchung in this.Produkt.Lagerbuchungen do
  if buchung.Lager = this.'von Quell-Lager' then
    "Verarbeitung";
  end
end
```

**Problem**: `this` kann in bestimmten Kontexten (z.B. in Schleifen, verschachtelten Funktionen, oder bei komplexeren Operationen) den falschen Kontext referenzieren oder unerwartetes Verhalten zeigen.

### ✅ RICHTIG: this in Variable speichern
```ninox
"this in Variable speichern, um Kontext-Probleme zu vermeiden";
let my := this;
for buchung in my.Produkt.Lagerbuchungen do
  if buchung.Lager = my.'von Quell-Lager' then
    "Verarbeitung";
  end
end
```

**Grund**: 
- `let my := this;` speichert den aktuellen Kontext zuverlässig
- `my` behält den Kontext auch in verschachtelten Strukturen bei
- Vermeidet Probleme mit `this` in Schleifen oder komplexeren Operationen
- Standard-Pattern für zuverlässigen Kontext-Zugriff

**Wann verwenden**:
- Immer wenn `this` mehrfach verwendet wird
- In Schleifen, die auf `this` zugreifen
- Bei verschachtelten Operationen
- Bei komplexeren Skripten, um Kontext-Probleme zu vermeiden

**Best Practice**: 
- Zu Beginn des Skripts: `let my := this;`
- Dann überall `my` statt `this` verwenden
- Besonders wichtig bei Relationen: `my.Relation` statt `this.Relation`

---

## Fehler 14: Beziehungsfelder direkt in select verwenden

### ❌ FALSCH
```ninox
"Beziehungsfeld kann nicht direkt in select verwendet werden";
let artikelPositionen := select 'Pos Produkte /Leistungen' where Servicebericht = thisServicebericht and 'Produktart' = 2;
```

**Problem**: `'Pos Produkte /Leistungen'` ist ein Beziehungsfeld (Relation), keine Tabelle. Beziehungsfelder können nicht direkt in `select`-Statements verwendet werden.

### ✅ RICHTIG: Tabelle verwenden
```ninox
"Verwende die zugrundeliegende Tabelle statt des Beziehungsfelds";
let artikelPositionen := select 'Pos Produkte' where Servicebericht = thisServicebericht and 'Produktart' = 2;
```

**Grund**: 
- Beziehungsfelder sind nur Referenzen auf Datensätze in anderen Tabellen
- `select` benötigt den Namen der tatsächlichen Tabelle
- Die Tabelle enthält die Datensätze, das Beziehungsfeld zeigt nur darauf

**Wichtig**: 
- Beziehungsfelder können direkt in `for`-Schleifen verwendet werden: `for pos in 'Pos Produkte /Leistungen' do`
- Für `select` mit `where` muss die Tabelle verwendet werden: `select 'Pos Produkte' where ...`
- Siehe auch `rules/relations-and-loops.md` für Details zu Relationen

---

## Fehler 15: Dynamische Auswahl-Felder mit Record-Objekt setzen

### ❌ FALSCH
```ninox
"Fehler: Field must return dynamic values";
let lagerort := first(select Lagerorte where Warenwirtschaft = warenwirtschaft and Nutzer = mitarbeiterBenutzer);
newAbbuchung.(
    Lager := lagerort;  "Funktioniert nicht bei dynamischen Auswahl-Feldern!"
)
```

**Problem**: Dynamische Auswahl-Felder erwarten eine Collection oder einen numerischen Wert, nicht direkt ein Record-Objekt. Der Fehler "Field must return dynamic values" tritt auf.

### ✅ RICHTIG: number() verwenden
```ninox
"Verwende number() um Record in numerischen Wert zu konvertieren";
let lagerort := first(select Lagerorte where Warenwirtschaft = warenwirtschaft and Nutzer = mitarbeiterBenutzer);
newAbbuchung.(
    Lager := number(lagerort);  "Konvertiert Record zu numerischem Wert"
)
```

**Grund**: 
- Dynamische Auswahl-Felder basieren auf Tabellen-Datensätzen
- `number(record)` konvertiert den Record in einen numerischen Wert (ID/Nr)
- Dieser numerische Wert kann dann im dynamischen Auswahl-Feld verwendet werden

**Alternative Lösungen** (falls `number()` nicht funktioniert):
- Collection mit einem Element: `Lager := select Lagerorte where Nr = lagerort.Nr;`
- Direktes Select im Zuweisungsblock: `Lager := first(select Lagerorte where ...);`

**Hinweis**: 
- Funktioniert nur, wenn das dynamische Auswahl-Feld auf der gleichen Tabelle basiert
- Bei Relation-Feldern kann der Record direkt verwendet werden: `RelationFeld := record;`

---

## Fehler 16: Keine Prüfung gegen doppelte Ausführung

### ❌ FALSCH
```ninox
"Operation wird bei jedem Aufruf ausgeführt, auch wenn bereits erledigt";
"Lagerbuchungen für verwendete Artikel erstellen";
let warenwirtschaft := first(select Warenwirtschaft);
"Erstellt Lagerbuchungen, auch wenn bereits vorhanden";
```

**Problem**: Wenn ein Skript mehrfach ausgeführt wird (z.B. durch erneutes Klicken auf einen Button oder durch Fehlerbehandlung), werden Operationen mehrfach ausgeführt, was zu Duplikaten führt.

### ✅ RICHTIG: Flag-Feld verwenden
```ninox
"Prüfung mit Flag-Feld verhindert doppelte Ausführung";
if not 'Lagerbuchungen für eingesetzte Artikel bereits erstellt' then
    "Lagerbuchungen für verwendete Artikel erstellen";
    let warenwirtschaft := first(select Warenwirtschaft);
    "Erstellt Lagerbuchungen nur einmal";
    "Am Ende:";
    'Lagerbuchungen für eingesetzte Artikel bereits erstellt' := true;
end
```

**Grund**: 
- Flag-Feld (Boolean) markiert, ob Operation bereits ausgeführt wurde
- Prüfung zu Beginn verhindert erneute Ausführung
- Flag wird am Ende gesetzt, nach erfolgreicher Ausführung

**Best Practices**:
- Flag-Feld sollte einen aussagekräftigen Namen haben
- Flag sollte erst am Ende gesetzt werden, nach erfolgreicher Ausführung
- Bei Fehlern sollte das Flag nicht gesetzt werden, damit Retry möglich ist
- Alternativ: Prüfung auf bereits existierende Datensätze statt Flag-Feld

---

## Checkliste zur Fehlervermeidung

Vor jedem Skript prüfen:

- [ ] **Feldnamen klar?** Wenn nicht eindeutig → NACHFRAGEN (siehe `rules/context-queries.md`)
- [ ] **Tabellennamen klar?** Wenn nicht eindeutig → NACHFRAGEN
- [ ] **Relationen klar?** Wenn Kontext unklar → NACHFRAGEN
- [ ] Verwende `select ... where` statt nachträglicher Filterung
- [ ] Vermeide `select` in Schleifen
- [ ] Bei Relationen: Iteriere direkt über die Relation, nicht mit `select ... where` in der for-Schleife
- [ ] Verwende `do as transaction` bei mehreren Schreiboperationen
- [ ] Verwende Aggregatfunktionen statt Loops
- [ ] Verwende nur dokumentierte Funktionen
- [ ] Kennzeichne undokumentierte Features
- [ ] Validiere Eingaben
- [ ] Verwende `limit` bei großen Datensätzen
- [ ] Vermeide verschachtelte Selects
- [ ] Verwende `let my := this;` zu Beginn, um this-Kontext-Probleme zu vermeiden
- [ ] Verwende Tabellennamen statt Beziehungsfelder in `select`-Statements
- [ ] Verwende `number(record)` für dynamische Auswahl-Felder
- [ ] Prüfe mit Flag-Feldern gegen doppelte Ausführung von Operationen

---

**Quellen**:
- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Performance-Regeln: `rules/performance-rules.md`
- Forbidden Patterns: `rules/forbidden-patterns.md`
- Kontext-Abfragen: `rules/context-queries.md` - Wann nachfragen statt raten