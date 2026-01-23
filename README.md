# Ninox AI Knowledge Base

Eine universelle Knowledge Base für KI-Codierungs-Assistenten (**[Cursor](https://cursor.sh)**, **Google Antigravity**, etc.), die mittels RAG sicherstellt, dass generierte **[Ninox](https://ninox.com)**-Skripte nur dokumentierte Funktionen verwenden.

**Problem**: KI-Modelle erfinden oft Funktionen oder übernehmen Syntax aus anderen Sprachen (wie JavaScript-Array-Methoden), die Ninox nicht unterstützt.
**Lösung**: Diese Knowledge Base nutzt **RAG (Retrieval-Augmented Generation)**. Die Regeln werden als Kontext eingebunden, sodass die KI genau weiß, was in Ninox erlaubt ist und was nicht.

---

## 🚀 Schnellstart

1.  **Repository klonen** oder herunterladen.
2.  **In Cursor oder Google Antigravity öffnen**: Die Regeln in `.cursor/rules/` bzw. Skills in `.agent/skills/` werden automatisch erkannt.
3.  **Skripte erstellen**: Erstelle deine `.nx` Dateien im Ordner `workspace/`.

---

## 📖 Detaillierte Einrichtungsanleitung

### 1. Installation
Klone das Repository in einen lokalen Ordner deiner Wahl:
```bash
git clone https://github.com/christianphilie/ninox-knowledge-ai.git
cd ninox-knowledge-ai
```

### 2. Konfiguration für verschiedene Tools

#### Für Cursor (Auto-Loading)
Cursor liest automatisch alle `.mdc` Dateien im Ordner `.cursor/rules/`. Sobald du den Projektordner in Cursor öffnest, sind die "Leitplanken" aktiv. Du musst nichts weiter tun.

#### Für Google Antigravity
Antigravity erkennt den `.agent/`-Ordner. Die Datei `.agent/skills/ninox-scripting/SKILL.md` definiert die Fähigkeiten und verweist auf die Regeldateien im Projekt. Auch hier erfolgt die Erkennung automatisch beim Öffnen des Folders.

#### Für ChatGPT (Custom GPT)
In dem Ordner `.custom-gpt/` findest du Anleitungen und Texte, um dir ein eigenes "Ninox GPT" in ChatGPT zu erstellen. Lade dazu die Markdown-Dateien aus `rules/` als Knowledge-Dateien in dein Custom GPT hoch.

---

## 📁 Projekt-Struktur

- `rules/` - Die Kern-Regeln (Whitelist, Verbotene Patterns, Performance)
- `.cursor/rules/` - Spezielle Konfiguration für den Cursor Editor
- `.agent/` - Spezielle Konfiguration für Google Antigravity (Skills & Workflows)
- `.custom-gpt/` - Anleitungen und Texte für ChatGPT (Custom GPT)
- `docs/` - Tiefergehende Dokumentation zu Scripting und Automatisierung
- `examples/` - Best-Practice Beispiele für Ninox-Skripte
- `workspace/` - Dein Arbeitsbereich für neue Skripte

---

## 🔍 Die Goldenen Regeln

Jedes von der KI generierte Ninox-Skript muss:
1.  Nur Funktionen aus der `rules/function-whitelist.md` verwenden.
2.  Keine Muster aus `rules/forbidden-patterns.md` enthalten (z.B. kein `.map()`).
3.  Saubere Syntax gemäß `rules/style-guide.md` einhalten.

---

## ⚖️ Lizenz
Creative Commons Attribution 4.0 International (CC-BY 4.0).
Ninox ist eine Marke der Ninox Software GmbH. Diese Knowledge Base ist ein Community-Projekt.

