---
description: >-
  Detta är en liten lathund till MySQL. Den beskriver de vanligaste kommandona i
  deras enklaste form.
---

# Lathund

## Skapa en tabell \(CREATE TABLE\) 

```sql
MariaDB> CREATE TABLE test (id INT, namn VARCHAR(50)); 
Query OK, 0 rows affected (0.05 sec) 
```

Ovanstående skapar tabellen test med två fält, id och namn. Namn är ett fält som innehåller text \(upp till 50 bokstäver\) och id är en siffra.

## Mata in data \(INSERT INTO\)

```sql
MariaDB> INSERT INTO test (namn) VALUES ('Kalle Anka'); 
Query OK, 1 row affected (0.14 sec) 
```

Ovanstående matar in ”Kalle Anka”, som namn i tabellen test. Vill jag mata in värden i flera fält åtskiljer jag dem med komma \(,\), likadant gör jag då med värdena. Till exempel:

```sql
MariaDB> INSERT INTO test (id, namn) VALUES (10, 'Kajsa Anka'); 
Query OK, 1 row affected (0.07 sec) 
```

Vill jag mata in flera poster \(rader\) åt gången, gör man såhär:

```sql
MariaDB> INSERT INTO test (namn) VALUES          
    -> ("Kalle"),
    -> ("Alexander"),
    -> ("Joakim");
Query OK, 3 rows affected (0.02 sec)
Records: 3  Duplicates: 0  Warnings: 0
```

## Ställa frågor \(SELECT ... FROM\) 

```sql
MariaDB> SELECT * FROM test; 
+------+------------+ 
| id   | namn       | 
+------+------------+ 
| NULL | Kalle Anka | 
| 10   | Kajsa Anka | 
+------+------------+ 
2 rows in set (0.10 sec) 
```

_Ovanstående väljer allt \(_\) från tabellen test. 

## Ändra data \(UPDATE\) 

VARNING!! Detta kommando förändrar data, det finns inget ”undo”, var försiktig! 

```sql
MariaDB> UPDATE test SET id=9 WHERE id=10; 
Query OK, 1 row affected (0.07 sec) 
Rows matched: 1 Changed: 1 Warnings: 0 
```

Ovanstående uppdaterar fältet id till 9 för alla poster där id är 10. Observera att ALLA poster med id=10 kommer att få id 9, vilket kanske inte är vad man vill alla gånger. Se till att det finns ett fält som är unikt för alla poster.

## Radera poster \(DELETE FROM\) 

VARNING!! Detta kommando tar bort data, det finns inget ”undo”, var försiktig! 

```sql
MariaDB> DELETE FROM test WHERE id=9; 
Query OK, 1 row affected (0.06 sec)
```

Ovanstående tar bort ALLA poster med id=9.

## Tips och trix! 

* Du kan bläddra mellan tidigare kommandon du skrivit med tangenterna pil upp och pil ned.
* Dokumentera dina kommandon genom att kopiera dem och klistra in dem i ett textredigeringsprogram, de kan vara bra att ha senare.

