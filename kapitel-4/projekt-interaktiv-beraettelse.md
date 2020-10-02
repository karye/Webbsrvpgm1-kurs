---
description: Skapa en interaktiv berättelse
---

# Projekt: interaktiv berättelse

## Interaktiv berättelse

Använd **if-else**-satser tillsammans med det du lärt dig tidigare för att konstruera en interaktiv berättelse med minst två beslut och tre olika slut.

## Flödesschema

Börja med att designa din berättelse. Använd ett enkelt beslutsträd, tex något av dessa:  


![](https://docs.google.com/drawings/u/0/d/sCVbah0fMe_4baeG0KFlTag/image?w=572&h=171&rev=1&ac=1&parent=14wTbpTkwo_McghrUHrnIT7yZQJ79HvoMWTnrXWkoWLM)

## Instruktioner

* Använd **Console.ReadLine\(\)** och **Console.WriteLine\(\)**
* Använd variabler med datatypen **string**
* Använd **if-else**-satser för att undersöka vilket val spelaren gjort
* Skriv kommentarer i koden om vad de olika koderna gör.
* Minst en klasskamrat ska ha testat din berättelse & ha tittat på koden.

## Förbättringar

Om du har tid, fundera över förbättringar, t.ex:

* Lägg in snygg ASCII-art \(tips: skriv @ framför första citattecknet i strings för att undvika problem med tecknet \\)
* Välj färger till texten och bakgrunden \(**Console.ForegroundColor\(\)**, **Console.BackgroundColor\(\)**\).

### Avancerat

* Gör så att det inte spelar någon roll vilka stora eller små bokstäver man skriver in \(t.ex. via \|\| eller genom att använda **ToLower\(\)**\).
* Gör så att något val har tre alternativ istället för två.
* Använd en loop för att se till så att användaren inte kan gå vidare förrän hen skrivit ett svar \(inga tomma svar tex\)

### Ännu mer avancerat

* Lägg in varje “rum” i en egen metod, och anropa metoderna från varandra \(t.ex. att metod2 anropas inuti metod1\).
* Lägg in frågandet i en metod, som ställer frågan och inte avslutas innan spelaren skrivit in ett giltigt svar. Då returneras valet till koden där metoden anropades.

### Jätte dunderavancerat

* Skapa en klass för “rum”, som innehåller en string som beskriver rummet, och två variabler som pekar mot andra rumsinstanser som användaren kan kan välja att gå till. Skapa sedan alla rumsinstanser och se till så att variablerna pekar rätt.

