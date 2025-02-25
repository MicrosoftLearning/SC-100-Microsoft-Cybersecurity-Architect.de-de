---
lab: 4
title: Übung 3 - Verhinderung von Datenverlust
---

# Übung 4 - Aufgabe 3 - Verhinderung von Datenverlust

Contoso Ltd. ist momentan dabei, Tailwind Traders in ihre Projekte zu integrieren. Obwohl die Fusion noch im Gange ist, sind beide Unternehmen in getrennten Mandanten tätig. Mitarbeitende Personen von Tailwind Traders gelten als externe Benutzende und werden als Gäste in den Mandant von Contoso eingeladen, um die gemeinsame Nutzung von SharePoint-Sites und -Dateien zu erleichtern. In bestimmten Projekten empfangen ausgewählte mitarbeitende Personen von Tailwind Traders Windows 11-Clients, die von Contoso Ltd. verwaltet werden, um den vollen Zugriff auf interne Ressourcen zu gewährleisten und gleichzeitig die Sicherheitsüberwachung aufrechtzuerhalten. Der Zugriff auf M365-Desktop-Anwendungen ist für nicht verwaltete Geräte gesperrt, und diese Benutzende können nur über Webanwendungen auf die Umgebung zugreifen. Die verwalteten Geräte werden durch verschiedene Richtlinien in Endpoint Manager gesichert. Contoso Ltd. hat Microsoft Purview Information Protection implementiert, um sensible Dokumente auf der Grundlage des Typs der darin enthaltenen Informationen zu verschlüsseln. 

Als Cybersicherheitsarchitekt haben Sie kürzlich verschiedene Aktivitäten im Aktivitätsprotokoll von Defender for Cloud-Apps untersucht und festgestellt, dass einige als vertraulich gekennzeichnete Dokumente auf externe USB-Laufwerke kopiert werden. Sie haben auch festgestellt, dass es den Benutzender freisteht, alle Unternehmensdaten, auf die sie Zugriff haben, auf ihren nicht verwalteten, persönlichen Geräten zu speichern. Dies stellt ein großes Problem dar, das behoben werden muss. Als Lösung entwerfen Sie eine Sicherheitsrichtlinie, um die Speicherung von Unternehmensdaten auf nicht verwalteten, persönlichen Geräten einzuschränken. Dies trägt dazu bei, das Risiko zu minimieren, dass vertrauliche Daten kompromittiert werden.

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept zur Bewältigung der Risiken, denen Contoso Ltd. ausgesetzt ist.

### Entwurfsansatz

Der erste Schritt umfasst die Analyse der Anforderungen basierend auf dem beschriebenen Problem, das Verständnis der Ziele und die Definition der Anforderungen.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Verhindern der Datenübertragung auf USB-Laufwerke
- Einschränken des Zugriffs auf vertrauliche Daten von nicht verwalteten Geräten
- Blockieren des Herunterladens sensibler Daten von nicht verwalteten Geräten

Im zweiten Schritt untersuchen Sie die vorhandene Umgebung von Contoso Ltd.. Microsoft Purview und Microsoft Defender bieten verschiedene Lösungen für die Verwaltung von Data Flow, die Microsoft Purview Information Protection, Verhinderung von Datenverlusten, bedingten Zugriff und Aufbewahrungsrichtlinien umfassen. Untersuchen Sie, welche Steuerelemente bereits vorhanden sind. Greifen Sie auf verschiedene Portale zu, um aktuelle Konfigurationen und Richtlinien zu überprüfen, zu bestimmen, ob Anpassungen erforderlich sind oder ob neue Einstellungen/Richtlinien Implementierung benötigen.

Die dritte Phase umfasst das Erstellen des Lösungskonzepts. Bei der Untersuchung ist offensichtlich, dass keine der aktuellen Richtlinien die definierten Anforderungen erfüllt. Daher ist eine neue Reihe von Richtlinien unerlässlich.

### Vorgeschlagene Lösung

Entwerfen Sie eine Sicherheitsrichtlinie, um die Speicherung von Unternehmensdaten auf nicht verwalteten persönlichen Geräten einzuschränken. Dies trägt dazu bei, das Risiko zu minimieren, dass vertrauliche Daten kompromittiert werden. Die Richtlinie sollte die Datentypen beschreiben, die als vertraulich betrachtet werden, und die zulässigen Geräte, auf denen sie gespeichert werden können. Außerdem sollte die Richtlinie Leitlinien für die sichere Übertragung von Daten auf externe Geräte bereitstellen. Die Mitarbeitenden müssen eine Vereinbarung unterzeichnen, die ihr Verständnis der Richtlinie und ihre Verpflichtung zur Einhaltung der Richtlinie anerkennt. Die Richtlinie sollte allen Mitarbeitern mitgeteilt und durch regelmäßige Überprüfungen und disziplinarische Maßnahmen gegen Nichteinhaltung durchgesetzt werden. Außerdem sollten regelmäßige Schulungen durchgeführt werden, um sicherzustellen, dass die mitarbeitenden Personen sich der Risiken bewusst sind, die mit der Speicherung von Unternehmensdaten auf persönlichen Geräten verbunden sind, und um ihnen die Wichtigkeit der Einhaltung der Richtlinie zu verdeutlichen. Schließlich sollte die Richtlinie regelmäßig überprüft und aktualisiert werden, um sicherzustellen, dass sie wirksam und relevant bleibt. 

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Blockieren der Verschiebung von Daten auf USB-Laufwerke|Verhinderung von Endpunktdatenverlust|Verhindern, dass alle Daten mit einer vertraulichen Bezeichnung auf ein USB-Laufwerk kopiert werden|
|Einschränken des Zugriffs auf vertrauliche Daten von nicht verwalteten Geräten|Defender for Cloud-Apps|Blockieren von Kopieren/Ausschneiden/Einfügen von Daten für nicht verwaltete Geräte|
|Blockieren des Downloads sensibler Daten von nicht verwalteten Geräten|Defender for Cloud-Apps|Blockieren des Herunterladens von Daten von nicht verwalteten Geräten|

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1: Bereitstellen einer Richtlinie zur Verhinderung von Datenverlusten

Der erste Schritt des Lösungsentwurfs umfasst die Erstellung einer Regel zur Verhinderung von Datenverlusten für Endgeräte. Sie werden eine DLP-Regel bereitstellen, um das Kopieren von Daten auf USB-Laufwerke zu blockieren. 

1. Melden Sie sich beim Microsoft Purview Compliance-Portal **https://compliance.microsoft.com** als Allan Deyoung mithilfe seines Administratorkontos **MOD Administrator** an.
1. Wenn Sie aufgefordert werden, wieder zum klassischen Microsoft Purview Konformitäts-Portal zu wechseln, wählen Sie **Umschalten**.
1. Erweitern Sie im Microsoft Purview-Portal im linken Navigationsbereich **Verhinderung von Datenverlusten** und wählen Sie dann **Richtlinien**.
1. Wählen Sie auf der Seite **Richtlinien** die Option **+ Richtlinie erstellen** aus.
1. Auf der Seite **Starten Sie mit einer Vorlage oder erstellen Sie eine benutzerdefinierte Richtlinie** wählen Sie **Benutzerdefiniert**, **Benutzerdefinierte Richtlinie** und dann **Weiter**.
1. Geben Sie auf der Seite **Nennen Sie Ihre DLP-Richtlinie** einen Namen und eine Beschreibung ein und wählen Sie **Weiter**.
1. Auf der Seite **Admineinheiten zuweisen** wählen Sie **Weiter**.
1. Wählen Sie auf der Seite **Wählen Sie, wo die Richtlinie angewendet werden soll** nur **Geräte** und wählen Sie **Weiter**.
1. Wählen Sie auf der Seite **Richtlinieneinstellungen festlegen** **Weiter**.
1. Wählen Sie auf der Seite **Erweiterte DLP-Regeln anpassen** die Option **+ Regel erstellen**.
1. Geben Sie einen Namen und eine Beschreibung für die Regel ein. 
1. Unter **Bedingungen** wählen Sie **+ Bedingung hinzufügen** und wählen **Inhalt enthält**.
1. Legen Sie folgende Bedingungen fest:

    - **Inhalt enthält**: 
      - Wählen Sie **Hinzufügen**, wählen Sie dann **Vertraulichkeitsbezeichnungen** und wählen Sie die Kennzeichnungen **Vertraute Personen**, **Projekt - Falke**, **Vertraulich**, **Streng Vertraulich**, **Vertraulich - Finanzen**. Klicken Sie auf **Hinzufügen**.
13. Wählen Sie unter **Aktionen** die Option **+ Eine Aktion hinzufügen** und wählen Sie **Aktivitäten auf Geräten überprüfen oder einschränken**.
14. Legen Sie folgende Aktionen fest:
   -    Wählen Sie unter **Aktivitäten für alle Apps** die Option **Einschränkungen auf bestimmte Aktivitäten anwenden**.
      - Stellen Sie sicher, dass **Kopieren auf ein entfernbares USB-Gerät** ausgewählt ist und wählen Sie die Option **Sperren** aus dem Dropdownmenü für diese Einstellung.
      - Lassen Sie die anderen Einstellungen unverändert.
15. Wählen Sie **Speichern**.
16. Wählen Sie **Weiter** aus.
17. Wählen Sie auf der Seite **Richtlinienmodus** die Option **Die Richtlinie sofort einschalten**. Wählen Sie **Weiter** aus.
18.  Wählen Sie auf der Seite **Überprüfen und beenden** die Option **Absenden** aus.

Sie haben erfolgreich eine Richtlinie zur Verhinderung von Datenverlusten implementiert, die jegliches Kopieren von Daten auf USB-Laufwerke verhindert.

### Aufgabe 2: Onboarding von Anwendungen zur Kontrolle der App für bedingten Zugriff

Ein Teil der Lösung besteht darin, Sitzungsrichtlinien in Defender for Cloud-Apps zu erstellen. Sitzungsrichtlinien bieten umfassende Einblicke in Cloudanwendungen durch Echtzeitüberwachung von Sitzungen. Diese Richtlinien ermöglichen maßgeschneiderte Aktionen gemäß der angegebenen Richtlinie für jede Benutzersitzung. Um eine Sitzungsrichtlinie zu erstellen, muss die App-Steuerung für bedingten Zugriff in Ihren Anwendungen bereitgestellt werden. Die App-Steuerung für bedingten Zugriff bietet Echtzeitüberwachung und Steuerungsfunktionen für Ihre Apps. Das Erstellen einer Sitzungsrichtlinie ohne Onboarding einer App in die App-Steuerung für bedingten Zugriff wird nicht funktionieren. Der erste Schritt ist das Onboarding von Anwendungen, die Sie für die App-Steuerung für bedingten Zugriff schützen möchten. 

Es gibt 2 Möglichkeiten, Anwendungen in die App-Steuerung für bedingten Zugriff zu integrieren:

- Fügen Sie eine Anwendung manuell im Microsoft Defender-Portal hinzu (Einstellungen > Cloud-Apps > Verbundene Apps > App-Steuerung für bedingten Zugriff)
- Konfigurieren Sie eine Richtlinie für bedingten Zugriff zum Schutz von Apps mit Defender for Cloud-Apps

Eine Richtlinie für bedingten Zugriff leitet alle in der Richtlinie angegebenen Anwendungen an „Defender for Cloud-Apps - App-Steuerung für bedingten Zugriff“ weiter. Wenn sich ein Benutzender das nächste Mal bei den angegebenen Anwendungen anmeldet, wird die entsprechende Anwendung automatisch der App-Steuerung für bedingten Zugriff hinzugefügt. Sie können diese Anwendungen im Microsoft Defender-Portal anzeigen lassen. 
 
>**Tipp:** Bevor Sie diese Aufgabe starten, sollten Sie die vorhandenen Apps für die App-Steuerung für bedingten Zugriff überprüfen. Sie werden feststellen, dass noch keine Anwendungen integriert wurden. Versuchen Sie in diesem Stadium, eine Sitzungsrichtlinie in Defender für Cloud-Apps zu erstellen und die aufgetretenen Fehlermeldungen zu überprüfen.

In dieser Aufgabe stellen Sie die App-Steuerung für bedingten Zugriff für Ihre Anwendungen bereit, indem Sie eine Richtlinie für bedingten Zugriff in Microsoft Entra erstellen. 

1. Melden Sie sich beim Microsoft Entra-Portal **https://entra.microsoft.com** als Allan Deyoung mit seinem Administratorkonto **MOD-Administrator** an.
2. Erweitern Sie im Microsoft Entra Portal **Schutz** und wählen Sie **Bedingter Zugriff**.
3. Wählen Sie auf der Seite **Bedingter Zugriff | Übersicht** den Punkt **Richtlinien** und wählen Sie **+ Neue Richtlinie**.
4. Geben Sie einen Namen für die Richtlinie ein.
5. Unter **Zuweisungen** wählen Sie **Benutzer** und schließen **Alle Benutzenden** ein.
6. Unter **Zuweisungen** wählen Sie **Zielressourcen** und schließen **Alle Cloud Apps** ein.
7. Unter **Zugriffssteuerung** wählen Sie **Sitzung**.
8. Wählen Sie im Bereich **Sitzung** die Option **Benutzung der App-Steuerung für bedingten Zugriff** und wählen Sie **Benutzerdefinierte Richtlinie verwenden ...**, und schließen Sie dann den Bereich **Sitzung** mit der Schaltfläche **Auswählen**.
9. Unter **Richtlinie aktivieren** wählen Sie **Ein**.
10. Wenn Sie eine Warnung erhalten, dass der aktuelle Benutzende von der Richtlinie ausgeschlossen werden soll, wählen Sie **Ich verstehe, dass mein Konto von dieser Richtlinie betroffen sein wird. Fahren Sie trotzdem fort.**.
11. Geben Sie optional die Bedingungen an und gewähren Sie die Steuerelemente.
12. Klicken Sie auf **Erstellen**.

Melden Sie sich jetzt bei einer der Microsoft-Web-Apps an, z. B. bei [Outlook](https://outlook.office365.com). Die Anwendung, bei der Sie sich anmelden, wird automatisch in die App-Steuerung für bedingten Zugriff integriert. Melden Sie sich beim Microsoft Defender-Portal an, und sehen Sie sich die Anwendungen an, die unter die App-Steuerung für bedingten Zugriff fallen.

Sie haben erfolgreich eine Richtlinie für bedingten Zugriff erstellt, um alle Anwendungen an Defender for Cloud-Apps und Onboarding-Apps zur App-Steuerung für bedingten Zugriff weiterzuleiten.

### Aufgabe 3: Erstellen von Sitzungsrichtlinien in Defender for Cloud-Apps

Sie werden in Defender for Cloud-Apps zwei Richtlinien für Sitzungen erstellen, um das Herunterladen von Daten zu blockieren und die Berechtigungen für nicht verwaltete Geräte einzuschränken.

1. Melden Sie sich beim Microsoft Defender-Portal **https://security.microsoft.com** als Allan Deyoung mithilfe seines Administratorkontos **MOD-Administrator** an.
1. Wählen Sie im Microsoft Security-Portal **Cloud Apps** > **Richtlinien** > **Richtlinienverwaltung**.
1. Wählen Sie auf der Seite **Richtlinien** **+ Richtlinie erstellen** > **Sitzungsrichtlinie**.
1. Wählen Sie auf der Seite **Sitzungsrichtlinie erstellen** die Richtlinienvorlage **Download basierend auf Echtzeit-Inhaltsprüfung blockieren**.
1. Geben Sie einen Richtliniennamen ein.
1. Wählen Sie einen Schweregrad der Richtlinie und eine Kategorie.
1. Geben Sie eine Beschreibung ein.
1. Wählen Sie unter **Typ des Sitzungssteuerungstyp** die Option **Dateidownload (mit Prüfung)**.
1. Wählen Sie unter **Quelle der Aktivitäten** im Abschnitt **Aktivitäten, die mit allen der folgenden übereinstimmen** den folgenden Filter:

    - **Gerätetag**: Wählen Sie **Nicht gleich** und wählen Sie **Intune-konform**.

10. Wählen Sie im Abschnitt **Dateien, die auf alle der folgenden Punkte zutreffen**, den folgenden Filter:

    - **Vertraulichkeitsbezeichnung**: Wählen Sie **Gleich** und wählen Sie die Kennzeichnungen **Vertraulich**, **Streng vertraulich** und **Vertraulich - Finanzen**.

11. Unter **Inspektionsmethode** wählen Sie **Datenklassifizierungsdienst**, dann **beliebig**, dann **Typ sensibler Informationen...** und wählen Sie den entsprechenden Typ sensibler Informationen, auf den Sie diese Richtlinie anwenden möchten.
12. Wählen Sie unter **Aktionen** **Blockieren**.
13. Klicken Sie auf **Erstellen**, um die Richtlinie zu erstellen.
14. Erstellen Sie eine zweite Richtlinie wie oben beschrieben und wählen Sie die Richtlinienvorlage **Ausschneiden/Kopieren und Einfügen basierend auf Echtzeit-Inhaltsprüfung sperren**.
15. Unter **Aktivitätsquelle** in den **Aktivitäten, die zu allen der folgenden** passen, geben Sie die folgenden Informationen ein: 

    - **Typ der Aktivität**: Wählen Sie **Gleich** und wählen Sie **Element ausschneiden/kopieren, Element einfügen**
    - **Gerätetag**: Wählen Sie **Nicht gleich** und wählen Sie **Intune-konform**

16. Deaktivieren Sie **Inhaltsprüfung verwenden** und wählen Sie **Erstellen**, um die Richtlinie zu erstellen.

Sie haben erfolgreich zwei Sitzungsrichtlinien in Defender für Cloud-Apps erstellt.
