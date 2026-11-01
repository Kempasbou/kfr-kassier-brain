# Importdatei Lastschriftvorlagen (Bank)

Format: CSV, Trennzeichen `;`, UTF-8 mit BOM, CRLF. Dateiname: `Lastschriftvorlagen_JJJJ-MM-TT.csv`

| Spalte | Feld | Inhalt |
|---|---|---|
| A | Vorlagenbezeichnung | `Nachname, Vorname` |
| B | IBAN des Zahlungsempfängers | immer `DE56830654080005298148` |
| C | IBAN des Zahlungspflichtigen | vom Antrag, ohne Leerzeichen |
| D | BIC | aus BLZ (Stellen 5–12 der IBAN) |
| E | Kreditinstitut | aus BLZ |
| F | Zahlungspflichtiger | Kontoinhaber, `Vorname Nachname` |
| G–L | Strasse … Länderkennzeichen | **leer** |
| M | Betrag | Jahresbeitrag, deutsches Format `12,00` |
| N | Verwendungszweck | immer `Beitrag Kulturfreunde Rieden @JJJJ@` |
| O | LastschriftArt | immer `Basis-Lastschrift` |
| P | Mandatsart | immer `WIEDERHOLEND` |
| Q | Mandatsreferenz | `KFR Mitglied <Mitgliedsnummer>` |
| R | Gläubiger-ID | immer `DE76ZZZ00002581711` |
| S | unterschrieben am | Datum der Unterschrift auf dem Antrag, `TT.MM.JJJJ` |
| T | Abweichender Zahlungsempfänger | **leer** |

Abbuchung immer im März.
