# MVP-Datenmodell

**Datei:** `02a_MVP_Datenmodell.md`  
**Projekt:** Teacher Intelligence System (TIS)  
**Version:** 0.2  
**Status:** Entwurf  
**Letzte Änderung:** 2026-06-23

---

## 1. Zweck dieses Dokuments

Dieses Dokument beschreibt das minimale, aber arbeitsfähige Datenmodell für den ersten Prototypen des Teacher Intelligence Systems.

Das vollständige Zielmodell befindet sich in:

`02_Datenmodell.md`

Dieses MVP-Datenmodell reduziert das Zielmodell auf die Tabellen, die notwendig sind, um erste echte Schülerakten im Schulalltag zu führen.

---

## 2. Ziel des MVP

Das MVP soll ermöglichen:

- Schülerakten anzulegen
- Schüler mehreren Lerngruppen zuzuordnen
- mehrere Schuljahre abzubilden
- regelmäßige Unterrichtstermine im persönlichen Stundenplan abzubilden
- Unterrichtsstunden zu dokumentieren
- Fehlzeiten pro Unterrichtsstunde zu erfassen
- Leistungen und Noten zu speichern
- Kompetenzen zu bewerten
- Beobachtungen zu dokumentieren
- Dokumente zu Schülern abzulegen oder zu verlinken
- einfache Berichte zu erzeugen

---

## 3. Grundprinzip

Die Schülerakte ist keine eigene Tabelle.

Sie ist eine zusammengesetzte Ansicht aus mehreren verknüpften Tabellen.

Zentrales Objekt ist:

`schueler`

Alle anderen Informationen werden direkt oder indirekt mit einem Schüler verknüpft.

---

## 4. Tabellenübersicht

Für das MVP werden folgende Tabellen benötigt:

1. `schueler`
2. `schuljahr`
3. `fach`
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

# 5. Tabellen

---

## 5.1 Tabelle: `schueler`

### Zweck

Speichert die zentralen Stammdaten eines Schülers.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `externe_id` | Text | nein | ID aus Fremdsystemen |
| `webuntis_id` | Text | nein | WebUntis-ID, falls vorhanden |
| `vorname` | Text | ja | Vorname |
| `nachname` | Text | ja | Nachname |
| `rufname` | Text | nein | Abweichender Rufname |
| `geburtsdatum` | Datum | nein | Geburtsdatum |
| `geschlecht` | Auswahl | nein | Geschlecht |
| `email_schueler` | Text | nein | Schüler-E-Mail |
| `telefon_schueler` | Text | nein | Schüler-Telefonnummer |
| `adresse` | Langer Text | nein | Adresse als Freitext im MVP |
| `eltern_kontakt` | Langer Text | nein | Elternkontakte als Freitext im MVP |
| `bemerkung` | Langer Text | nein | Allgemeine Bemerkung |
| `aktiv` | Checkbox | ja | Schüler ist aktiv |
| `archiviert` | Checkbox | ja | Schüler ist archiviert |
| `erstellt_am` | Datum/Zeit | ja | Erstellungszeitpunkt |
| `geaendert_am` | Datum/Zeit | nein | Letzte Änderung |

### Hinweise

Im Zielmodell werden Adresse und Elternkontakte später in eigene Tabellen ausgelagert.

Für das MVP genügt zunächst eine Freitextlösung, damit der Prototyp schneller nutzbar ist.

---

## 5.2 Tabelle: `schuljahr`

### Zweck

Speichert Schuljahre.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `bezeichnung` | Text | ja | Bezeichnung, z. B. 2026/2027 |
| `startdatum` | Datum | nein | Beginn des Schuljahres |
| `enddatum` | Datum | nein | Ende des Schuljahres |
| `aktiv` | Checkbox | ja | Aktuelles oder aktives Schuljahr |
| `bemerkung` | Langer Text | nein | Bemerkung |

### Beispiele

- 2025/2026
- 2026/2027

---

## 5.3 Tabelle: `fach`

### Zweck

Speichert Unterrichtsfächer.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `bezeichnung` | Text | ja | Fachbezeichnung |
| `kuerzel` | Text | nein | Fachkürzel |
| `fachbereich` | Text | nein | Fachbereich |
| `aktiv` | Checkbox | ja | Fach ist aktiv |

### Beispiele

- Naturwissenschaften
- Physik
- Chemie
- Informatik
- Mathematik
- Deutsch
- Englisch

---

## 5.4 Tabelle: `lerngruppe`

### Zweck

Speichert konkrete Unterrichtsgruppen einer Lehrkraft.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `bezeichnung` | Text | ja | Name der Lerngruppe |
| `schuljahr_id` | Verknüpfung | ja | Verweis auf `schuljahr` |
| `fach_id` | Verknüpfung | nein | Verweis auf `fach` |
| `jahrgang` | Zahl | nein | Jahrgangsstufe |
| `klasse` | Text | nein | Klassenbezeichnung |
| `kursart` | Auswahl | nein | Art der Lerngruppe |
| `niveau` | Auswahl | nein | Niveau |
| `wochenstunden` | Zahl | nein | Wochenstunden |
| `aktiv` | Checkbox | ja | Lerngruppe ist aktiv |
| `archiviert` | Checkbox | ja | Lerngruppe ist archiviert |
| `bemerkung` | Langer Text | nein | Bemerkung |

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

### Beispiele

- 6.5 Naturwissenschaften 2026/2027
- 10c Chemie 2026/2027
- 12gA Chemie GK 2026/2027
- Tutorengruppe Jahrgang 8 2026/2027

---

## 5.5 Tabelle: `schueler_lerngruppe`

### Zweck

Verknüpft Schüler mit Lerngruppen.

Ein Schüler kann mehreren Lerngruppen zugeordnet sein.

Eine Lerngruppe enthält viele Schüler.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `schueler_id` | Verknüpfung | ja | Verweis auf `schueler` |
| `lerngruppe_id` | Verknüpfung | ja | Verweis auf `lerngruppe` |
| `eintrittsdatum` | Datum | nein | Eintritt in die Lerngruppe |
| `austrittsdatum` | Datum | nein | Austritt aus der Lerngruppe |
| `status` | Auswahl | ja | Status der Zuordnung |
| `rolle` | Auswahl | nein | Rolle der Lehrkraft bezogen auf den Schüler |
| `bemerkung` | Langer Text | nein | Bemerkung |

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

---

## 5.6 Tabelle: `unterrichtstermin`

### Zweck

Speichert regelmäßige Unterrichtstermine einer Lerngruppe.

Ein Unterrichtstermin beschreibt nicht eine einzelne Unterrichtsstunde, sondern einen wiederkehrenden Termin im Stundenplan.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `lerngruppe_id` | Verknüpfung | ja | Verweis auf `lerngruppe` |
| `wochentag` | Auswahl | ja | Wochentag |
| `stunde_von` | Zahl/Text | nein | Erste Schulstunde |
| `stunde_bis` | Zahl/Text | nein | Letzte Schulstunde |
| `beginn` | Uhrzeit | nein | Beginn |
| `ende` | Uhrzeit | nein | Ende |
| `raum` | Text | nein | Raum |
| `rhythmus` | Auswahl | nein | Wiederholungsrhythmus |
| `gueltig_ab` | Datum | nein | Beginn der Gültigkeit |
| `gueltig_bis` | Datum | nein | Ende der Gültigkeit |
| `aktiv` | Checkbox | ja | Termin ist aktiv |
| `bemerkung` | Langer Text | nein | Bemerkung |

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

### Hinweise

Aus `unterrichtstermin` können konkrete Einträge in `unterrichtsstunde` erzeugt werden.

Die Tabelle ermöglicht eine Stundenplan- oder Kalenderansicht.

---

## 5.7 Tabelle: `unterrichtsstunde`

### Zweck

Speichert konkrete Unterrichtsstunden.

Unterrichtsstunden bilden die Grundlage für Fehlzeiten, Beobachtungen und stundenbezogene Leistungen.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `lerngruppe_id` | Verknüpfung | ja | Verweis auf `lerngruppe` |
| `datum` | Datum | ja | Datum der Stunde |
| `stunde` | Text/Zahl | nein | Schulstunde oder Stundenblock |
| `beginn` | Uhrzeit | nein | Beginn |
| `ende` | Uhrzeit | nein | Ende |
| `thema` | Text | nein | Unterrichtsthema |
| `inhalt` | Langer Text | nein | Unterrichtsinhalt |
| `hausaufgabe` | Langer Text | nein | Hausaufgabe |
| `material` | Langer Text | nein | Genutztes Material |
| `bemerkung` | Langer Text | nein | Allgemeine Bemerkung |
| `erstellt_am` | Datum/Zeit | ja | Erstellungszeitpunkt |
| `geaendert_am` | Datum/Zeit | nein | Letzte Änderung |

---

## 5.8 Tabelle: `anwesenheit`

### Zweck

Speichert Anwesenheit, Fehlzeiten und Verspätungen pro Schüler und Unterrichtsstunde.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `schueler_id` | Verknüpfung | ja | Verweis auf `schueler` |
| `unterrichtsstunde_id` | Verknüpfung | ja | Verweis auf `unterrichtsstunde` |
| `lerngruppe_id` | Verknüpfung | ja | Verweis auf `lerngruppe` |
| `datum` | Datum | ja | Datum, redundant zur besseren Filterung |
| `status` | Auswahl | ja | Anwesenheitsstatus |
| `entschuldigungsstatus` | Auswahl | nein | Status der Entschuldigung |
| `minuten_verspaetet` | Zahl | nein | Minuten der Verspätung |
| `quelle` | Auswahl | nein | Herkunft der Information |
| `bemerkung` | Langer Text | nein | Bemerkung |

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

---

## 5.9 Tabelle: `leistungsnachweis`

### Zweck

Speichert bewertete Leistungssituationen.

Ein Leistungsnachweis beschreibt das Ereignis, nicht das individuelle Ergebnis.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `lerngruppe_id` | Verknüpfung | ja | Verweis auf `lerngruppe` |
| `fach_id` | Verknüpfung | nein | Verweis auf `fach` |
| `schuljahr_id` | Verknüpfung | ja | Verweis auf `schuljahr` |
| `titel` | Text | ja | Titel des Leistungsnachweises |
| `datum` | Datum | nein | Datum |
| `bewertungsart` | Auswahl | ja | Art der Bewertung |
| `maximalpunkte` | Zahl | nein | Maximal erreichbare Punkte |
| `gewichtung` | Zahl | nein | Gewichtung |
| `bemerkung` | Langer Text | nein | Bemerkung |

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

---

## 5.10 Tabelle: `leistungsbewertung`

### Zweck

Speichert das Ergebnis eines Schülers zu einem Leistungsnachweis.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `leistungsnachweis_id` | Verknüpfung | ja | Verweis auf `leistungsnachweis` |
| `schueler_id` | Verknüpfung | ja | Verweis auf `schueler` |
| `punkte` | Zahl | nein | Erreichte Punkte |
| `prozent` | Zahl | nein | Prozentwert |
| `note` | Text/Zahl | nein | Note |
| `notenpunkte` | Zahl | nein | Notenpunkte 0-15 |
| `tendenz` | Auswahl | nein | Notentendenz |
| `kommentar` | Langer Text | nein | Kommentar zur Leistung |
| `paedagogische_anpassung` | Checkbox | nein | Bewertung wurde pädagogisch angepasst |
| `begruendung_anpassung` | Langer Text | nein | Begründung der Anpassung |
| `dokument_id` | Verknüpfung | nein | Verweis auf `dokument` |
| `erstellt_am` | Datum/Zeit | ja | Erstellungszeitpunkt |
| `geaendert_am` | Datum/Zeit | nein | Letzte Änderung |

### Auswahlwerte für `tendenz`

- plus
- neutral
- minus

---

## 5.11 Tabelle: `kompetenz`

### Zweck

Speichert bewertbare Kompetenzen.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `fach_id` | Verknüpfung | nein | Verweis auf `fach` |
| `bereich` | Text | nein | Kompetenzbereich |
| `bezeichnung` | Text | ja | Kompetenzname |
| `beschreibung` | Langer Text | nein | Beschreibung der Kompetenz |
| `aktiv` | Checkbox | ja | Kompetenz ist aktiv |

### Beispiele

- Argumentieren
- Präsentieren
- Experiment planen
- Daten auswerten
- Modelle verwenden
- Fachsprache nutzen
- Diagramme auswerten

---

## 5.12 Tabelle: `kompetenzbewertung`

### Zweck

Speichert den Kompetenzstand eines Schülers zu einem Zeitpunkt.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `schueler_id` | Verknüpfung | ja | Verweis auf `schueler` |
| `kompetenz_id` | Verknüpfung | ja | Verweis auf `kompetenz` |
| `lerngruppe_id` | Verknüpfung | nein | Verweis auf `lerngruppe` |
| `unterrichtsstunde_id` | Verknüpfung | nein | Verweis auf `unterrichtsstunde` |
| `leistungsnachweis_id` | Verknüpfung | nein | Verweis auf `leistungsnachweis` |
| `datum` | Datum | ja | Datum der Bewertung |
| `bewertung` | Auswahl | ja | Kompetenzbewertung |
| `kommentar` | Langer Text | nein | Kommentar |
| `quelle` | Auswahl | nein | Herkunft der Bewertung |
| `erstellt_am` | Datum/Zeit | ja | Erstellungszeitpunkt |
| `geaendert_am` | Datum/Zeit | nein | Letzte Änderung |

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

---

## 5.13 Tabelle: `beobachtung`

### Zweck

Speichert pädagogische Beobachtungen, Notizen und Gesprächsnotizen.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `schueler_id` | Verknüpfung | ja | Verweis auf `schueler` |
| `lerngruppe_id` | Verknüpfung | nein | Verweis auf `lerngruppe` |
| `unterrichtsstunde_id` | Verknüpfung | nein | Verweis auf `unterrichtsstunde` |
| `datum` | Datum | ja | Datum der Beobachtung |
| `kategorie` | Auswahl | ja | Beobachtungskategorie |
| `titel` | Text | nein | Kurztitel |
| `inhalt` | Langer Text | ja | Beobachtungstext |
| `relevanz` | Auswahl | nein | Relevanz |
| `ki_generiert` | Checkbox | ja | Eintrag wurde durch KI erzeugt |
| `geprueft` | Checkbox | ja | Eintrag wurde durch Lehrkraft geprüft |
| `erstellt_am` | Datum/Zeit | ja | Erstellungszeitpunkt |
| `geaendert_am` | Datum/Zeit | nein | Letzte Änderung |

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

---

## 5.14 Tabelle: `dokument`

### Zweck

Speichert Metadaten zu Dateien.

Dateien können lokal oder in einem Cloudspeicher liegen.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `titel` | Text | ja | Dokumenttitel |
| `dokumenttyp` | Auswahl | ja | Art des Dokuments |
| `dateiname` | Text | nein | Dateiname |
| `cloud_link` | URL | nein | Link zu OneDrive, SharePoint, Nextcloud etc. |
| `speicherort` | Auswahl | nein | Speicherort |
| `dateiformat` | Text | nein | PDF, DOCX, XLSX usw. |
| `beschreibung` | Langer Text | nein | Beschreibung |
| `quelle` | Auswahl | nein | Herkunft |
| `hochgeladen_am` | Datum/Zeit | nein | Zeitpunkt des Hochladens |
| `ki_analysiert` | Checkbox | nein | Dokument wurde KI-analysiert |
| `analyse_status` | Auswahl | nein | Status der Analyse |

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

---

## 5.15 Tabelle: `dokument_schueler`

### Zweck

Verknüpft Dokumente mit Schülern.

Ein Dokument kann einem oder mehreren Schülern zugeordnet sein.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `dokument_id` | Verknüpfung | ja | Verweis auf `dokument` |
| `schueler_id` | Verknüpfung | ja | Verweis auf `schueler` |
| `bezugstyp` | Auswahl | nein | Art des Bezugs |
| `bemerkung` | Langer Text | nein | Bemerkung |

### Auswahlwerte für `bezugstyp`

- gehört zu Schüler
- betrifft Schüler
- wurde von Schüler erstellt
- Bewertung zu Schüler
- Gesprächsdokument
- sonstiger Bezug

---

## 5.16 Tabelle: `bericht`

### Zweck

Speichert manuelle oder KI-generierte Berichte.

### Felder

| Feldname | Typ | Pflicht | Beschreibung |
|---|---|---:|---|
| `id` | Automatische ID | ja | Interne eindeutige ID |
| `schueler_id` | Verknüpfung | ja | Verweis auf `schueler` |
| `lerngruppe_id` | Verknüpfung | nein | Verweis auf `lerngruppe` |
| `schuljahr_id` | Verknüpfung | nein | Verweis auf `schuljahr` |
| `berichtstyp` | Auswahl | ja | Art des Berichts |
| `titel` | Text | ja | Berichtstitel |
| `inhalt` | Langer Text | ja | Berichtstext |
| `status` | Auswahl | ja | Bearbeitungsstatus |
| `ki_generiert` | Checkbox | ja | Bericht wurde durch KI erstellt |
| `geprueft` | Checkbox | ja | Bericht wurde durch Lehrkraft geprüft |
| `erstellt_am` | Datum/Zeit | ja | Erstellungszeitpunkt |
| `geaendert_am` | Datum/Zeit | nein | Letzte Änderung |

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

---

# 6. Zentrale Beziehungen

## Schüler

Ein Schüler kann haben:

- mehrere Lerngruppenzuordnungen
- mehrere Anwesenheitseinträge
- mehrere Leistungsbewertungen
- mehrere Kompetenzbewertungen
- mehrere Beobachtungen
- mehrere Dokumentzuordnungen
- mehrere Berichte

---

## Lerngruppe

Eine Lerngruppe gehört zu:

- einem Schuljahr
- optional einem Fach

Eine Lerngruppe kann haben:

- mehrere Schüler
- mehrere Unterrichtstermine
- mehrere Unterrichtsstunden
- mehrere Leistungsnachweise
- mehrere Beobachtungen
- mehrere Kompetenzbewertungen

---

## Unterrichtstermin

Ein Unterrichtstermin gehört zu:

- einer Lerngruppe

Ein Unterrichtstermin kann genutzt werden, um:

- konkrete Unterrichtsstunden zu erzeugen
- eine Wochen- oder Terminübersicht darzustellen

---

## Unterrichtsstunde

Eine Unterrichtsstunde gehört zu:

- einer Lerngruppe

Eine Unterrichtsstunde kann haben:

- mehrere Anwesenheitseinträge
- mehrere Beobachtungen
- mehrere Kompetenzbewertungen

---

## Leistungsnachweis

Ein Leistungsnachweis gehört zu:

- einer Lerngruppe
- einem Schuljahr
- optional einem Fach

Ein Leistungsnachweis kann haben:

- mehrere Leistungsbewertungen

---

## Dokument

Ein Dokument kann verknüpft sein mit:

- einem Schüler
- mehreren Schülern
- einer Leistungsbewertung
- einem Bericht
- einer Beobachtung über Freitextverweis im MVP

---

# 7. Bewusst nicht im MVP enthalten

Die folgenden Bestandteile des Zielmodells werden zunächst nicht umgesetzt:

| Bestandteil | Grund |
|---|---|
| separate Adresstabelle | Für MVP reicht Freitext in `schueler` |
| separate Kontaktpersonentabelle | Für MVP reicht Freitext in `schueler` |
| Halbjahr-Tabelle | Kann später ergänzt werden |
| Kompetenzkataloge | Für MVP reicht Feld `bereich` in `kompetenz` |
| Kompetenzskalen | Für MVP reicht feste vierstufige Auswahl |
| Notenschlüssel | Noten können zunächst manuell eingetragen werden |
| externe Fachnoten | Spätere Erweiterung für Tutorrolle |
| Importvorgang | Erst relevant beim Bau des Importassistenten |
| Importdatensatz | Erst relevant beim Bau des Importassistenten |
| KI-Auftrag | Erst relevant bei strukturierter KI-Protokollierung |
| Pseudonymtabelle | Erst relevant bei externer KI-Nutzung |
| eigene Gesprächsprotokolltabelle | Zunächst über `beobachtung` abbildbar |
| Timeline-Tabelle | Timeline kann aus bestehenden Tabellen erzeugt werden |

---

# 8. MVP-Datenfluss

## 8.1 Schülerakte

```text
schueler
  ├── schueler_lerngruppe
  ├── anwesenheit
  ├── leistungsbewertung
  ├── kompetenzbewertung
  ├── beobachtung
  ├── dokument_schueler
  └── bericht
```

---

## 8.2 Unterricht

```text
lerngruppe
  ├── unterrichtstermin
  └── unterrichtsstunde
        ├── anwesenheit
        ├── beobachtung
        └── kompetenzbewertung
```

---

## 8.3 Leistungen

```text
leistungsnachweis
  └── leistungsbewertung
        ├── schueler
        └── dokument
```

---

## 8.4 Dokumente

```text
dokument
  └── dokument_schueler
        └── schueler
```

---

# 9. MVP-Testfragen

Das MVP-Datenmodell muss folgende Fragen beantworten können:

## Schülerakte

- Welche Lerngruppen besucht ein Schüler?
- Welche Beobachtungen liegen zu einem Schüler vor?
- Welche Dokumente sind einem Schüler zugeordnet?
- Welche Berichte wurden zu einem Schüler erstellt?

## Unterrichtstermine

- Welche Unterrichtstermine hat eine Lerngruppe im Wochenplan?
- Welche Unterrichtsstunden sind aus einem Unterrichtstermin entstanden oder geplant?

## Fehlzeiten

- Wie viele Unterrichtsstunden hat ein Schüler gefehlt?
- Wie viele Fehlzeiten waren unentschuldigt?
- In welcher Lerngruppe fehlen besonders viele Stunden?

## Leistungen

- Welche Leistungsnachweise wurden in einer Lerngruppe geschrieben?
- Welche Bewertung hat ein Schüler in einem Leistungsnachweis erhalten?
- Welche Noten liegen zu einem Schüler in einem Schuljahr vor?

## Kompetenzen

- Welche Kompetenzen wurden bei einem Schüler bewertet?
- Wie entwickelt sich eine Kompetenz über die Zeit?
- Welche Schüler haben bei einer Kompetenz noch Förderbedarf?

## KI-Berichte

- Welche Daten liegen als Grundlage für einen Lernentwicklungsbericht vor?
- Welche Beobachtungen sind für eine Elterngesprächsvorbereitung relevant?

---

# 10. Modellierungsentscheidungen

## MVP-DM-001 Schülerakte als Ansicht

Die Schülerakte wird aus mehreren Tabellen zusammengesetzt und nicht als eigene Tabelle gespeichert.

## MVP-DM-002 Schuljahr früh einführen

Schuljahre werden bereits im MVP eingeführt, weil Schüler über mehrere Jahre begleitet werden.

## MVP-DM-003 Lerngruppe statt nur Klasse

Das System arbeitet mit Lerngruppen, weil Fachunterricht, Kurse, Tutorengruppen und Klassenunterricht unterschiedlich organisiert sein können.

## MVP-DM-004 Unterrichtstermine getrennt von Unterrichtsstunden

Ein Unterrichtstermin beschreibt einen wiederkehrenden Stundenplantermin.

Eine Unterrichtsstunde beschreibt eine konkrete Stunde an einem konkreten Datum.

## MVP-DM-005 Fehlzeiten pro Unterrichtsstunde

Fehlzeiten werden auf Unterrichtsstunden bezogen, nicht nur auf ganze Tage.

## MVP-DM-006 Leistungen zweistufig modellieren

Ein Leistungsnachweis beschreibt die Aufgabe.

Eine Leistungsbewertung beschreibt das Ergebnis eines einzelnen Schülers.

## MVP-DM-007 Kontakte zunächst vereinfacht

Eltern- und Adressdaten werden im MVP als Freitext in der Schülertabelle gespeichert.

## MVP-DM-008 Kompetenzen zunächst vereinfacht

Kompetenzen werden im MVP mit einer festen vierstufigen Skala bewertet.

## MVP-DM-009 Dokumente als Links

Dokumente werden im MVP primär über Cloud-Links oder Dateipfade referenziert.

## MVP-DM-010 KI vorbereitet, aber nicht vollständig modelliert

Berichte und KI-generierte Inhalte sind bereits vorbereitet.

Importassistent, KI-Aufträge und Pseudonymisierung werden später ergänzt.

---

# 11. Nächster Schritt

Aus diesem MVP-Datenmodell wird im nächsten Schritt eine konkrete NocoDB-Struktur abgeleitet.

Dazu werden für jede Tabelle festgelegt:

- Tabellenname
- Feldname
- Feldtyp in NocoDB
- Pflichtfeld
- Auswahloptionen
- Verknüpfungen
- sinnvolle Standardansichten
