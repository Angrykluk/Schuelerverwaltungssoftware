# Teacher Intelligence System (TIS)

**Version:** 0.3 
**Status:** Entwurf  
**Letzte Änderung:** 2026-06-23

---

## 1. Projektziel

Entwicklung eines persönlichen, KI-gestützten Systems zur Verwaltung eigener Lerngruppen.

Das System soll Lehrkräfte bei Dokumentation, Leistungsbewertung, Lernentwicklung, Schüleraktenführung und Berichtserstellung unterstützen.

Das System ist zunächst für einzelne Lehrkräfte konzipiert und nicht als vollständige Schulverwaltungssoftware für eine ganze Schule.

---

## 2. Zielgruppe

Primäre Zielgruppe:

- einzelne Lehrkraft

Spätere mögliche Zielgruppe:

- kleines Lehrkräfteteam
- Fachteam
- Jahrgangsteam

---

## 3. Leitprinzipien

- einfache Bedienung
- geringe technische Einstiegshürde
- lokale oder DSGVO-konforme Datenverarbeitung
- KI als Assistenzsystem, nicht als alleinige Entscheidungsinstanz
- vollständige Datenhoheit der Lehrkraft
- exportierbare Daten
- strukturierte Dokumentation statt verstreuter Notizen

---

# 4. Benutzerrollen

## Rolle: Lehrkraft

Die Lehrkraft kann:

- Schüler verwalten
- Klassen und Lerngruppen verwalten
- Fehlzeiten erfassen
- Kompetenzen bewerten
- Noten verwalten
- Dokumente hochladen
- Beobachtungen dokumentieren
- Unterrichtsstunden dokumentieren
- KI-Abfragen durchführen
- Berichte erzeugen
- Daten exportieren

---

# 5. Muss-Anforderungen

## Bereich A: Stammdaten und Organisation

### REQ-001 Schülerverwaltung

Schüler können einzeln angelegt, bearbeitet, deaktiviert und archiviert werden.

### REQ-002 Schülerimport

Schülerlisten können importiert werden.

Mögliche Formate:

- CSV
- Excel
- kopierte Tabellen aus WebUntis oder anderen Systemen

### REQ-003 Klassen- und Lerngruppenverwaltung

Klassen und Lerngruppen können angelegt und verwaltet werden.

### REQ-004 Schuljahre

Das System verwaltet mehrere Schuljahre.

Beispiele:

- 2025/2026
- 2026/2027

### REQ-005 Halbjahre

Daten können Halbjahren zugeordnet werden.

Beispiele:

- 1. Halbjahr
- 2. Halbjahr

### REQ-006 Fachzuordnung

Eine Lerngruppe besitzt ein Fach.

Beispiele:

- Physik
- Chemie
- Informatik
- Naturwissenschaften

### REQ-007 Mehrere Lerngruppen pro Schüler

Ein Schüler kann mehreren Lerngruppen zugeordnet werden.

### REQ-008 Archivierung

Abgeschlossene Lerngruppen und Schülerdaten werden archiviert und nicht direkt gelöscht.

---

## Bereich B: Schülerakte

### REQ-009 Digitale Schülerakte

Jeder Schüler besitzt eine digitale Akte.

Die Schülerakte bündelt:

- Stammdaten
- Lerngruppen
- Fehlzeiten
- Noten
- Kompetenzen
- Beobachtungen
- Dokumente
- Berichte

### REQ-010 Schülerfoto

Optional kann ein Schülerfoto hinterlegt werden.

### REQ-011 Individuelle Merkmale

Zu Schülern können individuelle Merkmale gespeichert werden.

Beispiele:

- Nachteilsausgleich
- Förderbedarf
- besondere Begabung
- organisatorische Hinweise

### REQ-012 Gesprächsprotokolle

Gesprächsprotokolle können einem Schüler zugeordnet werden.

Beispiele:

- Elterngespräch
- Beratungsgespräch
- Fördergespräch
- Klassenkonferenznotiz

### REQ-013 Chronologische Schüler-Timeline

Alle relevanten Einträge eines Schülers werden chronologisch angezeigt.

Beispiele:

- Fehlzeit
- Beobachtung
- Klassenarbeit
- Kompetenzbewertung
- Gesprächsprotokoll
- Dokument
- Bericht

---

## Bereich C: Fehlzeiten

### REQ-014 Fehlzeiten erfassen

Fehlzeiten können manuell erfasst werden.

### REQ-015 WebUntis-Import

Fehlzeiten sollen aus WebUntis übernommen werden können.

### REQ-016 Fehlzeitentypen

Fehlzeiten besitzen einen Typ.

Beispiele:

- entschuldigt
- unentschuldigt
- Krankheit
- Beurlaubung
- Verspätung
- schulische Veranstaltung

### REQ-017 Fehlzeitenstatistik

Das System berechnet Fehlzeitenstatistiken.

Beispiele:

- Fehltage
- Fehlstunden
- unentschuldigte Fehlzeiten
- Verspätungen

### REQ-018 Importhistorie

WebUntis-Importe werden protokolliert.

Gespeichert werden sollen:

- Importdatum
- Quelle
- importierte Datensätze
- erkannte Konflikte
- übersprungene Datensätze

---

## Bereich D: Noten und Leistungsbewertung

### REQ-019 Notenverwaltung

Noten und Notenpunkte können gespeichert werden.

### REQ-020 Bewertungsarten

Bewertungen können unterschiedlichen Arten zugeordnet werden.

Beispiele:

- Klassenarbeit
- Test
- Präsentation
- Experiment
- Mitarbeit
- Projekt
- mündliche Leistung

### REQ-021 Gewichtung

Bewertungen können gewichtet werden.

### REQ-022 Notenschlüssel

Punkte können über einen Notenschlüssel in Noten oder Notenpunkte umgerechnet werden.

### REQ-023 Notenvorschlag

Das System kann aus vorhandenen Bewertungen einen Notenvorschlag berechnen.

### REQ-024 Pädagogische Anpassung

Die Lehrkraft kann einen berechneten Notenvorschlag überschreiben.

Die Abweichung kann begründet dokumentiert werden.

---

## Bereich E: Kompetenzen

### REQ-025 Kompetenzraster

Kompetenzen können frei definiert werden.

### REQ-026 Kompetenzkataloge

Kompetenzen können in Katalogen oder Bereichen organisiert werden.

Beispiel:

- Kommunikation
  - Präsentieren
  - Argumentieren
- Erkenntnisgewinnung
  - Experimentieren
  - Auswerten

### REQ-027 Fachspezifische Kompetenzen

Kompetenzen können einem Fach zugeordnet werden.

### REQ-028 Kompetenzbewertung

Kompetenzen können für einzelne Schüler bewertet werden.

### REQ-029 Vierstufige Kompetenzskala

Das System unterstützt die vierstufige Gesamtschul-Skala:

- Trifft noch nicht zu
- Trifft teilweise zu
- Trifft fast zu
- Trifft zu

### REQ-030 Weitere Bewertungsmodelle

Neben der vierstufigen Skala sollen weitere Modelle möglich sein.

Beispiele:

- Noten
- Notenpunkte
- Prozentwerte
- Freitext
- bestanden/nicht bestanden

### REQ-031 Kompetenzentwicklung

Die Entwicklung einzelner Kompetenzen wird über die Zeit nachvollziehbar gespeichert.

### REQ-032 Kompetenzübersicht

Das System zeigt eine Übersicht über die Kompetenzstände eines Schülers oder einer Lerngruppe.

---

## Bereich F: Unterrichtsdokumentation

### REQ-033 Unterrichtsstunden

Unterrichtsstunden können dokumentiert werden.

### REQ-034 Unterrichtsthema

Zu jeder Unterrichtsstunde kann ein Thema gespeichert werden.

### REQ-035 Unterrichtsnotizen

Zu jeder Unterrichtsstunde können Notizen gespeichert werden.

### REQ-036 Hausaufgaben

Hausaufgaben können dokumentiert werden.

### REQ-037 Organisatorische Vorfälle

Organisatorische Vorfälle können dokumentiert werden.

Beispiele:

- Material vergessen
- Hausaufgaben vergessen
- Störung
- besondere Mitarbeit
- Präsentation gehalten

### REQ-038 Schülerbezogene Unterrichtsbeobachtungen

Während oder nach einer Unterrichtsstunde können Beobachtungen einzelnen Schülern zugeordnet werden.

---

## Bereich G: Dokumente

### REQ-039 Dokumentenablage

Dateien können hochgeladen und Schülern zugeordnet werden.

### REQ-040 Dokumententypen

Dokumente können typisiert werden.

Beispiele:

- Klassenarbeit
- Präsentation
- Bewertungsbogen
- Förderplan
- Gesprächsprotokoll
- sonstiges Dokument

### REQ-041 Mehrfachzuordnung

Ein Dokument kann mehreren Schülern zugeordnet werden.

### REQ-042 Dokumentenanalyse per KI

Hochgeladene Dokumente können durch KI analysiert werden.

Mögliche Ergebnisse:

- Zusammenfassung
- erkannte Bewertung
- erkannte Kompetenzen
- Hinweise für die Schülerakte

---

## Bereich H: KI-Funktionen

### REQ-043 KI-Abfragen über Schülerdaten

Die KI kann Fragen zu gespeicherten Schülerdaten beantworten.

Beispiel:

> Wie viele Tage hat Felix Schröder im Schuljahr gefehlt?

### REQ-044 Schülerzusammenfassung

Die KI kann eine sachliche Zusammenfassung zu einem Schüler erzeugen.

Beispiel:

> Was weißt du über Felix Schröder?

### REQ-045 Klassenübersicht

Die KI kann Übersichten über eine Lerngruppe erstellen.

Beispiele:

- Welche Schüler sind aktuell auffällig?
- Wer hat viele Fehlzeiten?
- Wer zeigt positive Entwicklung?

### REQ-046 Lernentwicklungsbericht

Die KI kann auf Basis vorhandener Daten einen Lernentwicklungsbericht erzeugen.

Verwendete Daten:

- Kompetenzen
- Noten
- Fehlzeiten
- Beobachtungen
- Dokumente
- Unterrichtsnotizen

### REQ-047 Elterngesprächsvorbereitung

Die KI kann eine Gesprächsvorbereitung für Elterngespräche erzeugen.

### REQ-048 Förderempfehlungen

Die KI kann Förderempfehlungen vorschlagen.

Die Entscheidung liegt immer bei der Lehrkraft.

### REQ-049 Beobachtungsassistent

Die KI kann aus Stichpunkten strukturierte Beobachtungseinträge erzeugen.

### REQ-050 Importassistent

Die KI kann beim Import unstrukturierter Schülerlisten unterstützen.

Beispiele:

- Spalten erkennen
- Namen trennen
- Lerngruppen zuordnen
- Dubletten erkennen

---

## Bereich I: Datenschutz, Sicherheit und Betrieb

### REQ-051 DSGVO-konforme Datenverarbeitung

Personenbezogene Daten müssen DSGVO-konform verarbeitet werden.

### REQ-052 Lokale KI bevorzugt

KI-Funktionen sollen bevorzugt lokal ausgeführt werden.

### REQ-053 Keine ungeprüfte Cloudübertragung

Schülerdaten dürfen nicht ohne bewusste Freigabe an externe KI-Dienste übertragen werden.

### REQ-054 Rollenmodell

Das System soll perspektivisch ein Rollenmodell unterstützen.

Beispiele:

- Lehrkraft
- Administrator
- Leserechte
- Schreibrechte

### REQ-055 Löschkonzept

Das System benötigt ein Lösch- und Archivierungskonzept.

### REQ-056 Export

Alle relevanten Daten müssen exportierbar sein.

### REQ-057 Backup

Das System soll regelmäßige Backups unterstützen.

### REQ-058 Protokollierung

Wichtige Aktionen werden protokolliert.

Beispiele:

- Import
- Export
- Löschung
- KI-Bericht erzeugt
- Dokument hochgeladen

## Bereich J: KI-gestützte Datenerfassung

### REQ-059 Cloudspeicher-Integration

Das System kann Dokumente in Cloudspeichern ablegen oder referenzieren.

Beispiele:

- OneDrive
- Nextcloud
- SharePoint
- lokale Netzlaufwerke
- SMB-Freigaben

---

### REQ-060 Zentrale Dokumentenablage

Dokumente müssen nicht zwingend in der Datenbank gespeichert werden.

Stattdessen können Referenzen auf externe Dateien gespeichert werden.

Beispiel:

- OneDrive-Link
- SharePoint-Datei
- Nextcloud-Datei

---

### REQ-061 Dokumentensynchronisation

Änderungen an verknüpften Dokumenten sollen erkannt werden.

Das System aktualisiert Metadaten und Verknüpfungen automatisch.

---

### REQ-062 KI-Importassistent

Der Benutzer kann Dateien hochladen.

Unterstützte Formate (mindestens perspektivisch):

- PDF
- CSV
- XLSX
- DOCX
- ODS
- HTML
- TXT

Die KI analysiert die Datei und erkennt automatisch relevante Informationen.

---

### REQ-063 Importvorschau

Vor dem Speichern zeigt das System die erkannten Datensätze an.

Der Benutzer entscheidet über die Übernahme.

Beispiel:

- Schüler erkannt
- Fehlzeiten erkannt
- Noten erkannt
- Kompetenzen erkannt

---

### REQ-064 Dublettenerkennung

Die KI erkennt mögliche doppelte Datensätze.

Beispiele:

- Felix Schröder
- Felix Schroeder

Der Benutzer entscheidet über die Zusammenführung.

---

### REQ-065 Automatische Schülerzuordnung

Die KI schlägt passende Schüler für erkannte Daten vor.

Beispiele:

- Dokumente
- Fehlzeiten
- Noten
- Beobachtungen

---

### REQ-066 Importprotokoll

Jeder Import wird dokumentiert.

Gespeichert werden:

- Datum
- Benutzer
- Quelldatei
- erkannte Datensätze
- importierte Datensätze
- Fehler
- Warnungen

---

### REQ-067 Universeller Schulsoftware-Import

Importe sollen unabhängig von einer bestimmten Schulsoftware möglich sein.

Beispiele:

- WebUntis
- IServ
- Schulmanager
- TeacherTool
- TeacherStudio
- Excel-Listen
- PDF-Auswertungen

Die KI unterstützt die Erkennung unbekannter Formate.

---

### REQ-068 KI-gestützte Schnellerfassung

Nach dem Unterricht können unstrukturierte Stichpunkte eingegeben werden.

Beispiel:

Felix:
- sehr gute Mitarbeit

Laura:
- Hausaufgaben vergessen

Paul:
- Präsentation gehalten

Die KI erstellt daraus strukturierte Beobachtungen und ordnet diese den passenden Schülerakten zu.

---

### REQ-069 Intelligente Feldzuordnung

Die KI erkennt automatisch die Bedeutung von Spalten in Importdateien.

Beispiele:

"Name" → Schülername

"Fehlstunden" → Fehlzeiten

"Punkte" → Bewertung

"Kompetenzstand" → Kompetenzbewertung

---

### REQ-070 Import-Lernfunktion

Das System merkt sich frühere Zuordnungen.

Beispiel:

Eine bestimmte WebUntis-Datei wurde bereits mehrfach importiert.

Die KI verwendet die bisherige Zuordnung automatisch als Vorschlag.

---

### REQ-071 Dokumentenklassifikation

Die KI erkennt den Dokumenttyp automatisch.

Beispiele:

- Klassenarbeit
- Präsentation
- Bewertungsbogen
- Gesprächsprotokoll
- Förderplan
- Elternbrief

---

### REQ-072 Massenimport

Mehrere Dateien können gleichzeitig importiert werden.

Die KI analysiert alle Dateien und erstellt einen gemeinsamen Importvorschlag.

---

### REQ-073 Unsicherheitsanzeige

Die KI gibt bei jedem erkannten Datensatz eine Vertrauensbewertung aus.

Beispiel:

- Schülerzuordnung: 98 %
- Kompetenzzuordnung: 82 %
- Dokumenttyp: 91 %

Unsichere Zuordnungen werden hervorgehoben.

---

### REQ-074 Korrekturfeedback

Korrekturen des Benutzers können für zukünftige Importe berücksichtigt werden.

Dadurch verbessert sich die Qualität der Vorschläge im Laufe der Nutzung.

---

### REQ-075 Import-Testmodus

Importe können zunächst simuliert werden.

Es werden keine Daten gespeichert.

Die Lehrkraft kann die Auswirkungen vorab prüfen.

---

# 6. Kann-Anforderungen

## NICE-001 Elternportal

Perspektivisch könnten ausgewählte Informationen für Eltern bereitgestellt werden.

## NICE-002 Schülerportal

Perspektivisch könnten Schüler eigene Rückmeldungen oder Dokumente einsehen.

## NICE-003 Sitzplan

Ein Sitzplan kann für Lerngruppen angelegt werden.

## NICE-004 Gruppenverwaltung

Arbeitsgruppen können verwaltet werden.

## NICE-005 Hausaufgabenübersicht

Hausaufgaben können systematisch nachverfolgt werden.

## NICE-006 Förderplaner

Fördermaßnahmen können geplant und überprüft werden.

## NICE-007 Präsentationsanalyse

Präsentationen können KI-gestützt analysiert werden.

## NICE-008 OCR

Scans und PDFs können per OCR ausgelesen werden.

## NICE-009 Zeugnistext-Export

Berichte können als Grundlage für Zeugnis- oder Lernentwicklungsformulierungen exportiert werden.

---

# 7. Nicht-Ziele

Das System soll zunächst nicht leisten:

- Stundenplanung
- Vertretungsplanung
- schulweite Verwaltung
- Sekretariatsfunktionen
- Elternkommunikation als offizieller Schulkanal
- Finanzverwaltung
- Raumplanung
- vollständiges LMS
- rechtssichere amtliche Schülerakte

---

# 8. Qualitätsanforderungen

## QA-001 Bedienbarkeit

Das System muss ohne tiefgehende Programmierkenntnisse bedienbar sein.

## QA-002 Nachvollziehbarkeit

KI-Ausgaben müssen auf gespeicherten Daten beruhen.

## QA-003 Quellenbezug

Bei KI-Antworten soll erkennbar sein, welche Daten Grundlage der Antwort waren.

## QA-004 Korrekturmöglichkeit

KI-generierte Inhalte müssen durch die Lehrkraft bearbeitet werden können.

## QA-005 Keine automatische Entscheidung

Die KI darf keine verbindlichen pädagogischen Entscheidungen treffen.

## QA-006 Erweiterbarkeit

Neue Felder, Tabellen und Bewertungsmodelle sollen ergänzt werden können.

## QA-007 Datenminimierung

Es sollen nur Daten gespeichert werden, die für den pädagogischen Zweck erforderlich sind.

---

# 9. Offene Fragen

- Welche WebUntis-Exportformate stehen konkret zur Verfügung?
- Welche Daten dürfen dienstrechtlich lokal gespeichert werden?
- Soll das System ausschließlich lokal laufen?
- Soll eine spätere Mehrbenutzerfähigkeit vorbereitet werden?
- Welche KI-Modelle erfüllen die Anforderungen an Datenschutz und Qualität?
- Wie lange sollen Schülerdaten aufbewahrt werden?
- Welche Dokumenttypen sollen in Version 1.0 zwingend unterstützt werden?
