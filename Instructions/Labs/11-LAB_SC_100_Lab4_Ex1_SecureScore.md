# Sicherheitslagemanagement

Das Sicherheitsteam von Contoso möchte seinen Sicherheitsstatus mithilfe der Microsoft-Sicherheitsbewertung verbessern, einem Tool, das Empfehlungen und Anleitungen zur Reduzierung der Angriffsfläche und zum Schutz vor Bedrohungen bereitstellt.

Das Sicherheitsteam überprüft die von der Sicherheitsbewertung empfohlenen Maßnahmen und delegiert sie an die erweiterte Teammitgliedschaft (Sicherheitsbotschafter bzw. Sicherheitsbotschafterinnen), die den Status und den Aktionsplan verwalten, die den Verbesserungsmaßnahmen zugeordnet sind. Das Sicherheitsteam möchte auch den Zugang zu den Informationen über die Sicherheitsbewertung und die Datenquellen, die sie speisen, kontrollieren. Joni Shermann ist ein Sicherheitsbotschafter und benötigt Zugriff auf das Gefährdungsmanagement.

Kürzlich gab es Berichte, dass nicht eingeladene Mitarbeitende automatisch zu Teams-Anrufen zugelassen wurden, zu denen sie nicht direkt eingeladen wurden.  Aufgrund der vertraulichen Art von Anrufen möchte das Sicherheitsteam dies kontrollieren.

## Teil 1: Entwerfen einer Lösung (erforderlich)

### Entwurfsansatz

Auf der Registerkarte Empfohlene Aktionen in der Microsoft-Sicherheitsbewertung werden die Sicherheitsempfehlungen aufgeführt, die mögliche Angriffsflächen betreffen. Diese Aktionen können freigegeben/delegiert werden.

Sicherheitsteams müssen den Zugriff auf die Informationen zum Sicherheitsstatus der Organisation und auf die spezifischen Datenquellen, die diese Informationen liefern, kontrollieren. Das RBAC-Modell (Rollenbasierte Zugriffssteuerung) von Microsoft Defender XDR bietet eine einzige Berechtigungsverwaltungsoberfläche, die Administrierenden einen zentralen Standort für die Steuerung von Benutzerberechtigungen über verschiedene Sicherheitslösungen hinweg bietet.

Um sicherzustellen, dass die Sicherheitsbotschafter bzw. Sicherheitsbotschafterinnen über die erforderlichen Rollenberechtigungen verfügen, müssen Sie eine benutzerdefinierte Rolle erstellen. Damit das Microsoft Defender XDR-Sicherheitsportal damit beginnt, die in Ihren neuen benutzerdefinierten Rollen oder importierten Rollen konfigurierten Berechtigungen und Zuweisungen durchzusetzen, müssen Sie das Microsoft Defender XDR Unified RBAC-Modell für einige oder alle Ihrer Workloads aktivieren.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Joni Shermann wird die Maßnahmen und den Status verwalten, die den Empfehlungen der Sicherheitsbewertung zugeordnet sind. |Gefährdungsmanagement – Sicherheitsbewertung und Defender XDR Unified RBAC | Erstellen Sie eine Rolle zur Verwaltung des Sicherheitsstatus und gewähren Sie Joni Shermann Zugriff. |
|Steuern sie den Zugriff auf Sicherheitsstatusinformationen und die Datenquellen, die sie feeden. | Microsoft Defender XDR Unified RBAC | Aktivieren Sie Microsoft Defender XDR Unified RBAC für benutzerdefinierte Rolle. |
|Empfohlene Aktion zum Freigeben der Sicherheitsbewertung |Sicherheitsbewertung | Empfohlene Aktionen freigeben |

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1 – Erstellen einer benutzerdefinierten Rolle zum Verwalten des Sicherheitsstatus für das Gefährdungsmanagement

In dieser Aufgabe richten Sie eine benutzerdefinierte Rolle ein, die sich auf den Sicherheitsstatus und genauer auf das Gefährdungsmanagement konzentriert. Als Teil der benutzerdefinierten Rolle gewähren Sie Joni Shermann Zugriff auf die Datenquelle für das Gefährdungsmanagement.

1. Melden Sie sich bei der Windows-Client-VM **LON-SC1** mit dem lokalen **Administrator**-Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste aus, navigieren Sie zu **`https://security.microsoft.com`** und melden Sie sich bei **Microsoft Defender** als MOD-Fachkraft in der IT-Verwaltung **admin@WWLxZZZZZZ.onmicrosoft.com** an (wobei ZZZZZZ Ihre eindeutige Mandanten-ID ist, die Sie von Ihrem Lab-Hosting-Anbieter erhalten haben). Das Passwort der administrierenden Person sollte von Ihrem Lab-Hosting-Anbieter bereitgestellt werden.
1. Aktivieren Sie im Dialogfeld **Angemeldet bleiben?** das Kontrollkästchen **Dies nicht mehr anzeigen** und wählen Sie dann **Nein**.
1. Schließen Sie den Dialog zum Speichern von Passwörtern von unten, indem Sie **Nie** wählen, um die Standard-Anmeldeinformationen für globale Administrierende nicht in Ihrem Browser zu speichern.
1. Wenn Sie oben rechts auf dem Bildschirm ein Informationsfeld **Multi-Faktor-Authentifizierung verwalten** sehen, schließen Sie es, indem Sie das **X** auswählen.
1. Erweitern Sie im linken Navigationsbereich **System** und wählen Sie dann **Berechtigungen**.
1. Wenn Sie zum ersten Mal auf die Einstellungen von Microsoft Defender zugreifen, müssen Sie ein paar Minuten warten, während Defender neue Speicherplätze für Ihre Daten vorbereitet und diese miteinander verbindet.  Sobald dies abgeschlossen ist, aktualisieren Sie die Seite mit den Berechtigungen, bis Sie eine Auflistung sehen, die Microsoft Defender XDR, Microsoft Entra ID, Endpunktrollen und -gruppen, E-Mail- und Zusammenarbeitsrollen sowie Cloud Apps enthält. Es kann einige Zeit dauern, bis alle diese Daten angezeigt werden.
1. Wählen Sie unter **Microsoft Defender XDR(1)**, **Rollen**.
1. Wählen Sie **Benutzerdefinierte Rolle erstellen**.
1. Geben Sie in das Feld Rollenname **`SecureScore Manager`** ein und wählen Sie **Weiter**.
1. Wählen Sie **Sicherheitsstatus** aus.
1. Im Fenster Sicherheitsstatus:
    - Wählen Sie **Benutzerdefinierte Berechtigungen auswählen**
    - Wählen Sie unter Statusmanagement **Benutzerdefinierte Berechtigungen auswählen**
    - Wählen Sie **Gefährdungsmanagement (verwalten)**
    - Wählen Sie **Übernehmen**.
    - Wählen Sie **Weiter** aus.
1. Auf der Seite **Benutzende und Datenquellen zuweisen** **Zuweisung hinzufügen** auswählen und die Felder wie folgt auffüllen:
    - Zuweisungsname: **`ExposureManagement`**
    - Benutzende und Gruppe zuweisen: **`Joni Sherman`** eingeben und dann auswählen.
    - Wählen Sie unter **Datenquellen** das Dropdownmenü aus, um eine Liste der verfügbaren Datenquellen anzuzeigen. Wählen Sie nur **Microsoft Security Exposure Management**.  Wenn andere Datenquellen aufgelistet sind, heben Sie die Auswahl auf.
    - Wählen Sie **Hinzufügen** aus.
    - Wählen Sie **Weiter** aus.
1. Auf der Seite Überprüfen und Fertig stellen überprüfen Sie Ihre Einstellungen, wählen Sie **Senden** und dann **Fertig**.
1. Sie sollten sich auf der Seite **Berechtigungen und Rollen** befinden und die benutzerdefinierte Rolle sehen, die Sie gerade erstellt haben. Lassen Sie diese Registerkarte geöffnet, Sie werden bei der nächsten Aufgabe darauf zurückkommen.

Sie haben erfolgreich eine benutzerdefinierte Rolle für den Sicherheitsstatus eingerichtet, die Joni Shermann Zugriff auf die Datenquelle für das Gefährdungsmanagement gewährt.

### Aufgabe 2 - Aktivieren von Defender XDR Unified RBAC für bestimmte Workloads

Damit das Microsoft Defender XDR-Sicherheitsportal die in Ihren neuen benutzerdefinierten Rollen konfigurierten Berechtigungen und Zuweisungen durchsetzen kann, müssen Sie das Microsoft Defender XDR Unified RBAC-Modell für Ihre Workloads aktivieren.

Wenn Sie einige oder alle Ihre Workloads für die Verwendung des neuen Berechtigungsmodells aktivieren, werden die Rollen und Berechtigungen für diese Workloads vollständig durch das Microsoft Defender XDR Unified RBAC-Modell im Microsoft Defender-Portal gesteuert.

In dieser Aufgabe erkunden Sie die Seite, auf der Workloads aktiviert werden.

1. Sie sollten weiterhin im Microsoft Defender-Portal angemeldet sein und sich auf der Seite **Berechtigungen und Rollen** befinden. Sie sollten die benutzerdefinierte Rolle sehen, die Sie gerade erstellt haben.
1. Beachten Sie die Informationen im grauen Banner, einige der Rollen sind noch nicht anwendbar, da Sie nicht alle Workloads aktiviert haben. Wählen Sie **Workloads aktivieren**.
1. Beachten Sie die Beschreibung unter **Aktivieren Sie die einheitliche rollenbasierte Zugriffskontrolle**.  Wenn Sie einige oder alle Ihre Workloads für die Verwendung des neuen Berechtigungsmodells aktivieren, werden die Rollen und Berechtigungen für diese Workloads vollständig durch das Microsoft Defender XDR Unified RBAC-Modell im Microsoft Defender-Portal gesteuert.
1. Für diese Übung ist die Datenquelle für das Gefährdungsmanagement standardmäßig aktiviert, weshalb es keine Einstellung gibt, um diesen Workload zu aktivieren. Wenn Sie eine benutzerdefinierte Rolle erstellt hätten, die Berechtigungen für andere Workloads wie z. B. Office 365 oder Geräte- und Sicherheitsrisikomanagement enthält, müssten Sie diese spezifischen Workloads aktivieren, um die benutzerdefinierte Rolle als Teil von Unified RBAC zu aktivieren.

Sie haben gelernt, wo Sie das Microsoft Defender XDR Unified RBAC-Modell für einige oder alle Ihre Workloads aktivieren.

### Aufgabe 3 – Freigeben einer empfohlenen Aktion

Geben Sie eine empfohlene Aktion aus der Microsoft-Sicherheitsbewertung frei. In dieser Aufgabe posten Sie die Aktion in einem Teams-Kanal. Durch die Veröffentlichung in Teams sehen Benutzernde im Kanal eine Benachrichtigung, haben jedoch keinen Zugriff auf die Datenquelle, um den Status zu bearbeiten oder die Aktion zu verwalten. Nur Joni Shermann, der Mitglied des Teams-Kanals ist und über Rollenberechtigungen verfügt, kann auf die empfohlene Aktion zugreifen.

1. Sie sollten weiterhin im Microsoft Defender XDR-Portal angemeldet sein.
1. Erweitern Sie im linken Navigationsbereich **Gefährdungsmanagement** und wählen Sie dann **Sicherheitsbewertung** aus.
1. Wählen Sie die Registerkarte **Empfohlene Aktionen**.
1. Suchen Sie nach **`Only invited users should be automatically admitted to Teams meetings`**, und wählen Sie diese Option aus.
1. Wählen Sie **Freigeben**, und wählen Sie im Dropdownmenü **Microsoft Teams**.
1. Im Feld **Team** wählen Sie **Mark 8 Projektteam** und im Feld **Kanal** wählen Sie **Kanal Recherche und Entwicklung**.
1. Wählen Sie **Nachricht in Teams veröffentlichen**.

Joni Sherman und sein Mark 8-Projektteam werden über die empfohlene Aktion im Teams-Kanal benachrichtigt.

### Aufgabe 4 – Empfehlungen verwalten

Als Joni Sherman haben Sie die Benachrichtigung des Teams erhalten, dass eine bestimmte Aktion zur Verbesserung des Sicherheitsstatus der Organisation empfohlen wurde.  Als erweitertes Mitglied des Sicherheitsteams verfügen Sie über die Rollenberechtigungen, um die empfohlene Aktion zu verwalten und die Lösung zu dokumentieren.

In dieser Aufgabe verwalten Sie empfohlene Aktionen und dokumentieren Ihre Lösungen.

1. Öffnen Sie ein Microsoft Edge InPrivate-Fenster, navigieren Sie zu **`https://office.com`** und melden Sie sich als **JoniS@WWLxZZZZZZ.onmicrosoft.com** an.
1. Wenn die Landing Page verschwommen angezeigt wird, aktualisieren Sie die Seite.
1. Wählen Sie das Symbol für das App-Startfeld links neben dem oberen Banner Contoso Electronics und wählen Sie **Teams**.
1. Wählen Sie im Fenster Willkommen bei Teams die Option **Erste Schritte**. Es kann eine oder zwei Minuten dauern, bis Teams eingerichtet wurde. Wenn ein Teams for Mobile QR-Code-Bildschirm angezeigt wird, schließen Sie ihn.
1. Teams öffnen. Für das **Mark 8-Projektteam** wählen Sie **Alle Kanäle anzeigen** und dann **Forschung und Entwicklung**.
1. Überprüfen Sie die Nachricht, die aus der vorherigen Aufgabe veröffentlicht wurde.
1. Wählen Sie in der veröffentlichten Nachricht den Link **https://security.microsoft.com/securescore?viewid=actions&actionId=meeting_autoadmitusers_v1**.  Da Ihnen, Joni Shermann, die Berechtigung über die benutzerdefinierte Rolle erteilt wurde, können Sie auf die Sicherheitsbewertung zugreifen.  Andere Mitglieder des Mark 8-Projektteams können den Beitrag sehen, haben aber keinen Zugriff auf die Sicherheitsbewertung.
1. Wählen Sie **Status und Aktionsplan bearbeiten** aus.
1. Prüfen Sie **Lösung durch Dritte**.
1. Fügen Sie dem Feld **Aktionsplan** einen Hinweis **Aktuell gesichert** hinzu.
1. Wählen Sie **Speichern und Schließen**.
1. Schließen Sie die inPrivate-Browserregisterkarten.

Als Joni Shermann haben Sie den Status für die empfohlene Aktion erfolgreich bearbeitet.

### Aufgabe 5 (Optional) – Adele Vance greift auf den Teams-Beitrag zu

In dieser Aufgabe greift Adele Vance auf den Kanal des Mark 8-Projektteams zu und wählt den Link in der veröffentlichten Nachricht aus.

1. Öffnen Sie ein Microsoft Edge InPrivate-Fenster, navigieren Sie zu **`https://office.com`** und melden Sie sich als Adele Vance, **AdeleV@WWLxZZZZZZ.onmicrosoft.com** an.
1. Wenn die Landing Page verschwommen angezeigt wird, aktualisieren Sie die Seite.
1. Wählen Sie das Symbol für das App-Startfeld links neben dem oberen Banner Contoso Electronics und wählen Sie **Teams**.
1. Wählen Sie im Fenster Willkommen bei Teams die Option **Erste Schritte**.
1. Teams öffnen. Für das **Mark 8-Projektteam** wählen Sie **Alle Kanäle anzeigen** und dann **Forschung und Entwicklung**.
1. Überprüfen Sie die Nachricht, die aus der vorherigen Aufgabe veröffentlicht wurde.
1. Wählen Sie den Link in der veröffentlichten Nachricht **https://security.microsoft.com/securescore?viewid=actions&actionId=meeting_autoadmitusers_v1**.
1. Sie werden direkt zur Microsoft-Sicherheitsbewertung weitergeleitet, haben jedoch keine Berechtigung für den Zugriff auf diese Daten, da Adele Vance nicht als Mitglied der von Ihnen erstellten benutzerdefinierten Rolle hinzugefügt wurde.
1. Schließen Sie die InPrivate-Browserregisterkarten.

In dieser Aufgabe haben Sie bestätigt, dass die Mitglieder des Mark 8-Projekts die Nachricht sehen können, die für die empfohlene Aktion zur Verbesserung des Sicherheitsstatus der Organisation veröffentlicht wurde, aber nur die Mitarbeitenden, die der benutzerdefinierten Rolle hinzugefügt wurden, können auf die Sicherheitsbewertungs-Informationen zugreifen.
