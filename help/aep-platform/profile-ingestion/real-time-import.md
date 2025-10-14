---
title: Echtzeit-Import
description: Erfahren Sie, wie Sie Daten in Echtzeit in AEP importieren.
exl-id: 0b6215a9-1160-49ae-8aa5-302b47357200
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# Streamen von Daten an AEP

Mit Adobe [!DNL Experience Platform] können Profil- und Erlebnisereignisse gestreamt und nahezu in Echtzeit verfügbar sein. Alle Daten, die über Streaming an AEP gesendet werden, bleiben im Data Lake erhalten. Daten können über APIs oder mithilfe von Adobe Launch an vorhandene Datensätze oder völlig neue Datensätze gestreamt werden.

Dieser Artikel behandelt Folgendes:

* Streaming an das individuelle XDM-Profil
* Streaming an das XDM ExperienceEvent
* Streamen mit der AEP Launch-Erweiterung

Die [Postman-](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wird im gesamten Artikel mithilfe der zugehörigen Aufrufe nach Nummer referenziert. Weitere Informationen zur Installation und Verwendung der Postman-Sammlung finden Sie auf der GitHub-Seite [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Es gibt auch Beispieldatensätze mit [Treueprogramm](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json)- und [Profil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json)Daten.

## Voraussetzungen

* [Authentifizierung bei der Plattform](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/authentication.html).
* Erfassen Sie die Werte für die erforderlichen Kopfzeilen aus dem oben verlinkten Authentifizierungs-Tutorial.

## Aufbauen einer Streaming-Verbindung

Um zu AEP zu streamen, müssen Sie zunächst eine Streaming-Verbindung erstellen. Streaming-Verbindungen enthalten Attribute wie die Quelle von Streaming-Daten und ob Sie Datensätze senden, die zu den [!DNL Experience Data Model] (XDM)-Schemata gehören oder nicht. Nachdem Sie eine Streaming-Verbindung erstellt haben, erhalten Sie eine eindeutige URL, mit der Sie Daten in AEP streamen können.

Unter [hier](https://docs.adobe.com/content/help/de-DE/experience-platform/ingestion/tutorials/create-streaming-connection.html) finden Sie Anweisungen zum Erstellen einer Streaming-Verbindung über eine API oder [hier](https://docs.adobe.com/content/help/de-DE/experience-platform/ingestion/tutorials/create-streaming-connection-ui.html) Anweisungen zum Erstellen einer Streaming-Verbindung über die Benutzeroberfläche.

```json
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

Antwort:

```json
 {
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

Denken Sie daran, die in der obigen Antwort angegebene ID für zukünftige Streaming-Aufnahmeaufrufe zu speichern (die Postman-Sammlung speichert diese für Sie in der Umgebungsvariablen CONNECTION_ID).

## Streamen von Profildaten an AEP

Verwenden Sie für diesen Abschnitt Postman-Aufrufordner: 3: Echtzeit-Import, 3a: Echtzeit-Import für Profildaten.

Detaillierte JSON-Anfragen mit Antworten für Streaming-Profildaten sind ([) &#x200B;](https://docs.adobe.com/content/help/de-DE/experience-platform/ingestion/tutorials/streaming-record-data.html).

Schritte:

1. Erstellen eines Schemas für ein individuelles XDM-Profil
1. Festlegen des Primären Identitätsdeskriptors für ein individuelles XDM-Profil (Primärschlüssel)
1. Erstellen eines Datensatzes für XDM Individual Profile-Datensätze
1. Aufrufen der Streaming-Aufnahme-APIs zum Erstellen eines Datensatzes mit einem individuellen XDM-Profil
1. Abrufen des neu erstellten Profils

## Streamen von Erlebnisereignissen an AEP

Verwenden Sie für diesen Abschnitt Postman-Aufrufordner: 3: Echtzeit-Import, 3b: Echtzeit-Import für Profildaten.

Detaillierte JSON-Anfragen mit Antworten für das Streaming von Erlebnisdaten sind ([) &#x200B;](https://docs.adobe.com/content/help/de-DE/experience-platform/ingestion/tutorials/streaming-time-series-data.html).

Schritte:

1. Erstellen eines XDM-ExperienceEvent-Schemas
1. Festlegen des Primären Identitätsdeskriptors für XDM ExperienceEvent (Primärschlüssel)
1. Erstellen eines Datensatzes für XDM ExperienceEvents
1. Aufrufen der Streaming-Aufnahme-APIs zum Erstellen eines XDM ExperienceEvent
1. Abrufen des neu erstellten Ereignisses

## Verwenden von Experience Platform-Tags zum Streamen an AEP

Die Adobe [!DNL Experience Platform] Launch-Erweiterung bietet eine Möglichkeit, über Launch zu AEP zu streamen. Weitere Informationen finden Sie [diesem Handbuch](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html).

## Referenzartikel

* [Datenaufnahme-APIs](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Streaming-Aufnahme - Übersicht](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/streaming_ingest_overview.md)
* [Entwicklerhandbuch zur Streaming-Aufnahme](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/getting_started_with_platform_streaming_ingestion.md)
* [Verwenden der AEP Launch-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)
