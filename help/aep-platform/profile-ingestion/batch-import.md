---
title: Importieren von Batch-Daten in AEP
description: Erfahren Sie, wie Sie Batch-Dateien in Experience Platform importieren
exl-id: 50576b67-b3ba-498e-86f6-7e1986b76985
TQID: https://experienceleague.adobe.com/sJjuydUOIwlu4gv6qmokidQJVrYLN4--M8m3DTkcjf0
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 646
ht-degree: 11%

---

# Importieren von Batch-Daten in AEP

AEP kann Batch-Dateien aufnehmen, die Profildaten aus einer flachen Datei (z. B. Parquet) oder Daten enthalten, die einem bekannten Schema in der Registrierung [!UICONTROL Experience-Datenmodell] (XDM) entsprechen.

AEP kann Daten mithilfe von Batch-Dateien aufnehmen. Die folgenden Formate werden akzeptiert: JSON, Parquet und CSV.

Dieser Artikel behandelt Folgendes:

* Voraussetzungen für die Batch-Aufnahme
* Best Practices und Einschränkungen bei der Batch-Aufnahme
* So wird ein Batch erstellt
* So wird ein Batch ausgeführt
* Überprüfen des Status eines Batches

Die [Postman-](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wird im gesamten Artikel mithilfe der zugehörigen Aufrufe nach Nummer referenziert. Weitere Informationen zur Installation und Verwendung der Postman-Sammlung finden Sie auf der GitHub-Seite [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Es gibt auch Beispieldatensätze mit [Treueprogramm](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json)- und [Profil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json)Daten.

Verwenden Sie für alle Aufrufe in diesem Tutorial Postman-Aufrufordner: 4: Batch-Import, 4a: Batch-Import für Profildaten ODER 4b: Batch-Import für EREIGNISDATEN.

## Voraussetzungen für die Batch-Aufnahme

* Definieren eines Schemas und Erstellen eines Datensatzes.
* Daten müssen in JSON, Parquet oder CSV formatiert sein.
* [Authentifizierung bei der Plattform](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/home.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).
* Erfassen Sie die Werte für die erforderlichen Kopfzeilen aus dem oben verlinkten Authentifizierungs-Tutorial.

## Best Practices und Einschränkungen bei der Batch-Aufnahme

* Maximale Batch-Größe: 100 GB
* Maximale Anzahl von Dateien pro Batch: 1.500
* Wenn eine Datei größer als 512 MB ist, muss sie in kleinere Abschnitte unterteilt werden. Weitere Informationen finden Sie im [Entwicklerhandbuch](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* Maximale Anzahl von Eigenschaften oder Feldern pro Zeile: 10.000
* Maximale Anzahl der Batches pro Minute und Anwender: 138

## Erstellen eines Batches

In diesem Tutorial verwenden wir JSON als Format. Weitere Beispiele für Formate finden Sie im [Entwicklerhandbuch](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
Erstellen Sie einen Batch mit JSON als Eingabeformat (stellen Sie sicher, dass Sie eine Datensatz-ID enthalten und Ihre Daten dem mit dem Datensatz verknüpften XDM-Schema entsprechen):

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
>Die API unterstützt nur den einteiligen Upload, d. h. jede Datei/jeder Mikrobatch muss mit einzelnen Aufrufen hochgeladen werden. Stellen Sie sicher, dass der Content-Type „application/octet-stream“ lautet.

Antwort:

```
200 OK
```

## Abschließen eines Batches

Nachdem alle Dateien hochgeladen wurden, signalisiert dieser Aufruf, dass der Batch zur Promotion bereit ist:

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

## Überprüfen des Status eines Batches

Der Batch-Status kann in der Benutzeroberfläche oder über die API überprüft werden (siehe Aufruf unten). Um die Benutzeroberfläche einzuchecken, navigieren Sie zum DataSet, um den Status anzuzeigen.

Die verschiedenen Batch-Erfassungsstatus finden Sie [hier](https://adobe.ly/2TMMCmj).


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

* [Datenaufnahme-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Übersicht über die Batch-Aufnahme](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/ingest_architectural_overview.md)
* [Entwicklerhandbuch zur Batch-Aufnahme](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* [Handbuch zur Fehlerbehebung bei der Batch-Aufnahme](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_troubleshooting_guide.md)
* [Datenerfassung - Postman-Sammlung](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json)
* [Authentifizierungs-Tutorial](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/home.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)
