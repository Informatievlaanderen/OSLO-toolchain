# OSLO toolchain publicatie flow

Deze pagina beschrijft de weg vanaf input bestanden tot gepubliceerde specificatie.

## Van input bestanden naar gegenereerde output bestanden

Voor elke branch van https://github.com/Informatievlaanderen/Data.Vlaanderen.be waarop de toolchain actief is,
worden commits op (een of meerdere) **publicatiebestanden** in de **config** directory bewaakt (bijvoorbeeld publication.json). 

Voor elk **publicatiepunt** dat werd aangepast in een publicatiebestand wordt output gegenereerd op de gelijknamige branch in
https://github.com/Informatievlaanderen/OSLO-Generated.

De input wordt gelezen uit een commit in een OSLO thema github repository.
Welk bestand, welke commit wordt in detail beschreven in de gebruikersdocumentatie....

De output bestaat uit een rapport en de te publiceren bestanden.
- Het rapport is te vinden in directory `report/{pad}` (bestand met extensie .report).
- De te publiceren bestanden zijn te vinden in directory `{pad}`. Deze worden enkel gemaakt als het proces goed afloopt (zie het rapport).

Hierin is `{pad}` de waarde van eigenschap `urlref` in het **publicatiepunt**.

### Een voorbeeld

Op de `test` branch in https://github.com/Informatievlaanderen/Data.Vlaanderen.be staat in `config/publication.json`
een publicatiepunt gedefinieerd als volgt:
```
{
   "urlref": "/doc/vocabularium/besluitvorming/kandidaatstandaard/2020-03-31",
   "repository": "https://github.com/Informatievlaanderen/OSLOthema-besluitvorming",
   ...
},
```

De input komt uit een commit in https://github.com/Informatievlaanderen/OSLOthema-besluitvorming.

De output komt terecht op de `test` branch in https://github.com/Informatievlaanderen/OSLO-Generated:
- rapport in `report/doc/vocabularium/besluitvorming/kandidaatstandaard/2020-03-31` 
- te publiceren bestanden in `report/doc/vocabularium/besluitvorming/kandidaatstandaard/2020-03-31` 

## Van output bestanden naar gepubliceerde specificatie

Een korte tijd (typisch 5 minuten) na de aanmaak van nieuwe te publiceren bestanden (zie hierboven), worden deze zichtbaar
op `{domein}/{pad}`.

Hierin is `{pad}` opnieuw de waarde van eigenschap `urlref` in het publicatiepunt. 
   
Het `{domein}` hangt als volgt af van de branch waarop het publicatiebestand zich bevindt.

| Branch | Domein | Bedoeling |
|--------|--------|-----------|
| `production` | https://data.vlaanderen.be | Uiteindelijke plaats voor alle officiële publicaties. |
| `test` | https://test.data.vlaanderen.be | Tijdelijke plaats om nieuwe publicaties voor te bereiden. |
| `dev` | https://dev.data.vlaanderen.be | Plaats om ontwikkelingen aan de tooling uit te testen. |
| `test-feature-checkout` | https://otl-test.data.vlaanderen.be | Binnenkort buiten dienst te stellen oude tijdelijke plaats om nieuwe publicaties voor te bereiden en om ontwikkelingen aan de tooling uit te testen. |

### Een voorbeeld

Aansluitend op het voorbeeld hierboven: de publicatie is te vinden op:
https://test.data.vlaanderen.be/doc/vocabularium/besluitvorming/kandidaatstandaard/2020-03-31.
