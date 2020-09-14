---
description: Att bearbeta strängar är mycket användbart
---

# Stränghantering

## Stränghantering

Stränghantering används ofta i samband med inmatning för användare. Ibland för att kontrollera så att en epost-adress är korrekt utformad, och ofta dessutom av säkerhetsskäl.

### **Ta bort mellanrum i början och slutet - trim\(\)**

Ibland kan användare av misstag råkat skriva extra mellanrum efter inmatningar av tex. adress eller telefonnummer. När man sedan sparar data i tex. en databas, vill man inte ha med mellanrummen. Därför använder man funktionen trim för att ta bort dem. Observera att detta enbart gäller mellanrum precis i början eller slutet av en sträng; aldrig mitt i. Funktionen tar förutom mellanslag även bort nyradtecken och tabtecken. Se [trim](http://php.net/manual/en/function.trim.php) på php.net. Om vi tex. har en variabel med namnet **$adress** kan vi göra så här:

```php
$adress = trim($adress);
```

### **Omvandla till små eller stora bokstäver - strtolower\(\) respektive strtoupper\(\)**

När man ska jämföra strängar tar php som standard hänsyn till små och stora bokstäver. Om $inmatat har värdet "Test" och **$kontroll** värdet "test" så kommer en jämförelse mellan dem med hjälp av == ej vara sann. Men om man då inte vill ta hänsyn till små och stora bokstäver? Då kan man använda **strtolower\(\)** eller **strtoupper\(\)**. Se [strtolower](http://php.net/manual/en/function.strtolower.php) på php.net. Om vi tar exemplet med jämförelsen av **$a** och **$b**:

```php
$kontroll = "test";
if (strtolower($inmatat) == $kontroll) {
    // gör något...
} else {
    // gör något annat...
}
```

Observera att **$inmatat** fortfarande har värdet "Test". Vill vi förändra detta gör vi så här:

```php
$inmatat = strtolower($inmatat);
```

Funktionen **strtoupper\(\)** fungerar på samma sätt, med skillnaden att alla bokstäver blir versaler.

### **Längden på en sträng - strlen\(\)**

Med **strlen\(\)** \(står för string length\) får vi reda på antalet tecken i en sträng. Se [strlen](http://php.net/manual/en/function.strlen.php) på php.net.

```php
$text = "Hej och hopp";
echo strlen($text); // Skriver ut 12
```

### **Plocka ut delar av en sträng - substr\(\)**

Följande exempel tar ut de tre första tecknen ur strängen **$text**:

```php
$text = "Hej och hopp";
$start = substr($text, 0, 3); // Plockar ut "Hej";
```

Observera att det första tecknet har position **0**! Först specificerar vi namnet på variabeln, sedan positionen och sist längden på den delsträng vi vill ha ut. Det går även att ta delsträngar från slutet:

```php
$text = "Hej och hopp";
$slut = substr($text, -4);// Plockar ut "hopp";
```

Här får vi alltså ut de sista fyra tecknen i strängen. Se [substr](http://php.net/manual/en/function.substr.php) på php.net.

### **Söka igenom en sträng - strstr\(\)**

Ibland vill man ta reda på om en viss text finns inuti en sträng. Detta gör man med **strstr\(\)**:

```php
$namn = "Ulrika Eriksson";
$efternamn = strstr($namn, " ");
```

Här söker vi efter strängen **" "** det vill säga ett mellanslag. Eftersom vi hittar ett mellanslag i strängen **$namn**, kommer nu resten av strängen efter mellanslaget returneras. Se [strstr](http://php.net/manual/en/function.strstr.php) på php.net.

Det går även att använda **strstr\(\)** i en **if**-sats för att köra olika kod beroende på om strängen hittades eller inte:

```php
$namn = "Ulrika Eriksson";
if (strstr($namn, " ")) {
    echo 'Variabeln $namn innehåller mellanslag';
} else {
    echo 'Variabeln $namn innehåller inte mellanslag';
}
```

```text
Note:
If you only want to determine if a particular needle occurs within haystack, use the faster and less memory intensive function strpos() instead.
```

### **Söka och ersätta - str\_replace\(\)**

Funktionen **str\_replace\(\)** används för att söka efter en delsträng och ersätta den med något annat. Se [str-replace](http://php.net/manual/en/function.str-replace.php) på php.net:

```php
$ny_variabel = str_replace("vit", "svart", "vit katt på taket");
echo $ny_variabel;
```

I detta fall kommer texten "svart katt på taket" skrivas ut.

## Uppgifter - stränghantering

### **Uppgift 6.1**

Gör ett **formulär** där användaren ska fylla i **namn, adress, postnr och postort**.

* Kontrollera att alla fälten är ifyllda, och innehåller minst 3 tecken.
* Kontrollera att postnumret innehåller 5 tecken och att de tecknen endast är siffror.

### **Uppgift 6.2**

Bygg på formuläret så att användaren också ska fylla i en **e-postadress**.

* Kontrollera sedan att e-postadressen innehåller ett @, och minst en punkt.
* Kontrollera också att e-postadressen är minst sex tecken lång.

### **Uppgift 6.3**

Utveckla skriptet i uppgift 6.2 så att det tar bort mellanslag i **postnumret** och därmed tillåter postnummer inskrivna enligt formen "415 22".

### **Uppgift 6.4**

Skapa en webbapplikation som testar styrkan på ett **lösenord**. Se [passwordmeter.com](http://www.passwordmeter.com/) för tips.

{% hint style="info" %}
Från PHP-kompendiet av Thomas Höjemo, © SNT 2006, www.snt.se
{% endhint %}

