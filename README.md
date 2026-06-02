# Visual Discord Bot

<p align="center">
  <a href="https://discord.gg/Visualise">
    <img src="https://discordapp.com/api/guilds/133049272517001216/widget.png?style=shield" alt="Discord Server">
  </a>
</p>

<p align="center">
  <a href="#übersicht">Übersicht</a>
  - 
  <a href="#funktionen">Funktionen</a>
  - 
  <a href="#voraussetzungen">Voraussetzungen</a>
  - 
  <a href="#installation">Installation</a>
  - 
  <a href="#bot-erstellen">Discord-Bot erstellen</a>
  - 
  <a href="#konfiguration">Konfiguration</a>
  - 
  <a href="#starten">Starten</a>
  - 
  <a href="#fehlerbehebung">Fehlerbehebung</a>
  - 
  <a href="#community">Community</a>
  - 
  <a href="#lizenz">Lizenz</a>
</p>

## Übersicht

Visual Discord Bot ist ein **self-hosted** Discord-Bot. Das bedeutet, dass der Bot auf einem eigenen System betrieben und eigenständig aktualisiert werden muss. Laut dem bisherigen README ist das Projekt so gedacht, dass die Verwaltung später weitgehend direkt über Discord erfolgen kann.

Die bisherige Projektbeschreibung nennt unter anderem Moderation, Ticket-System, Reaktionsrollen und anpassbare Berechtigungen als Kernfunktionen. Das alte README enthält außerdem Changelog-Einträge bis März 2025 und verweist auf den offiziellen Discord-Server.

## Funktionen

Der bisher dokumentierte Funktionsumfang umfasst unter anderem:

- Moderationsfunktionen wie Kick, Ban, Softban, Hackban, Mod-Log, Filter und Chat-Bereinigung.
- Admin-Automatisierung wie Self-Roles.
- Anpassbare Command-Berechtigungen.
- Ticket-System.
- Reaction Roles.
- Membercount.
- Anti-Nuke-Funktionen und ein `!nukeall`-Befehl.

> Hinweis: Diese Liste basiert auf dem bisherigen README. Je nach aktuellem Stand des Quellcodes können Funktionen ergänzt, entfernt oder umbenannt worden sein.

## Voraussetzungen

Vor der Installation sollte Folgendes vorhanden sein:

- Ein Linux-, Windows- oder macOS-System mit Terminalzugriff.
- [Git](https://git-scm.com/), um das Repository zu klonen.
- [Node.js](https://nodejs.org/) in einer aktuellen LTS-Version, falls das Projekt auf `discord.js` bzw. einer typischen Node.js-Struktur basiert.
- `npm`, das normalerweise mit Node.js mitgeliefert wird.
- Ein Discord-Bot-Token aus dem [Discord Developer Portal](https://discord.com/developers/applications).
- Optional ein VPS oder ein dauerhaft laufender Server, wenn der Bot 24/7 online sein soll.

> Warum Node.js? Viele selbst gehostete Discord-Bots mit vergleichbarem Aufbau verwenden `discord.js` und werden über `npm install` sowie `node index.js` oder `npm start` ausgeführt. Falls dieses Repository eine andere Laufzeitumgebung nutzt, müssen die Startbefehle entsprechend angepasst werden.

## Installation

### 1. Repository herunterladen

```bash
git clone https://github.com/naix1337/VisualDiscordBot.git
cd VisualDiscordBot
```

### 2. Abhängigkeiten installieren

Wenn das Projekt eine `package.json` enthält, können die benötigten Pakete in der Regel mit folgendem Befehl installiert werden:

```bash
npm install
```

Falls stattdessen `pnpm` oder `yarn` verwendet wird, nutze den passenden Paketmanager:

```bash
pnpm install
```

oder

```bash
yarn install
```

### 3. Projektstruktur prüfen

Achte nach dem Klonen besonders auf folgende Dateien:

- `package.json` – enthält Skripte und Abhängigkeiten.
- `.env.example`, `config.json` oder ähnliche Konfigurationsdateien.
- `index.js`, `main.js`, `src/index.js` oder ein ähnlicher Einstiegspunkt.

Wenn keine Beispiel-Konfiguration vorhanden ist, muss der Bot-Token meist manuell in einer Konfigurationsdatei oder in Umgebungsvariablen hinterlegt werden.

## Discord-Bot erstellen

Bevor der Bot gestartet werden kann, muss im Discord Developer Portal eine Anwendung erstellt werden:

1. Öffne das [Discord Developer Portal](https://discord.com/developers/applications).
2. Klicke auf **New Application** und vergib einen Namen.
3. Öffne den Bereich **Bot** und erstelle einen Bot.
4. Kopiere das **Bot Token** und speichere es sicher.
5. Aktiviere – falls vom Bot benötigt – die Privileged Gateway Intents, insbesondere:
   - Message Content Intent
   - Server Members Intent
   - Presence Intent
6. Gehe zu **OAuth2 > URL Generator**.
7. Wähle mindestens den Scope **bot** aus, bei Slash Commands zusätzlich **applications.commands**.
8. Vergib die Berechtigungen, die dein Bot wirklich benötigt, und lade ihn anschließend auf deinen Server ein.

> Das Token niemals öffentlich in GitHub hochladen. Wenn ein Token geleakt wurde, sollte es sofort im Developer Portal zurückgesetzt werden.

## Konfiguration

Je nach Aufbau des Projekts erfolgt die Konfiguration meistens über eine `.env`-Datei oder eine JSON-Datei.

### Beispiel mit `.env`

Erstelle im Projektordner eine Datei namens `.env`:

```env
DISCORD_TOKEN=dein_bot_token_hier
PREFIX=!
```

### Beispiel mit `config.json`

```json
{
  "token": "dein_bot_token_hier",
  "prefix": "!"
}
```

Falls das Projekt zusätzliche Werte benötigt, kommen häufig diese Felder vor:

- Guild- oder Server-ID.
- Client-ID der Discord-Anwendung.
- Rollen- oder Kanal-IDs.
- Datenbank-Zugangsdaten.
- Logging- oder Webhook-Konfiguration.

## Starten

Je nach Projektkonfiguration kann der Bot auf eine der folgenden Arten gestartet werden:

### Mit npm-Skript

```bash
npm start
```

### Direkt mit Node.js

```bash
node index.js
```

### Entwicklungsmodus

Falls ein Dev-Skript vorhanden ist:

```bash
npm run dev
```

Wenn der Bot erfolgreich startet, sollte im Terminal eine Meldung erscheinen, dass der Login bei Discord erfolgreich war oder der Bot als online angezeigt wird.

## Dauerbetrieb

Für den produktiven Betrieb empfiehlt sich ein Prozessmanager, damit der Bot nach einem Absturz automatisch neu startet.

### Mit PM2

```bash
npm install -g pm2
pm2 start index.js --name visual-discord-bot
pm2 save
pm2 startup
```

Alternativ kann der Bot in Docker, auf einem VPS oder über ein Hosting-Panel betrieben werden. Wichtig ist, dass die Anwendung dauerhaft läuft und Logs leicht einsehbar bleiben.

## Fehlerbehebung

### Bot startet nicht

- Prüfen, ob `node -v` und `npm -v` funktionieren.
- Sicherstellen, dass alle Abhängigkeiten mit `npm install` installiert wurden.
- Kontrollieren, ob die richtige Startdatei verwendet wird.

### `Invalid token`

- Token erneut aus dem Discord Developer Portal kopieren.
- Keine zusätzlichen Leerzeichen oder Anführungszeichen einfügen.
- Nach einem Leak das Token zurücksetzen und neu eintragen.

### Befehle reagieren nicht

- Prüfen, ob die nötigen Gateway Intents aktiviert sind.
- Sicherstellen, dass der Bot die richtigen Rechte auf dem Server besitzt.
- Kontrollieren, ob der konfigurierte Prefix korrekt ist.

### Slash Commands erscheinen nicht

- Prüfen, ob `applications.commands` beim Invite verwendet wurde.
- Möglicherweise müssen Commands erneut registriert werden.
- Änderungen können je nach Scope etwas Zeit benötigen.

## Changelog

### 28/02/2025

- Fixed Verify Timeout
- Fixed `!say` command bugging
- Fixed ticket system timeout
- Translated into English

### 25/03/2025

- Added membercount
- Fixed tickets
- Playing visualise status
- Fixed reaction roles
- Daily nuke 0:00 & 15:00 UTC+01:00
- Added `!nukeall` command

## Community

Der offizielle Community-Server ist hier erreichbar:

- [Official Discord Server](https://discord.gg/visualise)

## Lizenz

Das Projekt steht laut bisherigem README unter der [GNU GPL v3](https://www.gnu.org/licenses/gpl-3.0.en.html).

***

## Hinweis zur Anpassung

Diese README wurde auf Basis des bisherigen README-Textes strukturiert und um eine vollständige Installationsanleitung ergänzt. Für eine perfekte, technisch exakte Version sollten zusätzlich die tatsächlichen Projektdateien wie `package.json`, Einstiegspunkt, Konfigurationsdateien und eventuelle Datenbank-Abhängigkeiten geprüft und die Befehle anschließend final angepasst werden.
