# Architektur- und Projektentscheidungen

**Version:** 0.2  
**Status:** Entwurf  
**Letzte Änderung:** 2026-06-23

---

## ENT-001 NocoDB als primäre Benutzeroberfläche

**Datum:** 2026-06-23

### Entscheidung

NocoDB wird im MVP als primäre Benutzeroberfläche verwendet.

### Begründung

NocoDB ermöglicht schnelle Entwicklung bei geringer technischer Komplexität. Tabellen, Formulare, Filter und Ansichten können ohne umfangreiche Programmierung erstellt werden.

### Konsequenz

Die erste Version wird bewusst datenbanknah und tabellenorientiert aufgebaut.

---

## ENT-002 PostgreSQL als Datenbank

**Datum:** 2026-06-23

### Entscheidung

PostgreSQL wird als zentrale relationale Datenbank verwendet.

### Begründung

PostgreSQL ist stabil, weit verbreitet und zukunftssicher. Die Daten bleiben unabhängig von NocoDB nutzbar.

### Konsequenz

Das Datenmodell wird relational entworfen. NocoDB ist Oberfläche, nicht alleiniger Datenspeicher.

---

## ENT-003 Cloudserver statt reiner lokaler Installation

**Datum:** 2026-06-23

### Entscheidung

Das System soll perspektivisch auf einem Cloudserver betrieben werden.

### Begründung

Der Zugriff soll nicht an einen einzelnen lokalen Rechner gebunden sein. Backups, Verfügbarkeit und spätere Erweiterungen sind auf einem Server besser organisierbar.

### Konsequenz

Für den produktiven Betrieb werden Serverbetrieb, HTTPS, Zugriffsschutz und Backups relevant.

---

## ENT-004 OneDrive/SharePoint als Dokumentenspeicher möglich

**Datum:** 2026-06-23

### Entscheidung

OneDrive, SharePoint oder vergleichbare Cloudspeicher können als Dokumentenspeicher genutzt werden.

### Begründung

Dokumente wie Klassenarbeiten, Präsentationen oder WebUntis-Exporte sollen nicht zwingend in der Datenbank gespeichert werden. Die Datenbank verwaltet Metadaten und Links.

### Konsequenz

Die Tabelle `dokument` speichert unter anderem `cloud_link`, `speicherort`, `dateiname` und `dokumenttyp`.

---

## ENT-005 OneDrive ist kein Datenbankserver

**Datum:** 2026-06-23

### Entscheidung

OneDrive wird nicht als Betriebsumgebung für NocoDB oder PostgreSQL verwendet.

### Begründung

OneDrive ist ein Datei- und Synchronisationsdienst, aber keine geeignete Plattform für relationale Datenbankserver oder Webanwendungen.

### Konsequenz

NocoDB und PostgreSQL benötigen einen separaten Server oder lokalen Testbetrieb.

---

## ENT-006 KI-Betrieb über Datenschutzmodi

**Datum:** 2026-06-23

### Entscheidung

KI-Funktionen werden nicht auf einen einzigen Betriebsmodus festgelegt.

Stattdessen werden drei Datenschutzmodi vorgesehen:

1. lokale KI
2. pseudonymisierte Cloud-KI
3. vollständige Cloud-KI nur mit geeigneter Rechtsgrundlage und AVV

### Begründung

Die Anforderungen an Qualität, Datenschutz und technische Umsetzbarkeit können je nach Funktion unterschiedlich sein.

### Konsequenz

Das System muss vor KI-Aufrufen kontrollieren, welche Daten übertragen werden und welcher Datenschutzmodus aktiv ist.

---

## ENT-007 Pseudonymisierte Cloud-KI als wichtiger Zielmodus

**Datum:** 2026-06-23

### Entscheidung

Pseudonymisierte Cloud-KI wird als wichtiger Zielmodus für leistungsfähige KI-Funktionen vorgesehen.

### Begründung

Durch Pseudonymisierung können leistungsfähige externe Modelle genutzt werden, ohne Schülernamen, Schulnamen, Elternnamen oder andere direkte Identifikatoren zu übertragen.

### Konsequenz

Das Datenmodell bereitet Pseudonyme und spätere KI-Protokollierung vor. Im MVP wird dies zunächst konzeptionell berücksichtigt und später technisch umgesetzt.

---

## ENT-008 Einzel-Lehrkraft-System als Startpunkt

**Datum:** 2026-06-23

### Entscheidung

Das System wird zunächst für eine einzelne Lehrkraft entwickelt.

### Begründung

Dadurch bleibt der erste Prototyp beherrschbar. Mehrbenutzerfähigkeit, Rollen und schulweite Prozesse erhöhen die Komplexität erheblich.

### Konsequenz

Rollenmodell und Rechteverwaltung werden vorbereitet, aber nicht im MVP priorisiert.

---

## ENT-009 Schülerakte als zentrales fachliches Konzept

**Datum:** 2026-06-23

### Entscheidung

Die Schülerakte ist das zentrale fachliche Konzept des Systems.

### Begründung

Die Hauptfragen des Systems beziehen sich auf einzelne Schüler und deren Verlauf über Zeit, Lerngruppen, Leistungen, Kompetenzen, Fehlzeiten, Beobachtungen und Dokumente.

### Konsequenz

Die Schülerakte wird nicht als einzelne Tabelle gespeichert, sondern als aggregierte Ansicht aus verknüpften Tabellen erzeugt.

---

## ENT-010 Lerngruppe statt nur Klasse

**Datum:** 2026-06-23

### Entscheidung

Das System modelliert Lerngruppen als zentrale Unterrichtseinheit.

### Begründung

Eine Lehrkraft unterrichtet nicht nur Klassen, sondern auch Kurse, Wahlpflichtgruppen, Tutorengruppen, AGs oder Fachgruppen.

### Konsequenz

Schüler werden über die Tabelle `schueler_lerngruppe` Lerngruppen zugeordnet.

---

## ENT-011 Unterrichtstermin und Unterrichtsstunde getrennt modellieren

**Datum:** 2026-06-23

### Entscheidung

Regelmäßige Stundenplantermine und konkrete Unterrichtsstunden werden getrennt gespeichert.

### Begründung

Ein Unterrichtstermin beschreibt zum Beispiel „Dienstag, 3./4. Stunde“. Eine Unterrichtsstunde beschreibt eine konkrete Stunde an einem konkreten Datum.

### Konsequenz

Das MVP enthält sowohl `unterrichtstermin` als auch `unterrichtsstunde`.

---

## ENT-012 Fehlzeiten pro Unterrichtsstunde

**Datum:** 2026-06-23

### Entscheidung

Fehlzeiten werden pro Schüler und Unterrichtsstunde gespeichert.

### Begründung

Für Fachunterricht und Unterrichtsgruppen ist die stundenbezogene Erfassung präziser als reine Tagesfehlzeiten.

### Konsequenz

Die Tabelle `anwesenheit` verweist auf `schueler`, `unterrichtsstunde` und `lerngruppe`.

---

## ENT-013 Leistungen zweistufig modellieren

**Datum:** 2026-06-23

### Entscheidung

Leistungen werden in `leistungsnachweis` und `leistungsbewertung` getrennt.

### Begründung

Ein Leistungsnachweis beschreibt die Aufgabe oder Prüfung. Eine Leistungsbewertung beschreibt das Ergebnis eines einzelnen Schülers.

### Konsequenz

Eine Klassenarbeit wird einmal angelegt. Die individuellen Ergebnisse werden separat gespeichert.

---

## ENT-014 Dokumentenorientierte Entwicklung

**Datum:** 2026-06-23

### Entscheidung

Anforderungen, Datenmodell, Architektur, Testfälle und NocoDB-Schema werden als Markdown-Dokumente gepflegt.

### Begründung

Bei KI-gestützter Entwicklung müssen Anforderungen dauerhaft nachvollziehbar bleiben. Die Dokumente dienen als Single Source of Truth.

### Konsequenz

Änderungen sollen zuerst in den Dokumenten nachvollzogen und erst danach umgesetzt werden.

---

## ENT-015 MVP vor Vollausbau

**Datum:** 2026-06-23

### Entscheidung

Zuerst wird ein MVP umgesetzt, nicht der gesamte Funktionsumfang aus der Master-Spezifikation.

### Begründung

Das Projekt enthält viele sinnvolle Anforderungen, aber KI-Import, WebUntis-Integration, Pseudonymisierung und automatisierte Berichte erhöhen den Aufwand stark.

### Konsequenz

Der erste technische Aufbau orientiert sich an `02a_MVP_Datenmodell.md` und `09_NocoDB_Schema.md`.
