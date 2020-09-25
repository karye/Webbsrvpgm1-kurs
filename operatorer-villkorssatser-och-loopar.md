---
description: 'Operatorer, villkorssatser och loopar.'
---

# Operatorer, villkorssatser och loopar

## **Operatorer**

Det finns ett antal olika operatortyper i PHP. Från matematiken känner vi igen de [aritmetiska operatorerna](https://devdocs.io/php/language.operators.arithmetic), t.ex. **+, -, \*** och **/**. Dessa har vi tittat på tidigare. Tilldelningsoperatorn kallas likamed-tecknet \(=\). Den har vi också använt oss av för att ge en variabel ett värde. Några exempel:

```php
<?php
$a = 324; // Ger $a värdet 324
$a = a + 1; // Ökar $a med 1 till 325
$a = berakna(12); // $a får returvärdet av funktionen berakna
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

## **Villkorssatser**

Hittills har alla program vi skrivit körts igenom rad för rad, utan att vi kunnat styra in programmet på olika vägar beroende på vad användaren har matat in. Det är detta vi har styrstrukturer till. Styrstrukturer har det gemensamt att de kontrollerar om ett uttryck stämmer med ett annat och sedan beroende på resultatet gör ett val. På detta sätt kan man skriva mycket mer flexibla program. Det finns två huvudtyper av styrstrukturer: villkorssatser och loopar. Vi börjar med villkorssatser.

### if-satsen

```php
<?php
if ($losenord == "test123") {
   echo "Du är inloggad";
}
?>
```

I detta lilla skript använder vi en villkorssats, eller **if**-sats som den också heter. **if**-satsen är sig lik från nästan alla programmeringsspråk och är nödvändig för att man ska anpassa vad som händer efter vad användaren gör. Det som står innanför paranteserna är det s.k. jämförelseuttrycket. I detta fall kontrollerar vi om variabeln **$losenord** har innehållet "test123". Observera att vi använder två likamedtecken! Hade vi bara använt ett likamedtecken hade vi i stället tilldelat variabeln **$losenord** värdet test123.

Om lösenordet stämmer, körs allting som står innan för krullparanteserna. Om lösenordet inte stämmer, fortsätter programmet efter högerkrullparantesen. Vi kan också välja att ha med ett alternativ som ska inträffa då lösenordet inte stämmer. Då kan det se ut så här:

```php
<?php
if ($losenord == "test123") {
   echo "Du är inloggad";
} else {
   echo "Fel lösenord";
}
?>
```

I det här fallet kommer vi alltså att få meddelandet "Fel lösenord" om lösenordet inte stämmer.

Det finns fler jämförelseoperatorer än **==**, även om **==** är den överlägset vanligaste. Vi har bland annat **&lt;** som står för mindre än, **&gt;** som står för större än. Dessa två används endast för tal. **!=** står för inte lika med och kan däremot användas både för tal och strängar. Man kan bygga på **if**-satser med **elseif**. På detta sätt kan programmet ta fler än två olika vägar. Fler jämförelseoperatorer hittar du på [language.operators.comparison](http://php.net/manual/en/language.operators.comparison.php) på php.net.

```php
<?php
if ($veckodag == "lördag") {
   echo "Det är lördag och jag kan ta det lugnt.";
} elseif ($veckodag == "söndag") {
   echo "Söndag är vilodag.";
} else {
   echo "Vanlig vardag";
}
?>
```

Man kan även testa att två olika villkor i samma **if**-sats. Detta kan göras med **and** eller med **or**. Använder man **and** måste båda villkoren stämma. Med **or** räcker det att minst ett av dem stämmer. En tredje variant är **xor** eller exklusivt eller, då måste antingen det ena eller det andra villkoret stämma. En lista på alla logiska operatorer, som dessa kallas, finns på [language.operators.logical](http://php.net/manual/en/language.operators.logical.php) på php.net.

## **Loopar**

### **for-loopen**

Nu vidare till nästa variant på styrstrukturer, nämligen loopar. Den första varianten vi ska titta på är en [for-loop](https://devdocs.io/php/control-structures.for):

```php
<?php
for ($i = 1;$i < 20;$i = $i + 1) {
   echo "Detta är rad $i <br>";
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
   echo "Detta är rad $i <br>";
   $i++;
}
?>
```

Inuti [for-](https://devdocs.io/php/control-structures.for) och [while](https://devdocs.io/php/control-structures.while)-loopar kan man använda break för att omedelbart avbryta körningen av loopen och fortsätta direkt med koden som kommer efter loopens slut. Med [continue](https://devdocs.io/php/control-structures.continue) kan man fortsätta direkt till nästa varv av loopen.

## Uppgifter - operatorer, villkorssatser och loopar

### **Uppgift 1**

Modifiera **temperaturkonverteringsprogrammet** ytterligare en gång, så att användaren matar in en temperatur i ett textfält, och sedan väljer om konverteringen ska ske från F till C eller från C till F med hjälp av radioknappar.

### **Uppgift 2**

Gör ett skript som frågar efter **användarnamn** och **lösenord** via ett formulär. Om användarnamnet och lösenordet är korrekt ska en sida visas där det står "Du är inloggad". Annars ska användaren få upp inloggningsrutan igen.

### **Uppgift 3**

Skriv ett skript som frågar efter **två heltal** via ett formulär, det första talet ska vara lägre än det andra. Skriv ut **alla heltal** mellan de två som matats in. Separera med mellanslag.

### **Uppgift 4**

Gör ett skript som skriver ut **tal** och respektive **tals kvadrat** från **0 till 50**.

### **Uppgift 5**

Gör ett skript som är en **lånekalkylator**. Mha **radioknappar** ska användaren kunna välja mellan **1, 3 och 5 års lånetid**. I en ruta ska användaren skriva i **lånebeloppet** och i nästa **räntan** i hela procent. Programmet ska sedan räkna ut den totala lånekostnaden. Räknas ut genom ränta på ränta-principen, årsvis\). Så för ett tvåårigt lån på 5000 med räntan 4% skulle alltså lånekostnaden bli 5000\*1,04\*1,04 - 5000. Observera att lånet är "amorteringsfritt".

## Extra uppgifter

### Uppgift 6

Skapa ett skript som frågar användaren vilket land som vann fotbolls-VM för damer år 2015. Om användaren svarar USA ska programmet skriva ut att svaret var rätt, annars ska programmet skriva ut att svaret var fel. Det ska inte spela någon roll om användaren skriver svaret med stora eller små bokstäver.

### Uppgift 7

Skapa ett skript som frågar användaren vad hen heter. Om användaren heter **Stig** ska programmet säga att användaren har namnsdag idag. Om användaren istället heter **Abraham** ska användaren få veta att hen har namnsdag imorgon, men om användaren varken heter Stig eller Abraham ska hen få veta att hen inte har namnsdag vare sig idag eller imorgon.

### Uppgift 8

På det nationella provet i Matematik 1 våren 2018 så fanns följande poänggränser för olika provbetyg.

| Provbetyg | Poänggräns |
| :--- | :--- |
| A | 55 |
| B | 45 |
| C | 35 |
| D | 25 |
| E | 15 |

Skapa ett skript som frågar användaren hur många poäng hen fick på detta prov. Skriptet ska säga vilket provbetyg användaren fick.

{% hint style="info" %}
Från PHP-kompendiet av Thomas Höjemo, © SNT 2006, www.snt.se
{% endhint %}

