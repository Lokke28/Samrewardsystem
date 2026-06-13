# 🏆 SAM Reward System v2.0 - Premium Edition

Ein hochentwickeltes, modulares und extrem sicheres Belohnungssystem für **FiveM (ESX Legacy)**. Das Script ermöglicht es Spielern, durch aktive Spielzeit, Quests und Erfolge serverinterne Münzen (Coins) zu verdienen und diese im integrierten Shop gegen Items, Waffen, Kisten (Crates) oder Fahrzeuge einzutauschen.

---

## ✨ Haupt-Features

### 🪙 1. Dynamisches Coin-System
- **Stündliche Aktivitätsbelohnung:** Spieler erhalten in regelmäßigen Intervallen Münzen. Die Belohnung kann zwischen einem konfigurierbaren Minimum und Maximum variieren (`Config.HourlyReward`).
- **Anti-AFK-System:** Verhindert das Generieren von Coins durch reines Herumstehen. Spieler müssen sich innerhalb des Intervalls eine Mindestdistanz bewegen (`Config.AntiAFK`).
- **Wirtschafts-Balancing:** Einstellbares tägliches Limit für maximal verdienbare Münzen (`Config.Security.MaxDailyCoins`).

### 📅 2. Tägliche Login-Streak (Daily Streak)
- Belohnt treue Spieler für tägliche Logins in Folge.
- **7-Tage-Belohnungstabelle:** Vollständig anpassbare Coin-Mengen pro Tag.
- **Rekord-Tracking:** Speichert die aktuelle Streak sowie den Allzeit-Rekord (`streak_max`) in der Datenbank.
- Visualisierung der verbleibenden Tage und Vorschau auf die morgige Belohnung direkt im Dashboard.

### 📜 3. Aufgabensystem (Quest System)
- **12+ Vorkonfigurierte Quests** aus verschiedenen Bereichen (z. B. Spielzeit, Angeln, Fahren, Heilen, Lieferungen, NPC-Kills, zurückgelegte Distanz, verdienteres Geld, verkaufte Fahrzeuge).
- **Einmalige & Wiederholbare Aufgaben:** Nach Abschluss können wiederholbare Quests automatisch zurückgesetzt werden.
- Live-Fortschrittsanzeige und visuelle Balken im UI.

### 🛒 4. Reward Shop
- **Kategorisiertes Layout:** Schnelle Navigation durch anpassbare Kategorien (Fahrzeuge, Waffen, Essen, Trinken, Werkzeuge, seltene Gegenstände, Kisten usw.).
- **Fahrzeug-Kauf:** Fahrzeuge werden direkt in die Datenbank (`owned_vehicles`) eingetragen. Das Script ermittelt automatisch das Datenbank-Schema deines Servers (unterstützt gängige Spalten wie `stored`, `type`, `job`, `state`, `garage`, `parking` usw.) und generiert ein einzigartiges 8-stelliges Kennzeichen.
- **Überraschungskisten (Crate Opening):** Beim Kauf einer Kiste (z. B. Standard- oder Premium-Kiste) zieht das System serverseitig eine zufällige Belohnung und fügt sie dem Inventar hinzu.
- **Item- & Waffen-Käufe:** Voller Support für Standard-ESX sowie automatische Erkennung und Integration von `ox_inventory` (CanCarry- und AddItem-Checks).

### 🏅 5. Achievement-System (Erfolge)
- **12 integrierte Erfolge** für Spielzeit-Meilensteine, Münzsammlungen, Login-Streaks, getätigte Einkäufe und abgeschlossene Quests.
- Freigeschaltete Erfolge werden in der Datenbank gespeichert.
- Hübsche Benachrichtigungen im Spiel und farblich hervorgehobene Badges im NUI-Menü.

### 💸 6. Coin Transfer (Überweisungen)
- Ermöglicht es Spielern, Münzen an andere Mitspieler via Server-ID zu senden.
- Einstellbarer **Steuersatz** (`Config.CoinTransfer.TaxPercent`) sowie **Transfers-Cooldown** (`Config.CoinTransfer.Cooldown`) zur Vermeidung von Missbrauch.
- Live-Steuervorschau bei der Eingabe im NUI-Formular.

### ⚡ 7. Globales Event-System
- Ermöglicht Admins den Start von temporären Server-Events über Befehle (z. B. Doppelte Coins oder Quest-Marathon).
- Ein **animierter Event-Banner** mit Countdown-Timer blendet sich automatisch oben im NUI-Menü ein.

### 🛡️ 8. NUI Admin Panel (In-Game Verwaltung)
Administratoren (definiert in `Config.AdminGroups`) können direkt über das Menü:
- Coins an Spieler vergeben oder abziehen.
- Aufgaben für bestimmte Spieler zurücksetzen oder manuell abschließen.
- Den aktuellen Kontostand aller Online-Spieler einsehen.
- Die detaillierte Transaktionshistorie (die letzten 100 Transaktionen) eines Spielers einsehen.

### 🔒 9. Sicherheits- & Performance-Architektur
- **Token-Schutz:** Jede Client-Server-Kommunikation wird über ein dynamisch bei Login generiertes Security-Token abgesichert, um Trigger-Exploits durch Modder zu blockieren.
- **Event Rate-Limiting:** Serverseitiges Spam-Schutz-System für alle Events.
- **Plausibilitäts-Checks:** Validierung von Distanzberichten und Geldeinnahmen vor der Gutschrift.
- **Memory-Leak-Schutz:** Effiziente Bereinigung des serverinternen Caches und der Token-Datenbank beim Verlassen des Spiels.

---

## 📦 Systemvoraussetzungen & Abhängigkeiten

Das Script benötigt zwingend folgende Ressourcen:
1. **[es_extended](https://github.com/esx-framework/esx_core)** (ESX Legacy)
2. **[ox_lib](https://github.com/overextended/ox_lib)** (für Notifications, Dialoge & Initialisierung)
3. **[oxmysql](https://github.com/overextended/oxmysql)** (Datenbank-Konnektivität)

*Optionaler, empfohlener Support:*
- **[ox_inventory](https://github.com/overextended/ox_inventory)** (wird automatisch erkannt, um Tragekapazitäten und Waffen präzise zu handhaben).

---

## 🚀 Installation & Einrichtung

### 1. Ressourcen-Ordner anlegen
Platziere den Ordner `sam_rewardsystem` in deinem FiveM-Server-Verzeichnis (z. B. unter `resources/[scripts]/`).

### 2. Datenbank einrichten
Importiere die SQL-Struktur in deine Datenbank. Führe dazu die Abfragen aus der Datei [sql/install.sql](file:///c:/Users/samfa/Desktop/Upload/sam_rewardsystem/sql/install.sql) in deiner Datenbankumgebung aus.

### 3. Server-Startkonfiguration (server.cfg)
Trage die Ressource in deine `server.cfg` ein. **Achte auf die Start-Reihenfolge!** `sam_rewardsystem` muss nach seinen Abhängigkeiten gestartet werden:

```cfg
ensure es_extended
ensure ox_lib
ensure oxmysql
# ... andere Ressourcen
ensure sam_rewardsystem
```

### 4. Discord Webhook einrichten (optional)
Wenn du Transaktionen und Admin-Aktionen in einem Discord-Kanal protokollieren möchtest, öffne die `config.lua` und füge deine Webhook-URL ein:
```lua
Config.Logging = {
    Enabled = true,
    WebhookURL = "DEINE_DISCORD_WEBHOOK_URL",
    EmbedColor = 3447003 -- Standard HSL-Farbe
}
```

---

## ⌨️ Befehle & Bedienung

### Für Spieler
- **Tastendruck:** Standardmäßig `F5` zum Öffnen/Schließen des Menüs (anpassbar).
- Befehl: `/rewardshop` - Öffnet das Menü.
- Befehl: `/givecoin [ID] [Anzahl]` - Überweist Münzen an einen Mitspieler.

### Für Administratoren
- Befehl: `/addcoins [ID] [Anzahl]` - Vergibt Coins an einen Spieler.
- Befehl: `/removecoins [ID] [Anzahl]` - Zieht Coins ab.
- Befehl: `/resetquests [ID]` - Setzt den Quest-Fortschritt eines Spielers zurück.
- Befehl: `/startevent [event_id] [dauer_minuten]` - Startet ein globales Event (z. B. `/startevent double_coins 120`).
- Befehl: `/stopevent` - Beendet das aktuell laufende Event vorzeitig.
- Befehl: `/createcode [code] [coins] [max_uses] [expiration_hours]` - Erstellt einen Gutscheincode (0 bei max_uses/expiration_hours = unbegrenzt/nie ablaufend).

---

## 🔌 Schnittstellen für Entwickler (Exports)

Du kannst das Münz- und Questsystem problemlos in andere Scripte auf deinem Server einbinden:

### Coins abfragen (Serverseitig)
```lua
local coins = exports['sam_rewardsystem']:GetPlayerCoins(source)
print("Spieler Coins: " .. coins)
```

### Coins hinzufügen (Serverseitig)
```lua
local success = exports['sam_rewardsystem']:AddCoins(source, 100)
if success then
    print("Coins erfolgreich gutgeschrieben!")
end
```

### Coins abziehen (Serverseitig)
```lua
local success = exports['sam_rewardsystem']:RemoveCoins(source, 50)
if success then
    print("Coins erfolgreich abgezogen!")
else
    print("Nicht genügend Münzen vorhanden!")
end
```

### Quest-Fortschritt erhöhen (Serverseitig)
Erhöht den Fortschritt einer bestimmten Quest (z. B. nach dem Fangen eines Fisches):
```lua
exports['sam_rewardsystem']:AddQuestProgress(source, 'fish', 1)
```

#### Unterstützte Standard-Quest-Typen (`questType`):
- `playtime` - Spielzeit in Minuten (wird automatisch getrackt).
- `fish` - Gefangene Fische.
- `vehicles_driven` - Gefahrene Fahrzeuge.
- `heal_player` - Geheilte Spieler.
- `delivery` - Abgeschlossene Lieferungen.
- `npc_kill` - Eliminierte NPCs (wird über `gameEventTriggered` automatisch getrackt).
- `distance` - Zurückgelegte Distanz zu Fuß in Metern (wird automatisch getrackt).
- `money_earned` - Eingenommenes Geld (wird automatisch über ESX-Kontoüberwachung getrackt).
- `vehicles_sold` - Verkaufte Fahrzeuge.

---

## 🗄️ Tabellenstruktur in der Datenbank

- **`reward_system`**: Speichert die globale Spielerstatistik (derzeitige Münzen, Allzeit verdiente/ausgegebene Münzen, Gesamtspielzeit, tägliches Limit, Login-Streak).
- **`reward_quests`**: Speichert den Fortschritt jeder einzelnen Aufgabe pro Spieler samt Abschluss-Zeitstempel und Zähler.
- **`reward_achievements`**: Protokolliert alle freigeschalteten Erfolge der Spieler.
- **`reward_purchases`**: Dokumentiert alle getätigten Einkäufe im Shop.
- **`reward_transactions`**: Führt ein detailliertes Kassenbuch über alle Münzbewegungen (Erhalt, Käufe, Admin-Eingriffe, Überweisungen).

---

## 🎨 Anpassung der Benutzeroberfläche

- **Eigenes Server-Logo:** Du kannst ein Bild (`logo.png`) im Ordner `html/img/` platzieren und in der `config.lua` unter `Config.Logo` einstellen (`html/img/logo.png`).
- **Item-Bilder:** Das Script kann Bilder direkt aus deinem Inventar (z. B. `ox_inventory/web/images/`) ziehen. Aktiviere dazu `Config.ShopImages.Enabled = true`.
- **Fahrzeug-Bilder:** Lege deine Fahrzeug-Bilder unter `html/img/vehicles/` als `modelname.png` ab (z. B. `sultanrs.png`). Die Pfadauflösung erfolgt automatisch über die integrierte NUI-URL-Sicherheitsprüfung im Javascript.

---

## 💬 Support & Fragen

Für Support und Fragen nutze bitte den folgenden Discord-Link:

https://discord.gg/DfZSgWgcCv

---

**Entwickelt mit ❤️ von SAM Development**
