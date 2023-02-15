# Configuratie van een publicatiepunt

## Introductie

Een publicatiepunt is één versie van een specificatie die raadpleegbaar is op een unieke URL.

Een publicatiepunt wordt geconfigureerd op twee plaatsen.

De eerste plaats is een JSON bestand in de **config** directory van de **OSLO thema repository** die de bronbestanden bevat.
Dit JSON bestand legt alle gedetailleerde eigenschappen en verbanden vast, met betrekking tot de bronbestanden zelf.

De tweede plaats is een JSON bestand in de **config** directory van de **centrale repository**
<https://github.com/Informatievlaanderen/Data.Vlaanderen.be>.
Dit JSON bestand bevat URL-gerelateerde specificaties en de nodige coördinaten van en indexen in het eerste JSON bestand.  

## JSON bestand in de OSLO thema repository

Dit bestand bevat een JSON array. Hierdoor is het in principe mogelijk meerdere configuraties in één bestand vast te leggen,
bijvoorbeeld voor een vocabularium en een applicatieprofiel die samen in één OSLO thema repository zitten.
Meerdere bestanden met elk een array bestaande uit één element kunnen uiteraard ook.

Formaat (één element uit de array):
```
{
  "name": "...",
  "type": "...",
  "prefix": "...",
  "eap": "...",
  "diagram": "...",
  "template": "...",
  "title": "...",
  "publication-state": "...",
  "publication-date": "...",
  "license": "...",
  "contributors-file": "...",
  "contributors-column": "...",
  "site": "...",
  "feedbackurl": "...",
  "standaardregisterurl": "..."
}
```

Velden:

| Veld | Beschrijving | Van toepassing op |
|------|--------------|-------------------|
| name | Naam van de publicatie, uniek binnen dit JSON bestand. | voc, ap |
| type | `voc` of `ap`; geeft aan of deze publicatie een vocabularium of een applicatieprofiel betreft. | voc, ap |
| prefix | Als de baseURI van een vocabularium van de (normale) vorm `https://data.vlaanderen.be/ns/{namespace}#` is, verwijder dit veld.<br>Als de baseURI van een vocabularium van de vorm `https://data.vlaanderen.be/ns/{path}/{namespace}#` is, vul dan hier `{path]` in. | voc |
| eap | Naam van het Enterprise Architect (EA) bestand dat het UML model bevat. Locatie: repository root. | voc, ap |
| diagram | Naam van het diagram in het EA bestand waaruit de specificatie moet worden gehaald. | voc, ap |
| template | Naam van het template bestand dat de tekstuele fragmenten van de specificatie bevat. Locatie: **template** directory onder de repository root. | voc, ap |
| title | Titel van de publicatie. | voc, ap |
| publication-state | Status van de publicatie, een **id** uit [deze codelijst](https://data.vlaanderen.be/doc/conceptscheme/StandaardStatus). | voc, ap |
| publication-date | Datum van publicatie, in xsd:date formaat (YYYY-MM-DD). | voc, ap |
| license | Link naar de van toepassing zijnde licentie. | voc, ap |
| contributors-file | Naam van het bestand dat de medewerkers aan de specificatie bevat. Locatie: repository root. | voc, ap |
| contributors-column | Naam van de te gebruiken kolom in dit bestand. | voc, ap |
| site | Pad van extra bestanden (zoals overview.jpg), die aan de specificatie moeten worden toegevoegd. Relatief aan de repository root. | ap |
| feedbackurl | URL van de locatie te gebruiken om feedback op deze specificatie te geven: de issues locatie van de OSLO thema repository. | voc, ap |
| standaardregisterurl | URL van het OSLO standaardregister, of van de locatie in dit register, waar deze publicatie vermeld wordt. | voc, ap |

Voorbeeld (bestand met één vocabularium, zonder prefix):
```
[
{
  "name": "mijn-vocabularium-voc",
  "type": "voc",
  "eap": "MijnVocabularium-VOC.eap",
  "diagram": "OSLO-MijnVocabularium",
  "template": "mijn-vocabularium-voc.j2",
  "title": "Mijn Vocabularium",
  "publication-state": "https://data.vlaanderen.be/id/concept/StandaardStatus/OntwerpStandaard",
  "publication-date": "2020-01-31",
  "license": "https://data.vlaanderen.be/id/licentie/modellicentie-gratis-hergebruik/v1.0",
  "contributors-file": "stakeholders.csv",
  "contributors-column": "MijnKolom",
  "feedbackurl": "https://github.com/Informatievlaanderen/OSLOthema-mijnThema/issues",
  "standaardregisterurl": "https://data.vlaanderen.be/standaarden/"
}
]
```

Voorbeeld (bestand met één applicatieprofiel):
```
[
{
  "name": "mijn-applicatieprofiel-ap",
  "type": "ap",
  "eap": "MijnApplicatieprofiel-AP.eap",
  "diagram": "MijnApplicatieprofiel",
  "template": "mijn-applicatieprofiel-ap.j2",
  "title": "Mijn Applicatieprofiel",
  "publication-state": "https://data.vlaanderen.be/id/concept/StandaardStatus/OntwerpStandaard",
  "publication-date": "2020-01-31",
  "license": "https://data.vlaanderen.be/id/licentie/modellicentie-gratis-hergebruik/v1.0",
  "contributors-file": "stakeholders.csv",
  "contributors-column": "MijnKolom",
  "site": "site-skeleton/mijn-applicatieprofiel-ap",
  "feedbackurl": "https://github.com/Informatievlaanderen/OSLOthema-mijnThema/issues",
  "standaardregisterurl": "https://data.vlaanderen.be/standaarden/"
}
]
```

## Entry in een JSON bestand in de centrale repository

De entry hier besproken is een object in een array in een JSON bestand.
Meerdere JSON bestanden kunnen bestaan en ze bevinden zich alle in de repo <https://github.com/Informatievlaanderen/Data.Vlaanderen.be>, op een specifieke **branch**. Mogelijke paden:
- **config/publication.json** (één groot bestand)
- **config/\<branch\>/\*.publication.json** (één bestand per thema)

De **branch** bepaalt het domein waarop de publicaties zich zullen bevinden, volgens deze tabel:


| Branch | Domein van de publicatie | Bedoeling |
|--------|--------|-----------|
| `production` | https://data.vlaanderen.be | **Enkel voor OSLO medewerkers** Uiteindelijke plaats voor alle officiële publicaties. |
| `test` | https://test.data.vlaanderen.be | Tijdelijke plaats om nieuwe publicaties voor te bereiden. |
| `dev` | https://dev.data.vlaanderen.be | **Enkel voor OSLO medewerkers** Plaats om ontwikkelingen aan de toolchain uit te testen. |

### Geval 1: met geversioneerde URL

In principe worden alle publicaties gemaakt met een geversioneerde, persistente URL. Zie geval 2 voor vermeende afwijkingen.
 
Formaat (één element uit de array):
```
{
   "dummy": "...",
   "disabled" : true,
   "urlref": "...",
   "repository": "...",
   "branchtag" : "...",
   "name" : "...",
   "filename" : "...",
   "navigation" : {
      "prev": "...",
      "next": "..."
   }
}
```

Velden:

| Veld | Beschrijving |
|------|--------------|
| dummy | Optioneel veld: voeg toe of wijzig de toegekende waarde om de toolchain te forceren de publicatie opnieuw te bouwen, zelfs als er geen andere velden in dit element werden gewijzigd. |
| disabled | Optioneel veld: voeg toe met waarde `true` om te verhinderen dat de toolchain de publicatie bouwt. Bedoeld om andere publicaties te kunnen bouwen als de publicatie in kwestie niet kan gebouwd worden wegens fouten. |
| urlref | Relatieve URL (= URL zonder domein) waarop de publicatie te consulteren zal zijn. |
| repository | URL van de OSLO thema repository. |
| branchtag | Git branch naam, git commit hash of git tag: bepaalt welke versie van de bronbestanden in de OSLO thema repository gelezen worden om deze publicatie te maken.<br/> **Hint: Met een git branch naam is de bepaling van de versie van de bronbestanden niet deterministisch, wat bij het later opnieuw genereren van de publicatie voor afwijkende output of fouten kan zorgen; gebruik dit dus slechts tijdelijk tijdens ontwikkeling en vervang ten slotte altijd door een git commit hash of nog beter een git tag, die je eerst aanbracht op de OSLO thema repository (zie [versiecontrole](thema-repo-versiecontrole.md)).** |
| name | Naam van de publicatie. Bepaalt welke entry in het JSON configuratiebestand in de OSLO thema repository wordt geselecteerd: deze met een identieke waarde in het **name** veld aldaar. |
| filename | Pad vanaf de repository root + bestandsnaam van het JSON configuratiebestand in de OSLO thema repository. |
| navigation | Object met navigatie gegevens. Voeg altijd toe, zelfs indien leeg. |
| next | Optioneel veld in navigation: relatieve URL naar de versie die gesteld wordt als volgende ten opzichte van deze versie van de publicatie.<br>Moet overeen komen met het veld **urlref** van een ander publicatiepunt met geversioneerde URL. |
| previous | Optioneel veld in navigation: relatieve URL naar de versie die gesteld wordt als vorige ten opzichte van deze versie van de publicatie.<br>Moet overeen komen met het veld **urlref** van een ander publicatiepunt met geversioneerde URL. |

Voor het veld **urlref** geldt volgend formaat:
```
/doc/{documenttype}/{documentnaam}/{status}/{datum}
```

waarin:

| Veld | Beschrijving | Formaat |
|------|--------------|---------|
| `{documenttype}` | Geeft het type document aan. | `vocabularium` of `applicatieprofiel` of `implementatiemodel` | 
| `{documentnaam}` | Symbolische naam van het document. | kleine letters, spaties vervangen door `-` | 
| `{status}` | Label uit deze [status codelijst](https://data.vlaanderen.be/doc/conceptscheme/StandaardStatus), overeenstemmend met het veld **publication-state** in de gekozen entry in het JSON configuratiebestand in de OSLO thema repository. | kleine letters, spaties verwijderd | 
| `{datum}` | Datum van publicatie, in principe gelijk aan de waarde van het veld **publication-date** in de gekozen entry in het JSON configuratiebestand in de OSLO thema repository. | xsd:date formaat (YYYY-MM-DD) | 

Voorbeeld:
```
{
   "urlref": "/doc/vocabularium/besluitvorming/ontwerpstandaard/2020-03-17",
   "repository": "https://github.com/Informatievlaanderen/OSLOthema-besluitvorming",
   "branchtag" : "ontwerp-2020-03-17",
   "name" : "besluitvorming-voc",
   "filename" : "config/besluitvorming-voc.json",
   "navigation" : {
      "prev": "/doc/vocabularium/besluitvorming/ontwerpstandaard/2020-02-26",
      "next": "/doc/vocabularium/besluitvorming/kandidaatstandaard/2020-03-31"
   }
}
```

### Geval 2: met versieloze URL

Eén publicatie gemaakt met een geversioneerde, persistente URL wordt gedupliceerd op een versieloze URL, om zo een URL van de verondersteld geldende versie te kunnen communiceren.

Voor vocabularia is dit tevens van belang omdat via die versieloze URL de URI's in het vocabularium kunnen gederefereerd worden.

**Opgelet:** zolang [deze issue](https://github.com/Informatievlaanderen/OSLO-toolchain/issues/68) open staat, pas [deze workaround](https://github.com/Informatievlaanderen/OSLO-toolchain/issues/68#issuecomment-701969630) toe.


Formaat (één element uit de array):
```
{
   "dummy": "...",
   "disabled" : true,
   "urlref": "/ns/besluitvorming",
   "seealso": "/doc/vocabularium/besluitvorming/kandidaatstandaard/2020-03-31",
   "type" : "voc"
}
```

Velden:

| Veld | Beschrijving |
|------|--------------|
| dummy | Optioneel veld: voeg toe of wijzig de toegekende waarde om de toolchain te forceren de publicatie opnieuw te bouwen, zelfs als er geen andere velden in dit element werden gewijzigd. |
| disabled | Optioneel veld: voeg toe met waarde `true` om te verhinderen dat de toolchain de publicatie bouwt. Bedoeld om andere publicaties te kunnen bouwen als de publicatie in kwestie niet kan gebouwd worden wegens fouten. |
| urlref | Relatieve URL (= URL zonder domein) waarop de publicatie te consulteren zal zijn. |
| seealso | Relatieve URL van de geversioneerde publicatie waarvan deze publicatie een duplicaat is. |
| type | `voc` of `ap`; geeft aan of deze publicatie een vocabularium of een applicatieprofiel betreft. |

Voor het veld **urlref** geldt volgend formaat in geval van een vocabularium:
```
/ns/[{path}/]{documentnaam}
```

Voor het veld **urlref** geldt volgend formaat in geval van een applicatieprofiel:
```
/doc/{documenttype}/{documentnaam}
```

waarin telkens:

| Veld | Beschrijving | Formaat |
|------|--------------|---------|
| `{path}` | Optioneel, komt overeen met het veld **prefix** van het vocabularium (enkel indien dit veld aanwezig is) | kleine letters, spaties vervangen door `-` | 
| `{documentnaam}` | Symbolische naam van het document | kleine letters, spaties vervangen door `-` | 
| `{documenttype}` | Geeft het type document aan | `applicatieprofiel` of `implementatiemodel` | 

Voorbeeld:
```
{
   "dummy": "martin-2020-04-07",
   "urlref": "/ns/besluitvorming",
   "seealso": "/doc/vocabularium/besluitvorming/kandidaatstandaard/2020-03-31",
   "type" : "voc"
}
```

Bij dit voorbeeld: op 2020-03-31 werd een Kandidaat Standaard gepubliceerd en dit is op dit ogenblik de geldende versie.

### Geval 3: een legacy publicatie

Vóór toolchain versie 2.0 bestonden geen publicaties met geversioneerde URL's. Om dergelijke publicaties opnieuw te kunnen genereren is volgend type publicatieëlement toegevoegd.

Het formaat (één element uit de array) is identiek aan dit van geval 1, behalve volgende uitbreiding:

Formaat (één element uit de array):
```
{
   ...
   "type" : "raw"
}
```

Om te kunnen publiceren op dezelfde URL als voorheen, gaat dit type publicatieëlement altijd gepaard met een element uit geval 2.

Voorbeeld:
```
[
{
   "urlref": "/doc/vocabularium/mandaat/standaard/2018-07-20",
   "repository": "https://github.com/Informatievlaanderen/OSLOthema-lokaleBesluiten",
   "branchtag" : "mandaat",
   "name" : "mandaat",
   "navigation" : {
   },
   "type" : "raw"
},
{
   "urlref": "/ns/mandaat",
   "seealso": "/doc/vocabularium/mandaat/standaard/2018-07-20",
   "type" : "voc"
}
]
```

Bij dit voorbeeld: de publicatie op deze (relatieve) URL `/doc/vocabularium/mandaat/standaard/2018-07-20` is een reconstructie uit de tijd van toolchain 1.0,
en is gedupliceerd op (relatieve) URL `/ns/mandaat`.

### Uitbreiding op geval 1: met afhankelijkheden naar andere publicatiepunten

TODO
