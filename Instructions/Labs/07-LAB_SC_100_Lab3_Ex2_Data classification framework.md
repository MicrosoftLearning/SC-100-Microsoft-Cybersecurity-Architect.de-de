# Datenklassifizierungsframework

Sie wurden mit der Aufgabe betraut, die Datenklassifizierung für Contoso Ltd. in Vorbereitung auf ein ISO-27001:2022-Audit zu strukturieren. Ziel ist es, einen soliden Rahmen zu schaffen, der für die Gewährleistung eines wirksamen Schutzes der Daten vor Weitergabe, Löschung und Verlust entscheidend ist. Ihre Rolle besteht darin, ein neues Projekt-ID-System für Konstruktionsprojekte in das Unternehmen zu integrieren. Um den staatlichen Vorschriften zu entsprechen, müssen alle Dokumente, die eine bestimmte Projekt-ID enthalten, 5 Jahre lang aufbewahrt werden.

Ihnen wurden folgende Beispiele zur Klassifizierung von Projekt-IDs gegeben:

|Projektkennung|
|----|
|PAR-1023-DA|
|BER-0822-AB|
|Rom-0419-bm|
|sTr*1223-Se|
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

1. Melden Sie sich beim Microsoft Purview Compliance Portal **`https://purview.microsoft.com/`** als Allan Deyoung mit seinem Administratorkonto **MOD-Admin** an.
1. Wenn Sie aufgefordert werden, die mehrstufige Authentifizierung einzurichten, befolgen Sie die Anweisungen.
1. Sie gelangen zur neuen Landing Page des Microsoft Purview-Portals. Aktivieren Sie das Kästchen neben der Erklärung **Ich stimme den Bedingungen für die Offenlegung des Datenflusses und den Datenschutzerklärungen zu** und wählen Sie dann **Erste Schritte** aus.
1. Wählen Sie im linken Bedienfeld **Lösungen** und dann **Informationsschutz** aus. Alternativ können Sie im Hauptfenster die Kachel **Alle Lösungen anzeigen** auswählen und dann die Kachel **Informationsschutz** auswählen, die unter Datensicherheit aufgeführt ist.
1. Erweitern Sie **Klassifizierungen** und wählen Sie dann **Sensible Informationstypen** aus.
1. Wählen Sie auf der Seite **Sensible Informationstypen** die Option **Sensiblen Informationstyp erstellen**.
1. Auf der Seite **Name des Typs vertraulicher Informationen** geben Sie folgende Informationen ein:
    - Name: **`Project Identification Number`**
    - Description (Beschreibung): **`Identifies project identification number`**
1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Muster für diesen vertraulichen Informationstyp definieren** die Option **Muster erstellen** aus.
1. Auf der Seite **Neues Muster** wählen Sie **Primärelement hinzufügen** und dann **Regulärer Ausdruck**.
1. Geben Sie auf der Seite **Hinzufügen eines regulären Ausdrucks** in das Textfeld **ID** **`ProjectID`** ein.
1. Geben Sie in das Textfeld **Regulärer Ausdruck** den folgenden Ausdruck ein:

    **`[a-zA-Z]{3}(\W)?[\d]{4}(\W)?[a-zA-Z]{2}`**

    >[!NOTE] Der angegebene reguläre Ausdruck ist so gestaltet, dass er eine Sequenz identifiziert, die durch drei Buchstaben, gefolgt von potenziell optionalen Nicht-Wort-Zeichen, dann vier Ziffern, wiederum gefolgt von optionalen Nicht-Wort-Zeichen und schließlich endend mit zwei Buchstaben gekennzeichnet ist. Das Vorhandensein von Nicht-Wort-Zeichen ist willkürlich, und das übergreifende Muster soll einem bestimmten Format oder einer bestimmten Struktur innerhalb der Daten entsprechen.

1. Wählen Sie unter dem Textfeld „Regulärer Ausdruck“ die Option **Zeichenfolgenübereinstimmung** und wählen Sie dann **Fertig**.
1. Wählen Sie im Fenster **Neues Muster** für das **Konfidenzniveau** die Option **Hohe Konfidenz**, wählen Sie **Erstellen** und wählen Sie dann **Weiter**.
1. Auf der Seite **Wählen Sie die empfohlene Konfidenzstufe, die in Richtlinien zur Konformität angezeigt werden soll**, lassen Sie die Einstellung auf **Hohe Konfidenzstufe** und wählen dann **Weiter**.
1. Überprüfen Sie auf der Seite **Einstellungen überprüfen und beenden** die Einstellungen, wählen Sie **Erstellen**, und wenn die Richtlinie erstellt ist, wählen Sie **Fertig**.

Sie haben erfolgreich einen neuen Typ für vertrauliche Informationen erstellt, um Projekt-IDs zu identifizieren.

### Aufgabe 2: Erstellen einer Aufbewahrungsbezeichnung

Sie erstellen eine Aufbewahrungsbezeichnung, um alle Dokumente im Zusammenhang mit Konstruktionsprojekten für 5 Jahre aufzubewahren.

1. Sie sollten weiterhin im Microsoft Purview-Portal **https://purview.microsoft.com/** angemeldet sein.
1. Wählen Sie im linken Navigationsbereich **Lösungen** und dann **Datenlebenszyklusverwaltung**.
1. Wählen Sie **Aufbewahrungsbezeichnungen** aus.
1. Auf der Seite **Kennzeichnungen** wählen Sie **Kennzeichnung erstellen**.
1. Geben Sie auf der Seite **Benennen Sie Ihre Vorratsspeicherung** die folgenden Informationen ein:

    - Name: **`Retention of Construction Project Documentation`**
    - Beschreibung für Benutzende: **`The construction project documentation Retention Policy dictates the retention of all project-related documents for five years following project completion.`**
    - Beschreibung für Administratoren: **`This label is applied to retain construction project documents for a period of five years, and it is utilized in conjunction with auto-labeling.`**

1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Bezeichnungseinstellungen festlegen** die Option **Elemente für immer oder für einen bestimmten Zeitraum aufbewahren** und wählen Sie **Weiter**.
1. Auf der Seite **Aufbewahrungszeitraum definieren** geben Sie die folgenden Informationen ein:

    - Elemente aufbewahren für: **5 Jahre**
    - Starten Sie die Aufbewahrungsfrist auf der Grundlage von: **Wann wurden die Elemente erstellt**

1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Auswählen, was nach der Aufbewahrungsfrist geschieht** die Option **Aufbewahrungseinstellungen deaktivieren** und wählen Sie dann **Weiter**.
1. Auf der Seite **Überprüfen und beenden** überprüfen Sie die Einstellungen und wählen **Kennzeichnung erstellen**.
1. Auf der Seite **Ihre Kennzeichnung für die Vorratsspeicherung wird erstellt** haben Sie mehrere Möglichkeiten.  Wählen Sie **Nichts tun** und wählen Sie dann **Fertig**.  Die Richtlinie für die automatische Anwendung wird in der nächsten Aufgabe erstellt. Wenn Sie die Option Automatische Bezeichnung für einen bestimmten Typ von Inhalt anwenden wählen, werden Sie ab Schritt 4 durch die Schritte der folgenden Aufgabe geführt.

1. Lassen Sie die Registerkarte des Browsers für die nächste Aufgabe geöffnet.

Sie haben erfolgreich eine Aufbewahrungsbezeichnung mit einem Aufbewahrungszeitraum von 5 Jahren erstellt.

### Aufgabe 3: Aufbewahrungsbezeichnung automatisch anwenden

Sie werden den Typ vertraulicher Informationen, die Sie in dieser Übung erstellt haben, verwenden, um die Aufbewahrungsbezeichnung automatisch anzuwenden.

1. Sie sollten weiterhin im Microsoft Purview-Portal bei der Data Lifecycle Management-Lösung angemeldet sein.  Falls nicht, navigieren Sie zu **`https://purview.microsoft.com/`** > **Lösungen** > **Datenlebenszyklusverwaltung**.
1. Wählen Sie im Bereich **Datenlebenszyklusverwaltung** die Option **Kennzeichnungsrichtlinien**.
1. Wählen Sie auf dem Blatt **Bezeichnungsrrichtlinien** die Option **Bezeichnung automatisch anwenden**.
1. Auf der Seite **Erste Schritte** die folgenden Informationen eingeben:

    - Name: **`Label documents related to construction projects`**
    - Description (Beschreibung): **`This policy automatically enforces the "Construction Project Documentation Retention" policy on any document pertaining to construction projects.`**

1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Wählen Sie den Inhaltstyp aus, auf den Sie diese Bezeichnung anwenden möchten**, wählen Sie **Bezeichnung auf Inhalte anwenden, die vertrauliche Informationen enthalten** und wählen Sie **Weiter**.
1. Wählen Sie auf der Seite **Inhalt, der vertrauliche Daten enthält** die Option **Benutzerdefiniert**, dann **Benutzerdefinierte Richtlinie** und **Weiter**.

1. Legen Sie auf der Seite **Inhalt bestimmen, der sensible Informationen enthält** die folgenden Einstellungen fest:
    - Gruppenname: **`Project ID lookup`**
    - Wählen Sie unter Typen vertraulicher Informationen **Hinzufügen** und wählen Sie **Typen vertraulicher Informationen**.  
    - Auf der Seite Typen vertraulicher Informationen geben Sie in das Suchfeld den Namen der von Ihnen erstellten Kennzeichnung **`Project Identification number`** ein und drücken die Eingabetaste.  Wählen Sie **Projektidentifikationsnummer** und dann **Hinzufügen**.
    - Lassen Sie das Konfidenzniveau auf **hohe Vertrauensstufe**.
    - Belassen Sie die Anzahl der Instanzen bei **1 bis Any**.
    - Wählen Sie **Weiter** aus.
1. Auf der Seite **Geltungsbereich der Richtlinie** lassen Sie die Einstellung für Admineinheiten auf **Volles Verzeichnis** und wählen **Weiter**.
1. Auf der Seite **Typ der zu erstellenden Aufbewahrungsrichtlinie**, wählen Sie **Statisch** und wählen Sie **Weiter**.
1. Überprüfen Sie unter „**Wählen Sie aus, wo die Kennzeichnung automatisch angebracht werden soll**“, ob der Status für alle verfügbaren Standorte auf „**Ein**“ gesetzt ist, und wählen Sie dann „**Weiter**“ aus.
1. Wählen Sie unter **Wählen Sie ein Kennzeichen zur automatischen Anwendung** die Option **Kennzeichen hinzufügen** aus, wählen Sie dann das Kennzeichen **Aufbewahrung von Bauprojektdokumenten** aus, das Sie in der vorherigen Aufgabe erstellt haben, wählen Sie **Hinzufügen** aus und wählen Sie dann **Weiter** aus.
1. Wählen Sie im Fenster **Entscheiden Sie, ob Sie Ihre Richtlinie testen oder ausführen möchten** die Option **Richtlinie einschalten** und wählen Sie dann **Weiter**.
1. Überprüfen Sie auf der Seite **Prüfen und beenden** alle Ihre Einstellungen, wählen Sie **Absenden** und dann **Erledigt**.

Sie haben die Aufbewahrungsbezeichnung erfolgreich veröffentlicht und automatisch auf alle Dokumente angewendet, die Projekt-IDs enthalten.
