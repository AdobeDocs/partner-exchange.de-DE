---
title: Echtzeitimport
description: Erfahren Sie, wie Sie Daten in Echtzeit in AEP importieren.
exl-id: 0b6215a9-1160-49ae-8aa5-302b47357200
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 2%

---

# Streamen von Daten an AEP

Adobe [!DNL Experience Platform] ermöglicht das Streamen von Profil- und Erlebnisereignissen und steht nahezu in Echtzeit zur Verfügung. Alle Daten, die über Streaming an AEP gesendet werden, bleiben im Data Lake erhalten. Daten können über APIs oder Adobe Launch an bestehende Datensätze oder an vollständig neue Datensätze gestreamt werden.

Dieser Artikel behandelt Folgendes:

* Streaming an das individuelle XDM-Profil
* Streaming in das XDM ExperienceEvent
* Verwenden von AEP für die Launch-Erweiterung zum Streamen

Die [Postman-Sammlung](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wird im gesamten Artikel mit den zugehörigen Aufrufen nach Anzahl referenziert. Weitere Informationen zur Installation und Verwendung der Postman-Sammlung finden Sie auf Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) Seite. Es gibt auch Beispieldatensätze von [Treue](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) und [profile](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) Daten.

## Voraussetzungen

* [Auf der Plattform authentifizieren](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/authentication.html).
* Erfassen Sie die Werte für erforderliche Kopfzeilen im oben verknüpften Authentifizierungs-Tutorial.

## Aufbauen einer Streaming-Verbindung

Um auf AEP zu streamen, müssen Sie zunächst eine Streaming-Verbindung erstellen. Streaming-Verbindungen enthalten Attribute wie die Quelle der Streaming-Daten und darüber, ob Sie Datensätze senden, die zum [!DNL Experience Data Model] (XDM)-Schemas. Nachdem Sie eine Streaming-Verbindung erstellt haben, erhalten Sie eine eindeutige URL, mit der Sie Daten in AEP streamen.

Los [here](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection.html) für Anweisungen zum Erstellen einer Streaming-Verbindung über APIs oder [here](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection-ui.html) für Anweisungen zum Erstellen einer Streaming-Verbindung über die Benutzeroberfläche.

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

Achten Sie darauf, die in der obigen Antwort angegebene ID für zukünftige Streaming-Erfassungsaufrufe zu speichern (die Postman-Sammlung speichert diese für Sie in der Umgebungsvariablen CONNECTION_ID ).

## Profildaten an AEP streamen

Verwenden Sie für diesen Abschnitt die Postman-Aufrufordner: 3: Echtzeitimport, 3a: Echtzeitimport für PROFILE-Daten.

Detaillierte JSON-Anfragen mit Antworten für Streaming-Profildaten werden dokumentiert. [here](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-record-data.html).

Schritte:

1. Erstellen eines XDM Individual Profile-Schemas
1. Festlegen des Primären Identitätsdeskriptors für XDM Individual Profile (Primärschlüssel)
1. Datensatz für individuelle XDM-Profildatensätze erstellen
1. Rufen Sie die Streaming-Aufnahme-APIs auf, um einen individuellen XDM-Profildatensatz zu erstellen
1. Abrufen des neu erstellten Profils

## Streamen von Erlebnisereignissen an AEP

Verwenden Sie für diesen Abschnitt die Postman-Aufrufordner: 3: Echtzeitimport, 3b: Echtzeitimport für PROFILE-Daten.

Detaillierte JSON-Anfragen mit Antworten für Streaming-Erlebnisdaten werden dokumentiert. [here](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-time-series-data.html).

Schritte:

1. Erstellen eines XDM ExperienceEvent-Schemas
1. Festlegen des Primären Identitätsdeskriptors für XDM ExperienceEvent (Primärschlüssel)
1. Datensatz für XDM ExperienceEvents erstellen
1. Rufen Sie die Streaming-Aufnahme-APIs auf, um ein XDM ExperienceEvent zu erstellen
1. Abrufen des neu erstellten Ereignisses

## Verwenden von Experience Platform-Tags zum Streamen an AEP

Die Adobe [!DNL Experience Platform] Die Launch-Erweiterung bietet eine Möglichkeit, über Launch zu AEP zu streamen. Weitere Informationen finden Sie unter [diesem Handbuch](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html).

## Referenzartikel

* [Data Ingestion-APIs](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Streaming-Erfassung - Überblick](https://docs.adobe.com/content/help/de-DE/experience-platform/ingestion/home.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/streaming_ingest_overview.md)
* [Entwicklerhandbuch zur Streaming-Erfassung](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/getting_started_with_platform_streaming_ingestion.md)
* [Verwenden der AEP Launch-Erweiterung](https://docs.adobe.com/content/help/de-DE/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)
