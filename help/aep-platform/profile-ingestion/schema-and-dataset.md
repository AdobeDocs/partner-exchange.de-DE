---
title: Erstellen von AEP-Schemata und -Datensätzen
description: Erstellen Sie Schemas und Datensätze in Experience Platform.
exl-id: a2773551-20a3-4a5b-ab53-60fa67e38ec0
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 13%

---

# Erstellen von Schemata und Datensätzen

Die [Postman-Sammlung](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) wird im gesamten Artikel mit den zugehörigen Aufrufen nach Anzahl referenziert. Weitere Informationen zur Installation und Verwendung der Postman-Sammlung finden Sie auf Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) Seite. Es gibt auch Beispieldatensätze von [Treue](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) und [profile](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) Daten.

## Schemata

Ein Schema ist ein Regelsatz, der die Datenstruktur und das Datenformat repräsentiert und überprüft. Auf hoher Ebene bieten Schemas eine abstrakte Definition eines realen Objekts (z. B. einer Person) und legen dar, welche Daten in jeder Instanz dieses Objekts enthalten sein sollen (z. B. Vorname, Nachname, Geburtstag usw.). Schemas können in der Benutzeroberfläche oder mithilfe der [!DNL Experience Platform] APIs.

Siehe [diese Dokumentation](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/schema_composition/schema_composition.md) für weitere Details.

### Erstellen eines Schemas

Partner können mithilfe der Benutzeroberfläche ein Schema erstellen, indem sie folgende Schritte ausführen: [Tutorial](https://docs.adobe.com/content/help/de-DE/experience-platform/xdm/tutorials/create-schema-ui.html). In diesem Beispiel wird das Profil-Schema des Treueprogramms verwendet. Während das Beispiel ein Profilschema ist, können ereignisbasierte Schemas mit einem ähnlichen Prozess verwendet werden.

Um die APIs verwenden zu können, müssen Partner über eine vorhandene Adobe I/O-Integration mit [!DNL Experience Platform] -Berechtigungen aktiviert sind. In diesem Handbuch finden Sie [Erstellen einer I/O-Integration](https://docs.adobe.com/content/help/de-DE/experience-platform/tutorials/home.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).

Dann Besuch [dieser Link](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-api.html) , um zu erfahren, wie Sie mit der API Schemas erstellen.

Um ein Schema über Postman zu erstellen, verwenden Sie die Aufrufe in den Ordnern 1: Schema erstellen, 1a: Schema für PROFILdaten erstellen ODER 1b: Schema für EREIGNISdaten erstellen.

## Datensätze

Alle Daten, die in die Adobe übertragen werden [!DNL Experience Platform] in Datensätzen enthalten ist. Ein Datensatz ist ein Konstrukt zur Datenspeicherung und -verwaltung, in dem Daten (in der Regel) in einer Tabelle erfasst werden, die ein Schema (Spalten) und Felder (Zeilen) beinhaltet. Datensätze enthalten auch Metadaten, die verschiedene Aspekte der in ihnen gespeicherten Daten beschreiben.

Catalog Service ist das Aufzeichnungssystem für Speicherort und Herkunft von Daten innerhalb von [!DNL Experience Platform]und wird zum Erstellen und Verwalten von Datensätzen verwendet. Catalog verfolgt die Metadaten für jeden Datensatz. Dazu gehört ein Verweis auf das Experience-Datenmodell (XDM)-Schema, dem der Datensatz entspricht (siehe nächsten Abschnitt), sowie die Anzahl der Datensätze, die in diesen Datensatz aufgenommen werden.

Los [here](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/overview.html) für eine detaillierte Datensatzübersicht.

### Erstellen eines Datensatzes

![Erstellen eines Datensatzanimierten GIF](images/creating_a_dataset.gif)

<!-- 
We don't yet support hover text in images (and we render it poorly when included). I removed "Creating a Dataset" from the above image link. We can add it back when we support it (Summer 2020?) -Bob
-->

Erstellen Sie einen Datensatz über die Benutzeroberfläche:

1. Klicks **[!UICONTROL Datensatz erstellen]**.

1. Klicks **[!UICONTROL Aus Schema erstellen]**.

1. Klicken Sie auf **[!UICONTROL Fertigstellen]**.

Los [here](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/user-guide.html) für ein Benutzerhandbuch zu Datensätzen.

[Datensatz mit APIs erstellen](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/create.html).

Um einen Datensatz über Postman zu erstellen, verwenden Sie die Ordner 2: Datensatz erstellen, 2a: Datensatz für PROFILE-Daten erstellen ODER 2b: Datensatz für EREIGNISdaten erstellen.

## Best Practices für Schema und Datensatz für Partner

* Partnerdaten sollten ein separates Profilschema verwenden oder eine Mischung für das vorhandene Profil- und Erlebnisschema eines Kunden erstellen.
* Partner sollten nach Möglichkeit Adobe-Klassen und Mix-Ins verwenden.
* Partner sollten ihre Daten mit einem separaten Datensatz hochladen, anstatt zu versuchen, ihre Daten in einem vorhandenen Datensatz zu kombinieren.
* Partner können ihre Schemata derzeit nicht in die globale Registrierung hochladen.
