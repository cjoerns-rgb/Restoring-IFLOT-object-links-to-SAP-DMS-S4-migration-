# Restoring-IFLOT-object-links-to-SAP-DMS-S4-migration-
Analysis and correction of object keys (OBJKY) in the DRAD table after an SAP S/4HANA migration. Checks the existence of migrated functional locations (IFLOT), (EQUI), (MARA), etc., and enables the correction of incorrect links.
# SAP DVS Objektschlüssel-Prüfung & Korrektur (ZIX_DVS_DRAD_ANALYSE)

**Ein ABAP-Report zur Analyse und Korrektur von Objektschlüsseln (OBJKY) in der Tabelle `DRAD` nach SAP-S/4HANA-Migrationen.**

---

## 📌 Zweck
Dieser Report hilft bei der **Prüfung und Korrektur von Objektschlüsseln** in der Dokumentenverwaltung (DVS) nach einer SAP-S/4HANA-Migration.
Häufig sind migrierte **Technische Plätze (IFLOT)**, **Ausrüstungen (EQUI)**, **Materialien (MARA)** oder andere Objekte nicht mehr korrekt mit DVS-Datensätzen verknüpft.
Der Report identifiziert fehlerhafte Verknüpfungen und ermöglicht deren Korrektur.

---

## 🔧 Funktionen
| Funktion | Beschreibung |
|----------|-------------|
| **Existenzprüfung** | Prüft, ob der Objektschlüssel (`OBJKY`) in der jeweiligen SAP-Stammdaten-Tabelle existiert (z. B. `MARA`, `EQUI`, `IFLOT`). |
| **Korrektur der Objektschlüssel** | Korrigiert fehlerhafte Schlüssel (aktuell nur für `IFLOT` implementiert). |
| **ALV-Ausgabe** | Zeigt die Ergebnisse in einer übersichtlichen Tabelle an. |

---

## 🛠 Unterstützte Dokumentobjekte (`DOKOB`)
| `DOKOB` | Beschreibung | Existenzprüfung | Korrektur |
|---------|-------------|----------------|-----------|
| `MARA` | Materialien | ✅ | ❌ |
| `PMAFVC` | Auftragsobjekte | ✅ | ❌ |
| `CRVS_B` | Seriennummern | ✅ | ❌ |
| `EQUI` | Ausrüstungen | ✅ | ❌ |
| `IFLOT` | Technische Plätze | ✅ | ✅ |
| `PMPLKO` | Arbeitspläne | ✅ | ❌ |

**Hinweis:** Die Korrekturlogik ist aktuell nur für `IFLOT` implementiert, lässt sich aber leicht erweitern.

---

## 🚀 Installation & Nutzung
### 1. Report in SAP einrichten
- Erstelle den Report **`ZIX_DVS_DRAD_ANALYSE`** in deinem SAP-System (Transaktion `SE38`).
- Kopiere den Quellcode aus [zix_dvs_drad_analyse.abap](zix_dvs_drad_analyse.abap).

### 2. Selektionsbildschirm
| Feld | Beschreibung |
|------|-------------|
| `DOKAR` | Dokumentart (z. B. `ZEICHNUNG`) |
| `DOKNR` | Dokumentnummer |
| `DOKOB` | Dokumentobjekt (z. B. `IFLOT`, `EQUI`) |
| `OBJKY` | Objektschlüssel (z. B. Technischer Platz, Ausrüstungsnummer) |
| **Existenzprüfung** | Aktiviert die Prüfung, ob der Objektschlüssel existiert. |
| **Korrektur der Objektschlüssel** | Aktiviert die Korrektur fehlerhafter Schlüssel (nur für `IFLOT`). |

### 3. Ausführung
- Führe den Report aus (`F8`).
- Die Ergebnisse werden in einer **ALV-Tabelle** angezeigt.

---

## ⚠ Wichtige Hinweise
- **Testsystem:** Teste den Report **vor dem Einsatz im Produktivsystem**!
- **Backup:** Erstelle ein Backup der Tabelle `DRAD`, falls Korrekturen durchgeführt werden.
- **Erweiterungen:** Der Report ist **erweiterbar** – weitere `DOKOB`-Typen können hinzugefügt werden.
- **Aktualisierung der Datenbank:** Die Korrektur der `DRAD`-Tabelle ist **auskommentiert** – aktiviere sie nur, wenn du sicher bist!

---

## 🔄 Anpassungsmöglichkeiten
### 1. Weitere `DOKOB`-Typen hinzufügen
Füge in der Methode `CHECK_EXISTENCE` weitere `WHEN`-Zweige hinzu, z. B. für `PRPS` (Projekte) oder `AUFK` (Aufträge).

### 2. Korrekturlogik erweitern
Erweitere die Methode `CORRECT_OBJKY`, um weitere `DOKOB`-Typen zu unterstützen.

### 3. Automatische Aktualisierung aktivieren
Entferne die Kommentare bei der `UPDATE`-Anweisung in `CORRECT_OBJKY`, um Korrekturen direkt in der Datenbank durchzuführen.

---

## 📂 Dateien
| Datei | Beschreibung |
|-------|-------------|
| [zix_dvs_drad_analyse.abap](zix_dvs_drad_analyse.abap) | ABAP-Quellcode des Reports. |

---

## 🤝 Beitrag & Feedback
- **Issues & Pull Requests:** Gerne kannst du Fehler melden oder Verbesserungen einreichen.
- **Fragen?** Kontaktiere mich unter [deine E-Mail oder SAP Community-Profil].

---
**© 2025 Christian Jörns**
*Dieser Report wird ohne Gewähr bereitgestellt. Nutze ihn auf eigenes Risiko!*
