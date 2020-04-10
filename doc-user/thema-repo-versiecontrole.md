# Versiecontrole in de OSLO thema repository

## Inleiding

De levensloop van een OSLO specificatie doorloopt enkele statussen zoals bepaald in deze [status codelijst](https://data.vlaanderen.be/doc/conceptscheme/StandaardStatus).

Elke publicatie van een specificatie is overigens verbonden aan een of andere commit van de bronbestanden, die zich in de OSLO thema repository bevinden.

Om publicaties te allen tijde te kunnen reconstrueren is het van belang die commit uniek te kunnen identificeren.
Dat kan in principe door de *commit hash* te gebruiken, maar dat is niet echt transparant.
Beter is om expliciet een **tag** toe te kennen, volgens een afgesproken naamgeving, zodat het verband publicatie vs. tag onmiddellijk afleesbaar is.
Dit is hieronder uitgewerkt in de sectie [Tags](#tags).

Normaal gezien zijn opeenvolgende statussen van een OSLO specificatie Ontwerp Standaard, Kandidaat Standaard, Erkende Standaard, ... eventueel gevolgd door een nieuwe cylus Ontwerp Standaard, ...
Als de opeenvolgende publicaties in chronologische volgorde gebeuren, is geen nood aan branches. Alles kan gedaan worden met opeenvolgende wijzigingen op één enkele branch, doorgaans `master`.
Er zijn nochtans omstandigheden waarin het gebruik van een extra **branch** nodig is.
Dit is hieronder uitgewerkt in de sectie [Branches](#branches).

Ten slotte worden in de sectie [Overzicht](#overzicht) enkele versiebomen getoond die het gebruik van tags en branches illustreren.

## Typografische afspraken op deze pagina

| Vorm | Betekenis |
|------|-----------|
| `[]` | een optionele term |
| `{}` | een variabele term |

## Tags
Principe: **_ken één tag toe per publicatiepunt_**.

Op github maak je op een eenvoudige manier een tag aan door een *release* aan te maken. Kies dezelfde naam voor release en tag.

Naamgeving voor tags:
```
[{documentMnemonic}-]{statusMnemonic}-{datum}[-{suffix}]
```

waarin:

| Veld | Beschrijving | Formaat |
|------|--------------|---------|
| `{documentMnemonic}` | Optionele term, enkel nodig als niet alle documenten in de repo tegelijk een nieuw publicatiepunt moeten krijgen. | camelCase, startend met kleine letter, alleen alfanumerische tekens |
| `{statusMnemonic}` | Afkorting voor de status waarin het document zich bevindt op het ogenblik van publicatie | zie volgende tabel |
| `{datum}` | Officiële publicatiedatum | xsd:date (YYYY-MM-DD) |
| `{suffix}` | Optionele term, enkel nodig als voor dezelfde publicatiedatum een correctie nodig is | integer: 1, 2, ... | 

statusMnemonic:

| status | {statusMnemonic} |
|--------|------------------|
| Ontwerp Standaard | `ontwerp` |
| Kandidaat Standaard | `kandidaat` |
| Erkende Standaard | `erkend` |
| Vervangen Standaard | `vervangen` |
| Verouderde Standaard | `verouderd` |
| Herroepen Standaard  | `herroepen` |

### Voorbeelden
- `ontwerp-2020-02-26`: bron voor publicatie op 2020-02-26 als Ontwerp Standaard van alle documenten (bijvoorbeeld een vocabularium en een applicatieprofiel) in een thema repository
- `kandidaat-2020-03-31`: bron voor publicatie op 2020-03-31 als Kandidaat Standaard van alle documenten (bijvoorbeeld een vocabularium en een applicatieprofiel) in een thema repository
- `kandidaat-2020-03-31-1`: zoals hierboven, nadat de volgende dag een typo werd gecorrigeerd
- `apPerceel-erkend-2020-04-30`: bron voor publicatie op 2020-04-30 als Erkende Standaard, enkel voor het applicatieprofiel Perceel

## Branches

### Branches, geval 1

Het moet mogelijk zijn om in bepaalde omstandigheden een update te maken van een publicatie waarvoor de bronbestanden intussen al gewijzigd zijn op de `master` branch.
Enkele voorbeelden:
- Een specificatie werd gepubliceerd als Erkende Standaard. Nadien is men verder aan het werken aan de bronbestandenop de `master` branch, tijdens een nieuwe ontwerp fase. Plots blijkt een editoriale wijziging (bijvoorbeeld om een typo te corrigeren) nodig aan de Erkende Standaard.
- Door een wijziging in de publicatieomgeving (zoals een niet-compatibele verandering in de toolchain, een extra vereiste op het publicatieplatform, ...) is het nodig updates te doen aan de bronbestanden in alle versies corresponderend met een publicatie die online staat.

Maak in dit geval een branch aan vertrekkend uit de tag verbonden aan de oorspronkelijke publicatie.

Tag naamgeving geval 1:
```
{tagName}-{branchSuffix}
```

waarin:

| Veld | Beschrijving | Formaat |
|------|--------------|---------|
| `{tagName}` | Naam van de tag waaruit de branch vertrekt. | - |
| `{branchSuffix}` | Korte aanduiding van de reden waarom de branch werd opgezet. | camelCase, startend met kleine letter, alleen alfanumerische tekens |

Voorbeeld
- `kandidaat-2020-03-31-1-fixToolchainCss`: branch waarop een schoonheidscorrectie werd gedaan aan de publicatie verbonden aan tag `kandidaat-2020-03-31-1`, omwille van een nodige css aanpassing.

### Branches, geval 2

Het mag mogelijk zijn om voor eender welke andere reden behalve die voor geval 1 een branch te gebruiken.
Een voorbeeld is het op een 'zijspoor' verder werken aan een afzonderlijke ontwikkeling.
Deze kan later eventueel teruggemergd worden naar de `master` branch.
Hierbij dient opgemerkt te worden dat de cruciale Enterprise Architect modelbestanden binaire bestanden zijn, die niet kunnen gemerged worden.

Tag naamgeving geval 2:

In dit geval is er geen vaste naamgeving vereist. Gebruik echter geen naamgeving die interfereert met de naamgeving voor geval 1.

Voorbeeld
- `AlternatieveMapping`: branch waarop een alternatieve mapping wordt uitgeprobeerd...

### Documenteren van branches

Documenteer in de README.md onder de root van de thema repository en op de `master` branch de verschillende branches en de reden van hun bestaan.
Dit is nodig omwille van de beperkte ondersteuning van versiebomen in github.
In de README.md template is een tabel voorzien voor deze documentatie.

## Overzicht

TODO


