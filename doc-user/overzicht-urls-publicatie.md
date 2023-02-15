# Overzicht van URLs bij het aanmaken van een publicatie

1. Thema repository: <https://github.com/Informatievlaanderen/OSLOthema-{naam}>
2. Centraal configuratiepunt: <https://github.com/Informatievlaanderen/Data.Vlaanderen.be/blob/{branch}/config/{branch}/{naam}.publication.json>
3. Publicatieproces volgen: <https://app.circleci.com/pipelines/github/Informatievlaanderen/Data.Vlaanderen.be>
4. Gegenereerde bestanden: <https://github.com/Informatievlaanderen/data.vlaanderen.be-generated/tree/{branch}/{urlref}>
5. Publicatie: <https://{branch1}data.vlaanderen.be/{urlref}>

Waarin:
- {naam}: naam gegeven aan het thema
- {branch}: github branch
- {urlref}: pad zoals aangegeven in het centraal configuratiepunt
- {branch1}: github branch gevolgd door '.' of leeg als de github branch 'production' is