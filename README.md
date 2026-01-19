# Shadowridge – Endless Descent

Ein **rundenbasierter Solo-Dungeon-Crawler** (2D, Web-first), inspiriert von **Four Against Darkness** (zugängliche Party-Mechaniken) und **Dungeon 100** (Tabellen-Vielfalt) mit einem **Baldur’s Gate 3**-inspirierten Interface (**inspiriert, nicht kopiert**).

> ## Status
> **Phase:** Setup / Prototype (Web-first)  
> **Spielbar:** Noch nicht (Grundgerüst wird gerade aufgebaut)  
> **Aktuell:** Godot-Projekt + Struktur + Web-Deployment via GitHub Pages wird eingerichtet  
> **Nächstes Ziel:** Erste spielbare Loop: Map → Bewegung → Encounter → Combat-Log

## Live-Demo

**Geplant (GitHub Pages):**  
`https://mazer666.github.io/Shadowridge-godot/`

> Hinweis: GitHub Pages zeigt erst dann etwas an, wenn ein Web-Export in `/docs` liegt (mindestens `docs/index.html`).

---

## Spielkonzept

- **Genre:** Solo Roguelike Dungeon-Crawler
- **Ziel:** Highscore – wie tief kommst du? Wie viel Gold sammelst du?
- **Core Loop:** Etage erkunden → Encounters/Fallen → Loot → Mini-Boss → nächster Floor  
  → alle 5 Etagen: Final-Boss

### Deine Party (fix 4 Helden)

| Held       | Rolle           | Stärken |
|------------|------------------|---------|
| Barbarian  | Melee-Tank       | Hohe HP, Rage-Bonus, Cleave |
| Ranger     | Range / Scout    | Fernkampf, Tracking, hohe Initiative |
| Wizard     | Magic-DPS        | Zauber (Kampf, Utility, Heilung, …) |
| Paladin    | Support / Tank-Light | Healing (Lay on Hands), Schutz |

- Jeder Held hat **8 Inventar-Slots** (kein Gewichtslimit)
- **Synchrone Bewegung:** Party bewegt sich als Gruppe

---

## Wichtige Mechaniken (geplant)

- **Combat:** Rundenbasiert – nur **Spieler würfelt** (D6 + Bonus vs. Gegner-Level), Würfel **explodieren**
- **Dungeon:** Prozedurale Etagen  
  - Desktop: ca. **29×20** (horizontal)  
  - Mobile: ca. **15×25** (vertikal)
- **Bosse:** Jede Etage endet mit **Mini-Boss**  
  → alle 5 Etagen **Final-Boss** mit Spezialfähigkeiten
- **Tabellen:** Erweiterte **D100**-Tabellen (Search, Combat, Fallen, Begegnungen, NPCs)
- **Shop:** Zwischen Etagen + zufällig in Räumen (wenn entdeckt)
- **Progression:** Level-Up nach Boss-Kill (z.B. +1 HP/ATK, neue Traits möglich)

---

## Roadmap (Prioritäten)

### MVP 1 — “First Playable Loop”
- [ ] Boot/Main Scene + State/Signals Grundgerüst
- [ ] Dungeon-Map (Grid) + einfache Sichtbarkeit/Fog
- [ ] Party Movement (Keyboard + Mouse + Touch) inkl. “Tap to Move”
- [ ] Basic Encounter Trigger
- [ ] Combat v0 (nur Spieler würfelt: D6 + Bonus vs. Gegner-Level, exploding dice)
- [ ] Combat Log (scrollbar, farblich)

### MVP 2 — “BG3-Feeling UI”
- [ ] Party Panel: Portraits, HP, Stats
- [ ] Inventar (8 Slots je Held)
- [ ] Quickcast-Hotbar (unten: Actions + Items, Hotkeys 1–0)
- [ ] Tooltips (lesbar, verdecken Buttons nicht)

### Post-MVP — “Content & Progression”
- [ ] D100 Tabellen aus JSON (Search/Traps/NPC/Events)
- [ ] Shop-UI & Gold-Wirtschaft
- [ ] Mini-/Final-Boss Varianten
- [ ] Highscore (LocalStorage)
- [ ] Mehr visuelles Feedback + SFX

---

## Controls (Ziel)

**Desktop**
- Keyboard: Movement / Shortcuts (Hotbar 1–0)
- Mouse: Click/Tap to Move, UI Interactions

**Mobile**
- Touch: Tap to Move, Drag/Drop Inventory (später), UI Buttons gut tappbar
- Ziel: Bedienung so angenehm wie möglich (BG3-inspiriertes Panel-/Hotbar-Feeling)

---

## Technik (Godot-idiomatisch)

- **Engine:** Godot **4.5.1** (2D, GDScript)
- **State:** Autoload-Singleton `GameState` als zentrale Quelle für Spielzustand
- **Events:** Godot **Signals** (UI ↔ Systems ↔ State lose gekoppelt)
- **Content:** Datengetrieben über JSON-Dateien in `/data/` (Tabellen, Items, Gegner)
- **UI:** Responsive UI für Desktop + Mobile (Touch/Mouse/Keyboard)
- **Web:** Export als WebAssembly/WebGL2 Build und Hosting über GitHub Pages

---

## Projektstruktur (Empfehlung)

- `scenes/` – Hauptszenen (Main, Dungeon, Combat, UI Screens)
- `ui/` – UI-Szenen (Panels, Hotbar, Tooltips, Widgets)
- `scripts/` – allgemeine Scripts
  - `scripts/autoload/` – Autoloads (GameState, ggf. EventBus)
- `systems/` – Systems (combat, generation, loot, tables, saving)
- `data/` – JSON Content (D100 Tabellen, Items, Gegner, Traits)
- `assets/` – Fonts/Sprites/UI-Art
- `docs/` – **Web-Export Output** (GitHub Pages Quelle für Option A)

---

## Getting Started (macOS)

### Voraussetzungen
- **Godot:** 4.5.1 (GDScript)
- **Git:** über Xcode Command Line Tools (`xcode-select --install`)

### Lokal starten
1) Repo klonen:
- `git clone https://github.com/mazer666/Shadowridge-godot.git`

2) Godot öffnen:
- Godot starten → **Import** → Repo-Ordner auswählen  
- Datei: `project.godot` → **Open**

3) Starten:
- **Play (F5)** drücken

---

## Deployment (Web-first über GitHub Pages) — Option A

Dieses Projekt wird während der Entwicklung zuerst als **Web-Version** gebaut und über **GitHub Pages** gehostet.

### Export (Godot → Web)
- Godot: `Project > Export...` → Preset **Web**
- Export-Pfad: `docs/index.html`
- Danach commit & push: der Inhalt in `docs/` ist die Live-Demo.

### GitHub Pages Settings
Repo → Settings → Pages → Source: `main` + Folder: `/docs`

---

## Known Issues (Work in Progress)

- Web-Export benötigt Hosting (nicht per Doppelklick öffnen).
- Mobile Bedienung (Zoom/Pan/Buttons) wird iterativ optimiert.
- Performance-Optimierung erfolgt nach MVP-Loop.
- UI/Tooltips/Layout werden laufend verbessert (BG3-inspiriert, nicht kopiert).

---

## Contributing / Feedback

Feedback, Bugs und Ideen sind willkommen!

### Bitte bei Bug-Reports angeben:
- **Was ist passiert?**
- **Was hättest du erwartet?**
- **Schritte zum Reproduzieren** (1–5 Schritte)
- **Browser/Device** (z.B. Chrome Android, Safari iOS)
- **Screenshot/Video** (wenn möglich)

### Ideen / Balancing / Tabellen
- Vorschläge für D100-Einträge, Items, Traits, Gegner sind besonders hilfreich.

---

## Lizenz & Drittanbieter-Assets

- Code: siehe `LICENSE` (Apache-2.0)
- Drittanbieter-Assets (Fonts/Icons/Asset-Packs) werden separat dokumentiert:
  - geplant: `THIRD_PARTY_NOTICES.md` oder Ordner `licenses/`

> Wichtig: Assets und Fonts können eigene Lizenzen haben. Bitte vor Nutzung/Weitergabe beachten.

---
