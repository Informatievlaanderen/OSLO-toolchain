# OSLO toolchain publicatie flow

Deze pagina is louter illustratief voor eindgebruikers.

Mogelijk nut is het nakijken van rapporten tijdens het troubleshooten of het vergelijken van de output tussen verschillende versies van publicaties.

## Van bronbestanden naar gegenereerde output bestanden

Voor elke wijziging aan een publicatiepunt vermeld in een **JSON bestand in de centrale repository** op een bepaalde branch, zoals beschreven in [configuratie van een publicatiepunt](configuratie-van-een-publicatiepunt.md),
wordt output gegenereerd op de gelijknamige branch in https://github.com/Informatievlaanderen/OSLO-Generated (later: https://github.com/Informatievlaanderen/data.vlaanderen.be-generated).

Dit proces kan overigens voor wie toegang heeft gevolgd worden op [CircleCI](https://circleci.com/gh/Informatievlaanderen/Data.Vlaanderen.be).

De output bestaat uit een rapport en de te publiceren bestanden.
- Het rapport is te vinden in directory `report/{pad}` (bestand met extensie .report).
- De te publiceren bestanden zijn te vinden in directory `{pad}`. Deze worden enkel gemaakt als het proces goed afloopt (zie het rapport).

Hierin is `{pad}` de waarde van eigenschap `urlref` in het publicatiepunt.

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

De bronbestanden staan in `https://github.com/Informatievlaanderen/OSLOthema-besluitvorming`.

De output komt terecht op de `test` branch in https://github.com/Informatievlaanderen/OSLO-Generated (later: https://github.com/Informatievlaanderen/data.vlaanderen.be-generated):
- rapport in `report/doc/vocabularium/besluitvorming/kandidaatstandaard/2020-03-31` 
- te publiceren bestanden in `report/doc/vocabularium/besluitvorming/kandidaatstandaard/2020-03-31` 

## Van output bestanden naar gepubliceerde specificatie

Een korte tijd (typisch 5 minuten) na de aanmaak van nieuwe te publiceren bestanden (zie hierboven), worden deze zichtbaar
op de URL zoals verder beschreven in beschreven in [configuratie van een publicatiepunt](configuratie-van-een-publicatiepunt.md).

### Een voorbeeld

Aansluitend op het voorbeeld hierboven: de publicatie is te vinden op:
`https://test.data.vlaanderen.be/doc/vocabularium/besluitvorming/kandidaatstandaard/2020-03-31`.
