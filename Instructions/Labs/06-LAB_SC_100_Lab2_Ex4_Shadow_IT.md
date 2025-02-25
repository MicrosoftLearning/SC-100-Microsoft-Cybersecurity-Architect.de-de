# Schatten-IT

Die IT-Infrastruktur von Contoso hat sich im Laufe der letzten Jahrzehnte weiterentwickelt und stellt verschiedene Serverinstanzen, Anwendungen und Dienste bereit. In den letzten zwei Jahren hat das Unternehmen die Sicherung seiner Umgebung durch die Implementierung von Gerätemanagement, Datengovernance sowie Identitäts- und Anwendungsschutz in den Vordergrund gestellt. Das Verfahren zur Beschränkung der Benutzenden auf bestimmte, vom Unternehmen bereitgestellte Anwendungen ist jedoch noch nicht eingeführt worden, so dass die Benutzenden Anwendungen aus verschiedenen Quellen installieren können. Als Cybersicherheitsarchitekt des Unternehmens ist es Ihr Ziel, einen vollständigen Überblick über alle von mitarbeitenden Personen genutzten Anwendungen zu haben. Ihre Schutzmaßnahme besteht darin, unsichere Anwendungen in Ihrer Umgebung zu blockieren. 

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept zur Bewältigung der Herausforderungen, mit denen Contoso Ltd. konfrontiert ist.

### Entwurfsansatz

In dem gegebenen Szenario besteht Ihre initiale Aktion darin, alle Anwendungen, die momentan von mitarbeitenden Personen genutzt werden, zu analysieren und aufzudecken. Von Benutzenden installierte, nicht autorisierte Anwendungen können ein Sicherheitsrisiko für das Unternehmen darstellen, was die Notwendigkeit unterstreicht, Schatten-IT zu identifizieren. Der nächste Schritt besteht darin, die von diesen unsicheren Anwendungen ausgehenden Risiken zu beseitigen.

Defender für Cloud Apps ist eine Sicherheitslösung, die für den Umgang mit Schatten-IT-Risiken in Cloudumgebungen entwickelt wurde. Es unterstützt Unternehmen bei der Erkennung und Überwachung von nicht autorisierten Cloud-Anwendungen, die von mitarbeitenden Personen genutzt werden, bei der Bewertung ihrer Sicherheitslage und bei der Erzwingung von Richtlinien zur Gewährleistung der Konformität und des Datenschutzes. Defender für Cloud Apps bietet Transparenz und Kontrolle über die Schatten-IT und unterstützt Unternehmen dabei, Sicherheitsrisiken abzuwehren, die mit einer nicht autorisierten Cloud-Nutzung verbunden sind, und so die Sicherheit ihrer Cloudumgebung zu erhöhen.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Ermitteln der Schatten-IT|Microsoft Defender für Cloud-Apps|Untersuchen aller Anwendungen in der Contoso-Umgebung|
|Blockieren aller unsicheren Anwendungen|Microsoft Defender für Cloud-Apps|Kennzeichnen von unsicheren Anwendungen als nicht genehmigt|

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1:Integrieren von Microsoft Defender for Endpoint in Defender for Cloud Apps 

Um die Verwendung von Apps auf den firmeneigenen Geräten der Benutzenden zu kontrollieren, müssen Sie Defender for Endpoint mit Defender for Cloud Apps integrieren.

1. Melden Sie sich beim Microsoft Defender-Portal **`https://security.microsoft.com`** als Allan Deyoung mithilfe seines Administratorkontos **MOD Administrator** an.
1. Erweitern Sie im Microsoft Defender-Portal **Untersuchung & Reaktion**, erweitern Sie dann **Suche** und wählen Sie **Erweiterte Suche**. Warten Sie auf den Abschluss der Vorbereitung der neuen Räume.  Dieser Schritt dient nur zum Einrichten der neuen Räume, es gibt keine Suche in diesem Schritt.
1. Erweitern Sie im Microsoft Defender-Portal auf der linken Navigationsseite **System** und wählen Sie dann **Einstellungen**.
1. Auf der Seite **Einstellungen** wählen Sie **Endpunkte**. HINWEIS: Es kann zwischen 10 Minuten und 1 Stunde dauern, bis diese Option angezeigt wird. Wenn Sie nach 10 Minuten noch nichts sehen, fahren Sie mit einer anderen Übung fort und kommen Sie dann zu diesem Schritt zurück.
1. Wählen Sie unter **Endpunkte** die Option **Erweiterte Funktionen**. Scrollen Sie nach unten, bis Microsoft Defender for Cloud-Apps angezeigt wird.  Wählen Sie den Schieberegler, um ihn auf **Ein** festzulegen.
1. Wählen Sie unten auf der Seite **Einstellungen speichern**.

Sie haben Microsoft Defender for Cloud Apps für Endpunkte erfolgreich aktiviert. Mit dieser Einrichtung werden alle Signale von Microsoft Defender für Endpunkten an Defender für Cloud-Apps weitergeleitet, sodass Sie unsichere Anwendungen blockieren können. Alle Anwendungen, die als **Ungesperrt** markiert sind, werden nun blockiert.

### Aufgabe 2: Untersuchen der Schatten-IT von Contoso Ltd

In dieser Aufgabe analysieren Sie alle Anwendungen, die momentan in Ihrem Unternehmen eingesetzt werden. Sie sehen sich verschiedene Anwendungen und deren jeweilige Risikobewertung sowie deren Bewertungsstruktur genauer an.

1. Sie sollten immer noch im Microsoft Defender-Portal angemeldet sein **https://security.microsoft.com/**.
1. Erweitern Sie im Microsoft Defender-Portal auf der linken Navigationsseite **Cloud-Apps** und wählen Sie **Cloud-Ermittlung**.
1. Auf der Seite **Cloud-Ermittlungen** wählen Sie **Entdeckte Apps**.
1. Das Blatt **Entdeckte Apps** zeigt alle Anwendungen an, die momentan in Ihrer Organisation genutzt werden. Erkunden Sie mehrere Anwendungen und die ihnen zugeordneten Risikobewertungen, indem Sie die jeweilige Anwendung auswählen.

> [!NOTE] Defender for Cloud-Apps bewertet die Risiken durch Auswertung von Zertifizierungen, Industriestandards und bewährten Methoden. Die Bewertung spiegelt den Reifegrad der App für den Einsatz in Unternehmen wider. Es errechnet eine Gesamtbewertung für jede App, indem es gewichtete Teilbewertungen für verschiedene Risikokategorien, die auch die Zuverlässigkeit berücksichtigen, zusammenfasst.

Sie haben mehrere Anwendungen, die momentan bei Contoso eingesetzt werden, erfolgreich überprüft.

### Aufgabe 3: Blockieren unsicherer Anwendungen

Sobald Sie sich einen Überblick über die Nutzung von Anwendungen in Ihrer Umgebung verschafft haben, besteht Ihre erste Abhilfemaßnahme darin, unsichere Anwendungen zu blockieren.

1. Sie sollten immer noch im Microsoft Defender-Portal angemeldet sein **https://security.microsoft.com/**.
1. Erweitern Sie im Microsoft Defender-Portal auf der linken Navigationsseite **Cloud-Apps** und wählen Sie **Cloud-Ermittlung**.
1. Auf der Seite **Cloud-Ermittlungen** wählen Sie **Entdeckte Apps**.
1. Legen Sie den Filter für **Risikobewertung** auf 0 - 4 fest.
1. Wählen Sie **Mehrfachauswahl** und dann **Alle**.
1. Wählen Sie die drei Punkte für **Weitere Aktionen**.
1. Wählen Sie **Tag als unzulässig markieren**.
1. Wählen Sie **Speichern**.

Sie haben anfällige Anwendungen erfolgreich blockiert, damit sie von den Benutzendern nicht verwendet werden können.

### Aufgabe 4: Unsichere Anwendungen automatisch blockieren

Um unsichere Anwendungen in Zukunft automatisch zu blockieren, erstellen Sie eine benutzerdefinierte Richtlinie für die Ermittlung von Apps. Mit dieser Richtlinie werden unsichere Anwendungen als **Unzulässig** markiert. Da Sie Defender for Endpoint mit Defender for Cloud Apps integriert haben, werden diese Anwendungen automatisch blockiert.

1. Sie sollten immer noch im Microsoft Defender-Portal angemeldet sein **https://security.microsoft.com/**.
1. Erweitern Sie im Microsoft Defender-Portal auf der linken Navigationsseite **Cloud-Apps** und wählen Sie **Cloud-Ermittlung**.
1. Auf der Seite **Ermittelte Apps** wählen Sie **+ Neue Richtlinie aus Suche**.
1. Geben Sie die folgenden Informationen ein:
    - **Richtlinienname**: Unsichere Apps als unzulässig kennzeichnen
    - **Schweregrad der Richtlinie**: Mittel
    - **Beschreibung für Benutzende**: Anträge mit einer Risikobewertung von 4 oder weniger werden nicht genehmigt und automatisch blockiert.
1. Fügen Sie unter **Apps, die auf alle der folgenden Punkte zutreffen** einen Filter hinzu und legen Sie ihn auf **Risikobewertung ist gleich 0-4** fest.
1. Wählen Sie unter **Warnungen** die Option **Erstelle eine Warnung für jedes passende Ereignis mit dem Schweregrad der Richtlinie** und legen Sie den Wert für **Tägliches Limit für Warnungen pro Richtlinie** auf 5 fest.
1. Wählen Sie unter **Governance-Aktionen** die Kategorie **App als unzulässig markieren**.
1. Klicken Sie auf **Erstellen**.

Sie haben erfolgreich eine Richtlinie zur Markierung von Anwendungen mit einer Risikobewertung von 5 oder weniger als unzulässig erstellt.