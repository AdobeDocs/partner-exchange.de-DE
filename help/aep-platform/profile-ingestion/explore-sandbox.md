---
title: Aufrufen und Erkunden der AEP-Sandbox
description: Erfahren Sie, wie Sie auf die Experience Platform-Sandbox zugreifen und sie erkunden können.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# Aufrufen und Erkunden der AEP-Sandbox

Dieser Artikel behandelt Folgendes:

* Die Unterschiede zwischen einer bestehenden Adobe Exchange Partner-Sandbox-Organisation und der freigegebenen AEP-Sandbox.
* Anfordern des Zugriffs auf die freigegebene AEP-Sandbox.
* Erhalten einer E-Mail-Einladung zur freigegebenen AEP-Sandbox.
* Neue Benutzer in die [!DNL Admin Console] einladen.
* Navigieren in der AEP-Benutzeroberfläche.

Einen allgemeinen Überblick über die Sandbox-Technologie in AEP finden Sie in diesem [Artikel](https://docs.adobe.com/content/help/de-DE/experience-platform/sandbox/home.html).

## Die freigegebene AEP-Sandbox

Exchange-Partner erhalten Zugriff auf verschiedene Adobe-[!DNL Experience Cloud]-Produkte (Nicht-AEP-Produkte wie [!DNL Analytics], [!DNL Target], Platform-Tags usw.) über ihre eigene Adobe-[!DNL Experience Cloud]-Organisation (nicht freigegeben). Partner erhalten Systemadministrator-Zugriffsrechte für ihre eigene Organisation, um Benutzer und andere Berechtigungen zu verwalten. Adobe [!DNL Experience Platform] (AEP) wird anders behandelt als andere Adobe-Sandboxes. Im Folgenden finden Sie die wichtigsten Unterschiede:

* Der Zugriff auf AEP erfolgt NICHT über die Partner-Haupt-Adobe [!DNL Experience Cloud] Sandbox-Organisation.
* Der Zugriff auf AEP erfolgt über eine freigegebene Adobe Exchange-Organisation.
* Viele andere Adobe Exchange-Partnerunternehmen greifen über dieselbe Organisation auf AEP zu
   * Über die AEP-Sandbox-Funktion können Daten und Aktivitäten innerhalb dieser freigegebenen Organisation von den anderen Partnern nicht angezeigt oder geändert werden. Jeder Partner hat Zugriff auf eine andere Sandbox innerhalb der freigegebenen Organisation.
* Die Administratorrechte innerhalb dieser freigegebenen Organisation sind sehr begrenzt.
* Nachdem Partnern Zugriff auf eine Sandbox auf AEP gewährt wurde, sehen sie zwei Organisationen im Organisations-Umschalter oben rechts in der Benutzeroberfläche, während sie sich auf der Startseite der Admin Console oder der Haupt-Experience Cloud befinden. Bei der Anmeldung bei AEP sollte jedoch nur die freigegebene Organisation sichtbar sein.

## Anfordern des Zugriffs auf die freigegebene AEP-Sandbox

Senden Sie [Support-Anfrage](https://adobeexchangeec.zendesk.com/hc/de-de/requests/new) mit den folgenden Informationen:

* E-Mail-Adresse
* Betreff: AEP-Sandbox-Anfrage
* Produkt: Allgemeine Bereitstellung/Sandbox
* Ticket-Typ: Programm-Support - Fragen zum Exchange-Programm/zur Bereitstellung
* Beschreibung: Geben Sie eine kurze Beschreibung des Anwendungsfalls/der Anwendungsfälle der Integration an, für den/die die Verwendung einer AEP-Sandbox erforderlich ist/sind
* Stellen Sie sicher, dass Sie auch alle Benutzernamen und E-Mails angeben, die der AEP-Sandbox hinzugefügt werden sollen. Es ist möglich, dass zusätzliche Benutzer hinzugefügt werden, nachdem die Anfrage gestellt wurde. Die Benutzer müssen jedoch per Adobe über ein zusätzliches Ticket hinzugefügt werden (siehe unten).

## E-Mail-Einladung empfangen

Der primäre Kontakt, der die AEP-Sandbox angefordert hat, erhält eine automatisierte E-Mail, in der er zur „ersten Schritte“ mit dem Adobe-[!DNL Experience Platform] eingeladen wird. Der primäre Kontakt verfügt auch über einige Administratorrechte, die im nächsten Abschnitt behandelt werden.

Anstatt die Schaltfläche „Erste Schritte“ in der E-Mail auszuwählen, navigieren Sie direkt zu `https://platform.adobe.com.` Anmelden bei der Adobe ID, die mit der E-Mail-Adresse in der Einladung verknüpft ist, oder erstellen Sie eine, wenn sie nicht mit einer Adobe ID verknüpft ist.

## Zusätzliche Benutzer einladen

Senden Sie [Support-Anfrage](https://adobeexchangeec.zendesk.com/hc/de-de/requests/new) mit den folgenden Informationen:

* E-Mail-Adresse des Antragstellers
* Betreff: AEP-Sandbox - Administrator/Benutzer hinzufügen
* Produkt: Allgemeine Bereitstellung/Sandbox
* Ticket-Typ: Programm-Support - Fragen zum Exchange-Programm/zur Bereitstellung
* Beschreibung: Liste der hinzuzufügenden Benutzer (Namen und E-Mails)

## Navigieren in der AEP-Benutzeroberfläche

Sehen Sie sich das Einführungsvideo zur AEP[Benutzeroberfläche ](https://docs.adobe.com/content/help/de-DE/platform-learn/tutorials/intro-to-platform/interface-tour.html)

Es gibt 12 primäre Bereiche in der AEP-Benutzeroberfläche, die über das linke Bedienfeld navigiert werden können. Die wichtigsten Abschnitte für diesen Integrationstyp sind jedoch Schemata, Datensätze und Profile.

* Startseite - der Startbildschirm

   * Schreibt einige erste Aktivitäten vor
   * Enthält einige Links zu Lerninhalten
   * Ermöglicht eine Dashboard-Ansicht für einige der wichtigsten AEP-Objekte, z. B. Schemata, Datensätze und Profile

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
