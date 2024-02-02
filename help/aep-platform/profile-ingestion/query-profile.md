---
title: Zugriff auf das einheitliche Profil
description: Verwenden Sie APIs für den Zugriff auf das einheitliche Profil.
exl-id: c9d2fa2d-9ffe-4e66-996f-ad930bee22c6
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 8%

---

# Zugriff auf das einheitliche Profil mithilfe der Profil-API

Die Adobe [!DNL Experience Platform] kann in Echtzeit auf das Kundenprofil zugreifen; die [[!DNL Experience Platform] Echtzeit-Kundenprofil-API](https://adobe.ly/2TtDHWr) wurde für die Interaktion mit diesem Projekt entwickelt. Siehe dies [Tutorial](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html) für den Zugriff auf die Echtzeit-Kundenprofildaten mithilfe der Profil-API.

Dieser Artikel verweist im Wesentlichen auf das oben verlinkte Tutorial.

Die [Postman-Sammlung](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wird im gesamten Artikel mit den zugehörigen Aufrufen nach Anzahl referenziert. Weitere Informationen zur Installation und Verwendung der Postman-Sammlung finden Sie auf Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) Seite. Es gibt auch Beispieldatensätze von [Treue](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) und [profile](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) Daten.

Verwenden Sie für diesen Abschnitt den Ordner Postman 5: Profile Lookup, 5a: Real-time lookup PROFILE data ODER 5b: Real-time lookup EVENT data.

## Verwenden der API

Die folgenden Abschnitte helfen Ihnen bei der Authentifizierung bei Experience Platform. Erfahren Sie mehr über den API-Pfad, Kopfzeileninformationen und mehr.

### Authentifizieren bei [!DNL Platform]

Siehe [this](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/authentication.html) Authentifizierungs-Tutorial , bevor Sie einen der folgenden Aufrufe ausführen.

### API-Pfad

Die Plattform-Gateway-URL, die für die Echtzeit-Kundenprofil-API benötigt wird, lautet: `https://platform.adobe.io/`

Der Basispfad für die API lautet: `/data/core/ups/access/entities`

Ein Beispiel für einen vollständigen Pfad ist: `https://platform.adobe.io/data/core/ups/access/entities`

### Kopfzeileninformationen

Die Kopfzeile muss Folgendes enthalten:

* Autorisierung
* x-gw-ims-org-id - Abrufen über console.adobe.io
* x-api-key - Abrufen über console.adobe.io
* x-sandbox-name - vom Adobe Integration Manager abgerufen
* Content-Type: application/json

Weitere Informationen zur Kopfzeile finden Sie im [Tutorial](https://adobe.ly/2PTHuKv).

## Zugriff auf Echtzeit-Kundenprofile mithilfe von Identitäten

Die Profil-API ermöglicht den Zugriff auf Profile mithilfe von Identitäten über eine GET-Anfrage. Die folgenden Abschnitte folgen diesem [Handbuch](https://docs.adobe.com/content/help/en/experience-platform/profile/api/entities.html).

### Profildaten mithilfe der Identität aufrufen

Die API ermöglicht den Zugriff auf Profilinformationen mithilfe der Identität. Dies geschieht, indem Sie eine GET-Anfrage an /access/entity mit der Entitäts-ID als einem der Parameter und dem Entitäts-ID-Namespace senden. HINWEIS: Beachten Sie, dass jede Anfrage, die 50 Datensätze zurückgibt, nur den HTTP-Status 422 und eine Meldung mit dem Wortlaut &quot;Zu viele verwandte Identitäten&quot;liefert. Die Suche muss mit mehr Parametern eingeschränkt werden.

Anfrage:

Die folgende Anfrage ruft die E-Mail-Adresse und den Namen eines Kunden mit einer Identität ab:

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Antwort:

```
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

### Zugriff auf Profile anhand der Identitätsliste

Die API ermöglicht den Zugriff auf Profile mithilfe einer Identitätsliste, indem sie eine POST-Anfrage an den Endpunkt /access/entity sendet und die Identitäten in der Payload angibt. Diese Identitäten bestehen aus einem ID-Wert (entityId) und einem Identitäts-Namespace (entityIdNS).

Anfrage: Mit der folgenden Anfrage werden die Namen und E-Mail-Adressen mehrerer Kunden anhand einer Liste von Identitäten abgerufen:

```
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema":{
        "name":"_xdm.context.profile"
    },
    "fields":["identities","person.name","workEmail"],
    "identities":[
        {
            "entityId":"89149270342662559642753730269986316601",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316900",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316602",
            "entityIdNS":{
                "code":"ECID"
            }
        }
    ]
}'
```

Antwort: Eine erfolgreiche Antwort gibt die angeforderten Felder von Entitäten zurück, die im Anfrageinhalt angegeben sind.

```
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## Zeitreihen-Ereignisse

Partner können auf Zeitreihenereignisse anhand der Identität der zugehörigen Profilentität zugreifen, indem sie eine GET an den Endpunkt /access/entity anfordern.

### Auf Zeitreihenereignisse für ein Profil nach Identität zugreifen

Auf Zeitreihenereignisse kann über die Identität der zugehörigen Profilentität zugegriffen werden, indem eine GET-Anfrage an den Endpunkt /access/entity gestellt wird. Diese Identität besteht aus einem ID-Wert (entityId) und einem Identitäts-Namespace (entityIdNS).

Anfrage: Die folgende Anfrage sucht nach einer Profilentität anhand der Kennung und ruft die Werte für die Eigenschaften endUserIDs, web und channel ab. **für alle** Zeitreihenereignisse, die mit der Entität verknüpft sind.

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Antwort:

Eine erfolgreiche Antwort gibt eine paginierte Liste von Zeitreihenereignissen und zugehörigen Feldern zurück, die in den Anfrageparametern angegeben wurden.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Paginierung für Zeitreihenereignisse für ein Profil

Ergebnisse werden beim Abrufen von Zeitreihenereignissen paginiert. Wenn es nachfolgende Ergebnisseiten gibt, enthält der Parameter _page.next der Antwort eine ID. Darüber hinaus stellt der Parameter _links.next.href der Antwort einen Anfrage-URI zum Abrufen der nachfolgenden Seite bereit.

Anfrage:

Die folgende Anfrage ruft die nächste Ergebnisseite ab, indem der URI _links.next.href als Anfragepfad verwendet wird.

```
curl -X GET \

  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Antwort:

Eine erfolgreiche Antwort gibt die nächste Ergebnisseite zurück. Dieses Beispiel zeigt eine Antwort, in der keine nachfolgenden Ergebnisseiten vorhanden sind, wie durch die leeren Zeichenfolgenwerte von _page.next und _links.next.href angegeben.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Referenzartikel

* [Echtzeit-Kundenprofil-API](https://adobe.ly/2TtDHWr)
* [Zugriff auf Echtzeit-Kundenprofildaten mithilfe des Profil-API-Tutorials](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html)
* [[!DNL Experience Platform] Authentifizierungshandbuch](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/authentication.html)
