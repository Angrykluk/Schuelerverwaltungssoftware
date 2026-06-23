# Datenmodell

**Version:** 0.2  
**Status:** Entwurf  
**Letzte Änderung:** 2026-06-23

---

## 1. Grundidee

Das Teacher Intelligence System (TIS) basiert auf einer digitalen Schülerakte.

Die Schülerakte ist keine einzelne Tabelle, sondern eine zusammengeführte Ansicht auf alle Daten, die zu einem Schüler gespeichert sind.

Zur Schülerakte gehören:

- Stammdaten
- Kontakt- und Erziehungsberechtigtendaten
- Schuljahreszuordnungen
- Lerngruppen
- Fächer
- Unterrichtsstunden
- Fehlzeiten
- Leistungen
- Noten
- Kompetenzen
- Beobachtungen
- Dokumente
- Berichte
- Importvorgänge
- KI-Auswertungen

Der Schüler ist das zentrale Objekt des Datenmodells.

---

# 2. Zentrale Entitäten

## 2.1 Schüler

Repräsentiert eine einzelne lernende Person.

### Zweck

Speichert die stabilen Stammdaten eines Schülers.

### Felder

- Schüler-ID
- Externe ID
- WebUntis-ID
- Vorname
- Nachname
- Rufname
- Geschlecht
- Geburtsdatum
- Schülerstatus
- Bemerkung
- Aktiv
- Archiviert
- Erstellt am
- Geändert am

### Hinweise

Die Schüler-ID ist die interne technische Identifikation.

Die externe ID dient der Zuordnung zu Importen aus WebUntis oder anderen Systemen.

---

## 2.2 Schülerakte

Die Schülerakte ist eine Ansicht und keine eigene Haupttabelle.

### Zweck

Bündelt alle Daten eines Schülers.

### Enthaltene Bereiche

- Stammdaten
- Kontakte
- Lerngruppen
- Fehlzeiten
- Leistungen
- Kompetenzen
- Beobachtungen
- Dokumente
- Berichte
- Timeline

---

## 2.3 Adresse

Speichert Adressdaten eines Schülers.

### Felder

- Adresse-ID
- Schüler-ID
- Straße
- Hausnummer
- PLZ
- Ort
- Land
- Adresstyp
- Gültig ab
- Gültig bis
- Bemerkung

### Adresstypen

- Hauptadresse
- Nebenadresse
- getrennte Elternadresse
- sonstige Adresse

---

## 2.4 Erziehungsberechtigte / Kontaktpersonen

Speichert Eltern, Sorgeberechtigte oder weitere Kontaktpersonen.

### Felder

- Kontakt-ID
- Schüler-ID
- Vorname
- Nachname
- Beziehung zum Schüler
- E-Mail
- Telefon
- Mobiltelefon
- Adresse-ID
- Sorgeberechtigt
- Notfallkontakt
- Darf kontaktiert werden
- Bemerkung

### Beispiele Beziehung zum Schüler

- Mutter
- Vater
- Sorgeberechtigte Person
- Pflegeperson
- sonstiger Kontakt

---

# 3. Schulische Organisation

## 3.1 Schuljahr

Repräsentiert ein Schuljahr.

### Felder

- Schuljahr-ID
- Bezeichnung
- Startdatum
- Enddatum
- Aktiv

### Beispiele

- 2025/2026
- 2026/2027

---

## 3.2 Halbjahr

Repräsentiert ein Halbjahr innerhalb eines Schuljahres.

### Felder

- Halbjahr-ID
- Schuljahr-ID
- Bezeichnung
- Startdatum
- Enddatum

### Beispiele

- 1. Halbjahr
- 2. Halbjahr

---

## 3.3 Fach

Repräsentiert ein Unterrichtsfach.

### Felder

- Fach-ID
- Bezeichnung
- Kürzel
- Fachbereich
- Aktiv

### Beispiele

- Physik
- Chemie
- Informatik
- Naturwissenschaften

---

## 3.4 Klasse

Repräsentiert eine organisatorische Klasse.

### Felder

- Klasse-ID
- Bezeichnung
- Jahrgang
- Schuljahr-ID
- Klassenleitung
- Bemerkung
- Aktiv
- Archiviert

### Beispiele

- 6.5
- 10c
- 12gA

---

## 3.5 Lerngruppe

Repräsentiert eine konkrete Unterrichtsgruppe einer Lehrkraft.

### Felder

- Lerngruppe-ID
- Bezeichnung
- Schuljahr-ID
- Halbjahr-ID
- Klasse-ID
- Fach-ID
- Kursart
- Niveau
- Wochenstunden
- Aktiv
- Archiviert
- Bemerkung

### Beispiele Kursart

- Klassenunterricht
- Grundkurs
- Leistungskurs
- Wahlpflichtkurs
- AG
- Tutorengruppe

### Beispiele Niveau

- G-Niveau
- E-Niveau
- grundlegend
- erhöht

---

## 3.6 Schüler-Lerngruppe

Verknüpft Schüler mit Lerngruppen.

### Zweck

Ein Schüler kann in mehreren Lerngruppen sein.

Eine Lerngruppe enthält viele Schüler.

### Felder

- Schüler-Lerngruppe-ID
- Schüler-ID
- Lerngruppe-ID
- Eintrittsdatum
- Austrittsdatum
- Status
- Bemerkung

### Status

- aktiv
- gewechselt
- ausgeschieden
- archiviert

---

## 3.7 Tutorenzuordnung

Dokumentiert, ob die Lehrkraft für einen Schüler eine Tutor-, Klassenleitungs- oder Beratungsfunktion hat.

### Felder

- Tutorenzuordnung-ID
- Schüler-ID
- Schuljahr-ID
- Rolle
- Zuständig ab
- Zuständig bis
- Bemerkung

### Rollen

- Tutor
- Klassenleitung
- Fachlehrkraft
- Beratungslehrkraft
- sonstige Rolle

---

# 4. Unterricht und Anwesenheit

## 4.1 Unterrichtsstunde

Repräsentiert eine konkrete Unterrichtsstunde.

### Felder

- Unterrichtsstunde-ID
- Lerngruppe-ID
- Datum
- Stunde
- Beginn
- Ende
- Thema
- Inhalt
- Hausaufgabe
- Material
- Bemerkung
- Erstellt am
- Geändert am

### Hinweise

Unterrichtsstunden sind wichtig, weil Leistungen, Beobachtungen und Fehlzeiten häufig auf eine konkrete Stunde bezogen sind.

---

## 4.2 Anwesenheit / Fehlzeit

Dokumentiert den Anwesenheitsstatus eines Schülers in einer Unterrichtsstunde.

### Felder

- Anwesenheit-ID
- Schüler-ID
- Unterrichtsstunde-ID
- Lerngruppe-ID
- Datum
- Stunde
- Status
- Entschuldigungsstatus
- Minuten verspätet
- Bemerkung
- Quelle
- Importvorgang-ID

### Status

- anwesend
- fehlend
- verspätet
- teilweise anwesend
- beurlaubt
- schulische Veranstaltung
- unbekannt

### Entschuldigungsstatus

- nicht erforderlich
- offen
- entschuldigt
- unentschuldigt
- nachgereicht
- strittig

### Quelle

- manuell
- WebUntis
- KI-Import
- sonstiger Import

---

# 5. Leistungen und Noten

## 5.1 Leistungsnachweis

Beschreibt eine bewertete Leistung oder Prüfung.

### Zweck

Ein Leistungsnachweis ist das Ereignis, z. B. eine Klassenarbeit oder Präsentation.

### Felder

- Leistungsnachweis-ID
- Lerngruppe-ID
- Fach-ID
- Schuljahr-ID
- Halbjahr-ID
- Titel
- Datum
- Bewertungsart
- Maximalpunkte
- Gewichtung
- Notenschlüssel-ID
- Bemerkung

### Bewertungsarten

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

## 5.2 Leistungsbewertung

Speichert das Ergebnis eines Schülers zu einem Leistungsnachweis.

### Felder

- Leistungsbewertung-ID
- Leistungsnachweis-ID
- Schüler-ID
- Punkte
- Prozent
- Note
- Notenpunkte
- Tendenz
- Kommentar
- Pädagogische Anpassung
- Begründung Anpassung
- Dokument-ID
- Erstellt am
- Geändert am

### Hinweise

Die Bewertung wird vom Leistungsnachweis getrennt.

Dadurch kann eine Klassenarbeit einmal angelegt und dann für alle Schüler bewertet werden.

---

## 5.3 Externe Fachnote

Speichert Noten aus anderen Fächern, wenn die Lehrkraft als Tutor oder Klassenleitung einen Gesamtüberblick führen möchte.

### Felder

- Externe-Fachnote-ID
- Schüler-ID
- Schuljahr-ID
- Halbjahr-ID
- Fach-ID
- Note
- Notenpunkte
- Quelle
- Bemerkung
- Erfasst am

### Beispiele Quelle

- Zeugnis
- Gespräch mit Fachlehrkraft
- Konferenz
- Import
- manuell

---

## 5.4 Notenschlüssel

Beschreibt die Umrechnung von Punkten oder Prozentwerten in Noten.

### Felder

- Notenschlüssel-ID
- Bezeichnung
- Skalentyp
- Maximalpunkte
- Beschreibung
- Aktiv

### Skalentypen

- Note 1-6
- Notenpunkte 0-15
- Prozent
- bestanden/nicht bestanden
- eigene Skala

---

# 6. Kompetenzen

## 6.1 Kompetenzkatalog

Gruppiert Kompetenzen.

### Felder

- Kompetenzkatalog-ID
- Bezeichnung
- Fach-ID
- Schuljahr-ID
- Beschreibung
- Aktiv

### Beispiele

- Kommunikation
- Erkenntnisgewinnung
- Bewertung
- Fachwissen

---

## 6.2 Kompetenz

Beschreibt eine bewertbare Kompetenz.

### Felder

- Kompetenz-ID
- Kompetenzkatalog-ID
- Fach-ID
- Bezeichnung
- Beschreibung
- Reihenfolge
- Aktiv

### Beispiele

- Argumentieren
- Präsentieren
- Experimentieren
- Daten auswerten
- Modelle verwenden

---

## 6.3 Kompetenzskala

Beschreibt ein Bewertungsmodell für Kompetenzen.

### Felder

- Kompetenzskala-ID
- Bezeichnung
- Beschreibung
- Aktiv

### Beispiele

- Vierstufige Gesamtschul-Skala
- Noten
- Notenpunkte
- Prozent
- Freitext

---

## 6.4 Kompetenzstufe

Beschreibt eine Stufe innerhalb einer Kompetenzskala.

### Felder

- Kompetenzstufe-ID
- Kompetenzskala-ID
- Bezeichnung
- Wert
- Reihenfolge
- Beschreibung

### Beispiel Vierstufige Gesamtschul-Skala

1. Trifft noch nicht zu
2. Trifft teilweise zu
3. Trifft fast zu
4. Trifft zu

---

## 6.5 Kompetenzbewertung

Speichert eine Kompetenzbewertung für einen Schüler.

### Felder

- Kompetenzbewertung-ID
- Schüler-ID
- Kompetenz-ID
- Kompetenzstufe-ID
- Lerngruppe-ID
- Unterrichtsstunde-ID
- Leistungsnachweis-ID
- Datum
- Kommentar
- Quelle
- Erstellt am
- Geändert am

### Quelle

- manuell
- Leistungsbewertung
- Beobachtung
- KI-Vorschlag
- Import

---

# 7. Beobachtungen und Berichte

## 7.1 Beobachtung

Speichert eine pädagogische Beobachtung zu einem Schüler.

### Felder

- Beobachtung-ID
- Schüler-ID
- Lerngruppe-ID
- Unterrichtsstunde-ID
- Datum
- Kategorie
- Titel
- Inhalt
- Sichtbarkeit
- Relevanz
- KI-generiert
- Geprüft durch Lehrkraft
- Erstellt am
- Geändert am

### Kategorien

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

---

## 7.2 Gesprächsprotokoll

Speichert strukturierte Gesprächsnotizen.

### Felder

- Gesprächsprotokoll-ID
- Schüler-ID
- Datum
- Gesprächsart
- Beteiligte
- Anlass
- Inhalt
- Vereinbarungen
- Wiedervorlage
- Dokument-ID
- Erstellt am
- Geändert am

### Gesprächsarten

- Elterngespräch
- Schülergespräch
- Beratungsgespräch
- Fördergespräch
- Klassenkonferenz
- sonstiges Gespräch

---

## 7.3 Bericht

Speichert erzeugte Berichte.

### Felder

- Bericht-ID
- Schüler-ID
- Lerngruppe-ID
- Schuljahr-ID
- Halbjahr-ID
- Berichtstyp
- Titel
- Inhalt
- Status
- KI-generiert
- Geprüft durch Lehrkraft
- Erstellt am
- Geändert am

### Berichtstypen

- Lernentwicklungsbericht
- Elterngesprächsvorbereitung
- Förderempfehlung
- Schülerzusammenfassung
- Klassenkonferenznotiz
- Zeugnistextentwurf

### Status

- Entwurf
- geprüft
- final
- archiviert

---

# 8. Dokumente

## 8.1 Dokument

Speichert Metadaten zu Dateien.

### Felder

- Dokument-ID
- Titel
- Dokumenttyp
- Dateiname
- Dateipfad
- Cloud-Link
- Speicherort
- Dateiformat
- Hochgeladen am
- Quelle
- Beschreibung
- KI-analysiert
- Analyse-Status

### Dokumenttypen

- Klassenarbeit
- Präsentation
- Bewertungsbogen
- Förderplan
- Gesprächsprotokoll
- Elternbrief
- Schülerarbeit
- sonstiges Dokument

### Speicherorte

- lokal
- OneDrive
- SharePoint
- Nextcloud
- Datenbank
- anderer Speicher

---

## 8.2 Dokument-Schüler-Zuordnung

Verknüpft Dokumente mit Schülern.

### Zweck

Ein Dokument kann einem oder mehreren Schülern zugeordnet werden.

### Felder

- Dokument-Schüler-ID
- Dokument-ID
- Schüler-ID
- Bezugstyp
- Bemerkung

### Bezugstyp

- gehört zu Schüler
- betrifft Schüler
- wurde von Schüler erstellt
- Bewertung zu Schüler
- Gesprächsdokument
- sonstiger Bezug

---

## 8.3 Dokument-Lerngruppe-Zuordnung

Verknüpft Dokumente mit Lerngruppen.

### Felder

- Dokument-Lerngruppe-ID
- Dokument-ID
- Lerngruppe-ID
- Bezugstyp
- Bemerkung

---

# 9. Import und KI-Verarbeitung

## 9.1 Importvorgang

Dokumentiert einen Import.

### Felder

- Importvorgang-ID
- Datum
- Quelle
- Importtyp
- Datei-ID
- Status
- Anzahl erkannter Datensätze
- Anzahl importierter Datensätze
- Anzahl Fehler
- Anzahl Warnungen
- Protokoll
- Erstellt am

### Quellen

- WebUntis
- IServ
- Schulmanager
- Excel
- CSV
- PDF
- KI-Import
- manuell

### Importtypen

- Schülerliste
- Fehlzeiten
- Noten
- Kompetenzen
- Dokumente
- Beobachtungen
- gemischter Import

---

## 9.2 Importdatensatz

Speichert erkannte Einträge aus einem Import vor oder nach der Übernahme.

### Felder

- Importdatensatz-ID
- Importvorgang-ID
- Erkannter Schüler
- Vorgeschlagene Schüler-ID
- Datentyp
- Erkannte Daten
- Vertrauenswert
- Status
- Fehlerhinweis
- Übernommen am

### Status

- erkannt
- vorgeschlagen
- bestätigt
- korrigiert
- übernommen
- abgelehnt
- Fehler

---

## 9.3 KI-Auftrag

Dokumentiert KI-Verarbeitungen.

### Felder

- KI-Auftrag-ID
- Auftragstyp
- Datum
- Status
- Eingabedaten
- Ausgabedaten
- Modell
- Datenschutzmodus
- Pseudonymisiert
- Geprüft durch Lehrkraft
- Fehlerhinweis

### Auftragstypen

- Schülerzusammenfassung
- Lernentwicklungsbericht
- Elterngesprächsvorbereitung
- Importanalyse
- Dokumentenanalyse
- Beobachtungsstrukturierung
- Kompetenzvorschlag

---

## 9.4 Pseudonym

Speichert interne Pseudonyme für KI-Verarbeitung.

### Felder

- Pseudonym-ID
- Schüler-ID
- Pseudonym
- Gültig ab
- Gültig bis
- Zweck
- Aktiv

### Beispiel

- Schüler-ID: 184
- Pseudonym: Student_A12

---

# 10. Timeline

## 10.1 Timeline-Eintrag

Die Timeline ist eine zusammengeführte Ansicht.

Sie kann aus folgenden Objekten gespeist werden:

- Fehlzeit
- Leistungsbewertung
- Kompetenzbewertung
- Beobachtung
- Gesprächsprotokoll
- Dokument
- Bericht
- KI-Auftrag
- Importvorgang

### Felder für die Ansicht

- Datum
- Schüler-ID
- Typ
- Titel
- Kurzbeschreibung
- Quelle
- Link zum Originaldatensatz

### Hinweis

Die Timeline muss nicht zwingend als eigene Tabelle gespeichert werden.

Sie kann aus vorhandenen Tabellen generiert werden.

---

# 11. Beziehungen

## Schüler

Ein Schüler hat:

- eine oder mehrere Adressen
- eine oder mehrere Kontaktpersonen
- eine oder mehrere Lerngruppen
- eine oder mehrere Anwesenheitseinträge
- eine oder mehrere Leistungsbewertungen
- eine oder mehrere Kompetenzbewertungen
- eine oder mehrere Beobachtungen
- eine oder mehrere Gesprächsprotokolle
- eine oder mehrere Dokumentzuordnungen
- eine oder mehrere Berichte
- eine oder mehrere KI-Verarbeitungen

---

## Schuljahr

Ein Schuljahr hat:

- mehrere Halbjahre
- mehrere Klassen
- mehrere Lerngruppen
- mehrere Leistungsnachweise
- mehrere Berichte

---

## Lerngruppe

Eine Lerngruppe hat:

- ein Fach
- ein Schuljahr
- optional ein Halbjahr
- viele Schüler
- viele Unterrichtsstunden
- viele Leistungsnachweise
- viele Beobachtungen
- viele Kompetenzbewertungen

---

## Unterrichtsstunde

Eine Unterrichtsstunde hat:

- eine Lerngruppe
- viele Anwesenheitseinträge
- viele Beobachtungen
- optional Kompetenzbewertungen

---

## Leistungsnachweis

Ein Leistungsnachweis hat:

- eine Lerngruppe
- ein Fach
- ein Schuljahr
- viele Leistungsbewertungen
- optional einen Notenschlüssel
- optional Dokumente

---

## Dokument

Ein Dokument kann verknüpft sein mit:

- einem Schüler
- mehreren Schülern
- einer Lerngruppe
- einem Leistungsnachweis
- einem Gesprächsprotokoll
- einem Bericht

---

# 12. Noch zu klärende Felder

Folgende Datenfelder sind fachlich wahrscheinlich relevant, müssen aber noch geprüft werden:

## Schülerbezogene Felder

- Religionszugehörigkeit
- Herkunftssprache
- Förderstatus
- Nachteilsausgleich
- sonderpädagogischer Unterstützungsbedarf
- medizinische Hinweise
- Allergien
- Abholberechtigungen

Diese Felder sind besonders sensibel und dürfen nur aufgenommen werden, wenn sie für den pädagogischen Zweck erforderlich sind.

---

## Leistungsbezogene Felder

- Gewichtung mündlich/schriftlich
- Quartalsnoten
- Zeugnisnoten
- Prognosen
- Mitarbeit pro Stunde
- Hausaufgabenstatus
- Materialstatus

---

## Organisationsfelder

- Sitzplatz
- Arbeitsgruppe
- Projektgruppe
- Wahlpflichtbereich
- Tutorengruppe
- Kurswechsel

---

# 13. Modellierungsentscheidungen

## DM-001 Schülerakte als Aggregat

Die Schülerakte wird nicht als einzelne Tabelle modelliert.

Sie wird aus mehreren verknüpften Tabellen zusammengesetzt.

## DM-002 Anwesenheit pro Unterrichtsstunde

Fehlzeiten werden nicht nur als Tageswert gespeichert.

Sie werden nach Möglichkeit auf konkrete Unterrichtsstunden bezogen.

## DM-003 Leistungen getrennt von Leistungsnachweisen

Ein Leistungsnachweis beschreibt die Aufgabe.

Eine Leistungsbewertung beschreibt das Ergebnis eines Schülers.

## DM-004 Schuljahre als eigene Entität

Alle relevanten schulischen Daten werden einem Schuljahr zugeordnet.

## DM-005 Kontakte getrennt vom Schüler

Eltern- und Kontaktdaten werden nicht direkt in der Schülertabelle gespeichert.

Sie werden als eigene Kontaktpersonen modelliert.

## DM-006 Pseudonymisierung vorbereitet

Das Datenmodell unterstützt pseudonymisierte KI-Verarbeitung.

## DM-007 Cloud-Dokumente als Referenzen

Dokumente müssen nicht in der Datenbank gespeichert werden.

Die Datenbank kann stattdessen auf externe Speicherorte verweisen.
