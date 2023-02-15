# OSLO toolchain: aan de slag!

## Introductie

Dit is een bondige stap per stap procedure om een eerst publicatie te doen van een OSLO standaard, startend van scratch.

## 1. Geraak aan een OSLO thema repository
Om te kunnen beginnen editeren, is een afzonderlijke github repository nodig onder <https://github.com/Informatievlaanderen>.

Deze repository wordt aangemaakt door iemand uit het OSLO team.

De editors krijgen de nodige rechten.

Initieel bevat deze repository al een aantal bestanden uit een template.
Deze kunnen (allicht na hernoemen of kopiëren) gebruikt worden in de volgende stappen.
Details over deze initiële bestanden zijn [hier](thema-repo-initiele-bestanden.md) te vinden.

## 2. Maak je UML model in een Enterprise Architect (EA) bestand

Maak je EA bestand in de repository root.

Bij de initiële bestanden is een (leeg) voorbeeld beschikbaar voor een vocabularium en voor een applicatieprofiel.
Misschien start je om te beginnen beter met een bestand waaruit beide kunnen worden gegenereerd en stel je de afsplitsing van het vocabularium uit tot later.

Hoe je het UML model opmaakt is buiten de scope van deze toolchain documentatie.

## 3. Schrijf het tekstuele gedeelte van de publicatie

Doe dit in een bestand in de **templates** directory van de repository.
Er is een voorbeeld beschikbaar in de initiële bestanden voor een vocabularium en voor een applicatieprofiel.

## 4. Voeg een beeldbestand van het diagram toe

Dit is enkel nodig voor een applicatieprofiel. Dit moet een JPEG bestand zijn met verplichte naam **overview.jpg** en het moet geplaatst worden
in een unieke directory onder de **site-skeleton** directory van de repository.
Maak best één subdirectory met de naam van het applicatieprofiel om voorbereid te zijn op eventuele additionele applicatieprofielen later.
Gebruik alleen kleine letters en geen spaties voor deze directory.
Een voorbeeld is beschikbaar bij de initiële bestanden.

## 5. Maak een lijst met medewerkers aan dit thema

Daartoe dient de al bij de initiële bestanden aangeleverde **stakeholders.csv** in de repository root. Voeg per lijn een medewerker toe.
Gebruik indien nodig afzonderlijke kolommen om medewerking aan de verschillende vocabularia/applicatieprofielen in deze repository te onderscheiden.
Een medewerker kan van het het type **A** (auteur), **E** (editor) of **C** (collaborator = medewerker) zijn. Plaats de overeenkomstige letter in de betreffende kolom.

Let wel: dit bestand moet in **UTF-8** codering worden opgemaakt.

## 6. Maak het paatselijke configuratiebestand voor de publicatie aan

Doe dit in een bestand in de **config** directory van de repository.
Er is een voorbeeld beschikbaar in de initiële bestanden voor een vocabularium en voor een applicatieprofiel.
Doorgaans volstaat het om een kopie hiervan te maken en aan te passen naar je eigen gegevens.

Let er goed op alle verwijzingen en ook de datum goed te zetten.

Gedetailleerde info over deze stap vind je in [configuratie van een publicatiepunt](configuratie-van-een-publicatiepunt.md),
sectie **JSON bestand in de OSLO thema repository**.

## 7. Push alles en maak een tag aan

Push nu zeker alles naar github en maak een tag aan van de vorm `ontwerp-YYYY-MM-DD`.
We komen later terug op dit taggen. Doe nu maar gewoon.

## 8. Maak de centrale configuratie voor de publicatie aan

***Het is raadzaam om voor deze stap een OSLO medewerker te raadplegen.***

Alle info over deze stap vind je in [configuratie van een publicatiepunt](configuratie-van-een-publicatiepunt.md),
sectie **JSON bestand in de centrale repository**.

Maak je publicatie aan voor raadpleging op <https://test.data.vlaanderen.be>.
Voeg daarom een entry toe in de **config/test** directory op de **test** branch
van <https://github.com/Informatievlaanderen/Data.Vlaanderen.be>.

Verwijs naar je OSLO thema repository, de gemaakte tag, het config bestand, de naam gegeven aan de publicatie in dat config bestand en maak alle overige velden aan zoals gedocumenteerd.

Commit de wijziging en de toolchain zal nu automatisch de publicatie aanmaken. Je kan dit proces volgen op [CircleCI](https://app.circleci.com/pipelines/github/Informatievlaanderen/Data.Vlaanderen.be). Door te klikken op de juiste link onder de kolom "Workflow" kan je details bekijken over wat goed en eventueel fout loopt.

Als alles goed gaat, bevinden de gegenereerde bestanden voor de publicatie zich op <https://github.com/Informatievlaanderen/data.vlaanderen.be-generated/tree/test/{urlref}>.

Een tijdje later zal de publicatie zichtbaar zijn op <https://test.data.vlaanderen.be/{urlref}>.

Om een publicatie te maken op <https://data.vlaanderen.be>, heb je na deze stap een OSLO medewerker nodig.

## En verder...
Als je tot hier geraakt bent, heb je een eerste versie van een nieuwe specificatie als Ontwerp Standaard gepubliceerd.

Om volgende versies van je specificatie te bouwen is het belangrijk om de gepaste versiecontrole afspraken te volgen in je OSLO thema repository.
Dit wordt [hier](thema-repo-versiecontrole.md) behandeld.

Happy publishing!
