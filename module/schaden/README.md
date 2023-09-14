# Schaden

Ein WarGear beinhaltet neben der Kanonen Technik auch Technik um Schaden zu erkennen und gegebenenfalls auch dessen Tiefe an Brücke oder andere Einrichtungen weiter zu geben. Da dies ein integraler Part eines WarGears ist wollen wir hier 3 Schadens Module gestaffelt anhand des Anwendungsfalls aufzählen und erklären. Die 3 Module werden jeweils einen WGP Server als Verarbeitung benutzen und handeln unabhängig voneinander. Für den Schaden unterscheiden wir die 3 Kategorien: Front, Seiten (Rechts und Links in Hauptschussrichtung) und dem Rest (also Oben, Unten und Hinten). Die Protokolle unterscheiden sich hierbei um wenige Bits oder bereiche und sind unabhängig einbaubar sowie skalierbar. Einzig das Front Modul ist als benötigt und Plfichtmodul eingestuft und muss eingebaut werden.

## Front Schaden

### Protokoll
```
#### bbbb #### bttt
```

Das Protokoll besteht aus 2 Paketen an den gleichen WGP Server. Das erste beinhaltet 4 Bits des Bereichs, wo schaden entstanden ist wobei die letzten 4 Bits noch ein Bit des Bereichs und die Tiefe beinhalten. Die Bereiche sind hierbei durch das 5 Bit in links (0) und rechts (1) unterteilt und werden durch die ersten 4 Bits weiter in 4*4 Bereiche eingeteilt. Ein Bereich darf auch nur aus einer Kanone bestehen, außerdem müssen nicht alle Bereiche von einem WarGear genutzt werden. Die ersten beiden Bits beschreiben dabei die 4 Höhen (00, 01, 10, 11) von unten nach oben und die folgenden 2 Bits die Breite (00, 01, 10, 11) von links nach rechts. Die Tiefe wird hierbei durch folgende Matrix beschrieben:

| Bits | 1ne Tiefe | 2 Tiefen | 3 Tiefen | 4 Tiefen | 5 Tiefen | 6 Tiefen | 7 Tiefen | 8 Tiefen |
| ---- | --------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| 000  | -------   | Tiefe 1  | Tiefe 1  | Tiefe 1  | Tiefe 1  | Tiefe 1  | Tiefe 1  | Tiefe 1  |
| 001  | Tiefe 1   | Tiefe 2  | Tiefe 3  | Tiefe 4  | Tiefe 5  | Tiefe 6  | Tiefe 7  | Tiefe 8  |
| 010  |           |          | -------  | Tiefe 2  | Tiefe 2  | Tiefe 3  | Tiefe 3  | Tiefe 3  |
| 011  |           |          | Tiefe 2  | Tiefe 3  | Tiefe 4  | Tiefe 4  | Tiefe 5  | Tiefe 5  |
| 100  |           |          |          |          | -------  | Tiefe 2  | Tiefe 2  | Tiefe 2  |
| 101  |           |          |          |          | Tiefe 3  | Tiefe 5  | Tiefe 4  | Tiefe 4  |
| 110  |           |          |          |          | -------  | -------  | -------  | Tiefe 6  |
| 111  |           |          |          |          | -------  | -------  | Tiefe 6  | Tiefe 7  |

Beispiel 1:
```
#### 0110 #### 1100
```
Angenommen sei das das sendende WarGear 7 Tiefen senden kann und wir 5 bis 8 Tiefen empfangen.

Dann steht `01` für die zweite Höhe und `10` für die dritte Breite auf der Rechten Seite beschrieben durch die folgende `1` und dieser Bereicht hat die Tiefe `2`.

Beispiel 2:
...

Beispiel 3:
...

## Seiten Schaden

### Protokoll
```
#### bbbb #### bstt
```

Auch dieses Protkoll besteht aus Paketen an den gleichen WGP Server. Das erste beinhaltet 4 Bits des Bereichs, wo schaden entstanden ist wobei die letzten 4 Bits noch ein Bit des Bereichs, die Seite des WarGears und die Tiefe beinhaltet. ie Bereiche sind hierbei durch das 5 Bit in links (0) und rechts (1) unterteilt und werden durch die ersten 4 Bits weiter in 4*4 Bereiche eingeteilt. Ein Bereich darf auch nur aus einer Kanone bestehen, außerdem müssen nicht alle Bereiche von einem WarGear genutzt werden. Die ersten beiden Bits beschreiben dabei die 4 Höhen (00, 01, 10, 11) von unten nach oben und die folgenden 2 Bits die Breite (00, 01, 10, 11) von links nach rechts. Neben der Tiefe welche durch die nachfolgende Matrix beschrieben wird gibt es noch die Seite, welche durch das 6te Bit entschieden wird 0 ist hierbei links, 1 rechts:

| Bits | 1ne Tiefe | 2 Tiefen | 3 Tiefen | 4 Tiefen |
| ---- | --------- | -------- | -------- | -------- |
| 00   | -------   | Tiefe 1  | Tiefe 1  | Tiefe 1  |
| 01   | Tiefe 1   | Tiefe 2  | Tiefe 3  | Tiefe 4  |
| 10   |           |          | -------  | Tiefe 2  |
| 11   |           |          | Tiefe 2  | Tiefe 3  |

Beispiel 1:
...

Beispiel 2:
...

Beispiel 3:
...

## Rest Schaden

### Protokoll
```
#### bbbb #### sstt
```

Auch dieses Protkoll besteht aus Paketen an den gleichen WGP Server. Das erste beinhaltet 4 Bits die den Bereich welche in einem 2*8 Bereich angeordnet sind. Wobei das erste Bit mit der 0 für unten und 1 mit oben für hinten und links und rechts für oben und unten. und dann die folgenden 3 Bits von vorne nach hinten bzw links nach rechts durchgezählt wird. Die ersten beiden Bits des zweiten Pakets beschreibt die Seite mit folgender Matrix:

| Bits | Seite  |
| ---- | ------ |
| 00   | Oben   |
| 01   | Unten  |
| 10   | Hinten |

Und die Tiefe wird mit der folgenden Matrix beschrieben:

| Bits | 1ne Tiefe | 2 Tiefen | 3 Tiefen | 4 Tiefen |
| ---- | --------- | -------- | -------- | -------- |
| 00   | -------   | Tiefe 1  | Tiefe 1  | Tiefe 1  |
| 01   | Tiefe 1   | Tiefe 2  | Tiefe 3  | Tiefe 4  |
| 10   |           |          | -------  | Tiefe 2  |
| 11   |           |          | Tiefe 2  | Tiefe 3  |

Beispiel 1:
...

Beispiel 2:
...

Beispiel 3:
...