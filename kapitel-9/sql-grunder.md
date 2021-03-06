---
description: Databashantering med MySQL.
---

# Grunder i SQL

I denna laboration skall du se till att du kommer åt databasmotorn och att det fungerar. Du kommer också att skapa en tabell i din databas och mata in några poster i den.

## Starta databasklienten

För att komma åt databasen måste man använda ett program som kallas för en databasklient. Det finns flera olika sådana och vi kommer längre fram i kursen att ansluta till databasen med PHP men tills vidare skall vi använda den klient som följer med MySQL. Denna databasklient heter **mysql** och kan startas med en mängd olika argument.  
Så här kan det se ut från terminalen:

```bash
root@3084f5616900:/# mysql -u admin -p
Enter password: pass
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 2
Server version: 10.1.44-MariaDB-0ubuntu0.18.04.1 Ubuntu 18.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

Som du ser så står du nu vid en ny kommandoprompt. Vid denna skriver du **kommandon till databasen**. Jämför med prompten innan som var för att ge kommandon till systemet. Även vid denna prompt har du samma historikfunktion som du hade vid systemprompten, men här bläddrar du mellan kommandona till databasen. Vi testar lite kommandon så att vi ser att det fungerar. Vi måste först välja en databas att arbeta med. Vi väljer databasen _**labb**_ med kommandot **USE labb** :

```sql
MariaDB [(none)]> USE labb;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
MariaDB [labb]>
```

{% hint style="warning" %}
**Alla kommandon till databasen avslutas med semikolon ”;”** \(det behöver de inte göra vid systemprompten\).
{% endhint %}

Nu kan vi titta efter vad som finns i databasen _**labb**_. Kommandot **SHOW TABLES** visar alla tabeller i databasen:

```sql
MariaDB [labb]> SHOW TABLES;
Empty set (0.00 sec)
MariaDB [labb]>
```

I detta fall fanns det inga tabeller att visa eftersom vi inte har skapat några ännu. Men vad hade hänt om vi glömt att skriva ett semikolon på slutet?

```sql
MariaDB [labb]> SHOW TABLES
->
-> ;
Empty set (0.00 sec)
MariaDB [labb]>
```

Nu när jag tryckte **Enter**-tangenten efter **SHOW TABLES** visades en ny prompt. Denna prompt visar att jag är på en ny rad men fortfarande på samma kommando. Jag tryckte **Enter**-tangenten två gånger, sedan skrev jag ett semikolon för att avsluta kommandot. Som du såg så gick det bra, det går att dela upp kommandon på flera rader om man vill bara man avslutar dem med semikolon.

För att lämna databasklienten så ger du kommandot **\q**. De kommandon som börjar med bakstreck ”\” är specialkommandon till databasklienten och dessa skall inte avslutas med semikolon.

```bash
MariaDB [labb]> \q
Bye
root@3084f5616900:/#
```

Starta nu databasklienten igen och upprepa det vi gjort nu **minst en gång**. Detta skall du kunna göra i sömnen. Anteckna gärna och titta i den lilla **lathunden till MySQL** som du har fått.

## Skapa en tabell

Skapar en tabell gör man med kommandot **CREATE TABLE** vi börjar med att skapa en liten testtabell med ett fält som vi kallar för namn och som innehåller text \(max 10 tecken\). Syntaxen för kommandot **CREATE TABLE** ser i sin enklaste form ut så här:

```sql
MariaDB [labb]> CREATE TABLE test (namn varchar(10));
Query OK, 0 rows affected (0.01 sec)
```

Vi skapar en tabell som heter _**test**_ och som innehåller ett fält av typen **char\(10\)**.

Vill man skapa en tabell med fler fält än ett så kan man naturligtvis göra det. Då anger man fälten inom parentesen efter tabellnamnet åtskilda med kommatecken. Till exempel:

```sql
MariaDB [labb]> CREATE TABLE test2 (fnamn varchar(20), enamn varchar(20));
Query OK, 0 rows affected (0.18 sec)
```

Men nu fortsätter vi med tabellen _**test**_. Vi kollar att tabellen verkligen skapades:

```sql
MariaDB [labb]> SHOW TABLES;
+-----------------+
| Tables_in_labb  |
+-----------------+
| test            |
| test2           |
+-----------------+
2 rows in set (0.00 sec)
```

Jodå, den verkar ju ha skapats. Vi kan titta närmare på fälten med kommandot **SHOW FIELDS FROM** eller **EXPLAIN.**

```sql
MariaDB [labb]> SHOW FIELDS FROM test;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| namn  | varchar(10) | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
1 row in set (0.04 sec)
MariaDB [labb]>
```

## Datatyper

Det finns många sorters datatyper. Vi ser lista nedan, med det vanligast använda i fetstil:

### Numeriska

| Datatyp | Bytes | Beskrivning |
| :--- | :--- | :--- |
| TINYINT | 1 | Ett heltal som spänner mellan -128 till 127 eller 0 till 255. |
| SMALLINT | 2 | Ett heltal som spänner mellan -2^15 till 2^15-1 eller 0 till 2^16. |
| MEDIUMINT | 3 | Ett heltal som spänner mellan -2^23 till 2^23-1 eller 0 till 2^24. |
| **INT** | **4** | **Ett heltal som spänner mellan -2^31 till 2^31-1 eller 0 till 2^32.** |
| BIGINT | 8 | Ett heltal som spänner mellan -2^63 till 2^63-1 eller 0 till 2^64. |
| FLOAT | 4 | Ett flyttal som lagras i ett format beroende på CPU. |
| DOUBLE | 8 | Ett flyttal som lagras i ett format beroende på CPU. |
| DECIMAL | L | Ett flyttal som lagras som en sträng med längden L. |

### Text

| Datatyp | Maxlängd | Beskrivning |
| :--- | :--- | :--- |
| CHAR | MAX &lt; 256 | Innehåller text eller bytes. Fix längd med maxlängd som bestäms då kolumnen skapas. Maxlängden måste dock bestämmas till ett tal &lt; 256. |
| **VARCHAR** | **MAX &lt; 256** | **Innehåller text eller bytes. Variabel längd \(L\) med en maxlängd som bestäms då kolumnen skapas. Maxlängden måste dock bestämmas till ett tal &lt; 256. 1 byte används för att lagra längden på texten.** |
| TINYTEXT | 255 | Innehåller text. Variabel längd \(L\) med en maxlängd 255. 1 byte används för att lagra längden på texten. |
| **TEXT** | **65,535** | **Innehåller text. Variabel längd \(L\) med en maxlängd 2^16. 2 byte används för att lagra längden på texten.** |
| MEDIUMTEXT | 16,777,215 | Innehåller text. Variabel längd \(L\) med en maxlängd 2^24. 3 byte används för att lagra längden på texten. |
| LONGTEXT | 4,294,967,295 | Innehåller text. Variabel längd \(L\) med en maxlängd 2^32. 4 byte används för att lagra längden på texten. |
| TINYBLOB | 255 | Innehåller bytes. Variabel längd \(L\) med en maxlängd 255. 1 byte används för att bestämma hur många bytes som lagras. |
| BLOB | 65,535 | Innehåller bytes. Variabel längd \(L\) med en maxlängd 2^16. 2 byte används för att bestämma hur många bytes som lagras. |
| MEDIUMBLOB | 16,777,215 | Innehåller bytes. Variabel längd \(L\) med en maxlängd 2^24. 3 byte används för att bestämma hur många bytes som lagras. |
| LONGBLOB | 4,294,967,295 | Innehåller bytes. Variabel längd \(L\) med en maxlängd 2^32. 4 byte används för att bestämma hur många bytes som lagras. |

### Datum

| Datatyp | Min/Max | Beskrivning |
| :--- | :--- | :--- |
| YEAR | 1901 till 2155 | Lagrar ett år. |
| DATE | 1000-01-01 till 9999-12-31 | Lagrar ett datum. |
| TIME | -838:59:59 till 838:59:59 | Lagrar en tidpunkt. |
| **DATETIME** | **1000-01-01 00:00:00 till 9999-12-31 23:59:59** | **Lagrar en tidpunkt med datum och tid.** |
| **TIMESTAMP** | **1970-01-01 00:00:00 till mitten av 2037** | **Lagrar en tidpunkt med datum och tid. Datumet uppdateras automatiskt vid varje INSERT eller UPDATE** |

## Mata in data i tabellen

Nu när vi har vår lilla tabell, vill vi stoppa in lite värden i den. De gör vi med kommandot **INSERT INTO**. Med **INSER INTO** stoppar man in en post i taget i sin tabell. Om posten har flera fält \(den tabell vi gjort nu har ju bara ett fält\) så se till att fylla alla fält, eller så många som möjligt, med data redan när posten skapas.

```sql
MariaDB [labb]> INSERT INTO test (namn) VALUES ("kalle");
Query OK, 1 row affected (0.00 sec)
```

Om man har flera fält i sin tabell och man vill skapa poster är det enklast att fylla alla fält på en gång. Till exempel:

```sql
MariaDB [labb]> INSERT INTO test2 (fnamn, enamn) VALUES ("Kalle", "Anka");
Query OK, 1 row affected (0.01 sec)
```

Stoppa nu in några fler namn i tabellen _**test**_.

## Ställa frågor till databasen, välja ur en tabell

Att ställa frågor till en databas innebär att man gör vissa operationer på poster. Det vi gjorde ovan som skapade tallen och posterna kallas också för frågor även om de kanske inte direkt ses som frågor. Den enklaste frågan är att välja poster ur en tabell. När man väljer ut data ur en eller flera tabeller kallas det ibland att man gör en urvalsfråga. Det gör man med kommandot **SELECT FROM** som i sin enklaste form ser ut enligt nedan.

```sql
MariaDB [labb]> SELECT * FROM test;
+--------+
|  namn  |
+--------+
| kalle  |
| kajsa  |
| knatte |
| tjatte |
| fnatte |
+--------+
5 rows in set (0.00 sec)
MariaDB [labb]>
```

Tecknet **\*** betyder ungefär **allt**, man kan läsa ut kommandot ovan som **VÄLJ ALLT FRÅN test.**

### Radera poster från en tabell

Man kan radera poster från en tabell med kommandot **DELETE FROM ...**, observera att detta är ett destruktivt kommando som raderar saker. Det finns inget **undo**. Gör man en **DELETE FROM tabell** så kommer allt i tabellen att tas bort. Vi måste begränsa vad som skall tas bort med hjälp av **WHERE**. Se nedanstående exempel:

```sql
MariaDB [labb]> DELETE FROM test WHERE namn="fnatte";
Query OK, 1 row affected (0.80 sec)
MariaDB [labb]>
```

Märk att _**fnatte**_ _\*\*_är inom apostrofer i exemplet ovan. Alla textsträngar måste vara inom apostrofer eller citationstecken för att tolkas rätt. Apostroferna hittar du på tangenten ovanför den högra shift-tangenten på tangentbordet.

I exemplet ovan raderades raden där fältet namn innehåller _**fnatte**_ . En **WHERE** -sats kan man använda tillsammans med de flesta andra satser. Till exempel **SELECT**. Som du ser så raderas posten utan minsta förvarning ovan. Ofta kan det vara bra att testa med ett oförstörande kommando som till exempel **SELECT** först.

```sql
MariaDB [labb]> SELECT * FROM test WHERE namn="tjatte";
+--------+
|  namn  |
+--------+
| tjatte |
+--------+
1 row in set (0.00 sec)
```

Som vi ser så verkar en post matcha **WHERE namn="tjatte"** så är det den vi vill radera är det bara att sätta igång:

```sql
MariaDB [labb]> DELETE FROM test WHERE namn="tjatte";
Query OK, 1 row affected (0.03 sec)
```

Nu skall _**tjatte**_ vara borta, vi kollar med **SELECT** igen:

```sql
MariaDB [labb]> SELECT * FROM test WHERE namn="tjatte";
Empty set (0.00 sec)
```

Nu vet vi att _**tjatte**_ är borta!

## Radera tabeller

Ibland vill man ta bort en hel tabell. Det kan man göra med **DROP TABLE**. Kommandon som börjar med **DROP** skall man vara extremt försiktiga med, nu snackar vi riktigt destruktiva saker, och som vanligt inget ångra.

```sql
MariaDB [labb]> DROP TABLE test;
Query OK, 0 rows affected (0.34 sec)
MariaDB [labb]>
```

Så, nu är tabellen _**test**_ ett minne blott.

## Uppgifter

### Uppgift 1

Nu skall du skapa tabellen bilar. Den skall innehålla fyra fält. Ett med **reg**, **marke, modell** och **arsmodell** \(observera att vi undviker svenska tecken\). Se exempel i lathunden för hur du skapar en tabell med flera fält.  
Den skall se ut enligt skärmdumpen nedan:

```sql
MariaDB [labb]> EXPLAIN bilar;
+-----------+-------------+------+-----+---------+-------+
| Field     | Type        | Null | Key | Default | Extra |
+-----------+-------------+------+-----+---------+-------+
| reg       | varchar(10) | YES  |     | NULL    |       |
| marke     | varchar(50) | YES  |     | NULL    |       |
| modell    | varchar(50) | YES  |     | NULL    |       |
| arsmodell | int(11)     | YES  |     | NULL    |       |
+-----------+-------------+------+-----+---------+-------+
4 rows in set (0.03 sec)
```

### Uppgift 2

Du skall nu fylla tabellen med data.  
Var noga med att det blir exakt som nedan. Använda de kommandon du lärt dig för att skapa tabellen. Se till att den är rätt innan du börjar mata in bilarna. När du matar in bilarna, se till att du matar in en hel post i taget. Alltså alla data om en bil i en fråga. Det finns exempel även på detta i [lathunden](lathund.md). Resultatet skall bli exakt som detta:

```sql
MariaDB [labb]> SELECT * FROM bilar;
+--------+------------+-----------+-----------+
| reg    | marke      | modell    | arsmodell |
+--------+------------+-----------+-----------+
| ABC123 | Saab       | 9-5       |      2003 |
| DEF123 | Volvo      | S80       |      2002 |
| GHI123 | Mazda      | 626       |      2001 |
| JKL123 | Audi       | A8        |      2001 |
| MNO123 | BMW        | 323       |      1998 |
| PQR123 | Ford       | Mondeo    |      2001 |
| STU123 | Volvo      | 740       |      1987 |
| VYX123 | Volkswagen | Golf      |      1988 |
| ABC456 | Volkswagen | Polo      |      2003 |
| DEF456 | Toyota     | Carina II |      1998 |
+--------+------------+-----------+-----------+
10 rows in set (0.00 sec)
```

När du är klar och fått en tabell som ser ut som ovan kopierar du den och klistrar in i en texteditor och lämnar in. Du är nu klar med den första laborationen.

