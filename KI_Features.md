Ein **lokaler KI-Assistent** (z. B. mit Ollama oder LM Studio) lässt sich hervorragend als Kern für das Projekt nutzen.

Anstelle einer rein browserbasierten Lösung läuft die KI dabei direkt als **lokaler Server auf dem Rechner** des Nutzers. Dadurch habt ihr ein extrem leistungsfähiges System mit echtem Kontext-Gedächtnis und vollständiger Datenkontrolle.

---

# Projekt-Aufgabenstellung: Personal LearnHub (Local-AI Edition)

**Ziel:** Entwickelt als 6er-Team eine lokale Web-Anwendung für einen **persönlichen KI-Lernassistenten**. Die KI läuft lokal auf dem Rechner (z. B. über **Ollama**), bietet ein Anmeldesystem, speichert den Lernfortschritt ab und besitzt ein Langzeit-Gedächtnis für frühere Unterhaltungen.

Das Frontend wird kollaborativ über GitHub entwickelt und lässt sich lokal oder über **GitHub Pages** ausführen.

---

## 1. Architektur-Konzept (Local AI + Local Storage)

```
┌─────────────────────────────────────────────────────────────┐
│ Web-App (Browser / GitHub Pages)                            │
│                                                             │
│  [ Login-Maske ] ──> [ Gedächtnis (indexedDB / LocalStorage)│
│                            │                                │
│                            ▼                                │
│                   [ Chat & Dashboard ]                      │
└────────────────────────────┬────────────────────────────────┘
                             │ REST API (http://localhost:11434)
                             ▼
┌─────────────────────────────────────────────────────────────┐
│ Lokaler KI-Server (Ollama / LM Studio)                      │
│ (z. B. Llama 3, Mistral, Gemma)                             │
└─────────────────────────────────────────────────────────────┘

```

---

## 2. Funktionale Anforderungen (Features)

* **Anmelde- & Profilsystem:**
* Login-Maske zum Anlegen persönlicher Lernprofile (Jahrgangsstufe, Fächer, bevorzugter Lerntyp).


* **Langzeit-Gedächtnis (Memory):**
* Speicherung von Gesprächsverläufen und Wissensständen in der lokalen Browser-Datenbank (`indexedDB`).
* Beim Senden einer Nachricht wird der relevante Chat-Kontext als Gedächtnis an die lokale KI übergeben.


* **Schnittstelle zur lokalen KI:**
* Anbindung an den lokalen Ollama-Server (`http://localhost:11434/api/generate`) über einfache `fetch`-Aufrufe.


* **Lernstand- & Fortschritts-Tracker:**
* Erfassung von verstandenen und noch zu wiederholenden Themen auf einem übersichtlichen Dashboard.



---

## 3. Technische Anforderungen

* **Frontend:** HTML5, CSS3, JavaScript (ES6 Modules).
* **Lokale KI-Engine:** [Ollama](https://ollama.com/) (kostenlos, lokal installierbar, z. B. mit `ollama run llama3`).
* **Datenbank:** Browser-interne `indexedDB` (für unbegrenzten Speicherplatz von Chat-Verläufen und Profilen).
* **Versionierung & Hosting:** Git, GitHub-Repository, GitHub Pages.

---

## 4. Rollen- und Aufgabenverteilung (6 Personen)

| Person | Modul / Rolle | Dateipfad | Konkrete Anforderung |
| --- | --- | --- | --- |
| **Person 1** | **Repository & App-Frame** | `index.html`, `js/app.js` | Erstellt das Grundgerüst, das Ansichten-Routing (Login vs. Chat-Dashboard) und verwaltet den `main`-Branch. |
| **Person 2** | **Anmelde- & Profil-System** | `js/auth.js` | Entwickelt die Benutzerverwaltung (Anmeldung, Profilauswahl, Speichern der Einstellungen). |
| **Person 3** | **Lokale KI-Schnittstelle** | `js/ollama-service.js` | Schreibt den Service zur Kommunikation mit der lokalen Ollama-API (`http://localhost:11434`). |
| **Person 4** | **Gedächtnis & Context-Engine** | `js/memory.js` | Baut die `indexedDB`-Anbindung auf, lädt frühere Chatverläufe und fügt sie als Kontext in neue Anfragen ein. |
| **Person 5** | **UI/UX & Fortschritts-Dashboard** | `style.css`, `js/dashboard.js` | Gestaltet die Benutzeroberfläche (Chat-Fenster, Theme-Switch, Fortschrittsanzeigen). |
| **Person 6** | **Doku, Setup-Guide & Pages** | `README.md`, `assets/` | schreibt die Anleitung zur Installation von Ollama/Modellen und richtet **GitHub Pages** ein. |

---

## 5. Git-Workflow-Vorgaben für das Team

1. **Haupt-Branch schützen:** Keine direkten Commits im `main`-Branch (Ausnahme: Initiales Setup durch Person 1).
2. **Branching-Konvention:** Jedes Teammitglied arbeitet in einer eigenen Branch: `feature/<modul-name>` (z. B. `feature/ollama-service`).
3. **Commit-Standards:** Regelmäßige Commits mit klaren Beschreibungen (`git commit -m "Add Ollama fetch handler"`).
4. **Pull Requests & Code Reviews:** Jedes Modul wird per GitHub Pull Request eingereicht und muss von mindestens einem anderen Teammitglied geprüft und getestet werden, bevor gemergt wird.