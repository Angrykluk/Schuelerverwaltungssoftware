# Datenmodell

**Version:** 0.1  
**Status:** Entwurf

## Ziel

Dieses Dokument beschreibt die fachlichen Datenobjekte des Teacher Intelligence Systems (TIS).

Technische Details wie Datenbanktypen oder Implementierungsdetails werden erst in späteren Versionen ergänzt.

---

# Entitäten

## Schüler

Repräsentiert einen einzelnen Schüler.

### Geplante Felder

- Schüler-ID
- Vorname
- Nachname
- Geburtsdatum
- E-Mail
- Bemerkungen
- Aktiv

---

## Klasse

Repräsentiert eine Klasse oder Lerngruppe.

### Geplante Felder

- Klassen-ID
- Bezeichnung
- Schuljahr
- Fach
- Jahrgang

---

## SchülerKlasse

Verknüpfung zwischen Schülern und Klassen.

Ein Schüler kann in mehreren Lerngruppen sein.

---

## Fehlzeit

Dokumentiert eine Fehlzeit.

### Geplante Felder

- Datum
- Stunde
- Art
- Bemerkung

---

## Kompetenz

Beschreibt eine bewertbare Kompetenz.

### Beispiele

- Argumentieren
- Präsentieren
- Experimentieren
- Teamarbeit

---

## Kompetenzbewertung

Bewertung einer Kompetenz für einen Schüler.

### Beispiele

- Trifft nicht zu
- Trifft teilweise zu
- Trifft fast zu
- Trifft zu

---

## Note

Leistungsbewertung eines Schülers.

### Beispiele

- Klassenarbeit
- Test
- Präsentation
- Mitarbeit

---

## Dokument

Dateien, die einem Schüler zugeordnet werden.

### Beispiele

- Klassenarbeiten
- Präsentationen
- Bewertungsbögen
- Förderpläne

---

## Beobachtung

Freitext-Einträge der Lehrkraft.

### Beispiele

- Unterrichtsbeobachtungen
- Gesprächsnotizen
- Elterngespräche

---

## Bericht

KI-generierte Berichte.

### Beispiele

- Lernentwicklungsbericht
- Förderempfehlung
- Elterngesprächszusammenfassung

---

# Beziehungen

Klasse
→ viele Schüler

Schüler
→ viele Fehlzeiten

Schüler
→ viele Noten

Schüler
→ viele Kompetenzbewertungen

Schüler
→ viele Dokumente

Schüler
→ viele Beobachtungen

Schüler
→ viele Berichte
