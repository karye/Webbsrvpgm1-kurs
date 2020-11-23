---
description: Använda fritextsökning.
---

# Fritextsökning

I denna labb skall vi jobba vidare på att söka efter olika saker. Vi skall använda så kallade wildcards eller jokertecken som det kallas på svenska. Du skall ha gjort Laboration 1, 2, 3 och 4 innan du gör denna.

## Från förra laborationen

Från förra laborationen skall ni ha två tabeller som ser ut ungefär så här:

```sql
MariaDB [labb]> DESCRIBE bilar;
+-----------+-------------+------+-----+---------+----------------+
| Field     | Type        | Null | Key | Default | Extra          |
+-----------+-------------+------+-----+---------+----------------+
| id        | int(11)     | NO   | PRI | NULL    | auto_increment |
| reg       | varchar(10) |      |     |         |                |
| marke     | varchar(50) | YES  |     | NULL    |                |
| modell    | varchar(50) | YES  |     | NULL    |                |
| arsmodell | int(11)     | YES  |     | NULL    |                |
| pris      | int(11)     | YES  |     | NULL    |                |
| agare     | int(11)     | YES  |     | NULL    |                |
+-----------+-------------+------+-----+---------+----------------+
7 rows in set (0.00 sec)
MariaDB [labb]> DESCRIBE personer;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| fnamn | varchar(50) | YES  |     | NULL    |                |
| enamn | varchar(50) | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```

Dessa har ungefär följande innehåll:

```sql
MariaDB [labb]> SELECT * FROM bilar;
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
11 rows in set (0.00 sec)
MariaDB [labb]> SELECT * FROM personer;
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
7 rows in set (0.01 sec)
```

Ser inte era tabeller ut exakt så så gör det inget. Men de bör vara ungefär lika.

## Jokertecken

Ibland när man ställer frågor till en databas så vet man inte exakt vad man söker efter. Man kanske bara en del av ett namn eller så söker man något som man inte riktigt vet hur det stavas. Då använder man sig av jokertecken. Ett jokertecken, eller wildcard som det kallas på engelska är ett tecken som man använder för att representera inget, ett eller flera andra tecken. De jokertecken som vi använder i SQL är **% \(procent\)** och **\_ \(understreck\)**.   
Några exempel:

| A% | Matchar alla strängar som börjar på A oavsett längd |
| :--- | :--- |
| A\_\_ | Matchar alla strängar som börjar på A och har tre bokstäver |
| A\_\_% | Matchar alla strängar som börjar på A och har minst tre bokstäver |
| %A% | Matchar alla strängar som innehåller ett A |

### WHERE ... LIKE ...

För att använda jokertecken använder man LIKE istället för ”=”. Till exempel kan man gör som i exemplet nedan för att ta fram alla förnamn som börjar på K.

```sql
MariaDB [labb]> SELECT * FROM personer WHERE fnamn LIKE "K%";
+----+--------+-------+--------------+
| id | fnamn  | enamn | fodelsedatum |
+----+--------+-------+--------------+
|  1 | Kalle  | Anka  | 1934-07-09   |
|  2 | Kajsa  | Anka  | 1937-09-01   |
|  3 | Knatte | Anka  | 1937-10-17   |
|  6 | Knase  | Anka  | 1964-08-02   |
+----+--------+-------+--------------+
4 rows in set (0.00 sec)
```

### Escape-tecken

Antag att man vill söka efter något som innehåller just **%** eller, tex ”kalle\_anka”. Då blir det genast problem. Skriver man ”kalle\_anka” så kommer ju också ”kalle+anka” att stämma och alla andra strängar som består av ”kalle” och ”anka” med ett tecken mellan. Samma problem uppstår om man vill söka efter en sträng som innehåller " eller ” eftersom dessa tecken används för att avgränsa själva strängen. Till vår hjälp då finns escape-tecknen. Escape-tecken används då man vill att specialtecken skall förekomma i en sträng. Man säger på svengelska att dessa tecken skall ”escapas”. Escape-tecknet i SQL är  \(bakåtstreck eller backslash\). Tecket efter escape-tecknet är det som escapas. Till exempel så matchar \ just ett \_ \(understreck\).

| \\_ | Matchar \_ |
| :--- | :--- |
| \% | Matchar % |
| \\ | Matchar \ |
| \” | Matchar ” |
| \" | Matchar " |

## Uppgifter

Naturligtvis provkör du dem innan du skriver ner dem här.

### Uppgift 1 

Skriv en fråga som listar alla knattar.

### Uppgift 2 

Polisen är i farten, skriv en fråga som listar namnen på alla dem som har en bil vars registreringsnummer börjar på A. Skriv en fråga som listar dessa.

### Uppgift 3 

Polisen har nu fått in lite mer vittnesuppgifter de vill ha tag i namnen på alla personer som har en bil med ett registreringsnummer vars bokstavsdel börjar på A och sifferdel med 1. Skriv en fråga som listar dessa.

### Uppgift 4 

Skriv en fråga som talar om hur många bilar som har ett registreringsnummer som börjar på A. Det skall se ut så här:

```sql
+---------------------------------------+
| Antal bilar med reg som startar med A |
+---------------------------------------+
|                                     2 |
+---------------------------------------+
1 row in set (0.13 sec)
```

### Uppgift 5 

Polisen igen, den här gången har de i en utredning fått tag på en del av ett papper. Det är sönderrivet men lite går att tyda. Det är ett brev som är adresserat till en person som heter något som börjar på ”Kn” och slutar på ”e” med ett efternamn som börjar på ”A”. Skriv en fråga som listar de som det kan vara.

### Uppgift 6 

Skriv en fråga som visar förnamnet på alla de som har ett \_ understreck i efternamnet.

### Uppgift 7 

Skriv en fråga som listar alla bilar med ett ”a” någonstans i namnet. Bokstaven a måste finnas på någon annan plats än första och sista bokstaven. Det gör inget om första eller sista bokstaven är ett ”a” men det måste då även finnas ett ”a” på någon annan plats i namnet.  
Lite krystat, jag vet, men det är mycket användbart i andra sammanhang.