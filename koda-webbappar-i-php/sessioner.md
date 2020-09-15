---
description: Använda sessioner för att hålla reda på om en användare är inloggad.
---

# Sessioner

## Sessioner

### **Lagra variabelvärden mellan sidor**

Ett problem som ofta uppkommer när man programmerar i PHP är att variabler inte behåller sitt värde mellan olika webbsidor. Detta beror på att http är ett sk. lägeslöst protokoll.

Det finns olika metoder att spara variabelvärden mellan sidor. Ett sätt är att skicka med gömda formulärfält - men detta blir snabbt ohanterligt då variablerna är många. Ett annat sätt är att skicka med information i själva adressen. Då stöter man dock på säkerhetsproblem. Dessutom finns en gräns i att en webbadress inte får vara längre än c:a 250 tecken.

För att göra det hela enklare har PHP stöd för sessioner. Detta innebär att man på ett enkelt sätt kan ha tillgång till samma variabelflora på hela webbplatsen, vilket är mycket använd bart för att t.ex. kontrollera att en användare är inloggad, eller för att genomföra ett köp i en webb-butik.

### **Varje session har ett unikt id**

När en session startas i PHP får den ett unikt id. Denna långa sträng av tecken är det enda som skickas fram och tillbaka mellan besökarens webbläsare och webbservern för att identifiera vilken session en viss användare tillhör. Detta sker vanligtvis med hjälp av en kaka - en liten textfil som sparas i webbläsarens minne. Om besökaren stängt av kakfunktionen känner PHP av det och lägger i stället till sessionsid:t i slutet av webbadressen.

## **Använda en session**

För att starta en session använder man sig av funktionen [session\_start\(\)](https://devdocs.io/php/function.session-start). Den måste komma allra högst upp i PHP-skriptet, annars får man felmeddelandet **Headers already sent**. Därefter kan man registrera sessionsvariabler genom att använda matrisen [$\_SESSION](https://devdocs.io/php/reserved.variables.session):

#### **Utskrift på fil1.php**

```php
<?php
session_start(); // Startar sessionen
$_SESSION['namn'] = "test";
?>
<a href="fil2.php">Fil 2</a>
```

### **Använda sessionsvariabler**

Varje PHP-sida som använder sessioner ska ha ett anrop till session\_start högst upp i skriptet. När session\_start har anropats så hämtas alla sessionsvariabler. Dessa finns sedan i matrisen [$\_SESSION](https://devdocs.io/php/reserved.variables.session).

#### **Utskrift på fil2.php**

```php
<?php
session_start();
echo $_SESSION['namn']; // Skriver ut test
?>
<a hre="fil3.php">Fil 3</a>
```

### **Avsluta en session**

Genom att tömma matrisen [$\_SESSION](https://devdocs.io/php/reserved.variables.session) tas alla sessionsvariabler bort. För att helt avsluta sessionen anropas sedan [session\_destroy\(\)](https://devdocs.io/php/function.session-destroy).

#### **Utskrift på fil3.php**

```php
<?php
session_start();
$_SESSION = Null; // Tar bort alla sessionsvariabler
session_destroy() // Avslutar sessionen
echo $_SESSION['namn']; // Skriver inte ut någonting.
?>
```

## Uppgifter - sessioner

### **Uppgift 10.1**

Skapa en enkel räknare som visar hur många gånger man varit inne på sidan. Spara sidan med namnet **raknare.php** och gör sedan en **submit**-knapp som går till samma sida \(**raknare.php**\). Kontrollera att räknaren räknar upp 1 steg för varje gång man varit inne på sidan.

### **Uppgift 10.2**

Utveckla programmet i övning 1 med en kryssruta där man kan bocka för att räknaren ska nollställas. Om kryssrutan är ikryssad när formuläret skickas iväg ska räknaren börja om från 0.

### **Uppgift 10.3**

Skapa ett inloggningssystem där användaren kan logga in på en sida via ett formulär och när användarnamn och lösenord är kontrollerade ska användaren kunna gå runt på tre fyra olika sidor. Användaren ska också kunna logga ut, och därefter inte kunna komma åt sidorna.

{% hint style="info" %}
Från PHP-kompendiet av Thomas Höjemo, © SNT 2006, www.snt.se
{% endhint %}

