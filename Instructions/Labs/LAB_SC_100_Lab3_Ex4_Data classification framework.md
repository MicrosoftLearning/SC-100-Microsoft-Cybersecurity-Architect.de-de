---
lab: 3
title: Übung 4 – Datenklassifizierungsframework
---


# Lab 3 – Übung 4 – Datenklassifizierungsframework

Sie wurden mit der Aufgabe betraut, die Datenklassifizierung für Contoso Ltd. in Vorbereitung auf ein ISO-27001:2022-Audit zu strukturieren. Ziel ist es, einen soliden Rahmen zu schaffen, der für die Gewährleistung eines wirksamen Schutzes der Daten vor Weitergabe, Löschung und Verlust entscheidend ist. Ihre Rolle besteht darin, ein neues Projekt-ID-System für Konstruktionsprojekte in das Unternehmen zu integrieren. Um den staatlichen Vorschriften zu entsprechen, müssen alle Dokumente, die eine bestimmte Projekt-ID enthalten, 5 Jahre lang aufbewahrt werden.

Ihnen wurden folgende Beispiele zur Klassifizierung von Projekt-IDs gegeben:

|Projektkennung|
|----|
|PAR-1023-DA
|BER-0822-AB
|Rom-0419-bm
|sTr*1223-Se
|BaR#0418-ag|
|dui0522-in|

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept, um die Probleme zu beheben, denen Contoso Ltd. gegenübersteht.

### Entwurfsansatz

Die Einführung einer neuen Projekt-ID erfordert die Schaffung eines entsprechenden sensiblen Informationstyps (SIT), was die Entwicklung eines benutzerdefinierten Musters mit einem regulären Ausdruck erfordert. Anschließend kann diese SIT verwendet werden, um ein Aufbewahrungsbezeichnung und eine damit verbundene automatische Bezeichnungsrichtlinie zu entwickeln.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Identifizieren von Dokumenten mit Projekt-IDs|Microsoft Purview Information Protection|Benutzerdefinierten Typ für vertrauliche Informationen erstellen|
|Einhaltung der gesetzlichen Vorschriften zur Aufbewahrung von Daten für 5 Jahre| Microsoft Purview-Datenlebenszyklusverwaltung|Bereitstellen einer Aufbewahrungsrichtlinie|

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1: Erstellen eines benutzerdefinierten Typs vertraulicher Informationen

Sie werden einen benutzerdefinierten sensiblen Typ vertraulicher Informationen erstellen, um Dokumente zu erkennen, die Projekt-IDs enthalten.

1. Melden Sie sich beim Microsoft Purview Compliance Portal **https://compliance.microsoft.com/** als Allan Deyoung mithilfe seines Administratorkontos **MOD Administrator** an.
1. Erweitern Sie im Microsoft Purview-Complianceportal im linken Navigationsbereich **Datenklassifizierung** und wählen Sie dann **Klassifizierer**.
3. Wählen Sie auf der Seite **Klassifikatoren** die Option **Typen vertraulicher Informationen** > **Typ vertraulicher Informationen erstellen**.
4. Auf der Seite **Name des Typs vertraulicher Informationen** geben Sie folgende Informationen ein:
    - **Name**: Projektidentifikationsnummer
    - **Beschreibung**: Identifiziert die Projektidentifikationsnummer
1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Definieren Sie Muster für diesen Typ vertraulicher Informationen** die Option **Muster erstellen**.
1. Auf der Seite **Neues Muster** wählen Sie **Primärelement hinzufügen** und dann **Regulärer Ausdruck**.
1. Geben Sie auf der Seite **Hinzufügen eines regulären Ausdrucks** in das Textfeld **ID** **ProjectID** ein.
1. Geben Sie in das Textfeld **Regulärer Ausdruck** den folgenden Ausdruck ein:
```regex   
[a-zA-Z]{3}(\W)?[\d]{4}(\W)?[a-zA-Z]{2}
```
> [!NOTE] Der angegebene reguläre Ausdruck ist so gestaltet, dass er eine Sequenz identifiziert, die durch drei Buchstaben, gefolgt von potenziell optionalen Nicht-Wort-Zeichen, dann vier Ziffern, wiederum gefolgt von optionalen Nicht-Wort-Zeichen und schließlich endend mit zwei Buchstaben gekennzeichnet ist. Das Vorhandensein von Nicht-Wort-Zeichen ist willkürlich, und das übergreifende Muster soll einem bestimmten Format oder einer bestimmten Struktur innerhalb der Daten entsprechen.

1. Wählen Sie **Übereinstimmung der Zeichenfolge** für die **regulären Ausdrücke** und wählen Sie **Fertig**.
1. Wählen Sie oben **Hohe Konfidenz** für **Konfidenzniveau** und wählen Sie **Erstellen**.
1. Schließen Sie die Konfiguration ab und erstellen Sie den Typ vertrauliche Informationen.

Sie haben erfolgreich einen neuen Typ für vertrauliche Informationen erstellt, um Projekt-IDs zu identifizieren.

### Aufgabe 2: Erstellen einer Aufbewahrungsbezeichnung

Sie erstellen eine Aufbewahrungsbezeichnung, um alle Dokumente im Zusammenhang mit Konstruktionsprojekten für 5 Jahre aufzubewahren.

1. Sie sollten weiterhin im Microsoft Purview-Complianceportal **https://compliance.microsoft.com/** angemeldet sein.
1. Erweitern Sie im Microsoft Purview-Complianceportal im linken Bereich der Navigation **Datenlebenszyklusverwaltung** und wählen Sie **Microsoft 365** aus.
1. Auf der Seite **Datenlebenszyklusverwaltung** das Blatt **Bezeichnungen** auswählen.
1. Wählen Sie auf dem Blatt **Bezeichnungen** die Option **Neue Bezeichnung**.
1. Geben Sie auf der Seite **Benennen Sie Ihre Aufbewahrungsrichtlinie** die folgenden Informationen ein:

    - **Name**: Aufbewahrung der Bauprojektdokumentation
    - **Beschreibung für Benutzende**: Die Aufbewahrungsrichtlinie für Bauprojekte schreibt die Aufbewahrung aller projektbezogenen Dokumente für fünf Jahre nach Abschluss des Projekts vor.
    - **Beschreibung für Admins**: Diese Bezeichnung wird verwendet, um Bauprojektdokumente für einen Zeitraum von fünf Jahren aufzubewahren, und es wird in Verbindung mit der automatischen Bezeichnung verwendet.

1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Bezeichnungseinstellungen festlegen** die Option **Elemente für immer oder für einen bestimmten Zeitraum aufbewahren** und wählen Sie **Weiter**.
1. Auf der Seite **Aufbewahrungszeitraum definieren** geben Sie die folgenden Informationen ein:

    - **Aufbewahrung von Elementen für**: 5 Jahre
    - **Beginn des Aufbewahrungszeitraums basierend auf**: Zeitpunkt der Elementerstellung
    - **Am Ende des Aufbewahrungszeitraums**: Nichts tun

1. Wählen Sie **Weiter** aus.
1. Auf der Seite **Auwählen, was nach dem Aufbewahrungszeitraum geschehen soll** **Aufbewahrungseinstellungen deaktivieren** auswählen.
1. Beenden Sie die Konfiguration, und erstellen Sie die Aufbewahrungsbezeichnung, ohne sie zu veröffentlichen.

Sie haben erfolgreich eine Aufbewahrungsbezeichnung mit einem Aufbewahrungszeitraum von 5 Jahren erstellt.

### Aufgabe 3: Aufbewahrungsbezeichnung automatisch anwenden

Sie werden den Typ vertraulicher Informationen, die Sie in dieser Übung erstellt haben, verwenden, um die Aufbewahrungsbezeichnung automatisch anzuwenden.

1. Sie sollten weiterhin im Microsoft Purview-Complianceportal **https://compliance.microsoft.com/** angemeldet sein.
1. Erweitern Sie im Microsoft Purview-Complianceportal **Datenlebenszyklusverwaltung** und wählen Sie **Microsoft 365** aus.
1. Im Bereich **Datenlebenszyklusverwaltung** das Blatt **Bezeichnungsrichtlnien** auswählen.
1. Wählen Sie auf dem Blatt **Bezeichnungsrrichtlinien** die Option **Bezeichnung automatisch anwenden**.
1. Auf der Seite **Erste Schritte** die folgenden Informationen eingeben:

    - **Name**: Bezeichnung von Dokumenten zu Bauprojekten
    - **Beschreibung**: Diese Richtlinie setzt automatisch die Richtlinie „Aufbewahrung von Bauprojektdokumenten“ für alle Dokumente durch, die sich auf Bauprojekte beziehen.

1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Wählen Sie den Inhaltstyp aus, auf den Sie diese Bezeichnung anwenden möchten**, wählen Sie **Bezeichnung auf Inhalte anwenden, die vertrauliche Informationen enthalten** und wählen Sie **Weiter**.
1. Wählen Sie auf der Seite **Inhalt, der vertrauliche Daten enthält** die Option **Benutzerdefiniert**, dann **Benutzerdefinierte Richtlinie** und **Weiter**.
Fügen Sie auf der Seite **Inhalte definieren, die vertrauliche Informationen enthalten** den von Ihnen erstellten benutzerdefinierten Typ vertraulicher Informationen **Projektidentifikationsnummer** hinzu. Geben Sie dann die folgenden Einstellungen an:

    - **Gruppenname**: Projekt-ID-Suche
    - **Konfidenzniveau**: Hohe Konfidenz
    - **Anzahl der Instanzen**: 1 bis beliebig

1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Richtlinienbereich** **Weiter**.
1. Auf der Seite **Typ der zu erstellenden Aufbewahrungsrichtlinie**, wählen Sie **Statisch** und wählen Sie **Weiter**.
1. Wenden sie die Bezeichnung auf alle verfügbaren Speicherorte an.
1. Wählen Sie auf der Seite **Wählen Sie eine Bezeichnung, die automatisch angewendet werden soll** die Option **Bezeichnung hinzufügen**, wählen Sie dann die Bezeichnung **Aufbewahrung der Bauprojektdokumentation**, das Sie in Aufgabe 2 erstellt haben, und wählen Sie **Hinzufügen**.
1. Aktivieren und beenden Sie die Konfiguration, um die Richtlinie für die automatische Bezeichnung zu erstellen.

Sie haben die Aufbewahrungsbezeichnung erfolgreich veröffentlicht und automatisch auf alle Dokumente angewendet, die Projekt-IDs enthalten.