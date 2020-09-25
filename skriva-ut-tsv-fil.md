---
description: Läsa från textfil och "parsa" data som är tsv-formaterat.
---

# Labb: skriva ut tsv-fil

## Resultatet

![](.gitbook/assets/image%20%2811%29.png)

## **Syfte**

* Skriv ut restauranger i en csv-fil i tabellform

## Startkod

* Referens till funktioner som används:
  * Funktionen [is\_readable\(\)](https://devdocs.io/php/function.is-readable)
  * Funktionen [file\(\)](https://devdocs.io/php/function.file)
  * Funktionen[ ](https://devdocs.io/php/function.array)[foreach](https://devdocs.io/php/control-structures.foreach)
  * Funktionen [explode\(\)](https://devdocs.io/php/function.explode)

{% tabs %}
{% tab title="salar.php" %}
```php
<!DOCTYPE html>
<html lang="sv">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Skolans salar</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="kontainer">
        <h1>Skolans salar</h1>
        <?php
        /* 1. Läs in textfilen */
        $textfil = "salar.tsv";
        if (is_readable($textfil)) {
            
            $rader = file($textfil);
            
            /* 2. Visa salar i en tabell: nr, namn, bokbar */
            echo "<table>";
            echo "<tr><th>Nr</th><th>Namn</th><th>Typ</th><th>Bokbar</th></tr>";
            foreach ($rader as $rad) {
                //echo "<p>$rad</p>";

                /* Dela upp raden i dess delar */
                $delar = explode("\t", $rad);
                //var_dump($delar);

                /* Plocka ut det som vi behöver */
                $salNrNamn = $delar[1]; // Dvs "410/Dali"
                $bokbar = $delar[3]; // Dvs 1

                /* Plocka ut salsnr och salsnamn */
                if ((strstr($salNrNamn, "/") || $salNrNamn == "430" || $salNrNamn == "522" || substr($salNrNamn, 0, 1) == "A" || $salNrNamn == "Biblioteket" || $salNrNamn == "Dr Kristinas sal") && $salNrNamn != "APL" && $salNrNamn != "Annan plats") {

                    /* Om Salsnr innehåller "/" */
                    if (strstr($salNrNamn, "/")) {
                        $delar = explode("/", $salNrNamn);
                        $salNr = $delar[0]; // Dvs "410"
                        $salNamn = $delar[1]; // Dvs "Dali"
                    } else {
                        $salNr = $delar[1]; // Dvs "A1"
                        $salNamn = ""; 
                    }

                    /* Plocka ut salsnr och salsnamn för Annexet */
                    if (strstr($salNrNamn, "(")) { // Dvs "A1 (Mattesal)"
                        $delar = explode(" (", $salNrNamn);
                        $salNr = $delar[0];
                        $salNamn = substr($delar[1], 0, -1); // Ta bort sista parantesen
                    }

                    /* Om salNr har ett bindestreck, dela upp igen */
                    if (strstr($salNr, "-")) { // Dvs 506-grupprum
                        $delar = explode("-", $salNr);
                        $salNr = $delar[0];
                        $salTyp = $delar[1];
                    } else {
                        $salTyp = "sal";
                    }
                    
                    if ($bokbar == "1") {
                        echo "<tr><td>$salNr</td><td>$salNamn</td><td>$salTyp</td><td class=\"grön\"></td></tr>";
                    } else {
                        echo "<tr><td>$salNr</td><td>$salNamn</td><td>$salTyp</td><td class=\"röd\"></td></tr>";
                    }
                }
            }
            echo "</table>";
        } else {
            echo "<p>$textfil går inte att läsa!</p>";
        }
        
        /* 3. Visa om salen är bokad med röd färg, om ledig med grön färg */

        ?>
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="style.css" %}
```css
@import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro&display=swap');

/* Enkel CSS-reset */
html {
    box-sizing: border-box;
}
*, *:before, *:after {
    box-sizing: inherit;
}
body, h1, h2, h3, h4, h5, h6, p, ul {
    margin: 0;
    padding: 0;
}

body {
    background: #F9F6EB;
}
.kontainer {
    width: 600px;
    padding: 2em;
    margin: 3em auto;
    background: #fff;
    border-radius: 5px;
    font-family: 'Source Sans Pro', sans-serif;
    border: 1px solid #ddd;
    box-shadow: 0 0 12px #f0e9d1;
    color: #4e4e4e;
}
.kol2 {
    margin: 1em 0;
    display: grid;
    grid-template-columns: 1fr 2fr;
    grid-gap: 1em;
}
.kol3 {
    margin: 1em 0;
    display: grid;
    grid-template-columns: 1fr 2fr 1fr;
    grid-gap: 1em;
}
form {
    margin: 1em 0;
    color: #4e4e4e;
}
label {
    text-align: right;
    align-self: center;
    font-size: 0.9em;
}
input, textarea {
    padding: 0.7em;
    border-radius: 0.3em;
    border: 1px solid #ccc;
    font-weight: bold;
    box-shadow: inset 0 2px 2px rgba(0, 0, 0, 0.1);
}
textarea {
    height: 5em;
    width: 100%;
}
button {
    margin: 1em 0;
    padding: 0.7em;
    border-radius: 0.3em;
    border: none;
    font-weight: bold;
    color: #FFF;
    background-color: #55a5d2;
}
h1, h2, h3 {
    color: #9c813d;
}
h1, h2, h3, p {
    margin: 0.5em 0;
}
h3 {
    margin-top: 2em;
}

table {
    width: 100%;
    border-collapse: collapse;
    margin: 2em 0;
}
th, td {
    padding: 0.5em;
    text-align: left;
}
th {
    background: #305A85;
    color: #FFF;
}
tr:nth-child(even) {
    background: #E6F2F8;
}
tr:nth-child(odd) {
    background: #FFF;
}
table .fa {
    color: #55a5d2;
}
table img {
    width: 50px;
}
table .grön {
    background: #aeffae;
}
table .röd {
    background: #ffa6a6;
}
form img {
    width: 30px;
}
form label {
    display: flex;
    align-items:center;
}
form span {
    padding: 10px;
}
```
{% endtab %}

{% tab title="salar.tsv" %}
```text
id	name	description	bookable	doublebook
559	410/Dali	410/Dali	1	0
558	415/Warhol	415/Warhol	1	0
557	417/Kubrick	417/Kubrick	1	0
1263	418-studio/Kraftwerk	418-studio/Kraftwerk	1	1
484	419-studio/Coppola	419-studio/Coppola	1	1
551	429/Saville	429/Saville	1	0
1264	430	430	0	1
1895	432-grupprum/Bowie	432-grupprum/Bowie	1	0
566	433/Garbo	433/Garbo	1	0
567	434/Miller	434/Miller	1	0
569	505/Postel	505/Postel	1	0
1869	506-grupprum/King	506-grupprum/King	0	0
573	509/Kahn	509/Kahn	1	0
575	511/Samus	511/Samus	1	0
2388	512	512/Grupprum	1	0
577	513/Ericsson	513/Ericsson	1	0
2266	515	515/Personalrum	0	0
1782	522	522	0	0
582	523/Allen	523/Allen	1	0
584	525/Estrin	525/Estrin	1	0
585	526/Pearlman	526/Pearlman	1	0
589	606/Newton	606/Newton	1	0
590	607/Gates	607/Gates	1	1
591	607A-grupprum/Jobs	607A-grupprum/Jobs	1	0
593	609/Hopper	609/Hopper	1	1
594	610-grupprum/Arkimedes	610-grupprum/Arkimedes	1	0
595	611/Makerspace	611/Makerspace	0	0
1261	612-grupprum/Da Vinci	612-grupprum/Da Vinci	1	0
600	620A-labbsal/Cerf	620A-labbsal/Cerf	1	0
601	620B-labbsal/Silicon Valley	620B-labbsal/Silicon Valley	0	0
602	622/Curie	622/Curie	1	0
604	624-labbsal/Ohm	624-labbsal/Ohm	1	0
1789	A1 (Mattesal)	A1 (Mattesal)	1	1
1953	A10-grupprum	A10-grupprum	1	1
1791	A2	A2	1	1
1825	A3 (Mattesal)	A3 (Mattesal)	1	1
1875	A4 (FysikLabb)	A4 (FysikLabb)	1	1
1876	A5 (KemiLabb)	A5 (KemiLabb)	1	1
1793	A6	A6	1	1
1815	A7	A7	1	1
1814	A8	A8	1	1
1952	A9-grupprum	A9-grupprum	1	1
1811	Annan plats	Annan plats	0	1
1446	APL	APL	0	1
1657	Biblioteket	Biblioteket	0	1
839	Dr Kristinas sal	Dr Kristinas sal	0	0
1084	Handels	Handels	0	1
1788	Idrottshall	Idrottshall	0	1
1262	Musikhuset	Musikhuset	0	1
605	Nordic Wellness	Nordic Wellness	0	0
2394	Provsk�rmsvagn 2 Annexet	Provsk�rmsvagn 2 Annexet	1	0
1973	Provsk�rmsvagn 410	Provsk�rmsvagn 410	1	0
1971	Provsk�rmsvagn 505	Provsk�rmsvagn 505	1	0
1972	Provsk�rmsvagn 606	Provsk�rmsvagn 606	1	0
1974	Provsk�rmsvagn Annexet 1	Provsk�rmsvagn Annexet	1	0

```
{% endtab %}
{% endtabs %}

## Förbättringar



