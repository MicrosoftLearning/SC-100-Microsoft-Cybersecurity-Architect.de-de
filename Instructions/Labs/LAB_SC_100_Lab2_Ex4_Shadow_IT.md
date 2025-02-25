---
lab: 3
title: Übung 4 - Schatten-IT
---


# Übung 2 - Aufgabe 4 - Schatten-IT

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

1. Melden Sie sich beim Microsoft Defender-Portal **https://security.microsoft.com/** als Allan Deyoung mithilfe seines Administratorkontos **MOD Administrator** an.
2. Erweitern Sie im Microsoft Defender-Portal **Hunting** und wählen Sie **Advanced Hunting**. Warten Sie auf den Abschluss der Vorbereitung der neuen Räume.
3. Wählen Sie im Microsoft Defender-Portal auf der linken Navigationsseite **Einstellungen**.
4. Auf der Seite **Einstellungen** wählen Sie **Endpunkte**.
5. Wählen Sie auf der Seite **Endpunkte** unter **Allgemein** die Option **Erweiterte Funktionen**.
6. Aktivieren Sie **Microsoft Defender for Cloud Apps**.
7. Wählen Sie **Einstellungen speichern** am unteren Rand.

Sie haben Microsoft Defender for Cloud Apps für Endpunkte erfolgreich aktiviert. Mit dieser Einrichtung werden alle Signale von Microsoft Defender for Endpoints an Defender for Cloud Apps weitergeleitet, so dass Sie unsichere Anwendungen blockieren können. Alle Anwendungen, die als **Ungesperrt** markiert sind, werden nun blockiert.

### Aufgabe 2: Untersuchen der Schatten-IT von Contoso Ltd.

In dieser Aufgabe analysieren Sie alle derzeit in Ihrem Unternehmen verwendeten Anwendungen. Sie sehen sich verschiedene Anwendungen und deren jeweilige Risikobewertung sowie deren Bewertungsstruktur genauer an.

1. Sie sollten immer noch im Microsoft Defender-Portal angemeldet sein **https://security.microsoft.com/**.
2. Erweitern Sie im Microsoft Defender-Portal auf der linken Navigationsseite **Cloud-Apps** und wählen Sie **Cloud-Ermittlung**.
3. Auf der Seite **Cloud-Ermittlungen** wählen Sie **Entdeckte Apps**.
4. Das Blatt **Entdeckte Apps** zeigt alle Anwendungen an, die momentan in Ihrer Organisation genutzt werden. Erkunden Sie mehrere Anwendungen und die ihnen zugeordneten Risikobewertungen, indem Sie die jeweilige Anwendung auswählen.

> [!NOTE] Defender for Cloud-Apps bewertet die Risiken durch Auswertung von Zertifizierungen, Industriestandards und bewährten Methoden. Die Bewertung spiegelt den Reifegrad der App für den Einsatz in Unternehmen wider. Es errechnet eine Gesamtbewertung für jede App, indem es gewichtete Teilbewertungen für verschiedene Risikokategorien, die auch die Zuverlässigkeit berücksichtigen, zusammenfasst.

Sie haben mehrere Anwendungen, die momentan bei Contoso eingesetzt werden, erfolgreich überprüft.

### Aufgabe 3: Blockieren unsicherer Anwendungen

Sobald Sie sich einen Überblick über die Nutzung von Anwendungen in Ihrer Umgebung verschafft haben, besteht Ihre erste Abhilfemaßnahme darin, unsichere Anwendungen zu blockieren.

1. Sie sollten immer noch im Microsoft Defender-Portal angemeldet sein **https://security.microsoft.com/**.
2. Erweitern Sie im Microsoft Defender-Portal auf der linken Navigationsseite **Cloud-Apps** und wählen Sie **Cloud-Ermittlung**.
3. Auf der Seite **Cloud-Ermittlungen** wählen Sie **Entdeckte Apps**.
4. Legen Sie den Filter für **Risikobewertung** auf 0 - 4 fest.
5. Wählen Sie **Mehrfachauswahl** und dann **Alle**.
6. Wählen Sie die drei Punkte für **Weitere Aktionen**.
7. Wählen Sie **Tag als unzulässig markieren**.
8. Wählen Sie **Speichern**.
   
Sie haben anfällige Anwendungen erfolgreich blockiert, damit sie von den Benutzendern nicht verwendet werden können.

### Aufgabe 4: Unsichere Anwendungen automatisch blockieren

Um unsichere Anwendungen in Zukunft automatisch zu blockieren, erstellen Sie eine benutzerdefinierte Richtlinie für die Ermittlung von Apps. Mit dieser Richtlinie werden unsichere Anwendungen als **Unzulässig** markiert. Da Sie Defender for Endpoint mit Defender for Cloud Apps integriert haben, werden diese Anwendungen automatisch blockiert.

1. Sie sollten immer noch im Microsoft Defender-Portal angemeldet sein **https://security.microsoft.com/**.
2. Erweitern Sie im Microsoft Defender-Portal auf der linken Navigationsseite **Cloud-Apps** und wählen Sie **Cloud-Ermittlung**.
3. Auf der Seite **Ermittelte Apps** wählen Sie **+ Neue Richtlinie aus Suche**.
4. Geben Sie die folgenden Informationen ein:
    - **Richtlinienname**: Unsichere Apps als unzulässig kennzeichnen
    - **Schweregrad der Richtlinie**: Mittel
    - **Beschreibung für Benutzende**: Anträge mit einer Risikobewertung von 4 oder weniger werden nicht genehmigt und automatisch blockiert.
5. Fügen Sie unter **Apps, die auf alle der folgenden Punkte zutreffen** einen Filter hinzu und legen Sie ihn auf **Risikobewertung ist gleich 0-4** fest.
6. Wählen Sie unter **Warnungen** die Option **Erstelle eine Warnung für jedes passende Ereignis mit dem Schweregrad der Richtlinie** und legen Sie den Wert für **Tägliches Limit für Warnungen pro Richtlinie** auf 5 fest.
7. Wählen Sie unter **Governance-Aktionen** die Kategorie **App als unzulässig markieren**.
8. Klicken Sie auf **Erstellen**.

Sie haben erfolgreich eine Richtlinie zur Markierung von Anwendungen mit einer Risikobewertung von 5 oder weniger als unzulässig erstellt.