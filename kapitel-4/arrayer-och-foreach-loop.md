---
description: Att använda arrayer.
---

# Arrayer och foreach-loop

## Arrayer

![Sk&#xE5;p med 3 l&#xE5;dor](../.gitbook/assets/image%20%286%29.png)

En [array ](https://devdocs.io/php/function.array)är en samling av variabler, tänk er ett helt skåp med kökslådor. Matrisen är då hela skåpet och innehåller flera kökslådor. I varje kökslåda finns ett innehåll dvs ett värde. I de flesta programmeringsspråk så börjar man av någon outgrundlig anledning alltid att räkna från och med **0** i stället för **1**. Detta innebär att den första "lådan" / indexet är **0**, den andra **1** och så vidare. För att skapa den här matrisen i form av en kökslåda i PHP skulle vi göra så här:

```php
<?php
$koksskap[0] = "bestick";
$koksskap[1] = "servetter";
$koksskap[2] = "påsar";
?>
```

Vi fyller alltså helt enkelt "lådorna" en i taget med innehåll. Vi behöver inte ens ta med siffrorna, utan kan låta PHP räkna ut dessa åt oss:

```php
<?php
$koksskap[] = "bestick";
$koksskap[] = "servetter";
$koksskap[] = "påsar";
?>
```

Detta ger alltså samma resultat. För att sedan komma åt innehållet i respektive låda \(värdet\) så gör vi så här:

```php
<?php
$koksskap[0] = "bestick";
$koksskap[1] = "servetter";
$koksskap[2] = "påsar";
echo "<p>Översta lådan innehåller $koksskap[0] </p>";
echo "<p>Mittenlådan innehåller $koksskap[1] </p>";
echo "<p>Understa lådan innehåller $koksskap[2] </p>";
?>
```

Man kan i stället för att använda 0, 1, 2 ge strängnamn åt indexen.

```php
<?php
$koksskap["topp"] = "bestick";
$koksskap["mitten"] = "servetter";
$koksskap["botten"] = "påsar";
echo "<p>Översta lådan innehåller $koksskap["topp"] </p>";
echo "<p>Mittenlådan innehåller $koksskap["mitten"] </p>";
echo "<p>Understa lådan innehåller $koksskap["botten"] </p>";
?>
```

När använder man sig då av matriser? Man skulle ju i princip lika gärna kunna använda sig av variabler var och en för sig. Det finns några olika anledningar. Bland annat kan man på ett enkelt sätt sortera i [array](https://devdocs.io/php/function.array). Man kan också enkelt systematiskt gå igenom en [array ](https://devdocs.io/php/function.array)och använda alla värdena. När man använder sig av funktioner kommer ofta returvärdet i form av en matris.

Genom [unset\(\)](https://devdocs.io/php/function.unset) kan man ta bort element ur matriser:

```php
$namn[0] = "Gult";
$namn[1] = "Blått;
unset($namn[0]);
```

Nu togs alltså elementet Gult med nyckeln / indexet **0** bort ur matrisen.

## **foreach-loopen**

Tillsammans med [arrayer ](https://devdocs.io/php/function.array)används ofta [foreach-loopen](https://devdocs.io/php/control-structures.foreach). Den går igenom arrayen ett index i taget.

```php
<?php
$domains['se'] = "Sverige";
$domains['de'] = "Tyskland";
$domains['no'] = "Norge";
foreach ($domains as $index => $varde) {
    echo "<p>$index är landskod för $varde </p>";
}
?>
```

Detta exempel skriver ut följande på skärmen:

```php
se är landskod för Sverige
de är landskod för Tyskland
no är landskod för Norge
```

### **Sortera en array**

Funktionen sort sorterar [arrayen ](https://devdocs.io/php/function.array)efter deras värde, se följande exempel:

```php
<?php
$tal[] = 321;
$tal[] = 3;
$tal[] = 7;
sort($tal);
foreach ($tal as $a) {
    echo "<p>" . $a . "</p>";
}
?>
```

Detta exempel sorterar helt enkelt talen i nummerordning och skriver sedan ut dem i tur och ordning. Fler exempel på sorteringsfunktioner finns i boken i kapitlet om matriser.

## **Strängar och arrayer**

### **Dela upp en sträng med explode\(\)**

Med hjälp av [explode\(\)](https://devdocs.io/php/function.explode) kan man dela upp en vanlig sträng i bitar och "stoppa in" bitarna i en array.

```php
$text = "detta är en testtext.";
$pattern = " ";
$ord = explode($pattern, $text);
echo "$ord[2] $ord[3] $ord[1] $ord[0]";
```

I exemplet delas först upp innehållet i variabeln text i delar med mellanslag som skiljetecken. Inuti ord kommer först på position **0** att finnas "detta", därefter "är" på position **1** osv.

### **Slå samman en array med implode\(\)**

Med [implode\(\)](https://devdocs.io/php/function.implode) så gör vi tvärtom - slår samman delarna i en [array ](https://devdocs.io/php/function.array)till en vanlig sträng. 

```php
$ord[0] = "detta";
$ord[1] = "är";
$ord[2] = "en";
$ord[3] = "variabel";
echo implode(" ", $ord);
```

I det här fallet så slås alla delarna i matrisen **$ord** ihop, ett mellanslag läggs i varje sammanfogning och resultatet skrivs ut.

### String som en array

Man kan också använda array-notationen för komma bokstäverna i en sträng.

```php
$meddelande = "hello world";
echo $meddelande[0]; // -> h
```

## **Skapa matriser automatiskt i formulär**

Genom att avsluta namnet på till exempel en textruta med hakparanteser, exempelvis **namn\[\]** skapar automatiskt en motsvarande [array ](https://devdocs.io/php/function.array)i PHP.

```markup
<form action="phpskript.php" method="post">
    <input type="text" name="namn[]">
    <input type="text" name="namn[]">
    <input type="submit">
</form>
```

I det här fallet får **$\_POST\['namn'\]\[0\]** innehållet som skrivits i den första textrutan och **$\_POST\['namn'\]\[1\]** innehållet i den andra textrutan.

## Uppgifter

### **Uppgift 1**

Skapa ett skript med ett formulär där användaren kan mata in **5 st namn**.  
Kalla textrutorna för **namn\[\]**. [**Sortera** ](https://devdocs.io/php/function.sort)sedan namnen och skriv ut dem i bokstavsordning, ett på varje rad.

![](../.gitbook/assets/image%20%2821%29.png)

### **Uppgift 2**

Utveckla skriptet i uppgift 1 så att det skriver ut namnen i en **tabell med ett radnummer** först i tabellraden.   
Tabellraderna ska ha **alternerande** färger, \(den första raden i grått den andra i vitt osv\).

### **Uppgift 3**

Skapa ett skript där användaren matar in ett tal **1-9** och sedan returnerar det svenska namnet för talet \(**ett, två, tre osv**\).   
Om talet är större än 9 så returnerar du i stället talet som vanligt \(tex. 11\). 

![](../.gitbook/assets/image%20%2822%29.png)

### **Uppgift 4**

Utöka skriptet i uppgift 3 så att användaren matar in **två siffror**, lägger ihop dem och presenterar resultatet i bokstavsform. \(Ex: **fyra plus tre blir sju**.\)

## Extra uppgifter för loopar

### Uppgift 5

Skapa ett skript som skriver ut talen **19** till **1** med hjälp av en loop.  
Ett tal ska skrivas ut per rad, **19** ska skrivas på första raden och **1** på den sista.

### Uppgift 6

Skapa ett skript som skriver ut vart **5:e årtal** på 1500-talet med början på 1595 och sedan nedåt.  
Det vill säga 1595, 1590, 1585 och så vidare ända till 1500.

### Uppgift 7

Skapa ett skript som ber användaren mata in ett **meddelande**.  
Skriptet skriver sedan ut ett meddelande **vertikalt**, en bokstav per rad.  
Meddelandet ska dessutom skrivas ut **baklänges**.

## Extra uppgifter för arrayer

### Uppgift 8

Skapa ett skript som ber användaren om ett **heltal**.  
Berätta för användaren om någon av siffrorna **3** eller **7** fanns i talet.

### Uppgift 9

Skapa ett skript som innehåller en **array** som ska innehålla namnen på tre svenska städer.   
Skriv in två av namnen i koden \(hårdkoda\) men låt användaren få skriva in namnet på den tredje staden. Skriv avslutningsvis ut alla stadsnamnen på **samma rad**.

### Uppgift 10

Skapa ett skript som innehåller en **array** med **strängar** där varje sträng är en **mening**.   
Skriv ut varje mening med hjälp av en **loop.**  
Gör så att varje mening hamnar i ett eget **stycke**.

### Uppgift 11

Skapa ett skript som innehåller en **array** med 10 heltal.   
Gå igenom arrayen med hjälp av en **loop** och hitta det största talet i arrayen.

### Uppgift 12

Skapa ett skript som innehåller en array med minst **5** årtal, minst ett av årtalen ska finnas med **två gånger**. 

Användaren ska få skriva in ett **årtal** när programmet körs.   
Skriptet ska skriva ut **alla index** som detta årtal finns på i arrayen.   
Om årtalet inte fanns på någon plats så ska programmet skriva "**Årtalet kunde inte hittas**".

### Uppgift 13

Skapa ett skript som innehåller en array med minst **5** heltal.   
Beräkna summan av alla heltal i arrayen med hjälp av en **foreach**-loop.

### Uppgift 14

Skapa ett skript där användaren själv väljer hur många **heltal** hen vill skriva in i en **array**.   
Efter att användaren har skrivit in alla tal ska skriptet välja ett av talen som skrevs in slumpvis och därefter skriva ut detta tal samt vilket index detta tal hade i arrayen. Se funktionen [rand\(\)](https://devdocs.io/php/function.rand).

### Uppgift 15

Skapa ett skript där användaren får skriva in en **mening**.   
Skapa en **array** där varje ord i meningen blir ett element i arrayen.   
Skriv därefter ut varje ord i meningen på en egen rad med radnummer.

