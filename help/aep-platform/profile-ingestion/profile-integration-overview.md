---
title: "[!DNL Platform] Übersicht über Profilaufnahme und Zugriffsintegration"
description: Informationen zur Integration für [!DNL Experience Platform] Profilerfassung und -zugriff.
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Integrationsleitfaden: [!DNL Experience Platform] Profilerfassung und -zugriff

Partner sollten dieses Integrationsleitfaden verwenden, um sie beim Aufbau der Ein- und Ausstiegsfunktion mit der Adobe zu unterstützen. [!DNL Experience Platform] (AEP). Es gibt APIs für die Batch-Erfassung, Streaming-Erfassung und Unified Profile Access (Egress).

Um die Entwicklung zu unterstützen, muss eine [Postman-Sammlung](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wurde vom Adobe Exchange-Team erstellt. Auf diese Postman-Sammlung wird im Integrationshandbuch verwiesen.

Weitere Informationen zur Installation und Verwendung der Postman-Sammlung finden Sie auf Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) Seite. Es gibt auch Beispieldatensätze von [Treue](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) und [profile](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) Daten.

## Anwendungsbeispiel für die Integration: Interaktives Sprachreaktionssystem

Bei Integratoren wird die [!DNL Experience Platform] APIs bieten alle Funktionen der Plattform, die in der gesamten Benutzeroberfläche angeboten werden. Jetzt können jedoch Kunden-Workflows und automatisierte Datenflüsse erstellt werden. Als Integrator überprüfen Sie regelmäßig den Status von Datensätzen, richten neue Datenerfassungsverfahren ein und integrieren Ihre eigene Zielgruppenaktivierungslösung in das Unified Profile.

Betrachten Sie die Welt der Interactive Voice Response (IVR) Systeme und der Call Center Management Software. Der Anbieter kann die [!DNL Experience Platform] APIs zum Erfassen historischer Informationen zur Callcenter-Aktivität des Kunden im Experience Data Lake. Wenn die Daten im XDM erfasst werden `ExperienceEvent` Schema (ein Schema, das Kundeninteraktionen ausdrückt), können diese Interaktionen ohne Reibung direkt in den Unified Profile Service aufgenommen werden. In diesem Fall wird die `callerId` wird als Kundenkennung verwendet. Der Identitätsdienst kümmert sich um die Identitätsauflösung und unterstützt den Unified Profile Service beim Hinzufügen von Datenpunkten aus jüngsten Interaktionen mit dem Callcenter zum Kundenprofil.

Wenn ein Kunde das nächste Mal das Call Center anruft, wird er zunächst von der IVR beantwortet. Um die Nachricht zu personalisieren und ein auf den Anrufer zugeschnittenes Angebot bereitzustellen, muss das IVR-System mehr über den Anrufer wissen. Hier kommt die API-Integration mit dem einheitlichen Profil zum Einsatz. Das IVR-Backend kann sich für eine Punktsuche an den Unified Profile Service wenden. Konsultieren Sie dann entweder die Profilattribute, die nur für die Callcenter-Interaktionen gelten, oder das vollständige Kundenprofil, das auch Attribute für Interaktionen an anderen Touchpoints enthält. Durch die Kombination von Daten aus mehreren Datenquellen, die Verwendung der Identitätsauflösung und des Unified Profile können das Callcenter und der IVR-Anbieter ein maßgeschneidertes Kundenerlebnis bieten, das durch Adobe unterstützt wird [!DNL Experience Platform].&quot;

## Allgemeine Ressourcen

* AEP [Produktdokumentation](https://docs.adobe.com/content/help/de-DE/experience-platform/landing/documentation/overview.html).
* AEP [Erweiterbarkeit](https://www.adobe.com/insights/experience-platform-api-extensibility.html).

## Fragen oder Feedback?

Senden Sie alle Fragen und Feedback über [Support-Kanal](https://adobeexchangeec.zendesk.com/hc/de-de/requests/new)
