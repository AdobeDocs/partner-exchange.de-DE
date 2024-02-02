---
title: Aufrufen und Erkunden der AEP-Sandbox
description: Erfahren Sie, wie Sie auf die Experience Platform-Sandbox zugreifen und sie durchsuchen können.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 1%

---

# Aufrufen und Erkunden der AEP-Sandbox

Dieser Artikel behandelt Folgendes:

* Die Unterschiede zwischen einer bestehenden Adobe Exchange Partner-Sandbox-Organisation und der freigegebenen AEP-Sandbox.
* Anfordern des Zugriffs auf die freigegebene AEP-Sandbox.
* Erhalt einer E-Mail-Einladung zur freigegebenen AEP-Sandbox.
* Einladen neuer Benutzer in die [!DNL Admin Console].
* Navigieren in der AEP-Benutzeroberfläche.

Eine allgemeine Übersicht über die Sandbox-Technologie in AEP finden Sie in diesem [Artikel](https://docs.adobe.com/content/help/de-DE/experience-platform/sandbox/home.html).

## Die freigegebene AEP-Sandbox

Exchange-Partner erhalten Zugriff auf verschiedene Adobe [!DNL Experience Cloud] Produkte (Nicht-AEP-Produkte wie [!DNL Analytics], [!DNL Target], Platform-Tags usw.) über ihre eigene Adobe [!DNL Experience Cloud] Organisation (nicht freigegeben). Partner erhalten Systemadministratorzugriffsrechte auf ihre eigene Organisation, um Benutzer und andere Berechtigungen zu verwalten. Adobe [!DNL Experience Platform] (AEP) anders behandelt als andere Adobe-Sandboxes. Hier sind die wichtigsten Unterschiede:

* Der Zugriff auf AEP erfolgt NICHT über die Adobe der Partner [!DNL Experience Cloud] Sandbox-Organisation.
* Der Zugriff auf AEP erfolgt über eine freigegebene Adobe Exchange-Organisation.
* Viele andere Adobe Exchange-Partnerunternehmen greifen mit derselben Organisation auf AEP zu
   * Über die AEP-Sandbox-Funktion können Daten und Aktivitäten innerhalb dieser freigegebenen Organisation von den anderen Partnern nicht gesehen oder geändert werden. Jeder Partner hat Zugriff auf eine andere Sandbox in der freigegebenen Organisation.
* Die Administratorrechte in dieser freigegebenen Organisation sind sehr eingeschränkt.
* Nachdem Partner Zugriff auf eine Sandbox in AEP erhalten haben, sehen sie oben rechts in der Benutzeroberfläche zwei Org im Org-Umschalter, während sie sich auf der Startseite der Admin Console oder des Haupt-Experience Cloud befinden. Bei der Anmeldung bei AEP sollte jedoch nur die freigegebene Organisation sichtbar sein.

## Anfordern des Zugriffs auf die freigegebene AEP-Sandbox

Senden einer [Support-Anfrage](https://adobeexchangeec.zendesk.com/hc/de-de/requests/new) mit den folgenden Informationen:

* E-Mail-Adresse
* Betrifft: AEP-Sandbox-Anfrage
* Produkt: Allgemeine Bereitstellung/Sandbox
* Tickettyp: Programm-Support - Fragen zu Exchange-Programm/Provisioning-Anfragen
* Beschreibung: Geben Sie eine kurze Beschreibung der Anwendungsfälle für die Integration, die die Verwendung einer AEP-Sandbox erfordern.
* Stellen Sie sicher, dass Sie auch alle Benutzernamen und E-Mails angeben, die zur AEP-Sandbox hinzugefügt werden sollen. Es ist möglich, dass zusätzliche Benutzer hinzugefügt werden, nachdem die Anfrage gestellt wurde, aber die Benutzer müssen von Adobe über ein zusätzliches Ticket hinzugefügt werden (siehe unten).

## E-Mail-Einladung erhalten

Der Hauptkontakt, der die AEP-Sandbox angefordert hat, erhält eine automatische E-Mail, in der er zum &quot;Einstieg&quot;mit der Adobe eingeladen wird [!DNL Experience Platform]. Der Hauptkontakt verfügt außerdem über einige Administratorberechtigungen, die im nächsten Abschnitt behandelt werden.

Anstatt in der E-Mail die Schaltfläche &quot;Erste Schritte&quot;auszuwählen, navigieren Sie direkt zu `https://platform.adobe.com.` Melden Sie sich mit der Adobe ID an, die der E-Mail-Adresse in der Einladung zugeordnet ist, oder erstellen Sie eine, wenn sie keiner Adobe ID zugeordnet ist.

## Zusätzliche Benutzer einladen

Senden einer [Support-Anfrage](https://adobeexchangeec.zendesk.com/hc/de-de/requests/new) mit den folgenden Informationen:

* E-Mail-Adresse des Anforderers
* Betrifft: AEP-Sandbox - Admin/Benutzer hinzufügen
* Produkt: Allgemeine Bereitstellung/Sandbox
* Tickettyp: Programm-Support - Fragen zu Exchange-Programm/Provisioning-Anfragen
* Beschreibung: Liste der hinzuzufügenden Benutzer (Namen und E-Mails)

## Navigieren in der AEP-Benutzeroberfläche

AEP-Benutzeroberfläche ansehen [Einführungsvideo](https://docs.adobe.com/content/help/en/platform-learn/tutorials/intro-to-platform/interface-tour.html)

Es gibt 12 Hauptbereiche in der AEP-Benutzeroberfläche, die über das linke Bedienfeld navigiert werden können. Die wichtigsten Abschnitte für diese Art der Integration sind jedoch Schemas, Datensätze und Profile.

* Startseite - Landingpage

   * Hier werden einige erste Schritte vorgeschlagen
   * Enthält einige Links zu Lerninhalten
   * Bietet eine Dashboard-Ansicht für einige der wichtigsten AEP-Objekte wie Schemas, DataSets und Profile

* Workflows - Einführung in gemeinsame Workflows für die Datenübernahme in AEP
* Verbindungen/Quellen - Verwalten von Datenquellen, die in AEP eingehen
* Verbindungen/Ziele - Verwalten von Verbindungen zum Senden von Daten an externe Systeme
* Profile - Anzeigen und Verwalten einzelner Kundenprofile
* Segmente - Kundensegmente durchsuchen, erstellen und ändern
* Identitäten - Suchen, Erstellen und Ändern von Identitäts-Namespaces. Hierbei handelt es sich um die Typen von primären IDs, die zur eindeutigen Identifizierung eines Kunden verwendet werden
* Modelle (Datenwissenschaft) - Teilnahme an Data Science-Aktivitäten, einschließlich der Verwendung einer eingebetteten Jupyter Notebooks-Umgebung
* Dienste (Data Science) - Veröffentlichen von Datenwissenschaftsrezepten als Dienste
* Schemata - Schemata durchsuchen, erstellen und ändern; dies sind die detaillierten Datendefinitionen, die verwendet werden, um die Organisation der Daten zu gewährleisten
* DataSets - Durchsuchen, Erstellen und Verwalten von DataSets; ein DataSet wird durch ein Schema definiert und befindet sich dort, wo sich Daten in AEP befinden
* Abfragen - Durchsuchen, Erstellen, Ändern und Verwenden eines Repositorys von Abfragen, um Einblicke aus den Daten in DataSets zu gewinnen.
* Überwachung - Anzeigen des Status aller Daten, die sowohl für Batch als auch für Streaming in und aus AEP verschoben werden
