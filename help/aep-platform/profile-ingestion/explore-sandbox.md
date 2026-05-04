---
title: Aufrufen und Erkunden der AEP-Sandbox
description: Erfahren Sie, wie Sie auf die Experience Platform-Sandbox zugreifen und diese erkunden können.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
TQID: https://experienceleague.adobe.com/A5sl-xNZBPjIKn6HO1iwM78IaQWQs4yBgbw9wwpMrGw
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
feature_v2:
  - id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
subfeature_v2:
  - id: b75843fa-0a67-4a44-a6b1-cc627b0481dc
  - id: fef08361-6ac5-460c-93fe-d063e40b6a49
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 772
ht-degree: 3%

---

# Aufrufen und Erkunden der AEP-Sandbox

Dieser Artikel behandelt Folgendes:

* Unterschiede zwischen einer bestehenden Adobe Exchange Partner-Sandbox-Organisation und der freigegebenen AEP-Sandbox.
* Anfordern des Zugriffs auf die freigegebene AEP-Sandbox.
* Erhalten einer E-Mail-Einladung zur freigegebenen AEP-Sandbox.
* Neue Benutzer in die [!DNL Admin Console] einladen.
* Navigieren in der AEP-Benutzeroberfläche.

Einen allgemeinen Überblick über die Sandbox-Technologie in AEP finden Sie in diesem [Artikel](https://docs.adobe.com/content/help/de-DE/experience-platform/sandbox/home.html).

## Die freigegebene AEP-Sandbox

Exchange-Partner erhalten Zugriff auf verschiedene Adobe [!DNL Experience Cloud]-Produkte (Nicht-AEP-Produkte wie [!DNL Analytics], [!DNL Target], Platform-Tags usw.) über ihre eigene Adobe [!DNL Experience Cloud]-Organisation (nicht freigegeben). Partner erhalten Systemadministrator-Zugriffsrechte für ihre eigene Organisation, um Benutzer und andere Berechtigungen zu verwalten. Adobe [!DNL Experience Platform] (AEP) wird anders als andere Adobe-Sandboxes behandelt. Im Folgenden finden Sie die wichtigsten Unterschiede:

* Der Zugriff auf AEP erfolgt NICHT über die Adobe [!DNL Experience Cloud] Sandbox-Hauptorg der Partner.
* Der Zugriff auf AEP erfolgt über eine freigegebene Adobe Exchange-Organisation.
* Viele andere Adobe Exchange-Partnerunternehmen greifen über dieselbe Organisation auf AEP zu
   * Über die AEP-Sandbox-Funktion können Daten und Aktivitäten innerhalb dieser freigegebenen Organisation von den anderen Partnern nicht angezeigt oder geändert werden. Jeder Partner hat Zugriff auf eine andere Sandbox innerhalb der freigegebenen Organisation.
* Die Administratorrechte innerhalb dieser freigegebenen Organisation sind sehr begrenzt.
* Nachdem Partnern Zugriff auf eine Sandbox in AEP gewährt wurde, sehen sie zwei Organisationen im Organisations-Umschalter oben rechts in der Benutzeroberfläche, während sie sich auf der Admin Console- oder Experience Cloud-Hauptseite befinden. Bei der Anmeldung bei AEP sollte jedoch nur die freigegebene Organisation angezeigt werden.

## Anfordern des Zugriffs auf die freigegebene AEP-Sandbox

Senden Sie [Support-Anfrage](https://adobeexchangeec.zendesk.com/hc/de-de/requests/new) mit den folgenden Informationen:

* E-Mail-Adresse
* Betreff: AEP Sandbox-Anfrage
* Produkt: Allgemeine Bereitstellung/Sandbox
* Ticket-Typ: Programm-Support - Fragen zum Exchange-Programm/zur Bereitstellung
* Beschreibung: Geben Sie eine kurze Beschreibung des Anwendungsfalls/der Anwendungsfälle der Integration an, für den/die eine AEP-Sandbox verwendet werden muss/müssen
* Stellen Sie sicher, dass Sie auch alle Benutzernamen und E-Mails angeben, die der AEP-Sandbox hinzugefügt werden sollen. Es ist möglich, dass zusätzliche Benutzer hinzugefügt werden, nachdem die Anfrage gestellt wurde. Die Benutzer müssen jedoch von Adobe über ein zusätzliches Ticket hinzugefügt werden (siehe unten).

## E-Mail-Einladung empfangen

Der Hauptkontakt, der die AEP-Sandbox angefordert hat, erhält eine automatisierte E-Mail, in der er zur ersten Verwendung der Adobe-[!DNL Experience Platform] eingeladen wird. Der primäre Kontakt verfügt auch über einige Administratorrechte, die im nächsten Abschnitt behandelt werden.

Anstatt die Schaltfläche „Erste Schritte“ in der E-Mail auszuwählen, navigieren Sie direkt zu `https://platform.adobe.com.` Anmelden bei der Adobe ID, die mit der E-Mail-Adresse in der Einladung verknüpft ist, oder erstellen Sie eine, wenn sie nicht mit einer Adobe ID verknüpft ist.

## Zusätzliche Benutzer einladen

Senden Sie [Support-Anfrage](https://adobeexchangeec.zendesk.com/hc/de-de/requests/new) mit den folgenden Informationen:

* E-Mail-Adresse des Antragstellers
* Betreff: AEP Sandbox - Administrator/Benutzer hinzufügen
* Produkt: Allgemeine Bereitstellung/Sandbox
* Ticket-Typ: Programm-Support - Fragen zum Exchange-Programm/zur Bereitstellung
* Beschreibung: Liste der hinzuzufügenden Benutzer (Namen und E-Mails)

## Navigieren in der AEP-Benutzeroberfläche

AEP-Benutzeroberfläche ansehen [Einführungsvideo](https://docs.adobe.com/content/help/de-DE/platform-learn/tutorials/intro-to-platform/interface-tour.html)

Es gibt 12 primäre Bereiche in der AEP-Benutzeroberfläche, die über das linke Bedienfeld navigiert werden können. Die wichtigsten Abschnitte für diesen Integrationstyp sind jedoch Schemata, Datensätze und Profile.

* Startseite - der Startbildschirm

   * Schreibt einige erste Aktivitäten vor
   * Enthält einige Links zu Lerninhalten
   * Ermöglicht eine Dashboard-Ansicht für einige der wichtigsten AEP-Objekte wie Schemata, Datensätze und Profile

* Workflows - Starten in allgemeine Workflows zum Übertragen von Daten in AEP
* Verbindungen/Quellen - Verwalten von Datenquellen, die in AEP eingehen
* Verbindungen/Ziele - Verbindungen verwalten, um Daten an externe Systeme zu senden
* Profile : Anzeigen und Verwalten einzelner Kundenprofile
* Segmente : Durchsuchen, Erstellen und Ändern von Kundensegmenten
* Identitäten - Durchsuchen, Erstellen und Ändern von Identity-Namespaces. Dies sind die Typen von primären IDs, die zur eindeutigen Identifizierung eines Kunden verwendet werden
* Modelle (Datenwissenschaft) - Betreiben Sie datenwissenschaftliche Aktivitäten, einschließlich der Verwendung einer eingebetteten Jupyter-Notebook-Umgebung
* Services (Datenwissenschaft) - Veröffentlichen von Datenwissenschaftsrezepten als Services
* Schemata : Durchsuchen, Erstellen und Ändern von Schemata. Dies sind die detaillierten Datendefinitionen, die zum Organisieren von Daten verwendet werden
* Datensätze : Durchsuchen, Erstellen und Verwalten von Datensätzen; ein Datensatz wird durch ein Schema definiert und ist der Ort, an dem sich Daten in AEP befinden
* Abfragen : Durchsuchen, Erstellen, Ändern und Verwenden eines Repositorys von Abfragen, um Einblicke aus den Daten in Datensätzen zu erhalten
* Monitoring : Zeigt den Status aller Daten an, die in AEP ein- und ausgelagert werden, sowohl für Batch als auch für Streaming.
