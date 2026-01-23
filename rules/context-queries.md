# Kontext-Abfragen - Wann nachfragen?

## Übersicht

Dieses Dokument beschreibt, wann du bei Ninox-Anfragen nachfragen solltest, um Fehler zu vermeiden und bessere Ergebnisse zu liefern.

**Grundsatz**: Wenn etwas unklar ist oder vermutlich falsch sein könnte, frage nach, bevor du Code generierst.

---

## KRITISCHE SITUATIONEN - IMMER NACHFRAGEN

### 1. Feldnamen sind unklar oder vermutlich falsch

#### Situationen:
- Benutzer erwähnt Feldnamen, die nicht eindeutig sind
- Feldnamen könnten verschiedene Varianten haben (z.B. `Pos` vs `Pos Nr`, `Einheit` vs `Mengeneinheit`)
- Feldnamen enthalten Sonderzeichen oder Leerzeichen (z.B. `'Abrechnungsdatum von'`)

#### Beispiel:
```
❌ NICHT TUN: Annahme treffen, dass das Feld "Pos" heißt
✅ RICHTIG: "Wie heißt das Feld für die Positionsnummer genau? Ist es 'Pos', 'Pos Nr' oder etwas anderes?"
```

#### Häufige Feldnamen-Varianten:
- Positionsnummern: `Pos`, `Pos Nr`, `Position`, `PosNr`
- Einheiten: `Einheit`, `Mengeneinheit`, `Mengeneinheit_alt`, `Unit`
- Datumsfelder: `Datum`, `Erstellungsdatum`, `'Datum Rechnung'`, `'Abrechnungsdatum von'`
- Beziehungen: `Kunde`, `Customer`, `'Artikel / Leistung'`

**Regel**: Wenn ein Feldname nicht eindeutig ist oder verschiedene Varianten möglich sind, IMMER nachfragen.

---

### 2. Tabellennamen sind unklar

#### Situationen:
- Benutzer erwähnt Tabellennamen, die nicht eindeutig sind
- Tabellennamen könnten verschiedene Varianten haben
- Tabellennamen enthalten Sonderzeichen oder Leerzeichen

#### Beispiel:
```
❌ NICHT TUN: Annahme treffen, dass die Tabelle "Rechnungen" heißt
✅ RICHTIG: "Wie heißt die Tabelle genau? Ist es 'Rechnungen', 'Rechnung' oder 'Invoices'?"
```

---

### 3. Relationen sind unklar

#### Situationen:
- Benutzer erwähnt Relationen, aber der Kontext ist unklar
- Es ist nicht klar, ob es eine Relation oder eine Tabelle ist
- Der Name der Relation ist nicht eindeutig

#### Beispiel:
```
❌ NICHT TUN: Annahme treffen, dass 'Rechnung Positionen' eine Relation ist
✅ RICHTIG: "Ist 'Rechnung Positionen' eine Relation in der Tabelle 'Rechnungen' oder eine separate Tabelle?"
```

---

### 4. Syntax oder Funktionalität ist unklar

#### Situationen:
- Benutzer beschreibt eine Funktionalität, die nicht eindeutig ist
- Es gibt mehrere mögliche Implementierungswege
- Die Anforderung könnte auf verschiedene Weise interpretiert werden

#### Beispiel:
```
❌ NICHT TUN: Annahme treffen, wie etwas funktionieren soll
✅ RICHTIG: "Soll die Kopie alle Felder übernehmen oder nur bestimmte? Sollen Positionen automatisch sortiert werden?"
```

---

### 5. Datenbankstruktur ist unklar

#### Situationen:
- Beziehungen zwischen Tabellen sind nicht klar
- Feldtypen sind nicht bekannt
- Es ist unklar, welche Felder existieren

#### Beispiel:
```
❌ NICHT TUN: Annahme treffen über die Datenbankstruktur
✅ RICHTIG: "Welche Felder hat die Tabelle 'Rechnungen'? Gibt es ein Feld 'Lieferdatum'?"
```

---

## WICHTIGE FRAGEN ZU STELLEN

### Bei Feldnamen:
- "Wie heißt das Feld genau? [Liste mögliche Varianten auf]"
- "Enthält der Feldname Leerzeichen oder Sonderzeichen?"
- "Ist das Feld eine Relation oder ein normales Feld?"

### Bei Tabellennamen:
- "Wie heißt die Tabelle genau?"
- "Ist das eine Tabelle oder eine Relation?"

### Bei Relationen:
- "Ist '[Name]' eine Relation oder eine separate Tabelle?"
- "Zu welcher Tabelle gehört diese Relation?"

### Bei Funktionalität:
- "Soll [Funktion] alle Datensätze betreffen oder nur bestimmte?"
- "Wie soll [Verhalten] genau funktionieren?"
- "Gibt es spezielle Anforderungen, die ich beachten sollte?"

---

## WANN NICHT NACHFRAGEN

### Nicht nachfragen, wenn:
- Die Information bereits klar aus der Anfrage hervorgeht
- Es sich um Standard-Ninox-Syntax handelt
- Die Anfrage bereits alle notwendigen Informationen enthält
- Du sicher bist, dass deine Annahme korrekt ist

**Aber**: Im Zweifel lieber nachfragen als falsch zu raten!

---

## CHECKLISTE VOR CODE-GENERIERUNG

Vor dem Generieren von Code prüfe:

- [ ] Sind alle Feldnamen eindeutig?
- [ ] Sind alle Tabellennamen eindeutig?
- [ ] Ist klar, welche Relationen verwendet werden?
- [ ] Ist die Funktionalität vollständig beschrieben?
- [ ] Ist die Datenbankstruktur klar?
- [ ] Gibt es spezielle Anforderungen, die nicht erwähnt wurden?

**Wenn eine Frage mit "Nein" beantwortet wird**: Nachfragen!

---

## BEISPIEL-INTERAKTION

### Schlechte Interaktion:
```
Benutzer: "Erstelle ein Skript, das Rechnungen kopiert"
AI: [Generiert Code mit Annahmen über Feldnamen]
Benutzer: "Das funktioniert nicht, die Feldnamen sind falsch"
```

### Gute Interaktion:
```
Benutzer: "Erstelle ein Skript, das Rechnungen kopiert"
AI: "Bevor ich das Skript erstelle, brauche ich einige Informationen:
- Wie heißt das Feld für die Positionsnummer genau? (Pos, Pos Nr, Position?)
- Wie heißt das Feld für die Einheit? (Einheit, Mengeneinheit?)
- Welche Felder sollen kopiert werden? Alle oder nur bestimmte?"
Benutzer: [Antwortet mit korrekten Informationen]
AI: [Generiert korrekten Code]
```

---

## BEST PRACTICES

1. **Proaktiv nachfragen**: Lieber zu viele Fragen als falsche Annahmen
2. **Konkrete Fragen stellen**: Nicht "Ist das richtig?", sondern "Wie heißt das Feld genau?"
3. **Mögliche Varianten auflisten**: Zeige, dass du verschiedene Möglichkeiten kennst
4. **Nachfragen bei Unsicherheit**: Wenn du dir nicht sicher bist, frage nach
5. **Dokumentiere Annahmen**: Wenn du Annahmen triffst, erwähne sie im Code

---

## ZUSAMMENFASSUNG

**Goldene Regel**: Wenn etwas unklar ist oder vermutlich falsch sein könnte, frage nach, bevor du Code generierst.

**Prioritäten**:
1. Feldnamen - IMMER nachfragen, wenn nicht eindeutig
2. Tabellennamen - Nachfragen, wenn nicht eindeutig
3. Relationen - Nachfragen, wenn Kontext unklar
4. Funktionalität - Nachfragen, wenn mehrdeutig
5. Datenbankstruktur - Nachfragen, wenn nicht klar

---

**Quellen**:
- Common Mistakes: `rules/common-mistakes.md`
- Relations and Loops: `rules/relations-and-loops.md`
