---
description: Hur man läser textfiler och skriva i textfiler.
---

# Filhantering

## Filhantering

Innan vi går in på databashantering, så är det bra att känna till att det finns en enklare metod att spara data; att helt enkelt skriva dem till en fil på servern. Denna metod lämpar sig bäst när behöver en lagra mindre mängd data och inte har något behov av att sortera eller välja ut en delmängd av det sparade.

För att öppna en fil i PHP används [fopen\(](https://devdocs.io/php/function.fopen)\). Observera att vi måste ha rättighet att öppna filen. På **UNIX** och **Linux**-system finns ett rättighetssystem där man med hjälp av kommandot **chmod** ställer in vilka som har rättigheter att läsa och skriva filer. Just nu räcker det att känna till att ni behöver skriva:

```bash
chmod ugo+r filnamn
```

För att PHP ska kunna läsa filen. Det finns olika sätt att öppna en fil, vi kommer först att titta på möjligheten att öppna en fil för läsning. En komplett beskrivning av alla valmöjligheter finns i boken i avsnittet om filhantering. Vi ska titta på ett första exempel där vi läser hela filinnehållet i en fil och skriver ut det på skärmen.

### **Öppna fil för läsning**

```php
<?php
$fil = fopen("filnamn.txt", "r") or die("Kunde inte öppna fil");
$text = fread($fil, filesize("filnamn.txt"));
echo "<pre>$text</pre>";
fclose($fil);
?>
```

Den första raden öppnar filen. Den börjar med att beskriva vilken variabel som ska agera som filhandtaget. Filhandtaget använder vi för att komma åt filen. Det första argumentet till [fopen\(\)](https://devdocs.io/php/function.fopen) ****innehåller filnamnet. Eftersom vi inte skrivit in någon sökväg, antar PHP att vi menar en fil i samma katalog som skriptet ligger. Det andra argumentet "**r**" talar om att vi vill öppna filen för läsning \(**read**\). Till sist har vi hängt på en konstruktion som ser lite konstig ut, men vad den gör är att helt enkelt skriva ut raden "Kunde inte öppna fil" om inte filen fanns där vi trodde att den skulle finnas.

På rad 2 i skriptet läser vi in allt innehåll från filen i variabeln **$text**. Detta görs med [fread\(\)](https://devdocs.io/php/function.fread), som tar filhandtaget som första argument, och antalet tecken vi vill läsa in som andra argument. I detta fall vill vi läsa in hela filen, och då måste vi veta filstorleken, vilken vi får fram med funktionen [filesize\(\)](https://devdocs.io/php/function.filesize). På nästa rad skriver vi ut hela filen på skärmen. Vi använder HTML-taggen **&lt;pre&gt;** för att radbrytningar i filen också ska synas på webbsidan. Till sist stänger vi filen med hjälp av [fclose\(\)](https://devdocs.io/php/function.fclose).

### **Öppna fil för skrivning**

Nästa sak vi ska titta på är hur man öppnar en fil för skrivning. Med den metoden vi går igenom kommer allt innehåll från filen att raderas om filen existerar sedan tidigare. För att kunna skriva till en fil behöver vi en annan typ av filrättighet. Den får vi genom att skriva **chmod ugo+w filnamn.txt** vid kommandoprompten.

```php
<?php
$fil = fopen("filnamn.txt", "w") or die("Kunde inte öppna fil");
$text = "Hej hopp!";
fwrite($fil, $text);
fclose($fil);
echo "Texten $text har skrivits till fil.";
?>
```

[fopen\(\)](https://devdocs.io/php/function.fopen) används på nästan samma sätt, den enda förändringen är att vi bytt ut **r** mot **w** \(**write**\). För att skriva till filen använder vi [fwrite**\(\)**](https://devdocs.io/php/function.fwrite). Sedan är allt klart.

En specialfiness med [fopen\(\)](https://devdocs.io/php/function.fopen) är att man lika gärna kan använda den för att öppna en webbsida på en annan server:

```php
<?php
$fil = fopen("http://www.dn.se/", "r") or die("Gick ej");
$text = fread($fil, filesize("filnamn.txt"));
fclose($fil);
?>
```

Sedan kan man söka efter speciell information inuti texten, t.ex. för att ta ut viss information som man har användning för.

## Läsa in allt på en gång

### file\(\): läsa i en array

Med [file\(\)](https://devdocs.io/php/function.file) läses hela filen in i en array.

```php
<?php
$lines = file('http://www.example.com/');

foreach ($lines as $line_num => $line) {
    echo "Line #<b>{$line_num}</b> : " . htmlspecialchars($line) . "<br />\n";
}
?>
```

### file\_get\_contents: läsa i en sträng

Med [file\_get\_contents\(\)](https://devdocs.io/php/function.file-get-contents) läses hela filen i en sträng.

```php
<?php
$homepage = file_get_contents('http://www.example.com/');
echo $homepage;
?>
```

## Uppgifter filhantering

### **Uppgift 1**

Gör en webbapplikation som tar den inmatade texten ur ett formulärs "textarea" och sparar den i en fil.

### **Uppgift 2**

Gör en webbapp  som i en textruta frågar efter ett filnamn på servern. Öppna filen och skriv ut filinnehållet på skärmen.   
\(Om du kan, kontrollera före filnamnet så att det endast innehåller bokstäver, siffror och punkt.\)

### **Uppgift 3**

Utveckla webbappen i uppgift 1 till ett enkelt gästboksskript. Skapa en sida kallad "Lägg till gästbok", där användaren får fylla i namn, e-post-adress och meddelande. När användaren skickar i väg formuläret ska informationen sparas snyggt formaterad i en fil. Snyggt formaterad innebär att du har mellanrum mellan namnet och e-post-adressen, och ny rad \(&lt;br&gt;\) innan du skriver meddelandet, och dessutom ny rad \(&lt;br&gt;\) efter själva meddelandet. Obs! Använd append \(a\) som filöppningsmetod, ej write \(w\), eftersom du då skriver över tidigare innehåll! Längst ned på varje sida ska en rubrik med texten "Skrivet i gästboken" samt filinnehållet visas.

### **Uppgift 4**

Skapa ett loggningsskript som sparar en filrad om varje besök i en fil kallad "**log.txt**". Loggningsskriptet ska logga användarens IP-adress, och vilken sida användaren kom ifrån, och vilken webbläsare användaren hade. Variabler skickas till PHP med denna information.   
Skapa ett nytt PHP-skript, och skriv **&lt;?php phpinfo\(\) ?&gt;** så hittar du denna information längst ned på sidan.

### **Uppgift 5**

Gör en webbapp som kort presenterar den nuvarande kursen på Ericsson-aktien. Ta kontakt med tex. [aktiekurser](http://www.privataaffarer.se/borsguiden/aktiekurser) för att ta reda på kursen.

{% hint style="info" %}
Från PHP-kompendiet av Thomas Höjemo, © SNT 2006, www.snt.se
{% endhint %}

