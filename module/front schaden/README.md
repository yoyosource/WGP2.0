# Front Schaden

Der Frontale Schaden wird durch einen WGP2.0 Server abgearbeitet. Das Protokoll selber sieht eine doppelte Belegung der Werte 1-15 vor. Hierbei werden immer Paare versendet, welche aus einem Bereich und einer Schadens Tiefe bestehen. Dieses Modul ist für jedes WarGear welches ein WGP2.0 beinhalten soll verpflichtend.

## Protokoll
```
#### ???? #### ???1
```

Das Paket besteht aus 2 Teilen:
```
#### ????
```
und
```
#### ???1
```

Der erste Teil beschreibt eine Zahl zwischen 1-15, welcher den Bereich oder Kanone beschreibt, wo der Schaden entstanden ist. Hierbei wird das WarGear in ein 3*5 Raster unterteilt. 3 Bereiche Übereinander und 5 Nebeneinander werden hierbei abgebildet. Die Zahlen 1-5 bilden den untersten Bereich dar, 6-10 den Mittleren und 11-15 dann den Obersten.

Der zweite Teil beschreibt die Tiefe des Schadens und wird auf 3 Binär Stellen beschränkt mit einer Statischen 1 am Ende um eine Wertübertragung und einfachere Verarbeitung zu ermöglichen. Der variable Teil kann in 3 Ausführungen implementiert werden, wobei die einfachste Implementierung nur 2 Tiefen ermöglicht. Erweitern kann man dies auf 4 oder 8 Tiefen. Hier frei wählbar wie viel man auf Empfängerseite wirklich implementieren und umsetzten will. Damit das decoden der Bits in den 3 Modi so einfach und gleich wie Möglich geschehen kann werden 3 Raster der Bit Belegung vorgegeben.

| Bits | 1ne Tiefe | 2 Tiefen | 3 Tiefen | 4 Tiefen | 5 Tiefen | 6 Tiefen | 7 Tiefen | 8 Tiefen |
| ---- | --------- | -------- | -------- | -------- | -------- | -------- | -------- | -------- |
| 000  | Tiefe 1   | Tiefe 1  | Tiefe 1  | Tiefe 1  | Tiefe 1  | Tiefe 1  | Tiefe 1  | Tiefe 1  |
| 001  | --------- | Tiefe 2  | Tiefe 3  | Tiefe 4  | Tiefe 5  | Tiefe 6  | Tiefe 7  | Tiefe 8  |
| 010  |           |          | -------  | Tiefe 2  | Tiefe 2  | Tiefe 3  | Tiefe 3  | Tiefe 3  |
| 011  |           |          | Tiefe 2  | Tiefe 3  | Tiefe 4  | Tiefe 4  | Tiefe 5  | Tiefe 5  |
| 100  |           |          |          |          | -------  | Tiefe 2  | Tiefe 2  | Tiefe 2  |
| 101  |           |          |          |          | Tiefe 3  | Tiefe 5  | Tiefe 4  | Tiefe 4  |
| 110  |           |          |          |          | -------  | -------  | -------  | Tiefe 6  |
| 111  |           |          |          |          | -------  | -------  | Tiefe 6  | Tiefe 7  |