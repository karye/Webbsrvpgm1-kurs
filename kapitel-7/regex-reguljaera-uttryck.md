---
description: Söka i text med regex.
---

# Regex - reguljära uttryck

## **Testa reguljära uttryck**

* Du kan enkelt testa dina regex på [phpliveregex](https://www.phpliveregex.com/).

## preg\_match\(\): söka med reguljära uttryck

Med reguljära uttryck kan man göra en sk. mönstermatchning av ett uttryck. Reguljära uttryck tillhör de svåraste områdena av PHP. I kapitlet om strängar i boken finns en utförligare beskrivning av reguljära uttryck. De används ofta för att göra en kontroll av inkommande formulärdata för att säkerställa att dessa håller sig inom vissa givna ramar och därigenom säkra programmet från angrepp och fel.

Det finns två olika typer av reguljära uttryck i PHP, Posix-kompatibla och Perl-kompatibla. I grundsyntaxen är de ganska lika men de Perl-kompatibla reguljära uttrycken har fler avancerade funktioner. I PHP-manualen på [pcre.pattern.syntax](http://php.net/manual/en/pcre.pattern.syntax.php) finns en detaljerad guide. Vi börjar med ett enkelt exempel:

```php
$text = "Test 123";
if (preg_match("/123/",$text)) {
    echo 'Variabeln $text innehåller 123';
} else {
    echo 'Variabeln $text innehåller inte 123';
}
```

Funktionen [preg\_match\(\)](http://php.net/manual/en/function.preg-match.php) används för mönstermatchning. Sökbegreppet står alltid mellan snedstreck. I exemplet söker vi efter teckenföljden 123 i strängen **$text**.

### **Matcha vissa tecken**

```php
$text = "Test 123";
if (preg_match("/[a-zåäö]/",$text)) {
    echo 'Variabeln $text innehåller minst en bokstav';
} else {
    echo 'Variabeln $text innehåller inte några bokstäver';
}
```

Genom att använda hakparanteser kan vi specificera en följd av tecken i mönstret. Strängen kommer att matchas om det finns minst en av de gemena \(små\) bokstäverna a-z, å, ä eller ö i den.

### **Negativ matchning**

```php
$text = "Test 123";
if (preg_match("/[^0-9]/",$text)) {
    echo "Variabeln innehåller minst ett tecken som inte är en siffra";
}
```

Genom att sätta **^** direkt till höger om hakparantesen inverteras mönstret.

### **Matcha oberoende av små och stora bokstäver**

```php
$text = "Test 123";
if (preg_match("/[a-zåäö]/i",$text)) {
    echo 'Variabeln $text innehåller minst en bokstav';
} else {
    echo 'Variabeln $text innehåller inte några bokstäver';
}
```

Genom växeln **/i** som står för case-insensitive så matchar vi både små och stora bokstäver.

### **Matcha ett visst antal av ett mönster**

Genom specialtecknen **?**, **\*** och **+** kan vi matcha 0 eller 1, 0 eller flera respektive 1 eller flera av ett visst mönster.

```php
$text = "abbc";
if (preg_match("/ab+c/", $text)) {
    echo "Innehåller ett a följt av ett eller flera b följt av ett c";
}
```

Med **+** matchar vi ett eller flera b:n enligt ovan.

```php
$text = "abbc";
if (preg_match("/ab{1,2}c/", $text)) {
    echo "Innehåller ett a följt av ett eller två b följt av ett c";
}
```

Det går också att specificera exakt antal av ett visst tecken. Det gör man genom att skriva **{x,y}** där x står för minsta antal och y för största antal.

### **Matcha från början till slutet av en sträng**

Hur gör vi då om vi ska kontrollera att strängen endast innehåller bokstäver och inget annat?

```php
$text = "Test 123";
if (preg_match("/^[a-zåäöA-ZÅÄÖ]+$/",$text)) {
    echo 'Variabeln $text innehåller bara bokstäver';
} else {
    echo 'Variabeln $text innehåller inte bara bokstäver';
}
```

Här ser vi några små förändringar. Tecknet **^** står för "början av strängen" när det kommer som första tecken inuti mönstret. Detta innebär att strängen måste börja med en bokstav. Tecknet **+** står för "en eller flera av föregående mönster". Till sist kommer **$** som står för "slutet av strängen" när den är inskriven på sista platsen i mönstret.

Observera att **+** måste vara med annars matchar vi bara strängar med endast ett tecken! Genom växeln **/m** kan man använda **^** och **$** rad för rad i strängen. Detta innebär att mönstret endast behöver matcha minst en rad i stället för hela strängen.

### **Alternativmönster**

```php
$text = "gurka";
if (preg_match("/banan|gurka/", $text)) {
    echo 'Variabeln $text innehåller banan eller gurka';
} else {
    echo 'Variabeln $text innehåller varken banan eller gurka';
}
```

Specialtecknet **\|** betyder **eller** - matcha ett visst mönster eller ett annat.

### **Delmönster**

Genom att använda parenteser kan man gruppera mönstret i delmönster.

```php
$text = "använd";
if (preg_match("/använd(armanual|ningsområde|)/", $text)) {
    echo "Matchar använd, användarmanual, användningsområde";
}
```

Mönstret matchar använd, eftersom det är tomt till höger om den sista **\|**.

## **preg\_replace\(\): byta ut text mot en annan text**

Funktionen [preg\_replace\(\)](http://php.net/manual/en/function.preg-replace.php) byter ut en viss text mot en annan.

```php
$text = 'Min e-post-adress är thohoj02@student.chalmers.se';
$pattern = 'thohoj02@student.chalmers.se';
$replace = "thomas@snt.se";
$nytext = preg_replace("/$pattern/", $replace, $text);
echo $nytext;
```

Det första argumentet är mönstret som ska sökas efter, den andra strängen som det ska ersättas med och det tredje variabeln som ska sökas igenom. Som returnerat värde från kommer variabeln med innehållet ersatt enligt önskemålet.

## **Lathund för reguljära uttryck**

```text
\ generellt escape-tecken
\n matchar ny rad-tecken – newline
\t matchar tabb-tecken
\d siffra - samma sak som [0-9]
\D inte siffra - samma sak som [^0-9]
\s matchar mellanrumstecken - mellanslag, ny rad, tabb, formfeed, return
\S matchar allt utom mellanrumstecken
^ matchar från början av sträng (eller början av rad med växeln /m )
\A matchar från början av sträng (oberoende av växeln /m )
$ matchar till slutet av sträng (eller slutet av rad med växeln /m )
\Z matchar till slutet av sträng (oberoende av växeln /m )
. matchar vilket tecken som helst för utom ny rad-tecken ( \n )
[a-z] teckenföljd
| logiskt "eller"
(x) delmönster
? matchar 0 eller 1 av föregående mönster
* matchar 0 eller fler av föregående mönster
+ matchar 1 eller fler av föregående mönster
{x,y} matchar mellan x och y gånger av föregående mönster
```

## Uppgifter - reguljära uttryck

### **Uppgift 1**

Gör ett formulär där användaren ska fylla i en text.   
Kontrollera med ett reguljärt uttryck att texten innehåller ett "**t**" följt av ett eller två "**o**", dvs "**to**" eller "**too**". Endast små bokstäver ska matchas.  
Prova med Unicode tecknet '[✓](https://www.compart.com/en/unicode/U+2714)' och '[✕](https://www.compart.com/en/unicode/U+2715)'.

![](../.gitbook/assets/image%20%2858%29.png)

### **Uppgift 2**

Gör ett formulär där användaren ska fylla i en längre text.   
Kontrollera med ett reguljärt uttryck att texten matchar en sträng som börjar med "**Det var en gång**". Det spelar ingen roll om det första d:et är **stort** eller **litet**.

![](../.gitbook/assets/image%20%2859%29.png)

### **Uppgift 3**

Gör ett formulär där användaren ska fylla i en text.   
Konstruera ett reguljärt uttryck som ska kontrollera adresser som ska föras in i en databas. Adresserna får endast bestå av **små** och **stora** bokstäver, **punkt**, **siffror** och **mellanslag**. Använd [preg-match-all\(\)](https://devdocs.io/php/function.preg-match-all).

![](../.gitbook/assets/image%20%2857%29.png)

### **Uppgift 4**

Gör ett formulär där användaren ska fylla i ett domännamn. Kontrollera sedan att domännamnet slutar på .**com**, **.net** eller **.org**. Du ska också kontrollera att de övriga tecknen endast består av bokstäver **a-z**, siffror **0-9** eller bindestreck \(**-**\). Första tecknet måste vara en bokstav. Domännamnet ska vara minst **6** tecken och högst **200** tecken långt.

![](../.gitbook/assets/image%20%2854%29.png)

### **Uppgift 5**

Skapa en webbapplikation som testar styrkan på ett **lösenord** mha reguljära uttryck. Se tidigare uppgift i tidigare kapitel.

![](../.gitbook/assets/image%20%2862%29.png)

{% hint style="info" %}
Från PHP-kompendiet av Thomas Höjemo, © SNT 2006, www.snt.se
{% endhint %}

