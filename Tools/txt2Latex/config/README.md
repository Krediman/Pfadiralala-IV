# Hinweise zur Konfiguration

Diese Dokument enthält die Dokumentation der Konfigurationsdateien.

## config.py

Hier werden alle Wichtigen Konfigurationen durchgeführt. Der Einfachheit halber handelt es sich um ein Python-skript, sodass beliebige Funktionen direkt programmiert werden können.

##### Akkordstil
Erlaubte Werte: `'l'`, `'m'` oder `''`

Akkorde können in zwei Schreibweisen angegeben werden:

 * Großkleinschreibung: Dur-Akkorde werden groß geschrieben, Moll-Akkorde werden klein geschrieben
 * 'm'-Schreibweise: Akkorde werden groß geschrieben, Moll-Akkorde erhalten ein 'm'

Beide Schreibweise werden in der Eingabe unterstützt. Mit dem Parameter `Akkordstil` wird festgelegt, welcher Stil in der Ausgabe versendet werden soll.
`Akkordstil = ''` übernimmt die Akkorde so, wie sie in der Eingabedatei angegeben werden.
`Akkordstil = 'm'` konvertiert  die Akkorde in die m-Schreibweise, falls nötig.
`Akkordstil = 'l'` konvertiert  die Akkorde in Großkleinschreibweise, falls nötig.

#### REGEX
Um Label für unterschiedliche Blocktypen zu erkennen, werden Reguläre ausdrücke verwendet. Da die Eingabe intern Zeilenweise verarbeitet wird, werden die Regulären ausdrücke auf jede Zeile angewendet. REGEX für mehrzeiligen Text ist also nicht möglich.
Der gefundene Ausdruck wird aus der Eingabe entfernt. Es sollte nur eine Übereinstimmung in einer Zeile geben.
`STROPHENREGEX` ist der Reguläre Ausdruck für die Strophennummer von Nummerierten Strophen
`REFRAINREGEX` ist der Reguläre Ausdruck für die Markierung des Refrains
`INFOREGEX` ist der Reguläre Ausdruck, mit dem der Anfang des Infoblockes identifiziert wird.

`AKKOORDREGEX` wird auf Zeilen angewendet, die nur Akkorde enthalten. Jeder Treffer sollte ein einzelner Akkord sein.

#### Ersetzungsfunktionen
Vor und nach der Konvertierung der Zeilen mit Akkorden und Text zu einer gemeinsamen Ausgabezeile besteht die Möglichkeit, manuell Änderungen vorzunehmen. Das kann abhängig vom erkannten Typ des Blockes, aus dem die Zeilen stammen, in den unterschiedlichen Funktionen passieren. Üblicherweise werden Hier Zeichen, die Latex nicht 1:! übernimmt, z.B. das kaufmännische und (`&`)  durch escape-sequenzen ersetzt, im Prinzip sind aber beliebige Ersetzungen möglich.

Da im Titelblock und im Infoblock keine Akkordsymbole Verarbeitet werden, gibt es nur eine Ersetzungsfunktion.

Eine Besonderheit stellt die Funktion `formatMeta` dar. Hier können die aus der Eingabe extrahierten Metadaten als dict bearbeitet werden. Es empfiehlt sich, nur die Werte zu bearbeiten und die Schlüssel so zu lassen, wie sie sind.

Alle Funktionen deren Name mit einem Unterstrich beginnt, werden nur lokal verwendet.

#### Umgebungen:
Hier werden die Namen der verwendeten Latex-Umgebungen für die unterschiedlichen Blocktypen definiert. siehe auch Template.jinja, und die Dokumentation von jinja2
