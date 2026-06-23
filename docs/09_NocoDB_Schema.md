# NocoDB-Schema

**Datei:** `09_NocoDB_Schema.md`  
**Projekt:** Teacher Intelligence System (TIS)  
**Version:** 0.1  
**Status:** Entwurf  
**Letzte Änderung:** 2026-06-23  
**Quelle:** Abgeleitet aus `02a_MVP_Datenmodell.md`

---

## 1. Zweck dieses Dokuments

Dieses Dokument beschreibt die konkrete NocoDB-Struktur für das MVP des Teacher Intelligence Systems.

Es dient als Bauanleitung für die manuelle Einrichtung in NocoDB.

Für jede Tabelle werden festgelegt:

- Tabellenname
- Zweck
- Primäranzeigefeld
- Felder
- NocoDB-Feldtyp
- Pflichtfeld
- Auswahlwerte
- Verknüpfungen
- Standardansichten

---

## 2. Grundsätze für die NocoDB-Umsetzung

### 2.1 Tabellenbenennung

Alle Tabellen werden kleingeschrieben und mit Unterstrich getrennt.

Beispiele:

- `schueler`
- `schueler_lerngruppe`
- `leistungsbewertung`

### 2.2 Feldbenennung

Alle Felder werden kleingeschrieben und mit Unterstrich getrennt.

Beispiele:

- `vorname`
- `nachname`
- `schuljahr_id`
- `ki_generiert`

### 2.3 Primäranzeigefelder

Jede Tabelle benötigt ein aussagekräftiges Primäranzeigefeld.

Bei einfachen Tabellen ist das meist `bezeichnung` oder `titel`.

Bei Tabellen mit Verknüpfungen kann zunächst ein Textfeld wie `anzeige_name` genutzt werden, wenn NocoDB keine zusammengesetzten Anzeigen komfortabel abbildet.

### 2.4 Pflichtfelder

Pflichtfelder werden nur dort gesetzt, wo sie für die Datenlogik zwingend nötig sind.

Für das MVP gilt:

- lieber wenige Pflichtfelder
- Importfreundlichkeit vor perfekter Validierung
- Validierung später über Views, Tests und Automatisierungen ergänzen

### 2.5 Verknüpfungen

NocoDB-Feldtyp für Beziehungen:

`LinkToAnotherRecord`

Verknüpfungen werden erst angelegt, wenn die Zieltabellen bereits existieren.

### 2.6 Zeitstempel

Für zentrale Tabellen sollten folgende Felder genutzt werden:

- `erstellt_am` → `CreatedTime`
- `geaendert_am` → `LastModifiedTime`

Falls NocoDB in der konkreten Installation andere automatische Feldtypen verwendet, werden diese entsprechend angepasst.

---

## 3. Reihenfolge der Tabellenerstellung

Die Tabellen werden in folgender Reihenfolge angelegt:

1. `schuljahr`
2. `fach`
3. `schueler`
4. `lerngruppe`
5. `schueler_lerngruppe`
6. `unterrichtstermin`
7. `unterrichtsstunde`
8. `anwesenheit`
9. `leistungsnachweis`
10. `leistungsbewertung`
11. `kompetenz`
12. `kompetenzbewertung`
13. `beobachtung`
14. `dokument`
15. `dokument_schueler`
16. `bericht`

---

# 4. Tabellen

---

## 4.1 Tabelle: `schuljahr`

### Zweck

Speichert Schuljahre.

### Primäranzeigefeld

`bezeichnung`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `bezeichnung` | SingleLineText | ja | Bezeichnung des Schuljahres |
| `startdatum` | Date | nein | Beginn des Schuljahres |
| `enddatum` | Date | nein | Ende des Schuljahres |
| `aktiv` | Checkbox | ja | Markiert das aktive Schuljahr |
| `bemerkung` | LongText | nein | Freie Bemerkung |

### Beispielwerte

| bezeichnung | startdatum | enddatum | aktiv |
|---|---|---|---|
| 2025/2026 | 2025-08-01 | 2026-07-31 | nein |
| 2026/2027 | 2026-08-01 | 2027-07-31 | ja |

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Alle Schuljahre` | keine | `bezeichnung` absteigend |
| `Aktives Schuljahr` | `aktiv` ist wahr | `bezeichnung` absteigend |

---

## 4.2 Tabelle: `fach`

### Zweck

Speichert Unterrichtsfächer.

### Primäranzeigefeld

`bezeichnung`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `bezeichnung` | SingleLineText | ja | Name des Fachs |
| `kuerzel` | SingleLineText | nein | Fachkürzel |
| `fachbereich` | SingleLineText | nein | Fachbereich |
| `aktiv` | Checkbox | ja | Fach ist aktiv |

### Beispielwerte

| bezeichnung | kuerzel | fachbereich | aktiv |
|---|---|---|---|
| Naturwissenschaften | NW | Naturwissenschaften | ja |
| Physik | PH | Naturwissenschaften | ja |
| Chemie | CH | Naturwissenschaften | ja |
| Informatik | INF | Informatik | ja |

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Aktive Fächer` | `aktiv` ist wahr | `bezeichnung` aufsteigend |
| `Alle Fächer` | keine | `bezeichnung` aufsteigend |

---

## 4.3 Tabelle: `schueler`

### Zweck

Speichert die zentralen Stammdaten eines Schülers.

### Primäranzeigefeld

`anzeige_name`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `anzeige_name` | SingleLineText | ja | Anzeigename, z. B. Nachname, Vorname |
| `externe_id` | SingleLineText | nein | ID aus Fremdsystemen |
| `webuntis_id` | SingleLineText | nein | WebUntis-ID, falls vorhanden |
| `vorname` | SingleLineText | ja | Vorname |
| `nachname` | SingleLineText | ja | Nachname |
| `rufname` | SingleLineText | nein | Abweichender Rufname |
| `geburtsdatum` | Date | nein | Geburtsdatum |
| `geschlecht` | SingleSelect | nein | Geschlecht |
| `email_schueler` | Email | nein | Schüler-E-Mail |
| `telefon_schueler` | PhoneNumber | nein | Schüler-Telefonnummer |
| `adresse` | LongText | nein | Adresse als Freitext im MVP |
| `eltern_kontakt` | LongText | nein | Elternkontakte als Freitext im MVP |
| `bemerkung` | LongText | nein | Allgemeine Bemerkung |
| `aktiv` | Checkbox | ja | Schüler ist aktiv |
| `archiviert` | Checkbox | ja | Schüler ist archiviert |
| `erstellt_am` | CreatedTime | ja | Erstellungszeitpunkt |
| `geaendert_am` | LastModifiedTime | nein | Letzte Änderung |

### Auswahlwerte für `geschlecht`

- weiblich
- männlich
- divers
- keine Angabe

### Hinweise

`anzeige_name` wird im MVP manuell gepflegt, z. B. `Schröder, Felix`.

Später kann dieses Feld automatisiert aus `nachname` und `vorname` erzeugt werden.

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Aktive Schüler` | `aktiv` ist wahr und `archiviert` ist falsch | `nachname`, `vorname` |
| `Archivierte Schüler` | `archiviert` ist wahr | `nachname`, `vorname` |
| `Schüler mit WebUntis-ID` | `webuntis_id` ist nicht leer | `nachname`, `vorname` |
| `Schüler ohne WebUntis-ID` | `webuntis_id` ist leer | `nachname`, `vorname` |

---

## 4.4 Tabelle: `lerngruppe`

### Zweck

Speichert konkrete Unterrichtsgruppen einer Lehrkraft.

### Primäranzeigefeld

`bezeichnung`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `bezeichnung` | SingleLineText | ja | Name der Lerngruppe |
| `schuljahr_id` | LinkToAnotherRecord → `schuljahr` | ja | Zugehöriges Schuljahr |
| `fach_id` | LinkToAnotherRecord → `fach` | nein | Zugehöriges Fach |
| `jahrgang` | Number | nein | Jahrgangsstufe |
| `klasse` | SingleLineText | nein | Klassenbezeichnung |
| `kursart` | SingleSelect | nein | Art der Lerngruppe |
| `niveau` | SingleSelect | nein | Niveau |
| `wochenstunden` | Number | nein | Wochenstunden |
| `aktiv` | Checkbox | ja | Lerngruppe ist aktiv |
| `archiviert` | Checkbox | ja | Lerngruppe ist archiviert |
| `bemerkung` | LongText | nein | Bemerkung |

### Auswahlwerte für `kursart`

- Klassenunterricht
- Grundkurs
- Leistungskurs
- Wahlpflichtkurs
- AG
- Tutorengruppe
- sonstige Lerngruppe

### Auswahlwerte für `niveau`

- G-Niveau
- E-Niveau
- grundlegend
- erhöht
- gemischt
- nicht relevant

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Aktive Lerngruppen` | `aktiv` ist wahr und `archiviert` ist falsch | `bezeichnung` |
| `Archivierte Lerngruppen` | `archiviert` ist wahr | `bezeichnung` |
| `Lerngruppen aktuelles Schuljahr` | manuell nach aktuellem `schuljahr_id` filtern | `bezeichnung` |
| `Tutorengruppen` | `kursart` ist `Tutorengruppe` | `bezeichnung` |

---

## 4.5 Tabelle: `schueler_lerngruppe`

### Zweck

Verknüpft Schüler mit Lerngruppen.

### Primäranzeigefeld

`anzeige_name`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `anzeige_name` | SingleLineText | ja | Anzeige für die Zuordnung |
| `schueler_id` | LinkToAnotherRecord → `schueler` | ja | Verknüpfter Schüler |
| `lerngruppe_id` | LinkToAnotherRecord → `lerngruppe` | ja | Verknüpfte Lerngruppe |
| `eintrittsdatum` | Date | nein | Eintritt in die Lerngruppe |
| `austrittsdatum` | Date | nein | Austritt aus der Lerngruppe |
| `status` | SingleSelect | ja | Status der Zuordnung |
| `rolle` | SingleSelect | nein | Rolle der Lehrkraft bezogen auf den Schüler |
| `bemerkung` | LongText | nein | Bemerkung |

### Auswahlwerte für `status`

- aktiv
- gewechselt
- ausgeschieden
- archiviert

### Auswahlwerte für `rolle`

- Fachlehrkraft
- Tutor
- Klassenleitung
- Beratungslehrkraft
- sonstige Rolle

### Hinweise

`anzeige_name` kann im MVP manuell als Kombination aus Schüler und Lerngruppe gepflegt werden.

Beispiel:

`Schröder, Felix – 10c Chemie 2026/2027`

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Aktive Zuordnungen` | `status` ist `aktiv` | `lerngruppe_id`, `schueler_id` |
| `Nach Lerngruppe` | keine | gruppiert nach `lerngruppe_id` |
| `Tutor-Schüler` | `rolle` ist `Tutor` oder `Klassenleitung` | `schueler_id` |

---

## 4.6 Tabelle: `unterrichtstermin`

### Zweck

Speichert regelmäßige Unterrichtstermine einer Lerngruppe.

Ein Unterrichtstermin beschreibt einen wiederkehrenden Termin im Stundenplan.

### Primäranzeigefeld

`anzeige_name`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `anzeige_name` | SingleLineText | ja | Anzeigename des Termins |
| `lerngruppe_id` | LinkToAnotherRecord → `lerngruppe` | ja | Verknüpfte Lerngruppe |
| `wochentag` | SingleSelect | ja | Wochentag |
| `stunde_von` | SingleLineText | nein | Erste Schulstunde |
| `stunde_bis` | SingleLineText | nein | Letzte Schulstunde |
| `beginn` | Time | nein | Beginn |
| `ende` | Time | nein | Ende |
| `raum` | SingleLineText | nein | Raum |
| `rhythmus` | SingleSelect | nein | Wiederholungsrhythmus |
| `gueltig_ab` | Date | nein | Beginn der Gültigkeit |
| `gueltig_bis` | Date | nein | Ende der Gültigkeit |
| `aktiv` | Checkbox | ja | Termin ist aktiv |
| `bemerkung` | LongText | nein | Bemerkung |

### Auswahlwerte für `wochentag`

- Montag
- Dienstag
- Mittwoch
- Donnerstag
- Freitag
- Samstag

### Auswahlwerte für `rhythmus`

- wöchentlich
- A-Woche
- B-Woche
- einmalig
- unregelmäßig

### Beispiel für `anzeige_name`

`Dienstag 3./4. Stunde – 10c Chemie`

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Aktive Unterrichtstermine` | `aktiv` ist wahr | `wochentag`, `beginn` |
| `Wochenübersicht` | `aktiv` ist wahr | gruppiert nach `wochentag` |
| `Nach Lerngruppe` | `aktiv` ist wahr | gruppiert nach `lerngruppe_id` |

---

## 4.7 Tabelle: `unterrichtsstunde`

### Zweck

Speichert konkrete Unterrichtsstunden.

### Primäranzeigefeld

`titel`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `titel` | SingleLineText | ja | Kurzbezeichnung der Stunde |
| `lerngruppe_id` | LinkToAnotherRecord → `lerngruppe` | ja | Verknüpfte Lerngruppe |
| `unterrichtstermin_id` | LinkToAnotherRecord → `unterrichtstermin` | nein | Verknüpfter regelmäßiger Termin |
| `datum` | Date | ja | Datum der Stunde |
| `stunde` | SingleLineText | nein | Schulstunde oder Stundenblock |
| `beginn` | Time | nein | Beginn |
| `ende` | Time | nein | Ende |
| `thema` | SingleLineText | nein | Unterrichtsthema |
| `inhalt` | LongText | nein | Unterrichtsinhalt |
| `hausaufgabe` | LongText | nein | Hausaufgabe |
| `material` | LongText | nein | Genutztes Material |
| `bemerkung` | LongText | nein | Allgemeine Bemerkung |
| `erstellt_am` | CreatedTime | ja | Erstellungszeitpunkt |
| `geaendert_am` | LastModifiedTime | nein | Letzte Änderung |

### Beispiel für `titel`

`2026-09-01 – 10c Chemie – Säure-Base-Reaktionen`

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Alle Unterrichtsstunden` | keine | `datum` absteigend |
| `Heutige Unterrichtsstunden` | `datum` ist heute | `beginn` |
| `Nach Lerngruppe` | keine | gruppiert nach `lerngruppe_id`, dann `datum` |
| `Ohne Thema` | `thema` ist leer | `datum` absteigend |

---

## 4.8 Tabelle: `anwesenheit`

### Zweck

Speichert Anwesenheit, Fehlzeiten und Verspätungen pro Schüler und Unterrichtsstunde.

### Primäranzeigefeld

`anzeige_name`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `anzeige_name` | SingleLineText | ja | Anzeige für den Anwesenheitseintrag |
| `schueler_id` | LinkToAnotherRecord → `schueler` | ja | Verknüpfter Schüler |
| `unterrichtsstunde_id` | LinkToAnotherRecord → `unterrichtsstunde` | ja | Verknüpfte Unterrichtsstunde |
| `lerngruppe_id` | LinkToAnotherRecord → `lerngruppe` | ja | Redundanter Verweis für Filterung |
| `datum` | Date | ja | Redundantes Datum für Filterung |
| `status` | SingleSelect | ja | Anwesenheitsstatus |
| `entschuldigungsstatus` | SingleSelect | nein | Status der Entschuldigung |
| `minuten_verspaetet` | Number | nein | Minuten der Verspätung |
| `quelle` | SingleSelect | nein | Herkunft der Information |
| `bemerkung` | LongText | nein | Bemerkung |

### Auswahlwerte für `status`

- anwesend
- fehlend
- verspätet
- teilweise anwesend
- beurlaubt
- schulische Veranstaltung
- unbekannt

### Auswahlwerte für `entschuldigungsstatus`

- nicht erforderlich
- offen
- entschuldigt
- unentschuldigt
- nachgereicht
- strittig

### Auswahlwerte für `quelle`

- manuell
- WebUntis
- KI-Import
- sonstiger Import

### Beispiel für `anzeige_name`

`Schröder, Felix – 2026-09-01 – fehlend`

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Alle Fehlzeiten` | `status` ist nicht `anwesend` | `datum` absteigend |
| `Offene Entschuldigungen` | `entschuldigungsstatus` ist `offen` | `datum` absteigend |
| `Unentschuldigte Fehlzeiten` | `entschuldigungsstatus` ist `unentschuldigt` | `datum` absteigend |
| `Verspätungen` | `status` ist `verspätet` | `datum` absteigend |
| `Nach Lerngruppe` | `status` ist nicht `anwesend` | gruppiert nach `lerngruppe_id` |
| `Nach Schüler` | `status` ist nicht `anwesend` | gruppiert nach `schueler_id` |

---

## 4.9 Tabelle: `leistungsnachweis`

### Zweck

Speichert bewertete Leistungssituationen.

Ein Leistungsnachweis beschreibt das Ereignis, nicht das individuelle Ergebnis.

### Primäranzeigefeld

`titel`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `titel` | SingleLineText | ja | Titel des Leistungsnachweises |
| `lerngruppe_id` | LinkToAnotherRecord → `lerngruppe` | ja | Verknüpfte Lerngruppe |
| `fach_id` | LinkToAnotherRecord → `fach` | nein | Verknüpftes Fach |
| `schuljahr_id` | LinkToAnotherRecord → `schuljahr` | ja | Verknüpftes Schuljahr |
| `datum` | Date | nein | Datum |
| `bewertungsart` | SingleSelect | ja | Art der Bewertung |
| `maximalpunkte` | Decimal | nein | Maximal erreichbare Punkte |
| `gewichtung` | Decimal | nein | Gewichtung |
| `bemerkung` | LongText | nein | Bemerkung |

### Auswahlwerte für `bewertungsart`

- Klassenarbeit
- Test
- Präsentation
- Experiment
- Projekt
- mündliche Leistung
- Mitarbeit
- praktische Leistung
- sonstige Leistung

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Alle Leistungsnachweise` | keine | `datum` absteigend |
| `Nach Lerngruppe` | keine | gruppiert nach `lerngruppe_id`, dann `datum` |
| `Klassenarbeiten` | `bewertungsart` ist `Klassenarbeit` | `datum` absteigend |
| `Mündliche Leistungen` | `bewertungsart` ist `mündliche Leistung` oder `Mitarbeit` | `datum` absteigend |

---

## 4.10 Tabelle: `leistungsbewertung`

### Zweck

Speichert das Ergebnis eines Schülers zu einem Leistungsnachweis.

### Primäranzeigefeld

`anzeige_name`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `anzeige_name` | SingleLineText | ja | Anzeige für die Bewertung |
| `leistungsnachweis_id` | LinkToAnotherRecord → `leistungsnachweis` | ja | Verknüpfter Leistungsnachweis |
| `schueler_id` | LinkToAnotherRecord → `schueler` | ja | Verknüpfter Schüler |
| `punkte` | Decimal | nein | Erreichte Punkte |
| `prozent` | Percent | nein | Prozentwert |
| `note` | SingleLineText | nein | Note |
| `notenpunkte` | Number | nein | Notenpunkte 0-15 |
| `tendenz` | SingleSelect | nein | Notentendenz |
| `kommentar` | LongText | nein | Kommentar zur Leistung |
| `paedagogische_anpassung` | Checkbox | nein | Bewertung wurde pädagogisch angepasst |
| `begruendung_anpassung` | LongText | nein | Begründung der Anpassung |
| `dokument_id` | LinkToAnotherRecord → `dokument` | nein | Verknüpftes Dokument |
| `erstellt_am` | CreatedTime | ja | Erstellungszeitpunkt |
| `geaendert_am` | LastModifiedTime | nein | Letzte Änderung |

### Auswahlwerte für `tendenz`

- plus
- neutral
- minus

### Beispiel für `anzeige_name`

`Schröder, Felix – Klassenarbeit 1 Säure-Base`

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Alle Leistungsbewertungen` | keine | `erstellt_am` absteigend |
| `Nach Schüler` | keine | gruppiert nach `schueler_id` |
| `Nach Leistungsnachweis` | keine | gruppiert nach `leistungsnachweis_id` |
| `Pädagogisch angepasst` | `paedagogische_anpassung` ist wahr | `geaendert_am` absteigend |
| `Ohne Bewertung` | `punkte`, `note` und `notenpunkte` sind leer | `leistungsnachweis_id` |

---

## 4.11 Tabelle: `kompetenz`

### Zweck

Speichert bewertbare Kompetenzen.

### Primäranzeigefeld

`bezeichnung`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `bezeichnung` | SingleLineText | ja | Kompetenzname |
| `fach_id` | LinkToAnotherRecord → `fach` | nein | Verknüpftes Fach |
| `bereich` | SingleLineText | nein | Kompetenzbereich |
| `beschreibung` | LongText | nein | Beschreibung der Kompetenz |
| `aktiv` | Checkbox | ja | Kompetenz ist aktiv |

### Beispielwerte

| bereich | bezeichnung |
|---|---|
| Kommunikation | Argumentieren |
| Kommunikation | Präsentieren |
| Erkenntnisgewinnung | Experiment planen |
| Erkenntnisgewinnung | Daten auswerten |
| Fachwissen | Fachsprache nutzen |

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Aktive Kompetenzen` | `aktiv` ist wahr | `bereich`, `bezeichnung` |
| `Nach Fach` | `aktiv` ist wahr | gruppiert nach `fach_id` |
| `Nach Bereich` | `aktiv` ist wahr | gruppiert nach `bereich` |

---

## 4.12 Tabelle: `kompetenzbewertung`

### Zweck

Speichert den Kompetenzstand eines Schülers zu einem Zeitpunkt.

### Primäranzeigefeld

`anzeige_name`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `anzeige_name` | SingleLineText | ja | Anzeige für die Kompetenzbewertung |
| `schueler_id` | LinkToAnotherRecord → `schueler` | ja | Verknüpfter Schüler |
| `kompetenz_id` | LinkToAnotherRecord → `kompetenz` | ja | Verknüpfte Kompetenz |
| `lerngruppe_id` | LinkToAnotherRecord → `lerngruppe` | nein | Verknüpfte Lerngruppe |
| `unterrichtsstunde_id` | LinkToAnotherRecord → `unterrichtsstunde` | nein | Verknüpfte Unterrichtsstunde |
| `leistungsnachweis_id` | LinkToAnotherRecord → `leistungsnachweis` | nein | Verknüpfter Leistungsnachweis |
| `datum` | Date | ja | Datum der Bewertung |
| `bewertung` | SingleSelect | ja | Kompetenzbewertung |
| `kommentar` | LongText | nein | Kommentar |
| `quelle` | SingleSelect | nein | Herkunft der Bewertung |
| `erstellt_am` | CreatedTime | ja | Erstellungszeitpunkt |
| `geaendert_am` | LastModifiedTime | nein | Letzte Änderung |

### Auswahlwerte für `bewertung`

- Trifft noch nicht zu
- Trifft teilweise zu
- Trifft fast zu
- Trifft zu

### Auswahlwerte für `quelle`

- manuell
- Leistungsbewertung
- Beobachtung
- KI-Vorschlag
- Import

### Beispiel für `anzeige_name`

`Schröder, Felix – Argumentieren – Trifft fast zu`

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Alle Kompetenzbewertungen` | keine | `datum` absteigend |
| `Nach Schüler` | keine | gruppiert nach `schueler_id` |
| `Nach Kompetenz` | keine | gruppiert nach `kompetenz_id` |
| `Nach Lerngruppe` | keine | gruppiert nach `lerngruppe_id` |
| `Förderbedarf` | `bewertung` ist `Trifft noch nicht zu` oder `Trifft teilweise zu` | `datum` absteigend |
| `KI-Vorschläge` | `quelle` ist `KI-Vorschlag` | `datum` absteigend |

---

## 4.13 Tabelle: `beobachtung`

### Zweck

Speichert pädagogische Beobachtungen, Notizen und Gesprächsnotizen.

### Primäranzeigefeld

`titel`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `titel` | SingleLineText | nein | Kurztitel |
| `schueler_id` | LinkToAnotherRecord → `schueler` | ja | Verknüpfter Schüler |
| `lerngruppe_id` | LinkToAnotherRecord → `lerngruppe` | nein | Verknüpfte Lerngruppe |
| `unterrichtsstunde_id` | LinkToAnotherRecord → `unterrichtsstunde` | nein | Verknüpfte Unterrichtsstunde |
| `datum` | Date | ja | Datum der Beobachtung |
| `kategorie` | SingleSelect | ja | Beobachtungskategorie |
| `inhalt` | LongText | ja | Beobachtungstext |
| `relevanz` | SingleSelect | nein | Relevanz |
| `ki_generiert` | Checkbox | ja | Eintrag wurde durch KI erzeugt |
| `geprueft` | Checkbox | ja | Eintrag wurde durch Lehrkraft geprüft |
| `erstellt_am` | CreatedTime | ja | Erstellungszeitpunkt |
| `geaendert_am` | LastModifiedTime | nein | Letzte Änderung |

### Auswahlwerte für `kategorie`

- Mitarbeit
- Sozialverhalten
- Arbeitsverhalten
- Fachleistung
- Organisation
- Hausaufgaben
- Material
- Störung
- positive Entwicklung
- Förderhinweis
- Gesprächsnotiz
- sonstige Beobachtung

### Auswahlwerte für `relevanz`

- niedrig
- normal
- hoch
- kritisch

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Alle Beobachtungen` | keine | `datum` absteigend |
| `Beobachtungen heute` | `datum` ist heute | `schueler_id` |
| `Nach Schüler` | keine | gruppiert nach `schueler_id` |
| `Nach Lerngruppe` | keine | gruppiert nach `lerngruppe_id` |
| `Hohe Relevanz` | `relevanz` ist `hoch` oder `kritisch` | `datum` absteigend |
| `Ungeprüfte KI-Einträge` | `ki_generiert` ist wahr und `geprueft` ist falsch | `datum` absteigend |
| `Gesprächsnotizen` | `kategorie` ist `Gesprächsnotiz` | `datum` absteigend |

---

## 4.14 Tabelle: `dokument`

### Zweck

Speichert Metadaten zu Dateien.

Dateien können lokal oder in einem Cloudspeicher liegen.

### Primäranzeigefeld

`titel`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `titel` | SingleLineText | ja | Dokumenttitel |
| `dokumenttyp` | SingleSelect | ja | Art des Dokuments |
| `dateiname` | SingleLineText | nein | Dateiname |
| `cloud_link` | URL | nein | Link zu OneDrive, SharePoint, Nextcloud etc. |
| `speicherort` | SingleSelect | nein | Speicherort |
| `dateiformat` | SingleLineText | nein | PDF, DOCX, XLSX usw. |
| `beschreibung` | LongText | nein | Beschreibung |
| `quelle` | SingleSelect | nein | Herkunft |
| `hochgeladen_am` | DateTime | nein | Zeitpunkt des Hochladens |
| `ki_analysiert` | Checkbox | nein | Dokument wurde KI-analysiert |
| `analyse_status` | SingleSelect | nein | Status der Analyse |

### Auswahlwerte für `dokumenttyp`

- Klassenarbeit
- Präsentation
- Bewertungsbogen
- Förderplan
- Gesprächsprotokoll
- Elternbrief
- Schülerarbeit
- WebUntis-Export
- sonstiges Dokument

### Auswahlwerte für `speicherort`

- OneDrive
- SharePoint
- Nextcloud
- lokal
- Datenbank
- anderer Speicher

### Auswahlwerte für `quelle`

- manuell
- Import
- WebUntis
- KI-Import
- sonstige Quelle

### Auswahlwerte für `analyse_status`

- nicht analysiert
- in Bearbeitung
- analysiert
- Fehler

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Alle Dokumente` | keine | `hochgeladen_am` absteigend |
| `OneDrive-Dokumente` | `speicherort` ist `OneDrive` | `hochgeladen_am` absteigend |
| `WebUntis-Exporte` | `dokumenttyp` ist `WebUntis-Export` | `hochgeladen_am` absteigend |
| `Noch nicht analysiert` | `analyse_status` ist `nicht analysiert` oder leer | `hochgeladen_am` absteigend |
| `Analysefehler` | `analyse_status` ist `Fehler` | `hochgeladen_am` absteigend |

---

## 4.15 Tabelle: `dokument_schueler`

### Zweck

Verknüpft Dokumente mit Schülern.

Ein Dokument kann einem oder mehreren Schülern zugeordnet sein.

### Primäranzeigefeld

`anzeige_name`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `anzeige_name` | SingleLineText | ja | Anzeige für die Dokumentzuordnung |
| `dokument_id` | LinkToAnotherRecord → `dokument` | ja | Verknüpftes Dokument |
| `schueler_id` | LinkToAnotherRecord → `schueler` | ja | Verknüpfter Schüler |
| `bezugstyp` | SingleSelect | nein | Art des Bezugs |
| `bemerkung` | LongText | nein | Bemerkung |

### Auswahlwerte für `bezugstyp`

- gehört zu Schüler
- betrifft Schüler
- wurde von Schüler erstellt
- Bewertung zu Schüler
- Gesprächsdokument
- sonstiger Bezug

### Beispiel für `anzeige_name`

`Schröder, Felix – Klassenarbeit 1 Scan`

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Alle Dokumentzuordnungen` | keine | `schueler_id` |
| `Nach Schüler` | keine | gruppiert nach `schueler_id` |
| `Nach Dokument` | keine | gruppiert nach `dokument_id` |
| `Schülerarbeiten` | `bezugstyp` ist `wurde von Schüler erstellt` | `schueler_id` |

---

## 4.16 Tabelle: `bericht`

### Zweck

Speichert manuelle oder KI-generierte Berichte.

### Primäranzeigefeld

`titel`

### Felder

| Feldname | NocoDB-Feldtyp | Pflicht | Beschreibung |
|---|---|---:|---|
| `titel` | SingleLineText | ja | Berichtstitel |
| `schueler_id` | LinkToAnotherRecord → `schueler` | ja | Verknüpfter Schüler |
| `lerngruppe_id` | LinkToAnotherRecord → `lerngruppe` | nein | Verknüpfte Lerngruppe |
| `schuljahr_id` | LinkToAnotherRecord → `schuljahr` | nein | Verknüpftes Schuljahr |
| `berichtstyp` | SingleSelect | ja | Art des Berichts |
| `inhalt` | LongText | ja | Berichtstext |
| `status` | SingleSelect | ja | Bearbeitungsstatus |
| `ki_generiert` | Checkbox | ja | Bericht wurde durch KI erstellt |
| `geprueft` | Checkbox | ja | Bericht wurde durch Lehrkraft geprüft |
| `erstellt_am` | CreatedTime | ja | Erstellungszeitpunkt |
| `geaendert_am` | LastModifiedTime | nein | Letzte Änderung |

### Auswahlwerte für `berichtstyp`

- Lernentwicklungsbericht
- Elterngesprächsvorbereitung
- Schülerzusammenfassung
- Förderempfehlung
- Klassenkonferenznotiz
- Zeugnistextentwurf
- sonstiger Bericht

### Auswahlwerte für `status`

- Entwurf
- geprüft
- final
- archiviert

### Standardansichten

| Ansicht | Filter | Sortierung |
|---|---|---|
| `Alle Berichte` | keine | `erstellt_am` absteigend |
| `Entwürfe` | `status` ist `Entwurf` | `erstellt_am` absteigend |
| `Zu prüfen` | `ki_generiert` ist wahr und `geprueft` ist falsch | `erstellt_am` absteigend |
| `Nach Schüler` | keine | gruppiert nach `schueler_id` |
| `Lernentwicklungsberichte` | `berichtstyp` ist `Lernentwicklungsbericht` | `erstellt_am` absteigend |

---

# 5. Empfohlene globale Arbeitsansichten

Neben den tabellenspezifischen Ansichten sollten folgende Arbeitsansichten eingerichtet werden.

## 5.1 Schülerakte-Ansichten

Diese Ansichten werden über Filter auf den jeweiligen Tabellen umgesetzt.

Für einen konkreten Schüler werden jeweils die verknüpften Datensätze angezeigt.

Benötigte Ansichten:

- `Schüler – Stammdaten`
- `Schüler – Lerngruppen`
- `Schüler – Fehlzeiten`
- `Schüler – Leistungen`
- `Schüler – Kompetenzen`
- `Schüler – Beobachtungen`
- `Schüler – Dokumente`
- `Schüler – Berichte`

## 5.2 Tagesansichten

- `Heutige Unterrichtsstunden`
- `Beobachtungen heute`
- `Fehlzeiten heute`
- `Offene Einträge heute`

## 5.3 Kontrollansichten

- `Offene Entschuldigungen`
- `Ungeprüfte KI-Einträge`
- `Dokumente ohne Schülerzuordnung`
- `Leistungsbewertungen ohne Note`
- `Kompetenzbewertungen mit Förderbedarf`
- `Berichte im Entwurf`

---

# 6. Erste Testdaten

Vor echten Schülerdaten werden Testdaten angelegt.

## 6.1 Schuljahre

| bezeichnung | aktiv |
|---|---|
| 2026/2027 | ja |

## 6.2 Fächer

| bezeichnung | kuerzel |
|---|---|
| Chemie | CH |
| Physik | PH |
| Informatik | INF |
| Naturwissenschaften | NW |

## 6.3 Schüler

| anzeige_name | vorname | nachname | aktiv | archiviert |
|---|---|---|---:|---:|
| Schröder, Felix | Felix | Schröder | ja | nein |
| Meier, Laura | Laura | Meier | ja | nein |
| Beispiel, Paul | Paul | Beispiel | ja | nein |

## 6.4 Lerngruppe

| bezeichnung | fach | schuljahr | aktiv |
|---|---|---|---:|
| 10c Chemie 2026/2027 | Chemie | 2026/2027 | ja |

## 6.5 Testkette

Folgende Kette muss nach der Einrichtung funktionieren:

1. Schüler anlegen
2. Fach anlegen
3. Schuljahr anlegen
4. Lerngruppe anlegen
5. Schüler Lerngruppe zuordnen
6. Unterrichtstermin anlegen
7. Unterrichtsstunde anlegen
8. Anwesenheit erfassen
9. Beobachtung erfassen
10. Leistungsnachweis anlegen
11. Leistungsbewertung eintragen
12. Kompetenz anlegen
13. Kompetenzbewertung eintragen
14. Dokument anlegen
15. Dokument Schüler zuordnen
16. Bericht anlegen

---

# 7. MVP-Prüffragen

Nach der Einrichtung muss das Schema folgende Fragen beantworten können.

## 7.1 Schülerakte

- Welche Lerngruppen besucht Felix Schröder?
- Welche Beobachtungen liegen zu Felix Schröder vor?
- Welche Dokumente sind Felix Schröder zugeordnet?
- Welche Berichte wurden zu Felix Schröder erstellt?

## 7.2 Fehlzeiten

- Wie viele Unterrichtsstunden hat Felix Schröder gefehlt?
- Welche Fehlzeiten sind noch offen?
- Welche Fehlzeiten sind unentschuldigt?
- In welcher Lerngruppe gibt es viele Fehlzeiten?

## 7.3 Leistungen

- Welche Leistungsnachweise gibt es in 10c Chemie?
- Welche Bewertung hat Felix Schröder in Klassenarbeit 1 erhalten?
- Welche Noten liegen zu Felix Schröder im Schuljahr 2026/2027 vor?

## 7.4 Kompetenzen

- Welche Kompetenzen wurden bei Felix Schröder bewertet?
- Welche Kompetenzbewertungen zeigen Förderbedarf?
- Wie hat sich eine Kompetenz über die Zeit entwickelt?

## 7.5 Dokumente und Berichte

- Welche Dokumente sind noch keinem Schüler zugeordnet?
- Welche Berichte sind noch Entwürfe?
- Welche KI-generierten Berichte müssen geprüft werden?

---

# 8. Hinweise zur späteren Erweiterung

Dieses Schema ist bewusst MVP-orientiert.

Folgende Erweiterungen sind vorbereitet, aber noch nicht vollständig umgesetzt:

- echte Kontaktpersonen statt Freitext in `schueler`
- separate Adresstabelle
- Halbjahre
- Notenschlüssel
- Importvorgänge
- Importdatensätze
- KI-Aufträge
- Pseudonymisierung
- Kompetenzskalen
- Gesprächsprotokolle als eigene Tabelle
- automatische Timeline
- automatisierte Unterrichtsstundenerzeugung aus `unterrichtstermin`

---

# 9. Nächster Umsetzungsschritt

Nach Anlage dieser Datei erfolgt die praktische Einrichtung in NocoDB.

Empfohlene Reihenfolge:

1. NocoDB-Projekt anlegen
2. Tabellen nach Abschnitt 3 erstellen
3. Felder gemäß Abschnitt 4 anlegen
4. Verknüpfungen einrichten
5. Standardansichten erstellen
6. Testdaten eintragen
7. MVP-Prüffragen beantworten
8. Fehler im Schema dokumentieren
9. Schema auf Version 0.2 aktualisieren
