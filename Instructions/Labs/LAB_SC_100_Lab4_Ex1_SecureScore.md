# Lab 4 – Übung 1 – Sicherheitsstatusverwaltung

Contoso möchte seinen Sicherheitsstatus mithilfe der Microsoft-Sicherheitsbewertung verbessern, ein Tool, das Empfehlungen und Anleitungen zur Verringerung der Angriffsfläche und zum Schutz vor Bedrohungen bereitstellt. Contoso verfügt über ein dediziertes Sicherheitsteam, das das Dashboard für die Sicherheitsbewertung verwaltet und basierend auf ihren Rollen und Zuständigkeiten Aktionen verschiedenen Produktteams zuweist. Eines der Produktteams, das Mark 8-Projektteam, ist für die Verwaltung mobiler Geräte verantwortlich und muss sicherstellen, dass Geräte nach einer bestimmten Zeit der Inaktivität gesperrt werden, um unbefugten Zugriff zu verhindern.

## Teil 1: Entwerfen einer Lösung (erforderlich)

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage des beschriebenen Szenarios zu analysieren, die Ziele zu verstehen und die Anforderungen zu definieren.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Erhalten von weiteren Empfehlungen, um den Sicherheitsstatus zu erhöhen
- Gewähren des eingeschränkten Zugriffs auf Empfehlung 
- Informieren des verantwortlichen Teams

Die Microsoft-Sicherheitsbewertung bewertet den Sicherheitsstatus einer Organisation in allen Microsoft 365-Workloads. Es bietet zentrale Sichtbarkeit, bedrohungspriorisierte Einblicke und umfassende Kontrollen, um den Schutz vor Cyberangriffen zu verbessern und Cybersicherheit zu optimieren.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Hinzufügen weiterer Empfehlungen zur Erhöhung des Sicherheitsstatus | Zusätzliche Datenquellen | Aktivierenr zusätzlicher „Nicht-Workload“-Quellen |
|Gewähren des eingeschränkten Zugriffs auf Empfehlung |Defender XDR-Berechtigung und -Rollen |Gewähren des spezifischen Zugangs zu Joni Shermann |
|Informieren des verantwortlichen Teams |Sicherheitsbewertung |Informieren des Mark 8-Projektteams |

### Entwerfen von Kompromissen und alternativen Lösungen

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1 – Einrichten zusätzlicher Datenquelle in der Sicherheitsbewertung

In dieser Aufgabe aktivieren Sie zusätzliche Datenquellen für die Sicherheitsbewertung, um weitere Empfehlungen für Ihre Angriffsfläche zu erhalten.

1. Melden Sie sich an der Client 1 VM (LON-SC1) als **lon-sc1\admin** Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
2. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste aus, navigieren Sie zu <https://security.microsoft.com> und melden Sie sich im Microsoft 365 Admin Center  als **MOD-Admin**<admin@WWLxZZZZZZ.onmicrosoft.com> an (wobei ZZZZZZ Ihre eindeutige Mandant-ID ist, die Sie von Ihrem Lab-Hosting-Anbieter erhalten haben). Das Passwort der administrierenden Person sollte von Ihrem Lab-Hosting-Anbieter bereitgestellt werden.
3. Aktivieren Sie im Dialogfeld **Angemeldet bleiben?** das Kontrollkästchen **Dies nicht mehr anzeigen** und wählen Sie dann **Nein**.
4. Sie werden aufgefordert, die Multifaktor-Authentifizierung einzurichten, folgen Sie den Anweisungen.
5. Schließen Sie den Dialog zum Speichern von Passwörtern von unten, indem Sie **Nie** wählen, um die Standard-Anmeldeinformationen für globale Administrierende nicht in Ihrem Browser zu speichern.
6. Wählen Sie im linken Navigationsbereich **Einstellungen** aus.
7. Wählen Sie **Microsoft Defender XDR** aus.
8. Wählen Sie unter „Allgemein“ **Berechtigungen und Rollen** aus.
9. Möglicherweise müssen Sie einige Minuten warten, bis Microsoft Defender XDR eingerichtet wurde.
10. Aktivieren Sie **zusätzliche Datenquellen**.
11. Wechseln Sie zurück zum Dashboard für Sicherheitsbewertungen.

Sie haben erfolgreich zusätzliche Datenquellen aktiviert, um einen rollenbasierten Zugriff auf bestimmte Produktempfehlungen einzurichten.

### Aufgabe 2 – Einrichten des RBAC für die Sicherheitsbewertung

In dieser Aufgabe stellen Sie sicher, dass nur ausgewählte Personen auf diese Informationen zugreifen können. Sie aktivieren RBAC für die Sicherheitsbewertung und stützen sich dabei auf das Konzept des Zugriffs mit geringsten Privilegien.

1. Sie sollten weiterhin im Microsoft Defender XDR-Portal angemeldet sein.
2. Wählen Sie im linken Navigationsbereich **Einstellungen** aus.
3. Wählen Sie **Microsoft Defender XDR** aus.
4. Wählen Sie **Berechtigungen und Rollen** aus.
5. Wählen Sie die Registerkarte **Zu Berechtigungen und Rollen wechseln** aus.
6. Wählen Sie **Benutzerdefinierte Rolle erstellen**.
7. Rollenname: SecureScore-Apps
8. Wählen Sie **Weiter** aus.
9. Klicken Sie auf **Sicherheitsposition**, wählen Sie **Benutzerdefinierte Berechtigungen auswählen** und wählen Sie **Benutzerdefinierte Berechtigungen auswählen**.
10. Wählen Sie **Sicherheitsbewertung (verwalten)** aus.
11. Wählen Sie **Übernehmen**.
12. Wählen Sie **Weiter** aus.
13. Wählen Sie **Zuweisung hinzufügen** aus.
14. Zuordnungsname: SecureScore-Manager
15. Weisen Sie es **Joni Sherman** zu. 
16. Unter **Datenquellen** **deaktivieren Sie **alles außer **Microsoft-Sicherheitsbewertung – Zusätzliche Datenquellen**.
17. Wählen Sie **Hinzufügen** aus.
18. Wählen Sie **Weiter** aus.
19. Wählen Sie **Übermitteln** aus.

Sie haben RBAC erfolgreich für den Zugriff auf die zusätzlichen Datenquellenempfehlungen für Joni Sherman in der Sicherheitsbewertung implementiert.

### Aufgabe 3 – Delegieren einer Aktion

Das Mark 8-Projektteam von Contoso ist für die Weiterentwicklung der Verwaltung mobiler Geräte verantwortlich, daher informieren Sie das Projektteam über Ihre Sicherheitsempfehlung.

1. Sie sollten weiterhin im Microsoft Defender XDR-Portal angemeldet sein.
2. Wählen Sie im Navigationsbereich auf der linken Seite die Option **Sicherheitsbewertung** aus.
3. Wählen Sie auf der Registerkarte **Empfohlene Aktionen**.
4. Suchen Sie nach **Geräte nach einer gewissen Zeit der Inaktivität sperren, um unbefugten Zugriff zu verhindern** und wählen Sie es aus.
5. Wählen Sie **Freigeben**, und wählen Sie im Dropdownmenü **Microsoft Teams**.
6. Im Feld **Team** wählen Sie **Mark 8 Projektteam** und im Feld **Kanal** wählen Sie **Kanal Recherche und Entwicklung**.
7. Wählen Sie **Nachricht in Teams veröffentlichen**.

Joni Sherman und ihr Mark 8-Projektteam werden über die empfohlene Aktion in ihrem Teams-Kanal benachrichtigt.

### Aufgabe 4 – Empfehlungen verwalten

Als Joni Sherman haben Sie von Ihrem Team die Benachrichtigung erhalten, dass eine bestimmte Maßnahme zur Erhöhung Ihrer Sicherheitsstufe empfohlen wurde, und werden die empfohlene Maßnahme verwalten und die Lösung dokumentieren.

In dieser Aufgabe verwalten Sie empfohlene Aktionen und dokumentieren Ihre Lösungen.

1. Öffnen Sie ein Microsoft Edge-InPrivate-Fenster, navigieren Sie zu <https://office.com> und melden Sie sich als <JoniS@WWLxZZZZZZ.onmicrosoft.com> an.
2. Öffnen Sie Teams und öffnen Sie den Channel **Forschung und Entwicklung** im **Mark 8-Projektteam**.
3. Überprüfen Sie die Nachricht, die aus der Sicherheitsbewertungs-Aktion veröffentlicht wurde.
4. Öffnen Sie eine weitere Registerkarte im Microsoft Edge-inPrivate-Fenster und navigieren Sie zu <https://security.microsoft.com>.
5. Wählen Sie im Navigationsbereich auf der linken Seite die Option **Sicherheitsbewertung** aus.
6. Wählen Sie die Registerkarte **Empfohlene Aktionen** aus, um alle Aktionen anzuzeigen, auf die Sie Zugriff haben.
7. Suchen Sie nach **Geräte nach einer gewissen Zeit der Inaktivität sperren, um unbefugten Zugriff zu verhindern** und wählen Sie es aus.
8. Wählen Sie **Status und Aktionsplan bearbeiten** aus.
9. Prüfen Sie **Lösung durch Dritte**.
10. Fügen Sie dem Feld **Aktionsplan** die Notiz **Kurzfristig gesichert mit JAMF** hinzu.
11. Wählen Sie **Speichern und Schließen**.

Sie haben erfolgreich zusätzliche Workloads für die Sicherheitsbewertung eingerichtet, Berechtigungen auf der Grundlage des Zugriffs mit den geringsten Rechten zugewiesen und die empfohlenen Aktionen an das Identitätsteam von Contoso Ltd. verwaltet und delegiert.
