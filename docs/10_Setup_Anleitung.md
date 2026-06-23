# Setup-Anleitung: NocoDB + PostgreSQL

**Datei:** `10_Setup_Anleitung.md`  
**Projekt:** Teacher Intelligence System (TIS)  
**Version:** 0.1  
**Status:** Entwurf  
**Letzte Änderung:** 2026-06-23

---

## 1. Zweck

Diese Anleitung beschreibt die erste technische Arbeitsumgebung für das Teacher Intelligence System.

Ziel ist eine lauffähige NocoDB-Instanz mit PostgreSQL als Datenbank. Darauf wird anschließend das Schema aus `09_NocoDB_Schema.md` manuell aufgebaut.

Dokumente selbst werden im MVP nicht direkt in der Datenbank gespeichert, sondern über Links referenziert, z. B. auf OneDrive oder SharePoint.

---

## 2. Zielarchitektur für das MVP

```text
Browser
  ↓
NocoDB
  ↓
PostgreSQL
  ↓
Docker-Volumes / Server-Speicher

OneDrive / SharePoint
  ↳ Dokumente als externe Dateien
  ↳ NocoDB speichert nur Links und Metadaten
```

---

## 3. Voraussetzungen

Für den Start werden benötigt:

- Docker
- Docker Compose
- ein Projektordner für TIS
- Zugriff auf das Git-Repository
- optional ein OneDrive-/SharePoint-Ordner für Dokumente

Für einen lokalen Test reicht Docker Desktop auf Windows, macOS oder Linux.

Für einen dauerhaften Betrieb sollte später ein Server genutzt werden.

---

## 4. Empfohlene Ordnerstruktur

```text
Schuelerverwaltungssoftware/
├── docs/
│   ├── 01_Master_Spezifikation.md
│   ├── 02_Datenmodell.md
│   ├── 02a_MVP_Datenmodell.md
│   ├── 03_Architektur.md
│   ├── 04_Testfaelle.md
│   ├── 05_Entscheidungen.md
│   ├── 06_Glossar.md
│   ├── 07_Backlog.md
│   ├── 08_Changelog.md
│   ├── 09_NocoDB_Schema.md
│   └── 10_Setup_Anleitung.md
├── infra/
│   ├── docker-compose.yml
│   └── .env.example
└── README.md
```

---

## 5. Docker-Compose-Datei anlegen

Lege folgende Datei an:

```text
infra/docker-compose.yml
```

Inhalt:

```yaml
services:
  postgres:
    image: postgres:17
    container_name: tis_postgres
    restart: unless-stopped
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
      POSTGRES_DB: ${POSTGRES_DB}
    volumes:
      - tis_postgres_data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U ${POSTGRES_USER} -d ${POSTGRES_DB}"]
      interval: 10s
      timeout: 5s
      retries: 5

  redis:
    image: redis:7-alpine
    container_name: tis_redis
    restart: unless-stopped
    volumes:
      - tis_redis_data:/data

  nocodb:
    image: nocodb/nocodb:latest
    container_name: tis_nocodb
    restart: unless-stopped
    depends_on:
      postgres:
        condition: service_healthy
      redis:
        condition: service_started
    ports:
      - "8080:8080"
    environment:
      NC_DB: "pg://postgres:5432?u=${POSTGRES_USER}&p=${POSTGRES_PASSWORD}&d=${POSTGRES_DB}"
      NC_AUTH_JWT_SECRET: ${NC_AUTH_JWT_SECRET}
      NC_ADMIN_EMAIL: ${NC_ADMIN_EMAIL}
      NC_ADMIN_PASSWORD: ${NC_ADMIN_PASSWORD}
      NC_DISABLE_TELE: "true"
    volumes:
      - tis_nocodb_data:/usr/app/data

volumes:
  tis_postgres_data:
  tis_redis_data:
  tis_nocodb_data:
```

---

## 6. Umgebungsdatei anlegen

Lege folgende Datei an:

```text
infra/.env
```

Diese Datei darf nicht mit echten Passwörtern ins Repository eingecheckt werden.

Vorlage:

```env
POSTGRES_USER=tis_user
POSTGRES_PASSWORD=BITTE_ERSETZEN_DURCH_LANGES_PASSWORT
POSTGRES_DB=tis_db

NC_AUTH_JWT_SECRET=BITTE_ERSETZEN_DURCH_LANGEN_ZUFALLSWERT
NC_ADMIN_EMAIL=admin@example.local
NC_ADMIN_PASSWORD=BITTE_ERSETZEN_DURCH_ADMIN_PASSWORT
```

Zusätzlich kann eine ungefährliche Vorlage ins Repository:

```text
infra/.env.example
```

---

## 7. `.gitignore` prüfen

Die Datei `.env` muss ausgeschlossen werden.

Empfohlener Eintrag in `.gitignore`:

```gitignore
# Lokale Konfiguration und Zugangsdaten
.env
infra/.env

# Backups
*.backup
*.dump
*.sql.gz

# Betriebssystemdateien
.DS_Store
Thumbs.db
```

---

## 8. NocoDB starten

Im Terminal:

```bash
cd infra
docker compose up -d
```

Danach öffnen:

```text
http://localhost:8080
```

Wenn die Instanz auf einem Server läuft, wird später eine Domain mit HTTPS davor benötigt.

---

## 9. Logs prüfen

```bash
docker compose logs -f nocodb
```

PostgreSQL prüfen:

```bash
docker compose logs -f postgres
```

---

## 10. NocoDB-Projekt anlegen

In NocoDB:

1. einloggen
2. neues Workspace/Projekt anlegen
3. Name: `Teacher Intelligence System`
4. Schema gemäß `09_NocoDB_Schema.md` anlegen

Die Tabellen werden in der Reihenfolge aus `09_NocoDB_Schema.md` erstellt.

---

## 11. Empfohlene Tabellen-Erstellungsreihenfolge

```text
1. schuljahr
2. fach
3. schueler
4. lerngruppe
5. schueler_lerngruppe
6. unterrichtstermin
7. unterrichtsstunde
8. anwesenheit
9. leistungsnachweis
10. leistungsbewertung
11. kompetenz
12. kompetenzbewertung
13. beobachtung
14. dokument
15. dokument_schueler
16. bericht
```

---

## 12. Testdaten zuerst verwenden

Vor echten Schülerdaten werden nur Testdaten angelegt.

Beispiele:

```text
Felix Schröder
Laura Meier
Paul Beispiel
```

Testablauf:

```text
Schüler anlegen
→ Schuljahr anlegen
→ Fach anlegen
→ Lerngruppe anlegen
→ Schüler zu Lerngruppe zuordnen
→ Unterrichtstermin anlegen
→ Unterrichtsstunde anlegen
→ Anwesenheit erfassen
→ Beobachtung eintragen
→ Leistungsnachweis anlegen
→ Leistungsbewertung eintragen
→ Kompetenz anlegen
→ Kompetenzbewertung eintragen
→ Dokument verlinken
→ Bericht anlegen
```

---

## 13. OneDrive-/SharePoint-Dokumente im MVP

Im MVP werden Dokumente nicht automatisch synchronisiert.

Vorgehen:

1. Datei in OneDrive oder SharePoint ablegen
2. Freigabelink oder internen Link kopieren
3. In NocoDB in Tabelle `dokument` speichern
4. Über `dokument_schueler` mit Schüler verknüpfen

Wichtig:

- Keine öffentlichen Links für sensible Dokumente verwenden.
- Zugriff auf Dokumente wird außerhalb von NocoDB über OneDrive/SharePoint-Rechte geregelt.
- In NocoDB werden zunächst nur Metadaten und Links gespeichert.

---

## 14. Backup-Grundsatz

Für das MVP müssen mindestens PostgreSQL-Daten und NocoDB-Daten gesichert werden.

Zu sichern sind insbesondere:

- Docker-Volume `tis_postgres_data`
- Docker-Volume `tis_nocodb_data`
- Projekt-Repository
- OneDrive-/SharePoint-Dokumentordner

Ein konkretes Backup-Skript wird in einer späteren Datei ergänzt.

Vorgeschlagene spätere Datei:

```text
docs/11_Backup_und_Wiederherstellung.md
```

---

## 15. Sicherheitsgrundsätze für den MVP

- Keine echten Schülerdaten vor erfolgreichem Testlauf verwenden.
- `.env` niemals ins Repository hochladen.
- Starke Passwörter verwenden.
- Für Serverbetrieb HTTPS verwenden.
- Externe KI erst nach Pseudonymisierungskonzept nutzen.
- OneDrive-/SharePoint-Links nicht öffentlich freigeben.

---

## 16. Nächster Schritt nach erfolgreichem Setup

Nach erfolgreichem Start von NocoDB wird das Schema aus `09_NocoDB_Schema.md` manuell aufgebaut.

Danach folgt:

```text
1. Testdaten eintragen
2. MVP-Testfälle ausführen
3. erste echte Lerngruppe vorbereiten
4. Importstrategie für Schülerlisten definieren
```
