---
title: Zugreifen auf das einheitliche Profil
description: Verwenden Sie APIs, um auf das einheitliche Profil zuzugreifen.
exl-id: c9d2fa2d-9ffe-4e66-996f-ad930bee22c6
source-git-commit: 0690a52c3be0981a626e49729e51cb1729816c87
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 7%

---

# Zugreifen auf das einheitliche Profil mithilfe der Profil-API

Der Adobe-[!DNL Experience Platform] kann in Echtzeit auf das Kundenprofil zugreifen. Die [[!DNL Experience Platform] Echtzeit-Kundenprofil-API](https://adobe.ly/2TtDHWr) wurde für die Interaktion mit diesem Profil entwickelt. In diesem [Tutorial](https://docs.adobe.com/content/help/de-DE/experience-platform/profile/api/getting-started.html) finden Sie Informationen zum Zugriff auf die Echtzeit-Kundenprofildaten mithilfe der Profil-API.

In diesem Artikel wird im Wesentlichen auf das oben verlinkte Tutorial verwiesen.

Die [Postman-](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wird im gesamten Artikel mithilfe der zugehörigen Aufrufe nach Nummer referenziert. Weitere Informationen zur Installation und Verwendung der Postman-Sammlung finden Sie auf der GitHub-Seite [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Es gibt auch Beispieldatensätze mit [Treueprogramm](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json)- und [Profil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json)Daten.

Verwenden Sie für diesen Abschnitt den Postman-Ordner 5: Profilsuche, 5a: Echtzeit-Lookup-PROFILDATEN ODER 5b: Echtzeit-Lookup-EREIGNISDATEN.

## Verwenden der API

Die folgenden Abschnitte helfen Ihnen bei der Authentifizierung bei Experience Platform. Erfahren Sie mehr über den API-Pfad, Kopfzeileninformationen und mehr.

### Authentifizieren bei [!DNL Platform]

Lesen Sie [&#x200B; Authentifizierungs](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/authentication.html)Tutorial , bevor Sie einen der folgenden Aufrufe ausführen.

### API-Pfad

Die Plattform-Gateway-URL, die für die Echtzeit-Kundenprofil-API benötigt wird, lautet: `https://platform.adobe.io/`

Der Basispfad für die API lautet: `/data/core/ups/access/entities`

Beispiel für einen vollständigen Pfad: `https://platform.adobe.io/data/core/ups/access/entities`

### Kopfzeileninformationen

Die Kopfzeile muss Folgendes enthalten:

* Autorisierung
* x-gw-ims-org-id - Abruf über console.adobe.io
* X-API-Schlüssel - Abruf über console.adobe.io
* x-sandbox-name - abgerufen vom Adobe Integration Manager
* Content-Type: application/json

Weitere Informationen zur Kopfzeile finden Sie im [Tutorial](https://adobe.ly/2PTHuKv).

## Zugreifen auf Echtzeit-Kundenprofile mithilfe von Identitäten

Die Profil-API ermöglicht über eine GET-Anfrage den Zugriff auf Profile unter Verwendung von Identitäten. Die folgenden Abschnitte folgen diesem [Handbuch](https://docs.adobe.com/content/help/de-DE/experience-platform/profile/api/entities.html).

### Zugreifen auf Profildaten mithilfe von Identitäten

Die API ermöglicht den Zugriff auf Profilinformationen mithilfe von Identitäten. Dies geschieht, indem eine GET-Anfrage an /access/entities gesendet wird, wobei die Entitäts-ID einer der Parameter und der Entitäts-ID-Namespace ist. HINWEIS: Beachten Sie, dass jede Anfrage, die 50 Datensätze zurückgibt, nur einen 422-HTTP-Status und eine Nachricht mit dem Hinweis „zu viele verwandte Identitäten“ liefert und die Suche mit weiteren Parametern eingegrenzt werden muss.

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

### Zugriff auf Profile nach Liste der Identitäten

Die API ermöglicht den Zugriff auf Profile mithilfe einer Liste von Identitäten, indem sie eine POST-Anfrage an den Endpunkt /access/entities verwendet und die Identitäten in der Payload bereitstellt. Diese Identitäten bestehen aus einem ID-Wert (entityId) und einem Identity-Namespace (entityIdNS).

Anfrage:
Mit der folgenden Anfrage werden die Namen und E-Mail-Adressen mehrerer Kunden anhand einer Liste von Identitäten abgerufen:

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

Antwort:
Eine erfolgreiche Antwort gibt die angeforderten Felder von Entitäten zurück, die im Anfragetext angegeben sind.

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

Partner können auf Zeitreihenereignisse über die Identität der zugehörigen Profilentität zugreifen, indem sie eine GET-Anfrage an den Endpunkt /access/entities stellen.

### Auf Zeitreihenereignisse für ein Profil nach Identität zugreifen

Auf Zeitreihenereignisse kann über die Identität der zugehörigen Profilentität zugegriffen werden, indem eine GET-Anfrage an den Endpunkt /access/entities gestellt wird. Diese Identität besteht aus einem ID-Wert (entityId) und einem Identity-Namespace (entityIdNS).

Anfrage:
Die folgende Anfrage sucht nach einer Profilentität anhand der ID und ruft die Werte für die Eigenschaften endUserIDs, Web und Kanal (**alle**) ab, die mit der Entität verknüpft sind.

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Antwort:

Bei einer erfolgreichen Antwort wird eine paginierte Liste von Zeitreihenereignissen und zugehörigen Feldern zurückgegeben, die in den Anfrageparametern angegeben wurden.

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

Ergebnisse werden beim Abrufen von Zeitreihenereignissen paginiert. Wenn nachfolgende Ergebnisseiten vorhanden sind, enthält der Parameter &lowBar;page.next der Antwort eine ID. Darüber hinaus stellt der Parameter &lowBar;links.next.href der Antwort einen Anfrage-URI zum Abrufen der nachfolgenden Seite bereit.

Anfrage:

Die folgende Anfrage ruft die nächste Ergebnisseite ab, indem der _links.next.href-URI als Anfragepfad verwendet wird.

```
curl -X GET \

  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Antwort:

Eine erfolgreiche Antwort gibt die nächste Ergebnisseite zurück. Dieses Beispiel zeigt eine Antwort, bei der keine nachfolgenden Ergebnisseiten vorhanden sind, wie durch die leeren Zeichenfolgenwerte von &lowBar;page.next und &lowBar;links.next.href angegeben.

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
* [Tutorial zum Zugriff auf Echtzeit-Kundenprofildaten über die Profil-API](https://docs.adobe.com/content/help/de-DE/experience-platform/profile/api/getting-started.html)
* [[!DNL Experience Platform] Authentifizierungshandbuch](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/authentication.html)
