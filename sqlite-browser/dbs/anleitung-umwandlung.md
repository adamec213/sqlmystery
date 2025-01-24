# Umwandeln der Datenbanken in SQLite

## Escape für einfache Anführungszeichen korrigieren
Suche:
`
\'
`

Ersetzen mit:
`
''
`

## Extrahieren der Tabellendeklarationen (RegEx)
`
(CREATE TABLE (.|\n)*?;\n)
`

## Nicht unterstützte Parameter löschen (RegEx)
`
 ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_german1_ci
`

## Constraints
- Nachträgliche Constraints direkt in `CREATE TABLE`-Anweisungen übertragen
- `KEY`-Constraints können nicht übernommen werden, also löschen (TODO: trotzdem manuell Index erstellen?)

## Extrahieren einzufügender Werte (RegEx)
`
(INSERT INTO (.|\n)*?;\n)
`

## Hex-Strings in Bildern ersetzen (RegEx)
Suche:
`
 0x([0-9a-f]*)
`

Ersetzen mit:
`
 X'$1'
`

## Views

`CREATE ALGORITHM`-Anweisungen (konkret genutzt für `freund2` in gbuch) für Views müssen umgewandelt werden: `CREATE VIEW ... as SELECT ...`
