---
description: Att använda arrayer
---

# Arrayer och foreach-loop

## Arrayer

En array är en samling av variabler, tänk er ett helt skåp med kökslådor. Matrisen är då hela skåpet och innehåller flera kökslådor. I varje kökslåda finns ett innehåll dvs ett värde. I de flesta programmeringsspråk så börjar man av någon outgrundlig anledning alltid att räkna från och med **0** i stället för **1**. Detta innebär att den första "lådan" / indexet är **0**, den andra **1** och så vidare. För att skapa den här matrisen i form av en kökslåda i PHP skulle vi göra så här:

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

När använder man sig då av matriser? Man skulle ju i princip lika gärna kunna använda sig av variabler var och en för sig. Det finns några olika anledningar. Bland annat kan man på ett enkelt sätt sortera i matriser. Man kan också enkelt systematiskt gå igenom en matris och använda alla värdena. När man använder sig av funktioner kommer ofta returvärdet i form av en matris. Läs mer om matriser \([**array**](http://php.net/manual/en/language.types.array.php)\) på php.net .

Genom **unset\(\)** kan man ta bort element ur matriser:

```php
$namn[0] = "Gult";
$namn[1] = "Blått;
unset($namn[0]);
```

Nu togs alltså elementet Gult med nyckeln / indexet **0** bort ur matrisen.

## **foreach-loopen**

Tillsammans med matriser används ofta **foreach**-loopen. Den går igenom matrisen ett index i taget.

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

### **Sortera matriser**

Funktionen sort sorterar matriser efter deras värde, se följande exempel:

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

## **Dela upp en sträng med explode\(\)**

Med hjälp av **explode\(\)** kan man dela upp en vanlig sträng i bitar och "stoppa in" bitarna i en matris. Se [explode](http://php.net/manual/en/function.explode.php). Exempel:

```php
$text = "detta är en testtext.";
$pattern = " ";
$ord = explode($pattern, $text);
echo "$ord[2] $ord[3] $ord[1] $ord[0]";
```

I exemplet delas först upp innehållet i variabeln text i delar med mellanslag som skiljetecken. Inuti ord kommer först på position **0** att finnas "detta", därefter "är" på position **1** osv.

## **Slå samman en matris med implode**

Med **implode\(\)** så gör vi tvärtom - slår samman delarna i en matris till en vanlig sträng. Se [implode](http://php.net/manual/en/function.implode.php) på php.net.

```php
$ord[0] = "detta";
$ord[1] = "är";
$ord[2] = "en";
$ord[3] = "variabel";
echo implode(" ", $ord);
```

I det här fallet så slås alla delarna i matrisen **$ord** ihop, ett mellanslag läggs i varje sammanfogning och resultatet skrivs ut.

## **Skapa matriser automatiskt i formulär**

Genom att avsluta namnet på till exempel en textruta med hakparanteser, exempelvis namn\[\] så skapas automatiskt en motsvarande matris \(array\) i php.

```markup
<form action="phpskript.php" method="post">
    <input type="text" name="namn[]">
    <input type="text" name="namn[]">
    <input type="submit">
</form>
```

I det här fallet får **$\_REQUEST\['namn'\]\[0\]** innehållet som skrivits i den första textrutan och **$\_REQUEST\['namn'\]\[1\]** innehållet i den andra textrutan.

## Uppgifter - matriser och foreach-loopen

### **Uppgift 5.1**

Skapa ett formulär där användaren matar in **10 st namn**. Kalla textrutorna för **namn1, namn2 osv**. **Sortera** sedan namnen och skriv ut dem i bokstavsordning, ett på varje rad.

### **Uppgift 5.2**

Utveckla programmet i övning 1 så att det skriver ut namnen i en **tabell med ett radnummer** först i tabellraden. Tabellraderna ska ha **alternerande** färger, \(den första raden i grått den andra i vitt etc.\)

### **Uppgift 5.3**

Skriv en **funktion** som tar ett tal mellan 1 och 9 som ett argument och sedan returnerar det svenska namnet för talet \(**ett, två, tre osv**\). Om talet är större än 9 så returnerar du i stället talet som vanligt \(tex. 11\). Testa att funktionen fungerar som tänkt.

### **Uppgift 5.4**

Fortsätt med programmet i uppgift 3 och utöka programmet så att funktionen tar **två siffror**, lägger ihop dem och presenterar resultatet i bokstavsform. \(Ex: **fyra plus tre blir sju**.\)

