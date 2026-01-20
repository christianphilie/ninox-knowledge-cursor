# Ninox Automatisierung - API

## Übersicht

Diese Dokumentation beschreibt die API-Funktionalität in Ninox.

**Quelle**: https://forum.ninox.de/category/docs

---

## HTTP-Funktion

### Basis-HTTP-Request
```ninox
http(url, options)
```

### GET-Request
```ninox
let response := http("https://api.example.com/data", {
  method: "GET",
  headers: {
    "Authorization": "Bearer token"
  }
});
```

### POST-Request
```ninox
let response := http("https://api.example.com/data", {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: {
    "key": "value"
  }
});
```

**Quelle**: Ninox API-Dokumentation

---

## REST API

### Authentifizierung
Die Ninox REST API verwendet Bearer-Token für die Authentifizierung.

### Endpunkte
Die API-Endpunkte variieren je nach Cloud-Typ (Public Cloud, Private Cloud, On-Premises).

**Quelle**: https://forum.ninox.de/category/api

---

## Integration mit externen Tools

### Zapier
Ninox kann mit Zapier integriert werden.

### Make (ehemals Integromat)
Integration über die REST API möglich.

**Quelle**: Ninox API-Dokumentation

---

## Wichtige Hinweise

1. **Authentifizierung**: Immer korrekte Authentifizierung verwenden
2. **Error Handling**: HTTP-Requests können fehlschlagen, entsprechend behandeln
3. **Rate Limits**: Beachte mögliche Rate Limits der API

---

**Quellen**:
- Offizielle Dokumentation: https://forum.ninox.de/category/api
- API-Referenz: https://forum.ninox.de
