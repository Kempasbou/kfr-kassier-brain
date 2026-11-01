---
name: kfr-neues-mitglied
description: Erfasst einen neuen Mitgliedsantrag der Kulturfreunde Rieden (Foto) – Mail, neue Zeile in der Mitglieder-Excel und Lastschriftvorlage für die Bank.
---

# Neues Mitglied Kulturfreunde Rieden erfassen

Daniel ist Kassier der Kulturfreunde Rieden e.V. Er schickt ein Foto der Beitrittserklärung, die aktuelle Mitglieder-Excel und die leere Importdatei für Lastschriftvorlagen.

## 1. Antrag auslesen
Aus dem Foto übernehmen: Vorname, Nachname, Geburtsname, Straße, PLZ/Ort, Telefon, Mobil, E-Mail, Geburtsdatum, aktiv/passiv, Jahresbeitrag, Kontoinhaber, IBAN, Ort/Datum der Unterschrift.
- IBAN ohne Leerzeichen, Prüfsumme (mod 97 = 1) per Code prüfen. Schlägt sie fehl: unsichere Ziffern nennen und nachfragen.
- Unleserliche Felder kurz nachfragen, nicht raten.

## 2. Mail
Foto an **kulturfreunderieden@gmail.com** senden (Betreff z. B. „Beitrittserklärung Vorname Nachname“), wenn ein Mail-Connector verbunden ist. Sonst Daniel Bescheid geben, dass er die Mail selbst schickt.

## 3. Mitglieder-Excel
- Blatt „Aktuelle Mitglieder“, Spalten: Nr. | Vorname | Nachname | Mitglied seit | Beitrag.
- Genau eine Zeile anhängen: Nr. = höchste vorhandene Nr. + 1; Mitglied seit = Datum der Unterschrift (als echtes Datum); Beitrag als Zahl.
- Formatierung (Schrift, Zahlenformate) der Zeile darüber übernehmen (openpyxl).
- Speichern als `Aktuelle_Mitglieder_JJJJMMTT.xlsx` mit heutigem Datum.

## 4. Lastschriftvorlage (CSV für die Bank)
`;`-getrennt, UTF-8 mit BOM, CRLF, Kopfzeile unverändert. Die Vorlagezeile mit den festen Werten durch die Zeile des neuen Mitglieds ersetzen:

| Spalte | Inhalt |
|---|---|
| A Vorlagenbezeichnung | `Nachname, Vorname` |
| B IBAN Zahlungsempfänger | `DE56830654080005298148` (immer) |
| C IBAN Zahlungspflichtiger | IBAN vom Antrag |
| D BIC / E Kreditinstitut | aus der BLZ (IBAN-Stellen 5–12) per Websuche ermitteln |
| F Zahlungspflichtiger | Kontoinhaber als `Vorname Nachname` |
| G–L | leer |
| M Betrag | Jahresbeitrag, z. B. `12,00` |
| N Verwendungszweck | `Beitrag Kulturfreunde Rieden @JJJJ@` |
| O LastschriftArt | `Basis-Lastschrift` |
| P Mandatsart | `WIEDERHOLEND` |
| Q Mandatsreferenz | `KFR Mitglied <Nr.>` (ein Leerzeichen vor der Nummer) |
| R Gläubiger-ID | `DE76ZZZ00002581711` |
| S unterschrieben am | Datum der Unterschrift, `TT.MM.JJJJ` |
| T | leer |

Dateiname: `Lastschriftvorlagen_JJJJ-MM-TT.csv`.

## 5. Ablage
- Beide Dateien an Daniel senden; ist sein Computer verbunden, zusätzlich in seinen Download-Ordner schreiben.
- Im Repo `Kempasbou/kfr-kassier-brain` eine Zeile in `protokoll/neuaufnahmen.md` ergänzen (Nr., Name, Mitglied seit, Beitrag, Erfassungsdatum), committen und pushen. **Keine** IBAN, Adresse, Telefon, E-Mail, Geburtsdaten oder Fotos ins Repo.

## 6. Abschluss
Kurz auf Deutsch melden: Mitgliedsnummer, ermittelte Bank/BIC, was noch offen ist (z. B. Mail).
