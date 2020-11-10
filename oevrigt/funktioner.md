---
description: Hur man återanvänder kod.
---

# Funktioner

## Funktioner

Funktioner fungerar ungefär som ett snabbkommando för att göra en lång lista av kommandon i ett svep. Därmed slipper man upprepa kod i programmet, vilket gör det lättare att skriva och uppdatera. Förutom de många funktioner som PHP har inbyggt, kan man alltså skapa egna funktioner. Följande exempel skriver ut en början på ett HTML-dokument:

```php
<?php
function starthtml() {
    echo "<!DOCTYPE html><html><head><title></title></head><body>";
}
starthtml();
echo "testdokument";
echo "</body></html>";
?>
```

Det första vi gör är att deklarera funktionen. Detta gör vi med hjälp av [function\(\)](https://devdocs.io/php/functions.user-defined) följt av namnet på funktionen och sedan två paranteser. Längre ned i koden anropar vi funktionen. Detta gör vi genom att skriva funktionsnamnet följt av två paranteser.

**Skicka med argument**

Vi kan modifiera funktionen så att den tar emot argument. Argument skickas till funktionen och används sedan på något sätt inuti funktionen.

```php
<?php
function starthtml($title) {
    echo "<!DOCTYPE html><html><head><title>$title</title></head><body>";
}
starthtml("Test");
echo "testdokument";
echo "</body></html>";
?>
```

Nu har vi alltså gjort funktionen en aning mer flexibel, genom att vi kan ändra titeln på sidan. Vi skickar med strängen med innehållet **Test**, denna läggs sedan i variabeln **$title** efter funktionsanropet. Sedan kan funktionen använda denna variabel, i det här fallet för utskrift.

**Utgå från ett standardvärde**

En funktion kan definieras så att den har ett standardvärde, som används om inget värde anges vid funktionsanropet.

```php
<?php
function fargad_text($text = "exempeltext", $farg = "green") {
    echo "<p style=color:'$farg';> $text </p>";
}
?>
```

I exemplet ovan tar funktionen **fargad\_text\(\)** två argument. **$text** har standardvärdet "exempeltext" och **$farg** standardvärdet "green". Om man anropar funktionen utan några argument kommer standardvärdena att användas.

```php
fargad_text("annan text");
```

Skickas endast ett argument används det för **$text** och **$farg** behåller sitt standardvärde.

**Returnera ett värde**

Funktioner kan också returnera ett värde. Låt oss titta på ett exempel på detta.

```php
<?php
function area_cirkel($radie) {
    $area = $radie * $radie * M_PI;
    return $area;
}
echo area_cirkel(10);
?>
```

I och med att vi använder return skickas variabeln **$omkrets** innehåll tillbaka till det ställe som funktionen anropades från. \(**M\_PI** är en inbyggd konstant som innehåller ett värde av pi med många decimaler.\)

**Lokal räckvidd**

Det är viktigt att notera att variabler skapade inuti funktioner ej existerar utanför funktionens krullparanteser. Detta brukar på engelska kallas "**local scope**" dvs. lokal räckvidd. Se följande exempel:

```php
function berakna_summa($a, $b) {
    $summa = $a + $b;
    $c = 10;
    return $summa;
}
$resultat = berakna_summa($a, $b);
print $c;
```

Det första vi gör är att skapa funktionen **berakna\_summa\(\)**. Denna funktion tar två argument, **$a** och **$b**. Sedan lägger den ihop dessa två argument och stoppar i variabeln $summa. En ny variabel vid namn **$c** skapas på nästa rad. Men eftersom **$c** skapas inuti funktionen blir det en lokal variabel. Den existerar bara inom funktionens krullparanteser. När vi senare på sista raden försöker skriva ut variabeln **$c** kommer det inte att synas någonting på skärmen eftersom **$c** inte existerar utanför funktionen.

```php
function dubbla($a) {
    $a = $a * 2;
    global $c = 10;
    return $a;
}
$resultat = dubbla($a);
print $c;
```

I detta nya exempel kommer däremot 10 att skrivas ut. Detta eftersom vi talat om för PHP att **$c** ska vara en global variabel, som även existerar utanför funktionen den skapats i.

**Inbyggda funktioner**

PHP har massor med användbara inbyggda funktioner, som vi ska titta närmare på senare. En utmärkt referens till alla inbyggda funktioner är [PHP-manualen](http://php.net/manual).

## Uppgifter - funktioner

### **Uppgift 1**

Skriv en funktion som tar en variabel som argument och skriver ut följande på skärmen:

{% hint style="success" %}
Du skrev in variabeln: följt av innehållet i variabeln.
{% endhint %}

Testa sedan funktionen genom att skicka 456 i en variabel till den.

### **Uppgift 2**

Skriv en funktion som automatiskt returnerar argumentet med HTML-koder för fetstil och typsnittet Arial runt. Ex: Om man skickar "Rubrik" så ska funktionen skicka tillbaka **&lt;p style="font-family:Arial;"&gt;Rubrik&lt;/p&gt;**

### **Uppgift 3**

Skapa en funktion som tar två argument och skriver ut deras sammanlagda antal tecken på skärmen. Längden på en sträng fås genom den inbyggda funktionen [strlen\(\)](https://devdocs.io/php/function.strlen).

### **Uppgift 4**

Skapa en funktion som räknar ut omkretsen på en cirkel. Funktionen ska ta radien som ett argument. Definiera pi som en konstant i början av programmet, och använd 3,14 som ungefärligt mått på pi. Som en extrauppgift så avrunda värdet till närmaste heltal. Detta görs med den inbyggda funktionen [round\(\)](https://devdocs.io/php/function.round).

### **Uppgift 5**

Skapa ett program med en funktion **print\_table\_start\(\)** som skriver början på en tabell i html och tar ett argument i form av färgen på tabellen \(**red**, **blue** etc.\). Skapa en annan funktion som heter **print\_table\_row\(\)** och skriver ut en tabellrad och tar två argument, det som ska stå i första tabellcellen och det som ska stå i andra tabellcellen. Till sist skapar du en funktion kallad **print\_table\_end\(\)** som skriver ut slutet på tabellen. Ex på en tabell i html: **&lt;table&gt;** talar om att tabellen börjar. **&lt;tr&gt;** står för tabellrad, och **&lt;td&gt;** för tabellcell.

