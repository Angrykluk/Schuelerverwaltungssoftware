# Testfälle

**Version:** 0.1  
**Status:** Entwurf

---

# TEST-001 Schüler anlegen

## Gegeben

Keine Schüler vorhanden

## Wenn

Ein Schüler angelegt wird

## Dann

Der Schüler erscheint in der Schülerliste

---

# TEST-002 Schülerimport

## Gegeben

CSV-Datei mit Schülerliste

## Wenn

Import ausgeführt wird

## Dann

Alle Schüler werden angelegt

---

# TEST-003 Fehlzeiten zählen

## Gegeben

Felix Schröder besitzt 5 Fehlzeiten

## Wenn

Die KI gefragt wird:

"Wie viele Fehlzeiten hat Felix Schröder?"

## Dann

Die KI antwortet:

"Felix Schröder hat 5 Fehlzeiten."

---

# TEST-004 Kompetenzbewertung

## Gegeben

Kompetenz:

Argumentieren

Bewertung:

Trifft fast zu

## Dann

Die Bewertung wird korrekt gespeichert

---

# TEST-005 Dokumentenablage

## Gegeben

Eine PDF-Datei

## Wenn

Die Datei hochgeladen wird

## Dann

Sie erscheint in der Schülerakte

---

# TEST-006 Lernentwicklungsbericht

## Gegeben

- Noten
- Kompetenzen
- Beobachtungen

## Wenn

Ein Bericht erzeugt wird

## Dann

Die Informationen werden korrekt verarbeitet

---

# TEST-007 KI-Zusammenfassung

## Gegeben

10 Beobachtungen zu einem Schüler

## Wenn

Zusammenfassung angefordert wird

## Dann

Die KI erstellt eine sachliche Übersicht
