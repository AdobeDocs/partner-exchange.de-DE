---
title: Importieren von Batch-Daten in AEP
description: Erfahren Sie, wie Sie Batch-Dateien in Experience Platform importieren
exl-id: 50576b67-b3ba-498e-86f6-7e1986b76985
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 10%

---

# Importieren von Batch-Daten in AEP

AEP kann Batch-Dateien erfassen, die Profildaten aus einer reduzierten Datei (z. B. Parquet) oder Daten enthalten, die einem bekannten Schema im [!UICONTROL Experience-Datenmodell] (XDM)-Registrierung.

AEP kann Daten mithilfe von Batch-Dateien erfassen. Die folgenden Formate werden akzeptiert: JSON, Parquet und CSV.

Dieser Artikel behandelt Folgendes:

* Voraussetzungen für die Batch-Erfassung
* Best Practices und Einschränkungen bei der Batch-Erfassung
* Erstellen eines Batches
* Fertigstellen eines Batches
* Überprüfen des Status eines Batches

Die [Postman-Sammlung](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wird im gesamten Artikel mit den zugehörigen Aufrufen nach Anzahl referenziert. Weitere Informationen zur Installation und Verwendung der Postman-Sammlung finden Sie auf Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) Seite. Es gibt auch Beispieldatensätze von [Treue](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) und [profile](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) Daten.

Verwenden Sie für alle Aufrufe in diesem Tutorial Postman-Aufrufordner: 4: Batch-Import, 4a: Batch-Import für PROFILE-Daten ODER 4b: Batch-Import für EREIGNISdaten.

## Voraussetzungen für die Batch-Erfassung

* Definieren Sie ein Schema und erstellen Sie einen Datensatz.
* Die Daten müssen in JSON, Parquet oder CSV formatiert sein.
* [Auf der Plattform authentifizieren](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/home.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).
* Erfassen Sie die Werte für erforderliche Kopfzeilen im oben verknüpften Authentifizierungs-Tutorial.

## Best Practices und Einschränkungen bei der Batch-Erfassung

* Maximale Batch-Größe: 100 GB
* Maximale Anzahl von Dateien pro Batch: 1.500
* Wenn eine Datei größer als 512 MB ist, muss sie in kleinere Abschnitte unterteilt werden. Weitere Informationen finden Sie im [Entwicklerhandbuch](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* Maximale Anzahl von Eigenschaften oder Feldern pro Zeile: 10.000
* Maximale Anzahl der Batches pro Minute und Anwender: 138

## Erstellen eines Batches

In diesem Tutorial verwenden wir JSON als Format. Weitere Formatbeispiele finden Sie im Abschnitt [Entwicklerhandbuch](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
Erstellen Sie einen Batch mit JSON als Eingabeformat (stellen Sie sicher, dass Sie eine Datensatz-ID einschließen und dass Ihre Daten dem mit dem Datensatz verknüpften XDM-Schema entsprechen):

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

Antwort:

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

## Dateien hochladen

Dateien können jetzt in den neu erstellten Batch hochgeladen werden (mithilfe der batch_id aus der obigen Antwort).

```json
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

>[!NOTE]
>
>Die API unterstützt nur das Hochladen einzelner Teile, d. h. jede Datei/jeder Mikrobatch muss mit einzelnen Aufrufen hochgeladen werden. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet.

Antwort:

```
200 OK
```

## Batch abschließen

Sobald alle Dateien hochgeladen wurden, signalisiert dieser Aufruf, dass der Batch bereit zur Promotion ist:

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Antwort:

```
200 OK
```

## Status eines Batches überprüfen

Der Batch-Status kann in der Benutzeroberfläche oder über die API überprüft werden (siehe Aufruf unten). Um die Benutzeroberfläche einzuchecken, navigieren Sie zum DataSet , um den Status anzuzeigen.

Die verschiedenen Status der Batch-Erfassung finden Sie [here](https://adobe.ly/2TMMCmj).


```json
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Antwort:

```json
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

## Referenzartikel

* [Data Ingestion-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Batch-Erfassung - Übersicht](https://docs.adobe.com/content/help/de-DE/experience-platform/ingestion/home.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/ingest_architectural_overview.md)
* [Entwicklerhandbuch zur Batch-Erfassung](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* [Handbuch zur Fehlerbehebung bei der Batch-Erfassung](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_troubleshooting_guide.md)
* [Datenerfassung in Postman](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json)
* [Authentifizierungs-Tutorial](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/home.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)
