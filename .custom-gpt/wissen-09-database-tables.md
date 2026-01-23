# Ninox Datenbanken - Tabellen

## Übersicht

Diese Dokumentation beschreibt die Konzepte rund um Tabellen in Ninox.

**Quelle**: https://forum.ninox.de/category/docs

---

## Tabellen-Grundlagen

### Tabellen erstellen
Tabellen werden in der Ninox-Oberfläche erstellt und enthalten Datensätze.

### Datensätze
- Jede Tabelle enthält Datensätze (Records)
- Jeder Datensatz hat Felder (Fields)
- Felder können verschiedene Typen haben

**Quelle**: Ninox Dokumentation - Tabellen

---

## Select-Anweisungen

### Alle Datensätze
```ninox
select Table
```

### Gefilterte Datensätze
```ninox
select Table where condition
```

### Sortierte Datensätze
```ninox
select Table order by field
select Table order by field desc
```

### Begrenzte Anzahl
```ninox
select Table limit 10
```

**Quelle**: https://ninox.com/de/tutorials/advanced-tutorial-2

---

## Datensatz-Operationen

### Datensatz erstellen
```ninox
let newRecord := create Table;
newRecord.Field := value;
```

### Datensatz lesen
```ninox
let record := first(select Table where ID = 1);
let value := record.Field;
```

### Datensatz aktualisieren
```ninox
record.Field := newValue;
```

### Datensatz löschen
```ninox
delete record;
```

**Quelle**: Ninox Dokumentation

---

## Feld-Zugriff

### Einfache Felder
```ninox
record.TextField
record.NumberField
record.DateField
```

### Relation-Felder
```ninox
record.RelationField
record.RelationField.Field
```

**Quelle**: Ninox Dokumentation

---

## Tabellen-Beziehungen

### 1:N Beziehung
Eine Tabelle kann mehrere Datensätze in einer anderen Tabelle referenzieren.

### N:1 Beziehung
Mehrere Datensätze können auf einen Datensatz in einer anderen Tabelle verweisen.

### M:N Beziehung
Viele-zu-Viele-Beziehung über Zwischentabelle.

**Quelle**: https://forum.ninox.de/category/docs

---

## Wichtige Hinweise

1. **Performance**: Verwende `select ... where` für bessere Performance
2. **Beziehungen**: Nutze Relation-Felder für Verknüpfungen zwischen Tabellen
3. **Felder**: Direkter Zugriff über Punkt-Notation

---

**Quellen**:
- Offizielle Dokumentation: https://forum.ninox.de/category/docs
- Ninox Tutorials: https://ninox.com/de/tutorials
