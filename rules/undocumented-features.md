# Undokumentierte aber funktionierende Features

Diese Features sind **nicht** in der offiziellen Dokumentation beschrieben, funktionieren aber nachweislich. Sie dürfen verwendet werden, müssen aber **immer** mit entsprechender Kennzeichnung versehen werden.

## Verwendungsregel

**OBLIGATORISCHE KENNZEICHNUNG**: Immer mit Kommentar markieren:
```
⚠️ Nicht in offizieller Dokumentation, aber funktioniert
```

## Liste undokumentierter Features

### 1. Eckige Klammern `[]` als Filter nach `select`

**Beschreibung**: Nach einem `select` kann mit eckigen Klammern `[]` zusätzlich gefiltert werden.

**Beispiel**:
```ninox
// ⚠️ Nicht in offizieller Dokumentation, aber funktioniert
let records := select Tabelle[ Feld = "Wert" ];
```

**Hinweis**: 
- Funktioniert, aber Performance-Unterschied zu `select ... where`
- `select Tabelle where Feld = "Wert"` filtert bereits bei der Selektion (serverseitig)
- `select Tabelle[ Feld = "Wert" ]` holt zuerst alle Datensätze, dann Filterung (clientseitig)
- Bevorzuge `where` für bessere Performance

**Quelle**: Community-Beispiele im Forum

---

### Weitere Features

Diese Liste wird kontinuierlich erweitert, wenn neue undokumentierte aber funktionierende Features entdeckt werden.

## Hinzufügen neuer Features

Wenn du ein neues undokumentiertes aber funktionierendes Feature entdeckst:

1. Teste es gründlich
2. Stelle sicher, dass es konsistent funktioniert
3. Dokumentiere es hier mit:
   - Beschreibung
   - Beispiel-Code
   - Hinweise zur Verwendung
   - Quelle (wenn verfügbar)

## Wichtig

- Diese Features können sich ändern oder entfernt werden
- Keine Garantie für zukünftige Kompatibilität
- Immer dokumentierte Alternative bevorzugen, wenn verfügbar
