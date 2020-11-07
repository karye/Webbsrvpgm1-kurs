---
description: Hur man skickar data till en server.
---

# HTML och formulär

## **Formulär i HTML**

![](../.gitbook/assets/image%20%287%29.png)

Ett program eller ett skript är inte särskilt meningsfullt om det inte kan fråga efter information i från användaren. I vanliga program matar användaren oftast in information från en kommandoprompt, eller vanligare nuförtiden, genom att fylla i en dialogruta eller välja ett menyalternativ. För att få in information från användaren till ett PHP-skript används formulär. Formulär ingår som en del i html-standarden

Processen går alltså till på detta sätt:

1. Användaren fyller i ett formulär på en webbsida \(HTML-dokument\).  
****2. Formulärinformationen skickas till PHP-skriptet på webbservern.  
3. PHP-skriptet behandlar informationen.  
4. PHP-skriptet skriver ut en webbsida som användaren får som respons.

### **Form-taggen omsluter formuläret**

 Först ska vi titta på hur man utformar själva formuläret i html. Detta kan göras dels genom att koda för hand i ett redigeringsprogram som [VS Code](https://code.visualstudio.com/). Vi kommer att skriva koden för hand. Det första man behöver i ett formulär är två stycken [form](https://devdocs.io/html/element/form)-taggar som omsluter själva formuläret:

```markup
<form action="phpskript.php" method="post">
</form>
```

 **Action** talar här om sökvägen till det PHP-skript som ska ta hand om formulärinnehållet. Med **method** specificerar vi med vilken metod formulärdata ska sändas iväg. Det finns två metoder: **get** och **post**. Används metoden **get** skickas informationen med i adressen till PHP-skriptet. Denna metod används ofta av sökmotorer. Det kan t.ex. se ut så här: Man använder vanligen i stället **post**, eftersom man med **get** inte kan skicka mer än c:a 250 tecken. Med **post**-metoden så paketeras informationen och skickas med m.h.a. http-protokollet. Detta har också den fördelen att användaren inte ser all teknisk information som skickas - ett sätt att "gömma" information som skickas mellan webbsidorna.

#### **&lt;input type="text"&gt; ger en vanlig textruta**

Om vi matar in form-koden i föregående stycke, kommer ingenting alls att visas i webbläsaren. Vi behöver också ha rutor där användaren kan fylla i information. Ett vanligt textfält skrivs med [input](https://devdocs.io/html/element/input):

```markup
Ditt förnamn: <br>
<input type="text" name="fornamn" value="skriv här" size="30">
```

Nästan alltid har man en beskrivning av formulärfältet till vänster, så att användaren vet vad som ska fyllas i. Sedan kommer själva html-taggen. **name** måste finnas med - detta för att php senare ska kunna särskilja just detta fält och dess innehåll. När formuläret skickas iväg kommer nämligen automatiskt en variabel skapas med namnet **$fornamn** som innehåller det användaren har fyllt i detta fält. Observera att man ej bör ha svenska bokstäver i **name**-attributet. **value** används oftast inte, men ger ett standardvärde i fältet. Till sist bestämmer vi hur många tecken brett formulärfältet ska vara med **size**.

#### **&lt;input type="password"&gt; - skapar lösenordsruta**

Det här fältet fungerar precis som textrutan, med den skillnaden att det visas stjärnor när man fyller i fältet. Observera att informationen skickas helt i klartext till servern så ska man tillhandahålla känslig information med access via ett formulär är det lämpligt att skaffa en server med krypteringsfunktion.

Så här ser taggen ut:

```markup
Lösenord: <input type="password" name="losenord">
```

#### **&lt;input type="checkbox"&gt; - ger en kryssruta**

Det här fältet fungerar precis som kryssrutorna i t.ex. Windows - de kan antingen vara ikryssade eller ej ikryssade. Ett exempel:

```markup
<h2>Vilka semesterorter har du besökt</h2>
<input name="azorerna" type="checkbox" value="1"> Azorerna<br>
<input name="mallorca" type="checkbox" value="1"> Mallorca<br>
<input name="teneriffa" type="checkbox" value="1"> Teneriffa
```

**name** talar om vilket namn variabeln kommer att få. Har användaren t.ex. kryssat i rutorna för Azorerna och Mallorca, kommer variabeln **$azorerna** få värdet 1, **$mallorca** också värdet 1, medan variabeln **$teneriffa** kommer att vara tom.

#### **&lt;input type="radio"&gt; - skapa radioknappar**

Det finns ytterligare en typ av knapp, nämligen radioknappar. Ni känner säkert igen denna från Windows också. Den används när man ska välja ett, och endast ett alternativ av flera i en grupp. T.ex. om man behöver skriva in åldern – en person kan ju inte gärna ha två åldrar samtidigt! Vi kan ju tänka oss följande exempel vid beställning av en färdbiljett:

```markup
<input name="alder" type="radio" value="barn"> Under 16 år<br>
<input name="alder" type="radio" value="ungdom"> 16 - 25 år<br>
<input name="alder" type="radio" value="vuxen"> Över 25 år
```

  
****[input](https://devdocs.io/html/element/input)-taggen i exemplet har vi med för att få ny rad. Observera att det här är viktigt att alla radioknappar i samma grupp \(de man ska välja bland\) har samma **name**-attribut. Hade vi gett dem olika namn hade vi kunnat kryssa i alla rutorna, vilket inte hade varit så bra. I stället särskiljer vi respektive fält med olika värden i **value**. Om vi i exemplet fyllt i vuxen, så kommer PHP-skriptet att ta emot en variabel med namnet **$alder** och innehållet "vuxen".

#### **&lt;textarea&gt; - flerradiga textfält**

Flerradiga textfält används bland annat i webbmailtjänster som t.ex. gmail.com för att skriva in meddelandetexten. Då används [textarea](https://devdocs.io/html/element/textarea)-fältet i HTML-koden.

```markup
<textarea name="meddelande">
</textarea>
```

### **Andra formulärfält**

Det finns några till, mer ovanliga formulärfält, bland annat "dropdown"-menyer.

**&lt;input type="submit"&gt; - skicka iväg formuläret**

Till sist behöver vi en knapp som skickar iväg formulärinnehållet till servern. Detta gör vi med en submit-knapp.

```markup
<button type="submit">Skicka</button>
```

### **Komplett formulärexempel**

Så är det dags att binda ihop allting och skapa ett komplett formulär. Vi börjar med ett enkelt exempel:

```markup
<!DOCTYPE html>
<html>
        <meta charset="utf-8">
        <title></title>
        <link rel="stylesheet" href="style.css">
</head>
<body>
    <form action="phpskript.php" method="post">
        <h1>Biljettbokning</h1>
        <h2>Hur gammal är du</h2><input name="alder" type="radio" value="barn">
        Under 16 år<br>
        <input name="alder" type="radio" value="ungdom"> 16 - 25 år<br>
        <input name="alder" type="radio" value="vuxen"> Över 25 år<br>
        <button type="submit">Skicka</button>
    </form>
</body>
</html>
```

För att ta emot formulärinnehållet behöver vi också ett PHP-skript i "andra änden". Det kan till exempel se ut så här:

```php
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
    <?php
    echo "Vänta medan priset för din ";
    echo $_REQUEST['alder'];
    echo "-biljett räknas ut.";
    ?>
</body>
</html>
```

Alla formulärdata som skickats lagras i arrayen [$\_REQUEST](https://devdocs.io/php/reserved.variables.request). Hade formulärfältet i stället hetat namn skulle innehållet ha funnits i **$\_REQUEST\['namn'\]**.

## Uppgifter - HTML och formulär

Observera att dessa övningar endast innefattar HTML, i nästa övningsmoment ska du bygga på övningarna med kod i PHP som tar emot formulärinnehållet. Kod för formulär-element hittar du här: [https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic\_native\_form\_controls](https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic_native_form_controls)

### **Uppgift 1**

Gör ett formulär där användaren kan mata in två tal i två stycken **textrutor**.

![](../.gitbook/assets/image%20%2820%29.png)

### **Uppgift 2**

Gör ett komplett "kontaktformulär" med textrutor där du frågar efter **namn**, **epostadress** och **telefon**. Du ska även skapa en **kryssruta** där användaren kan bocka i sitt intresse för ett nyhetsbrev. Till sist ska du skapa två stycken **radioknappar**, där användaren kan välja mellan att bli kontaktad per telefon eller e-post.

![](../.gitbook/assets/image%20%2819%29.png)

### **Uppgift 3**

Skapa en sida där besökaren ska välja sin favoritfilm av tre olika filmer. Besökaren ska dessutom välja sin favoritbok bland tre olika böcker. Det ska gå att välja högst en bok och en film.

![](../.gitbook/assets/image%20%2823%29.png)

### **Uppgift 4**

Utforma ett formulär på en sida där användaren ska mata in en temperatur i Celsius.

![](../.gitbook/assets/image%20%2828%29.png)

### **Uppgift 5**

På din webbsida vill du ha ett formulär där besökaren kan lämna kommentarer. Kommentarerna ska kunna skrivas i ett **flerradstextfält**. Dessutom ska det finnas en vanlig **textruta** för att fylla i namn. På knappen för att skicka iväg formuläret ska det stå "Skicka kommentarer".

![](../.gitbook/assets/image%20%2827%29.png)

{% hint style="info" %}
Från PHP-kompendiet av Thomas Höjemo, © SNT 2006, www.snt.se  
[http://www.snt.se/phpkompendium.pdf](http://www.snt.se/phpkompendium.pdf)  
[http://www.snt.se/phpfacit.pdf](http://www.snt.se/phpfacit.pdf)
{% endhint %}

