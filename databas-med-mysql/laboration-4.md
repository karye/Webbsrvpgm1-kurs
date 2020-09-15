---
description: Använda inbyggda MySQL-funktioner
---

# Laboration 4

Det är i huvudsak två saker som brukar vara svårt när man jobbar med databaser, att skapa rätt struktur \(schema\) i sin databas och att sedan ställa rätt frågor till den. I denna labb jobbar vi vidare med SELECT. Du skall ha gjort Laboration 1, 2 och 3 innan du gör denna.

## Från förra laborationen

Från förra laborationen skall ni ha två tabeller som ser ut ungefär så här:

```text
mysql> DESCRIBE bilar;
+-----------+----------+------+-----+---------+-------+
| Field     | Type     | Null | Key | Default | Extra |
+-----------+----------+------+-----+---------+-------+
| reg       | char(10) |      | PRI |         |       |
| marke     | char(50) | YES  |     | NULL    |       |
| modell    | char(50) | YES  |     | NULL    |       |
| arsmodell | int(11)  | YES  |     | NULL    |       |
| pris      | int(11)  | YES  |     | NULL    |       |
| agare     | int(11)  | YES  |     | NULL    |       |
+-----------+----------+------+-----+---------+-------+
6 rows in set (0.01 sec)
mysql> DESCRIBE personer;
+-------+----------+------+-----+---------+----------------+
| Field | Type     | Null | Key | Default | Extra          |
+-------+----------+------+-----+---------+----------------+
| id    | int(11)  |      | PRI | NULL    | auto_increment |
| fnamn | char(50) | YES  |     | NULL    |                |
| enamn | char(50) | YES  |     | NULL    |                |
+-------+----------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```

Dessa har ungefär följande innehåll:

```text
mysql> SELECT * FROM bilar;
+--------+------------+-----------+-----------+--------+-------+
| reg    | marke      | modell    | arsmodell | pris   | agare |
+--------+------------+-----------+-----------+--------+-------+
| ABC123 | Saab       | 9-5       |      2003 | 130000 |     1 |
| DEF123 | Volvo      | S80       |      2002 | 140000 |     2 |
| GHI123 | Mazda      | 626       |      2001 |  80000 |     3 |
| JKL123 | Audi       | A8        |      2001 | 150000 |     5 |
| MNO123 | BMW        | 323       |      2001 |  60000 |     5 |
| PQR123 | Ford       | Mondeo    |      2001 |  90000 |     4 |
| STU123 | Volvo      | 740       |      1987 |  35000 |     5 |
| VYX123 | Volkswagen | Golf      |      1983 |  40000 |     5 |
| ABC456 | Volkswagen | Polo      |      2003 |  75000 |     1 |
| DEF456 | Toyota     | Carina II |      1998 |  30000 |     2 |
| XXX333 | Nissan     | Primera   |      2003 | 100000 |  NULL |
+--------+------------+-----------+-----------+--------+-------+
11 rows in set (0.03 sec)
mysql> SELECT * FROM personer;
+----+-----------+-------+
| id | fnamn     | enamn |
+----+-----------+-------+
|  1 | Kalle     | Anka  |
|  2 | Kajsa     | Anka  |
|  3 | Knatte    | Anka  |
|  4 | Fnatte    | Anka  |
|  5 | Tjatte    | Anka  |
|  6 | Knase     | Anka  |
|  7 | Alexander | Lukas |
+----+-----------+-------+
7 rows in set (0.03 sec)
```

Ser inte era tabeller ut exakt så så gör det inget. Men de bör vara ungefär lika.

### SELECT ... AS ... FROM ...

När man väljer olika fält från en tabell så blir rubriken det som man väljer1. Så vill man kanske inte ha det. Man vill kanske inte att det skall stå ”fnamn” och ”enamn” som det gör ovan utan ”Förnamn” och ”Efternamn” i stället. Det kan man åstadkomma genom att ställa sin fråga på följande sätt.

```text
mysql> SELECT fnamn AS Förnamn, enamn AS Efternamn FROM personer;
```

## Funktioner

Man kan i MySQL skriva enklare funktioner direkt i sina frågor. Vi har tidigare sett funktioner som SUM\(\), COUNT\(\) och AVG\(\). Nu skall vi titta på en del andra. Concat är en förkortning för engelskans ”concatenate” som betyder ungefär ”sätt ihop” och det är just vad funktionen gör.

### Funktionen CONCAT\(\)

Den fungerar så här:

```text
mysql> SELECT CONCAT(marke," ",modell) FROM bilar;
```

I exemplet så att det som kommer inom parenteserna kan vara godtyckliga strängar, inom citationstecken \(”\), och fältnamn. I vårt exempel så slår vi ihop ”marke” och ”modell” Med ett mellanslag emellan. Varje fält eller textsträng åtskiljs med ett kommatecken \(,\). Prova nu lite olika strängar.

### Datumfunktioner

För att kunna laborera med dessa utökar i persontabellen så att den ser ut som nedan. Titta bland dina tidigare laborationer om du inte minns hur man gör.

```text
mysql> DESCRIBE personer;
+--------------+----------+------+-----+---------+----------------+
| Field        | Type     | Null | Key | Default | Extra          |
+--------------+----------+------+-----+---------+----------------+
| id           | int(11)  |      | PRI | NULL    | auto_increment |
| fnamn        | char(50) | YES  |     | NULL    |                |
| enamn        | char(50) | YES  |     | NULL    |                |
| fodelsedatum | date     | YES  |     | NULL    |                |
+--------------+----------+------+-----+---------+----------------+
4 rows in set (0.00 sec)
```

Fyll \(populera\) sedan detta nya fält i tabellen så att den ser ut så här:

```text
mysql> SELECT * FROM personer;
+----+-----------+-------+--------------+
| id | fnamn     | enamn | fodelsedatum |
+----+-----------+-------+--------------+
|  1 | Kalle     | Anka  | 1934-07-09   |
|  2 | Kajsa     | Anka  | 1937-09-01   |
|  3 | Knatte    | Anka  | 1937-10-17   |
|  4 | Fnatte    | Anka  | 1937-10-17   |
|  5 | Tjatte    | Anka  | 1937-10-17   |
|  6 | Knase     | Anka  | 1964-08-02   |
|  7 | Alexander | Lukas | 1948-01-01   |
+----+-----------+-------+--------------+
7 rows in set (0.00 sec)
```

Som ni kanske har listat ut skall vi räkna ut hur gamla dessa figurer är. Men för att kunna veta det måste vi ju även veta vilken dag det är idag.

### Funktionen CURDATE\(\), CURTIME\(\) och NOW\(\)

Funktionen CURDATE\(\) ger som svar vilken dag det är idag. Man behöver inte alls välja några fält från tabeller utan man kan bara göra så här om man vill:

```text
mysql> SELECT CURDATE();
+------------+
| CURDATE()  |
+------------+
| 2004-03-11 |
+------------+
1 row in set (0.00 sec)
mysql> SELECT CURTIME();
+-----------+
| CURTIME() |
+-----------+
| 23:03:36  |
+-----------+
1 row in set (0.00 sec)
```

Samma sak gäller för CURTIME\(\) som naturligtvis ger aktuell tid. Det finns även NOW\(\) som visar både datum och tid. En sak som är väldigt trevligt för oss svenskar är att MySQL presenterar datumet i ett för oss väldigt vanligt format, nämligen det i använder i våra personnummer och tiden presenteras i 24- timmarsform som också passar oss2. Samma regler gäller vid inmatning av datum och tid.

MySQL är ju trots allt en Svensk produkt

MySQL är bra på att känna igen datum och klockslag i olika former så kommer man ihåg detta som kommer det att gå bra.

### Funktionen TO\_DAYS\(\)

Ibland vill man räkna hur långt det är mellan två datum. Då är det smidigt att räkna om datumen till dagar. Till detta finns funktionen TO\_DAYS\(\). Vill man veta hur många dagar det är kvar till midsommarafton så kan man göra det med nedanstående sats som också innehåller lite matematik. Jag kommer inte att behandla detta mer i detalj än så här just nu. Laborera och prova dig fram.

```text
mysql> SELECT TO_DAYS('2004-06-26') – TO_DAYS(CURDATE());
+--------------------------------------------+
| TO_DAYS('2004-06-26') - TO_DAYS(CURDATE()) |
+--------------------------------------------+
|                                        107 |
+--------------------------------------------+
1 row in set (0.00 sec)
```

### Funktionerna YEAR\(\), MONTH\(\) och DAYOFMONTH\(\)

Ofta vill man bryta upp ett datum i sina beståndsdelar. Det är MySQL väldigt bra på. Vill man till exempel veta hur många år en bil är så är man nog bara intresserad av vilket år det är nu och inte hela datumet. Vill man veta om det är den 15:e i vilken månad som helst måste man kunna välja bara dagen och vill man veta om det är månaden juni så är det smidigt med bara månaden. Några exempel:

```text
mysql> SELECT DAYOFMONTH('2003-12-21');
+--------------------------+
| DAYOFMONTH('2003-12-21') |
+--------------------------+
|                       21 |
+--------------------------+
1 row in set (0.00 sec)
mysql> SELECT MONTH('2003-12-21');
+---------------------+
| MONTH('2003-12-21') |
+---------------------+
|                  12 |
+---------------------+
1 row in set (0.00 sec)
mysql> SELECT YEAR('2003-12-21');
+--------------------+
| YEAR('2003-12-21') |
+--------------------+
|               2003 |
+--------------------+
1 row in set (0.01 sec)
```

Jag kommer inte att ta mer om detta nu utan laborera som vanligt vidare med dessa. Vill du lära dig mer om MySQL och datumfunktioner så rekommenderar jag följande webbadresser: MySQL-manualen: [http://www.mysql.com/doc/en/Date\_and\_time\_functions.html](http://www.mysql.com/doc/en/Date_and_time_functions.html) 

En artikel om datum- och tidsfunktioner i MySQL i två delar: [http://www.databasejournal.com/features/mysql/article.php/2172731](http://www.databasejournal.com/features/mysql/article.php/2172731) [http://www.databasejournal.com/features/mysql/article.php/2190421](http://www.databasejournal.com/features/mysql/article.php/2190421)

## Uppgifter 

Följande frågor skall du svara på. Visa eller lämna in dem till laborationshandledaren. Naturligtvis provkör du dem innan du skriver ner dem här.

### Uppgift 1 

Skriv en fråga som skriver ut hur många dagar det är till julafton.

### Uppgift 2 

Skriv en fråga som talar om hur många dagar du är.

### Uppgift 3 

Skriv en fråga som skriver ut följande:

```text
+-----------------+
| Person          |
+-----------------+
| Kalle Anka      |
| Kajsa Anka      |
| Knatte Anka     |
| Fnatte Anka     |
| Tjatte Anka     |
| Knase Anka      |
| Alexander Lukas |
+-----------------+
7 rows in set (0.00 sec)
```

### Uppgift 4 

Skriv en fråga som skriver ut alla som fyller år i oktober.

### Uppgift 5\* 

Skriv en fråga som skriver ut följande tabell:

```text
+------------------------------------+
| Biltabell                          |
+------------------------------------+
| Kalle Anka har en Saab 9-5         |
| Kajsa Anka har en Volvo S80        |
| Knatte Anka har en Mazda 626       |
| Tjatte Anka har en Audi A8         |
| Tjatte Anka har en BMW 323         |
| Fnatte Anka har en Ford Mondeo     |
| Tjatte Anka har en Volvo 740       |
| Tjatte Anka har en Volkswagen Golf |
| Kalle Anka har en Volkswagen Polo  |
| Kajsa Anka har en Toyota Carina II |
+------------------------------------+
10 rows in set (0.00 sec)
```

### Uppgift 6\*\* 

Skriv en fråga som skriver ut följande. Tänk på att rubriker och sortering.

```text
+--------------+------------------+-------+
| Ägare        | Bilmodell        | Ålder |
+--------------+------------------+-------+
| Anka, Fnatte | Ford Mondeo      |     3 |
| Anka, Kajsa  | Toyota Carina II |     6 |
| Anka, Kajsa  | Volvo S80        |     2 |
| Anka, Kalle  | Volkswagen Polo  |     1 |
| Anka, Kalle  | Saab 9-5         |     1 |
| Anka, Knatte | Mazda 626        |     3 |
| Anka, Tjatte | BMW 323          |     3 |
| Anka, Tjatte | Audi A8          |     3 |
| Anka, Tjatte | Volkswagen Golf  |    21 |
| Anka, Tjatte | Volvo 740        |    17 |
+--------------+------------------+-------+
10 rows in set (0.07 sec)
```

\\* Lite svårare uppgift  
\\*\* Lite Svårare uppgift

