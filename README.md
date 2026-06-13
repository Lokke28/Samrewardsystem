# 🏆 SAM Reward System

Ein vollständig funktionsfähiges Premium-Belohnungssystem für **FiveM (ESX Legacy)**.

Spieler verdienen Coins durch Aktivität und Aufgaben — kein Echtgeld erforderlich.

---

## ✨ Features

- 🪙 **Coin-System** — Automatische stündliche Belohnungen (konfigurierbar)
- 📋 **Aufgabensystem** — 12+ Quests mit Fortschrittsanzeige (erweiterbar)
- 🛒 **Reward Shop** — Fahrzeuge, Waffen, Items, Kisten, uvm.
- 🚗 **Fahrzeug-Shop** — Direkt kaufen, wird in `owned_vehicles` gespeichert
- 🌐 **Mehrsprachig** — Deutsch & Englisch (einfach erweiterbar)
- 🛡️ **Admin Panel** — Coins verwalten, Quests zurücksetzen, Spielerhistorie
- 🎨 **Premium NUI** — Dark Theme mit Neon-Blue Akzenten, Animationen
- 🔒 **Sicherheit** — Token-System, Rate-Limiting, Anti-AFK, Anti-Dupe
- 📊 **Discord Logging** — Optionale Webhook-Integration
- 📦 **Exports** — Integration in andere Ressourcen

---

## 📦 Abhängigkeiten

- [ESX Legacy](https://github.com/esx-framework/esx_core)
- [ox_lib](https://github.com/overextended/ox_lib)
- [oxmysql](https://github.com/overextended/oxmysql)

---

## 🚀 Installation

### 1. Dateien kopieren

Kopiere den Ordner `sam_rewardsystem` in deinen `resources/[scripts]/` Ordner.

### 2. Datenbank einrichten

Importiere die SQL-Datei in deine Datenbank:

```sql
-- Datei: sql/install.sql
-- Führe alle Befehle aus
```

### 3. server.cfg

Füge folgende Zeile in deine `server.cfg` ein:

```
ensure sam_rewardsystem
```

**Wichtig:** Stelle sicher, dass `es_extended`, `ox_lib` und `oxmysql` **vor** `sam_rewardsystem` gestartet werden.

### 4. Konfiguration

Passe die `config.lua` nach deinen Wünschen an:

```lua
Config.Locale = "de"        -- oder "en"
Config.HourlyReward = {
    Min = 5,
    Max = 25
}
```

---

## ⌨️ Befehle

| Befehl | Beschreibung | Berechtigung |
|--------|-------------|--------------|
| `/rewardshop` | Öffnet das Reward System | Alle |
| `/addcoins [ID] [Anzahl]` | Coins vergeben | Admin |
| `/removecoins [ID] [Anzahl]` | Coins entfernen | Admin |
| `/resetquests [ID]` | Alle Quests zurücksetzen | Admin |

**Keybind:** `F5` zum Öffnen (in config änderbar)

---

## 🔌 Exports (für andere Ressourcen)

```lua
-- Coins abfragen
local coins = exports['sam_rewardsystem']:GetPlayerCoins(source)

-- Coins hinzufügen
exports['sam_rewardsystem']:AddCoins(source, 50)

-- Coins entfernen
local success = exports['sam_rewardsystem']:RemoveCoins(source, 25)

-- Quest-Fortschritt aktualisieren
exports['sam_rewardsystem']:AddQuestProgress(source, 'fish', 1)
```

### Quest-Typen für `AddQuestProgress`:

| Typ | Beschreibung |
|-----|-------------|
| `playtime` | Spielzeit (automatisch) |
| `fish` | Fische fangen |
| `vehicles_driven` | Fahrzeuge fahren |
| `heal_player` | Spieler heilen |
| `delivery` | Lieferungen |
| `npc_kill` | NPCs töten |
| `distance` | Gelaufene Meter |
| `money_earned` | Geld verdient |
| `vehicles_sold` | Fahrzeuge verkauft |

---

## 🗃️ Datenbank-Tabellen

| Tabelle | Beschreibung |
|---------|-------------|
| `reward_system` | Spielerdaten (Coins, Spielzeit, etc.) |
| `reward_quests` | Quest-Fortschritt |
| `reward_transactions` | Transaktionsverlauf |
| `reward_purchases` | Kaufhistorie |

---

## 📁 Dateistruktur

```
sam_rewardsystem/
├── fxmanifest.lua
├── config.lua
├── client/
│   └── main.lua
├── server/
│   └── main.lua
├── locales/
│   ├── de.lua
│   └── en.lua
├── html/
│   ├── index.html
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── app.js
├── sql/
│   └── install.sql
└── README.md
```

---

## 🔧 Konfiguration

### Sprache ändern

```lua
Config.Locale = "de"  -- Deutsch
Config.Locale = "en"  -- English
```

### Neue Quests hinzufügen

```lua
-- In config.lua unter Config.Quests
{
    id = "custom_quest",
    titleKey = "quest_custom_title",     -- Muss in locales definiert sein
    descKey = "quest_custom_desc",
    reward = 100,
    target = 50,
    type = "custom_type",
    repeatable = true
}
```

### Neue Shop-Items hinzufügen

```lua
-- In config.lua unter Config.ItemShop
{
    type = "item",
    item = "item_name",
    labelKey = "item_custom",           -- Muss in locales definiert sein
    price = 50,
    category = "misc",
    amount = 1
}
```

### Neue Fahrzeuge hinzufügen

```lua
-- In config.lua unter Config.VehicleShop
{
    id = "custom_car",
    model = "vehicle_spawn_name",
    labelKey = "veh_custom",            -- Muss in locales definiert sein
    price = 500,
    category = "vehicles"
}
```

---

## 🔒 Sicherheit

- ✅ Serverseitige Validierung aller Coin-Operationen
- ✅ Token-basierte Client-Server-Kommunikation
- ✅ Rate-Limiting auf allen Events
- ✅ Anti-AFK System (Bewegungserkennung)
- ✅ Anti-Dupe (Kauf-Cooldown)
- ✅ Tägliches Coin-Limit
- ✅ Serverseitige Kennzeichengenerierung mit Uniqueness-Check
- ✅ Eingabevalidierung auf allen Endpunkten

---

## 📄 Lizenz

Dieses Projekt ist frei verwendbar. Erwähnung erwünscht.

---

**Erstellt mit ❤️ von SAM Development**
