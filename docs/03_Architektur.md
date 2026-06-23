# Architektur

**Version:** 0.1  
**Status:** Entwurf

## Zielarchitektur

```text
NocoDB
    ↓

PostgreSQL
    ↓

FastAPI
    ↓

Ollama
    ↓

Lokales Sprachmodell
```

---

# Komponenten

## NocoDB

Aufgaben:

- Benutzeroberfläche
- Formulare
- Listen
- Filter
- Dateneingabe

---

## PostgreSQL

Aufgaben:

- Zentrale Datenspeicherung

---

## FastAPI

Aufgaben:

- API
- Automatisierungen
- Schnittstellen
- KI-Anbindung

---

## Ollama

Aufgaben:

- Lokaler KI-Zugriff

---

## Sprachmodell

Beispiele:

- Qwen
- Llama
- Mistral

---

# Architekturprinzipien

## ARCH-001 DSGVO

Personenbezogene Daten sollen lokal gespeichert werden.

---

## ARCH-002 Datenhoheit

Alle Daten gehören der Lehrkraft.

---

## ARCH-003 Exportierbarkeit

Alle Daten müssen exportierbar sein.

---

## ARCH-004 Erweiterbarkeit

Neue Funktionen sollen ohne Datenmigration ergänzt werden können.

---

## ARCH-005 Offlinefähigkeit

Kernfunktionen sollen auch ohne Internet nutzbar sein.
