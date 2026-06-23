# Architektur

**Version:** 0.2  
**Status:** Entwurf  
**Letzte Änderung:** 2026-06-23

---

## 1. Zweck dieses Dokuments

Dieses Dokument beschreibt die technische Zielarchitektur des Teacher Intelligence Systems (TIS).

Die Architektur ist auf einen pragmatischen MVP-Betrieb ausgelegt:

- NocoDB als Benutzeroberfläche
- PostgreSQL als relationale Datenbank
- Cloudserver als Betriebsumgebung
- OneDrive/SharePoint oder vergleichbarer Cloudspeicher als Dokumentenablage
- KI-Funktionen über konfigurierbare Betriebsmodi

---

## 2. Grundentscheidung

Das System soll nicht nur lokal auf einem einzelnen Rechner laufen.

Stattdessen wird ein Betrieb auf einem Cloudserver vorgesehen. Dokumente können in einem Cloudspeicher wie OneDrive oder SharePoint liegen. Die Datenbank bleibt davon getrennt.

Wichtig:

OneDrive ist im Projekt als Dokumentenspeicher vorgesehen, nicht als Server für NocoDB oder PostgreSQL.

---

## 3. Zielarchitektur MVP

```text
Browser
  ↓
NocoDB
  ↓
PostgreSQL
  ↓
FastAPI / Automatisierungsdienst
  ↓
KI-Dienst
  ├── lokale KI
  ├── pseudonymisierte Cloud-KI
  └── DSGVO-konforme Cloud-KI mit AVV

Dokumente
  └── OneDrive / SharePoint / Nextcloud / lokaler Speicher
```

---

## 4. Komponenten

## 4.1 NocoDB

### Aufgabe

NocoDB dient im MVP als primäre Benutzeroberfläche.

### Verantwortlichkeiten

- Tabellenansichten
- Formulare
- Filter
- Sortierungen
- Schülerlisten
- Eingabe von Fehlzeiten
- Eingabe von Beobachtungen
- Eingabe von Leistungen
- Verknüpfung von Datensätzen

### Nicht verantwortlich für

- KI-Logik
- komplexe Importlogik
- Dokumentenspeicherung im Dateisystem
- rechtliche Datenschutzprüfung

---

## 4.2 PostgreSQL

### Aufgabe

PostgreSQL ist die zentrale relationale Datenbank.

### Verantwortlichkeiten

- Speicherung aller strukturierten Daten
- Schülerdaten
- Lerngruppen
- Unterrichtstermine
- Unterrichtsstunden
- Anwesenheiten
- Leistungen
- Kompetenzen
- Beobachtungen
- Berichte
- Dokument-Metadaten

### Hinweis

Dateien selbst werden im MVP nicht zwingend in PostgreSQL gespeichert. Die Datenbank speichert primär Metadaten und Links.

---

## 4.3 Cloudserver

### Aufgabe

Der Cloudserver betreibt die Kernanwendung.

### Enthaltene Dienste

- NocoDB
- PostgreSQL
- optional FastAPI
- optional Automatisierungsdienst
- optional Backup-Dienst

### Mögliche Anbieter

- Hetzner Cloud
- Netcup VPS
- IONOS VPS
- anderer Docker-fähiger Server
- eigener Schulserver

### Anforderungen

- verschlüsselte Verbindung per HTTPS
- regelmäßige Backups
- Zugriffsschutz
- möglichst Standort EU/Deutschland
- klare Verantwortlichkeit für Betrieb und Updates

---

## 4.4 Dokumentenspeicher

### Aufgabe

Der Dokumentenspeicher verwaltet Dateien.

### Mögliche Speicherorte

- OneDrive
- SharePoint
- Nextcloud
- lokales Dateisystem
- Netzlaufwerk

### Gespeichert werden können

- Klassenarbeiten
- Präsentationen
- Bewertungsbögen
- WebUntis-Exporte
- Schülerarbeiten
- Gesprächsprotokolle
- Förderpläne

### Datenbankbezug

In PostgreSQL werden gespeichert:

- Dokumenttitel
- Dokumenttyp
- Dateiname
- Cloud-Link
- Speicherort
- Beschreibung
- Zuordnung zu Schülern oder Lerngruppen

---

## 4.5 FastAPI / Automatisierungsdienst

### Aufgabe

FastAPI ist für Funktionen vorgesehen, die NocoDB allein nicht sinnvoll abbildet.

### Mögliche Verantwortlichkeiten

- KI-Importassistent
- WebUntis-Import
- Pseudonymisierung vor KI-Aufrufen
- Berichtsgenerator
- Dokumentenanalyse
- Erzeugung konkreter Unterrichtsstunden aus Unterrichtsterminen
- Exportfunktionen
- Schnittstellen zu externen Diensten

### Status im MVP

FastAPI ist für das MVP vorbereitet, muss aber nicht sofort vollständig umgesetzt werden.

---

## 4.6 KI-Dienst

### Aufgabe

Der KI-Dienst unterstützt die Lehrkraft bei Auswertung, Import und Berichtserstellung.

### Mögliche Funktionen

- Schülerzusammenfassung
- Lernentwicklungsbericht
- Elterngesprächsvorbereitung
- Förderempfehlung
- KI-gestützte Schnellerfassung
- KI-Import aus WebUntis-/Excel-/PDF-Dateien
- Dokumentenanalyse

### Betriebsmodi

#### Modus A: Lokale KI

Die KI läuft lokal oder auf einem eigenen Server.

Personenbezogene Daten verlassen die eigene kontrollierte Infrastruktur nicht.

#### Modus B: Pseudonymisierte Cloud-KI

Vor der Übertragung an externe KI-Dienste werden personenbezogene Daten ersetzt oder entfernt.

Beispiele:

- Name → Schüler-ID oder Pseudonym
- Schulname → entfernt
- E-Mail-Adresse → entfernt
- Elternnamen → entfernt
- Geburtsdatum → entfernt oder verallgemeinert

Die Rückzuordnung bleibt ausschließlich im eigenen System.

#### Modus C: DSGVO-konforme Cloud-KI

Externe KI-Dienste können mit personenbezogenen Daten genutzt werden, wenn eine geeignete Rechtsgrundlage, ein AVV und passende technische sowie organisatorische Maßnahmen vorhanden sind.

---

# 5. Datenschutz- und Sicherheitsprinzipien

## ARCH-001 Datenhoheit

Die Lehrkraft beziehungsweise die verantwortliche Stelle behält Zugriff und Kontrolle über die Daten.

---

## ARCH-002 Trennung von Datenbank und Dokumentenspeicher

Strukturierte Daten liegen in PostgreSQL.

Dateien liegen in einem Dokumentenspeicher.

Die Datenbank speichert nur Verweise und Metadaten.

---

## ARCH-003 Pseudonymisierung für externe KI

Externe KI-Systeme sollen standardmäßig nur pseudonymisierte oder minimierte Daten erhalten.

---

## ARCH-004 Keine ungeprüfte Cloudübertragung

Personenbezogene Schülerdaten dürfen nicht unbeabsichtigt an externe Dienste übertragen werden.

KI-Funktionen benötigen einen bewusst gewählten Datenschutzmodus.

---

## ARCH-005 Exportierbarkeit

Alle relevanten Daten müssen exportierbar sein.

Mindestformate:

- CSV
- Excel
- JSON perspektivisch
- PDF für Berichte perspektivisch

---

## ARCH-006 Backupfähigkeit

Datenbank und Dokumentenlinks müssen regelmäßig gesichert werden.

Backups müssen getrennt vom Produktivsystem gespeichert werden.

---

## ARCH-007 Erweiterbarkeit

Neue Tabellen, Felder und Funktionen sollen später ergänzt werden können, ohne das MVP-Datenmodell grundsätzlich zu brechen.

---

## ARCH-008 Nachvollziehbarkeit von KI-Ausgaben

KI-generierte Inhalte sollen nachvollziehbar bleiben.

Gespeichert werden soll mindestens:

- Berichtstyp
- Datengrundlage oder Bezug
- KI-generiert ja/nein
- geprüft ja/nein
- Erstellungsdatum

---

# 6. Betriebsvarianten

## 6.1 MVP-Betrieb

```text
Cloudserver:
- NocoDB
- PostgreSQL

Dokumente:
- OneDrive oder SharePoint

KI:
- zunächst manuell oder über späteren FastAPI-Dienst
```

Diese Variante ist für den ersten produktiven Prototypen ausreichend.

---

## 6.2 Erweiterter Betrieb

```text
Cloudserver:
- NocoDB
- PostgreSQL
- FastAPI
- Automatisierungsdienst

Dokumente:
- OneDrive / SharePoint / Nextcloud

KI:
- lokale KI oder pseudonymisierte Cloud-KI
```

Diese Variante wird für WebUntis-Importe, KI-Importe und Berichtsgeneratoren relevant.

---

## 6.3 Lokaler Testbetrieb

```text
Lokaler Rechner:
- NocoDB
- PostgreSQL
- Testdaten
```

Diese Variante eignet sich zum gefahrlosen Testen ohne echte Schülerdaten.

---

# 7. Nicht-Ziele der Architektur

Die Architektur soll zunächst nicht leisten:

- vollständiges Schulmanagementsystem
- schulweite Stundenplanung
- Vertretungsplanung
- Raumplanung
- offizielles Elternportal
- amtliche Schülerakte
- vollständiges LMS

Persönliche Unterrichtstermine und Terminübersichten der Lehrkraft sind hingegen Teil des Systems.

---

# 8. Offene Architekturfragen

- Welcher Cloudserver-Anbieter soll genutzt werden?
- Soll der Betrieb per Docker erfolgen?
- Wie wird HTTPS eingerichtet?
- Wie werden Backups verschlüsselt?
- Welcher Cloudspeicher wird zuerst angebunden?
- Soll Microsoft 365/OneDrive über Links oder später über API angebunden werden?
- Welcher KI-Modus wird für den ersten KI-Prototypen genutzt?
- Welche Daten dürfen dienstrechtlich überhaupt gespeichert werden?
