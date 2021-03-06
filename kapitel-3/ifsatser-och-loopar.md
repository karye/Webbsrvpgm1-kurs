---
description: 'Operatorer, villkorssatser och loopar'
---

# if-satser och loopar

## **Operatorer**

Det finns ett antal olika operatortyper i PHP. Från matematiken känner vi igen de [aritmetiska operatorerna](https://devdocs.io/php/language.operators.arithmetic), t.ex. **+, -, \*** och **/**. Dessa har vi tittat på tidigare. Tilldelningsoperatorn kallas likamed-tecknet \(=\). Den har vi också använt oss av för att ge en variabel ett värde. Några exempel:

```php
<?php
$a = 324;           // Ger $a värdet 324
$a = a + 1;         // Ökar $a med 1 till 325
$a = berakna(12);   // $a får returvärdet av funktionen berakna
?>
```

Ett ytterligare exempel på en operator är strängkonkateneringsoperatorn \(rekordlångt namn\). Den består av en punkt och gör med strängar vad + gör med siffror:

```php
<?php
$namn = "Thomas";
$a = "Hej " . $namn;
?>
```

Två andra vanliga operatorer är villkorsoperatorer och logiska operatorer. De används ofta tillsammans, vilket vi kommer att se nu.

## **Styrstrukturer**

Hittills har alla program vi skrivit körts igenom rad för rad, utan att vi kunnat styra in programmet på olika vägar beroende på vad användaren har matat in. Det är detta vi har styrstrukturer till.   
**Styrstrukturer** har det gemensamt att de kontrollerar om ett uttryck stämmer med ett annat och sedan beroende på resultatet gör ett val. På detta sätt kan man skriva mycket mer flexibla program. Det finns två huvudtyper av styrstrukturer: **villkorssatser** och **loopar**. Vi börjar med villkorssatser.

### Villkorssatser: if-satsen

```php
<?php
if ($losenord == "test123") {
   echo "<p>Du är inloggad </p>";
}
?>
```

I detta lilla skript använder vi en villkorssats, eller **if**-sats som den också heter. **if**-satsen är sig lik från nästan alla programmeringsspråk och är nödvändig för att man ska anpassa vad som händer efter vad användaren gör. Det som står innanför parenteserna är det sk jämförelseuttrycket. I detta fall kontrollerar vi om variabeln **$losenord** har innehållet "test123". Observera att vi använder två likamedtecken! Hade vi bara använt ett likamedtecken hade vi i stället tilldelat variabeln **$losenord** värdet test123.

Om lösenordet stämmer, körs allting som står innan för krullparanteserna. Om lösenordet inte stämmer, fortsätter programmet efter högerkrullparantesen. Vi kan också välja att ha med ett alternativ som ska inträffa då lösenordet inte stämmer. Då kan det se ut så här:

```php
<?php
if ($losenord == "test123") {
   echo "<p>Du är inloggad </p>";
} else {
   echo "<p>Fel lösenord </p>";
}
?>
```

I det här fallet kommer vi alltså att få meddelandet "Fel lösenord" om lösenordet inte stämmer.

Det finns fler jämförelseoperatorer än **==**, även om **==** är den överlägset vanligaste. Vi har bland annat **&lt;** som står för mindre än, **&gt;** som står för större än. Dessa två används endast för tal. **!=** står för inte lika med och kan däremot användas både för tal och strängar. 

![](../.gitbook/assets/image%20%2870%29.png)

Man kan bygga på **if**-satser med **elseif**. På detta sätt kan programmet ta fler än två olika vägar. 

```php
<?php
if ($veckodag == "lördag") {
   echo "<p>Det är lördag och jag kan ta det lugnt </p>";
} elseif ($veckodag == "söndag") {
   echo "<p>Söndag är vilodag </p>";
} else {
   echo "<p>Vanlig vardag </p>";
}
?>
```

Man kan även testa att två olika villkor i samma **if**-sats. Detta kan göras med **and** eller med **or**. Använder man **and** måste båda villkoren stämma. Med **or** räcker det att minst ett av dem stämmer. En tredje variant är **xor** eller exklusivt eller, då måste antingen det ena eller det andra villkoret stämma. En lista på alla logiska operatorer, som dessa kallas, finns på [language.operators.logical](http://php.net/manual/en/language.operators.logical.php) på php.net.

### Villkorssatser: switch

Istället för att använda flera if-else-satser efter varandra kan man använda switch-satsen.

```php
<?php
switch ($veckodag) {
    case "lördag":
        echo "<p>Det är lördag och jag kan ta det lugnt </p>";
        break;
    case "söndag":
        echo "<p>Söndag är vilodag </p>";
        break;
    default:
        echo "<p>Vanlig vardag </p>";
        break;
}
?>
```

## **Loopar**

### **for-loopen**

Nu vidare till nästa variant på styrstrukturer, nämligen loopar. Den första varianten vi ska titta på är en [for-loop](https://devdocs.io/php/control-structures.for):

```php
<?php
for ($i = 1;$i < 20;$i = $i + 1) {
   echo "<p>Detta är rad $i </p>";
}
?>
```

I detta exempel kommer vi att få 19 rader utskrivna. [for-loopen](https://devdocs.io/php/control-structures.for) har tre delar, det första kallas initiering, där vi sätter loop-variabeln till ett visst värde. I vårt fall har vi valt att ha **$i** som loop-variabel. Den andra delen kallas villkorssats, och den testas varje gång loopen körts. Den tredje satsen kallas uppräkningssats, och innebär att loop-variabeln räknas upp med 1 efter varje varv.

### while-loopen

[while-loopen](https://devdocs.io/php/control-structures.while) är en mer generell variant av [for-loopen](https://devdocs.io/php/control-structures.for). Den används för att upprepa något så länge ett visst villkor är uppfyllt. Motsvarande kod skulle alltså se ut så här:

```php
<?php
$i = 1;
while ($i < 20) {
   echo "<p>Detta är rad $i </p>";
   $i++;
}
?>
```

Inuti [for-](https://devdocs.io/php/control-structures.for) och [while](https://devdocs.io/php/control-structures.while)-loopar kan man använda break för att omedelbart avbryta körningen av loopen och fortsätta direkt med koden som kommer efter loopens slut. Med [continue](https://devdocs.io/php/control-structures.continue) kan man fortsätta direkt till nästa varv av loopen.

## Uppgifter

### **Uppgift 1**

Modifiera **temperaturkonverteringsskriptet** ytterligare en gång, så att användaren matar in en temperatur i ett textfält, och sedan väljer om konverteringen ska ske från F till C eller från C till F med hjälp av **radioknappar**.

### **Uppgift 2**

Gör ett skript som frågar efter **användarnamn** och **lösenord** via ett formulär.   
Om användarnamnet och lösenordet är korrekt ska en sida visas där det står "**Du är inloggad**".   
Annars ska användaren få upp inloggningsrutan igen.

![](../.gitbook/assets/image%20%2832%29.png)

### **Uppgift 3**

Skriv ett skript som frågar efter **två heltal** via ett formulär, det första talet ska vara lägre än det andra.   
Skriv ut **alla heltal** mellan de två som matats in.   
Separera med mellanslag.

![](../.gitbook/assets/image%20%2831%29.png)

### **Uppgift 4**

Gör ett skript som skriver ut **tal** och respektive **tals kvadrat** från **0 till 50**.

![](../.gitbook/assets/image%20%2829%29.png)

### **Uppgift 5**

Gör ett skript som är en **lånekalkylator**.   
Mha **radioknappar** ska användaren kunna välja mellan **1, 3 och 5 års lånetid**. I en ruta ska användaren skriva i **lånebeloppet** och i nästa **räntan** i hela procent.   
Skriptet ska sedan räkna ut den totala **lånekostnaden**, vilket räknas ut genom ränta på ränta-principen, årsvis.   
Så för ett tvåårigt lån på 5000 med räntan 4% skulle alltså lånekostnaden bli 5000\*1,04\*1,04 - 5000. Observera att lånet är "amorteringsfritt".

![](../.gitbook/assets/image%20%2825%29.png)

## Extra uppgifter

### Uppgift 6

Skapa ett skript som frågar vilket land som vann **fotbolls-VM i USA** för herrar år **1994**.   
Om användaren svarar **Sverige** ska skriptet skriva ut att svaret var **rätt**, annars att svaret var **fel**.   
Det spelar ingen roll om användaren gissar med stora eller små bokstäver. \(Använd [strtolower](https://devdocs.io/php/function.strtolower)\).

### Uppgift 7

Skapa ett skript som frågar användaren vad hen heter.   
Om användaren heter **Tova** ska skriptet säga att användaren har namnsdag idag.   
Om användaren istället heter **Abbe** ska skriptet svara "**Du har namnsdag imorgon**", men om användaren varken heter **Tova** eller **Abbe** ska skriptet svara "**Du har varken namnsdag vare sig idag eller imorgon**".

### Uppgift 8

På det nationella provet i Svenska 1 så fanns följande **poänggränser**.

| Betyg | Poänggräns |
| :--- | :--- |
| A | 55 |
| B | 45 |
| C | 35 |
| D | 25 |
| E | 15 |

Skapa ett skript som frågar användaren hur många poäng hen fick på provet.   
Skriptet ska svara med **betyget**.

### Uppgift 9

Skapa ett skript som frågar användaren, ”**Vilket är Europas folkrikaste land?**”.   
Så länge som användaren svarar fel ska hen få en ny chans att svara på frågan.

### Uppgift 10

För att få åka berg-och-dalbana på en nöjespark så måste man vara mellan **1,4 och 1,9** meter lång.   
Skapa ett skript som frågar om användarens längd.  
Skriptet skriver ut om hen får åka eller inte.

### Uppgift 11

Ett fik har en kampanj där personer äldre än **65** år och personer mellan **12 och 18** år erbjuds att köpa kaffe extra billigt.   
Skriv ett skript som kollar om användaren får köpa kaffe extra billigt.   
Skriptet får endast ha en **if-sats**.

### Uppgift 12

Skapa ett skript som frågar användaren vilken **plats** hen kom på i senaste idrottsturneringen.   
Skriptet ska sedan berätta om användaren fick **guld**, **silver**, **brons** eller **ingen** medalj.    
Skriptet får endast ha en **switch**-sats,

### Uppgift 13

Skapa ett skript som frågar användaren hur många **datorer** hen äger. Skriptet ska sedan skriva ut korrekt i singular eller plural.   
Det innebär att om användaren har en dator skrivs det ut "**Du har 1 dator**". Om användaren har tex 3 datorer skrivs det ut "**Du har 3 datorer**".  
Skriptet får endast ha en **if-sats**.

### Uppgift 14

För att få delta i en tävling måste man vara **mellan 16 och 19** år gammal.   
Skapa ett skript som frågar användaren hur gammal hen.  
Skriptet skriver sedan ut om hen får delta i tävlingen och om hen är **för** ung eller om hen är **för gammal**.

### Uppgift 15

Ett företag vill anställa gymnasiestudenter som personal.   
Skapa ett skript som frågar användaren om hen har gått ut gymnasiet. Användaren ska uppmanas att svara **j för ja** eller **n för ne**j.   
Skriptet ska också fråga hur gammal hen är.

Om hen har gått ut gymnasiet och är under 22 år så ska skriptet säga ”**Vi vill gärna anställa dig**”, annars ska skriptet säga ”**Vi letar tyvärr efter annan personal just nu**”.   
Skriptet får endast ha en **if-sats**.

