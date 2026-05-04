---
title: Handbuch zur Integration von [!DNL Platform]-Profilaufnahme und -zugriff - Übersicht
description: Erfahren Sie mehr über die Integration  [!DNL Experience Platform]  Profilaufnahme und -zugriff.
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
TQID: https://experienceleague.adobe.com/whnqurJyM4QXl5ikRvez7hpKWRDuU4onzROsUk-WeSI
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 492
ht-degree: 3%

---

# Integrationshandbuch: [!DNL Experience Platform] Profilaufnahme und -zugriff

Partner sollten dieses Integrationshandbuch verwenden, um sie beim Aufbau der Eingangs- und Ausgangsfunktionen mit der Adobe [!DNL Experience Platform] (AEP) zu unterstützen. Es gibt APIs für die Batch-Aufnahme, Streaming-Aufnahme und einheitlichen Profilzugriff (Ausgang).

Um Sie bei der Entwicklung zu unterstützen, [&#128279;](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) das Adobe Exchange-Team eine Postman-Sammlung erstellt. Diese Postman-Sammlung wird im gesamten Integrationshandbuch referenziert.

Weitere Informationen zur Installation und Verwendung der Postman-Sammlung finden Sie auf der GitHub-Seite [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Es gibt auch Beispieldatensätze mit [Treueprogramm](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json)- und [Profil](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json)Daten.

## Anwendungsbeispiel für Integration: Interaktives Sprachantwortsystem

Für Integratoren bieten die [!DNL Experience Platform]-APIs alle Funktionen der Plattform, die über die gesamte Benutzeroberfläche bereitgestellt werden, aber jetzt auch die Möglichkeit, Kunden-Workflows und automatisierte Datenflüsse zu erstellen. Als Integrator überprüfen Sie regelmäßig den Status der Datensätze, richten neue Datenaufnahmeverfahren ein und integrieren Ihre eigene Audience-Aktivierungslösung mit dem einheitlichen Profil.

Betrachten wir die Welt der IVR-Systeme (Interactive Voice Response) und der Call-Center-Managementsoftware. Der Anbieter kann die [!DNL Experience Platform]-APIs verwenden, um historische Informationen zur Callcenter-Aktivität des Kunden in den Experience Data Lake aufzunehmen. Wenn die Daten in das XDM-`ExperienceEvent`-Schema aufgenommen werden (ein Schema, das Kundeninteraktionen ausdrückt), können diese Interaktionen reibungslos direkt in den einheitlichen Profil-Service aufgenommen werden. In diesem Fall wird die `callerId` als Kundenkennung verwendet. Der Identity Service übernimmt die Identitätsauflösung und unterstützt den Unified Profile Service dabei, dem Kundenprofil alle Datenpunkte aus aktuellen Interaktionen mit dem Callcenter hinzuzufügen.

Wenn ein Kunde das nächste Mal im Callcenter anruft, wird er zunächst vom IVR beantwortet. Um die Nachricht zu personalisieren und ein auf den Anrufer zugeschnittenes Angebot zu unterbreiten, muss das IVR-System mehr über den Anrufer wissen. Hier kommt die API-Integration mit dem einheitlichen Profil ins Spiel. Das IVR-Backend kann den Unified Profile Service kontaktieren, um eine Punktsuche durchzuführen. Ziehen Sie dann entweder die Profilattribute zurate, die nur für die Callcenter-Interaktionen gelten, oder das gesamte Kundenprofil, das auch Attribute für Interaktionen an anderen Touchpoints hat. Durch die Kombination von Daten aus mehreren Datenquellen, die Verwendung der Identitätsauflösung und das einheitliche Profil können das Callcenter und der IVR-Anbieter ein maßgeschneidertes Kundenerlebnis bieten, das von Adobe [!DNL Experience Platform] unterstützt wird.“

## Allgemeine Ressourcen

* AEP [Produktdokumentation](https://docs.adobe.com/content/help/de-DE/experience-platform/landing/documentation/overview.html).
* AEP [Erweiterbarkeit](https://www.adobe.com/insights/experience-platform-api-extensibility.html).

## Fragen oder Feedback?

Bitte senden Sie alle Fragen und Feedback über den [Support-Kanal](https://adobeexchangeec.zendesk.com/hc/de-de/requests/new)
