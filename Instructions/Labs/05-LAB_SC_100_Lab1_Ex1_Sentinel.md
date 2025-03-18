# Security Operations Center

## Überblick über die Übung

Contoso verfügt über ein Security Operations Center (SOC), das Sicherheitsvorfälle im gesamten Unternehmen überwacht und auf sie reagiert. Das SOC ist mit Sicherheitsanalytikern bzw. -analytikerinnen, technischen Fachkräften für Sicherheit und Netzwerktechnikern bzw. -technikerinnen besetzt. Die SOC hat sich entschieden, Microsoft Sentinel als ihre SIEM-Lösung (Security Information and Event Management) zu verwenden. Um Sicherheitsprotokolle aus dem gesamten Unternehmen zu sammeln und zu analysieren, verfügt das SOC über einen Log Analytics-Arbeitsbereich. Das SOC hat eine Anforderung, den Zugriff auf den Log Analytics-Arbeitsbereich basierend auf dem Prinzip der geringsten Rechte zu sichern. Der SOC hat zwei verschiedene Rollen: Sicherheitsanalyst bzw. Sicherheitsanalystin und technische Fachkraft für Sicherheit, mit unterschiedlichen Berechtigungsanforderungen. Das Netzwerkteam hat eine Anforderung, nur auf die Cisco Umbrella-Protokolle zuzugreifen.

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept für die Überwachung und Reaktion auf Sicherheitsereignisse mit bestimmten Zugriffsberechtigungen für das Security Operations Center von Contoso.

### Entwurfsansatz

Der erste Schritt umfasst die Analyse der Anforderungen basierend auf dem beschriebenen Szenario, das Verständnis der Ziele und das Definieren der Anforderungen.

Auf der Grundlage des angegebenen Anwendungsfalls können die folgenden Anforderungen umrissen werden:

- Bereitstellen der SIEM/SOAR-Lösung
- Beschränken des Zugriffs auf bestimmte SOC-Rollen
- Erstellen eines Dashboards mit benutzerdefinierten Ansichten für Vorfälle und deren Warnungen

In diesem Szenario stellen Sie die SIEM SOAR-Lösung basierend auf Microsoft Sentinel bereit, richten die rollenbasierte Zugriffssteuerung im Arbeitsbereichkontext ein und beschränken den Zugriff für das Netzwerkteam auf eine einzelne Tabelle im Log Analytics-Arbeitsbereich. Arbeitsmappen ermöglichen es Sicherheitsanalysten bzw- analystinnen und Administrierenden, Sicherheitsdaten mithilfe grafischer Darstellungen zu visualisieren. Sie bieten ein Tool zum Präsentieren und Analysieren von Daten in einem Dashboard.

### Vorgeschlagene Lösung

| Anforderung | Lösung | Maßnahmenplan |
| ---- | ---- | ---- |
| Bereitstellen der SIEM/SOAR-Lösung | Microsoft Sentinel, Log Analytics-Arbeitsbereich | Einrichten Log Analytics-Arbeitsbereichs und Bereitstellen von Microsoft Sentinel |
| Beschränken des Zugriffs auf bestimmte SOC-Rollen | Log Analytics-Arbeitsbereich, rollenbasierte Zugriffssteuerung | Einrichten von RBAC für den Log Analytics-Arbeitsbereich |
| Erstellen eines Dashboards mit benutzerdefinierten Ansichten für Vorfälle und deren Warnungen | Microsoft Sentinel, Arbeitsmappe | Erstellen einer Arbeitsmappe mit einer benutzerdefinierten Ansicht zu aktuellen Vorfällen und Warnungen |

## Teil 2: Implementieren der Lösung (optional)

> [!NOTE]
> Für diesen Teil des Labs ist die Aufgabe, ein Dashboard mit benutzerdefinierten Ansichten für Vorfälle und deren Warnmeldungen zu erstellen (Aufgabe 4 dieser Übung), nicht funktionsfähig, da keine Daten vorhanden sind, auf denen diese Aufgabe basieren könnte. Die Schritte von Vorgang 4 sind nur zu Informationszwecken enthalten. Wenn Sie die Schritte ausführen, werden keine Daten zurückgegeben.

### Aufgabe 1: Erstellen eines Log Analytics-Arbeitsbereichs

In dieser Aufgabe erstellen Sie einen Log Analytics-Arbeitsbereich, in dem alle Daten gespeichert werden, die Microsoft Sentinel aufnimmt und für seine Erkennungen und Analysen verwendet.

1. Melden Sie sich an der Client 1 VM (LON-SC1) als **lon-sc1\admin** Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
2. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **`https://portal.azure.com`** und melden Sie sich im Azure-Portal als benutzende Person **Benutzer1-*******@LODSUATMCA.onmicrosoft.com** an (wobei ****** Ihre eindeutige Mandanten-ID ist, die Sie von Ihrem Lab-Hosting-Anbieter erhalten haben). Das Kennwort des Benutzernden sollte von Ihrem Provider für die Übung bereitgestellt werden.
3. Aktivieren Sie im Dialogfeld Angemeldet bleiben? das Kontrollkästchen Dies nicht mehr anzeigen und wählen Sie dann **Nein**.
4. Schließen Sie das Dialogfeld zum Speichern des Kennworts von unten, indem Sie Nie wählen, um die Anmeldeinformationen des globalen Admins nicht in Ihrem Browser zu speichern.
5. Bildschirm Willkommen bei Microsoft Azure abbrechen
6. Wählen Sie **Eine Ressource erstellen** und suchen Sie nach **Log Analytics-Arbeitsbereich**
7. Suchen Sie die **Kachel Log Analytics-Arbeitsbereich** und wählen Sie **Erstellen**.
8. Erstellen Sie auf der Site Log Analytics-Arbeitsbereich erstellen eine neue **Ressourcengruppe** und nennen Sie sie **`rg_eastus_soc`**.
9. In den Details der Instanz geben Sie den Namen **`law-sentinel`** ein und wählen als Region **USA, Osten**.
10. Wählen Sie **Überprüfen & Erstellen**
11. Wählen Sie **Erstellen** aus, um die Bereitstellung zu starten.

Sie haben den Log Analytics-Arbeitsbereich für Ihre Sentinel-Bereitstellung erfolgreich erstellt.

### Aufgabe 2 – Erstellen von Sentinel

In dieser Aufgabe fügen Sie Sentinel zu dem erstellten Log Analytics-Arbeitsbereich hinzu und fügen Demo-Protokolle hinzu. Da der Demo-Mandant keine vorhandenen Daten im Log Analytics-Arbeitsbereich hat, importieren Sie Demo-Protokolle, um eine bessere Vorstellung von der Funktionsweise von Sentinel zu bekommen.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
1. Geben Sie in der Suchleiste im blauen Banner oben auf der Seite **Microsoft Sentinel** ein und wählen Sie es dann aus den unter Dienste aufgelisteten Suchergebnissen aus.
1. Auf der Seite **Microsoft Sentinel** wählen Sie **Erstellen**.
1. Auf der Seite **Microsoft Sentinel zu einem Arbeitsbereich hinzufügen** sollte der zuvor erstellte Log Analytics-Arbeitsbereich aufgeführt sein.  Wählen Sie **law-sentinel** und wählen Sie dann **Hinzufügen**.
1. Es kann einige Minuten dauern, um Sentinel zum Arbeitsbereich hinzuzufügen.  Sobald es hinzugefügt wurde, wird die Seite **Microsoft Sentinel | Neuigkeiten und Leitfäden** angezeigt.  Sie werden benachrichtigt, dass die kostenlose Testversion von Microsoft Sentinel aktiviert ist.  Klicken Sie auf **OK**.
1. Wählen Sie in der Mitte der Seite **Zum Inhaltshub wechseln**.  Der Inhaltshub ist der Ort, an dem Sie Lösungen herunterladen würden. Erkunden Sie den Inhaltshub nach Belieben.

Sie haben Sentinel erfolgreich im Log Analytics-Arbeitsbereich bereitgestellt. 

### Aufgabe 3 – Einrichten des RBAC

Sie müssen den Zugriff auf der Grundlage des Prinzips der geringsten Privilegien sichern und Rollenzuweisungen für die spezifischen Rollenanforderungen erstellen. In Ihrer bevorstehenden produktiven Bereitstellung gibt es zwei verschiedene Rollen im Security Operation Center.
Außerdem benötigt das Netzwerkteam Zugriff auf die Cisco-Umbrella-Protokolle. Sie müssen sicherstellen, dass das Netzwerkteam nur auf diese Protokolle zugreifen kann.

#### Erforderliche Berechtigungen

| Rolle | Berechtigungen |
|---|---|
| Sicherheitsanalyst | Anzeigen von Daten, Vorfällen, Arbeitsbüchern und andere Sentinel-Ressourcen |
| | Zuweisen/Schließen von Vorfällen |
| Security Engineer | Erstellen und Bearbeiten von Arbeitsmappen und Analyseregeln |
| | Installieren und Aktualisieren von Lösungen aus dem Inhaltshub |
| Netzwerkteam | Leseberechtigungen für Gruppe: **NOC** in Tabelle: **Cisco_Umbrella_dns_CL**|

---

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
1. Suchen Sie in der oberen Suchleiste nach **Ressourcengruppen** und wählen Sie Ihre zuvor erstellte Ressourcengruppe **rg_eastus_soc** aus.
1. Wählen Sie im linken Navigationsbereich **Zugriffssteuerung (IAM)** aus.
1. Wählen Sie **Hinzufügen** aus und wählen Sie dann in der Dropdown-Liste **Rollenzuweisung hinzufügen** aus.
1. Suchen Sie nach **`Microsoft Sentinel Responder`** und wählen Sie **Anzeigen** in der Spalte „Details“.
1. Prüfen Sie, ob die Berechtigungen den Anforderungen entsprechen.
1. Schließen Sie das Fenster mit **X** in der oberen rechten Ecke.
1. Wählen Sie **Weiter** aus.
1. Wählen Sie **+Mitglieder auswählen**.
1. Suchen Sie nach der **`SOC Analysts`**-Gruppe, wählen Sie **SOC-Analysten** aus den Suchergebnissen, drücken Sie **Auswählen** und fügen Sie die Rollenzuweisung hinzu.
1. Wählen Sie **Überprüfen und zuweisen** aus.
1. Sie wiederholen die Schritte für die Sentinel Contributor-Teilnehmerrolle. Wählen Sie **Hinzufügen** aus und wählen Sie dann in der Dropdown-Liste **Rollenzuweisung hinzufügen** aus.
1. Suchen Sie nach **`Microsoft Sentinel Contributor`** und wählen Sie die Rolle.
1. Wählen Sie **Weiter** aus.
1. Wählen Sie **+Mitglieder auswählen**.
1. Suchen Sie auf dem Blatt **Mitglieder auswählen** nach der Gruppe **SOC-Techniker**.  Wählen Sie aus den Suchergebnissen **SOC-Techniker** und drücken Sie **Auswählen**, um die Rollenzuweisung hinzuzufügen.
1. Wählen Sie erneut **Überprüfen und zuweisen** aus.
1. Wählen Sie die Registerkarte **Rollenzuweisungen**. Bestätigen Sie, dass die Rollenzuweisungen festgelegt sind.
1. Jetzt fügen Sie eine benutzerdefinierte Rolle hinzu. Wählen Sie **Hinzufügen** aus und wählen Sie dann aus der Dropdown-Liste **Benutzerdefinierte Rolle hinzufügen** aus.
1. Nennen Sie es **`NOC-CiscoUmbrellaCL-Read`**.
1. Wählen Sie für die **Grundberechtigung** die Option **Von vorne beginnen**.
1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Registerkarte **Berechtigungen** die Option **Berechtigung hinzufügen** aus.
1. Suchen Sie nach **`Microsoft.OperationalInsights`**, wählen Sie die Karte **Azure Protokollanalyse** aus.
1. Fügen Sie die folgenden Berechtigungen hinzu.
    - Microsoft.OperationalInsights/workspaces
        - Read : Get Workspace
        - Other : Search Workspace Data

    - Microsoft.OperationalInsights/workspaces/analytics
        - Other : Search

    - Microsoft.OperationalInsights/workspaces/query
        - Read : Query Data in Workspace

    - Microsoft.OperationalInsights/workspaces/tables/query
        - Read : Query workspace table data

1. Klicken Sie auf **Überprüfen + erstellen**.
1. Wählen Sie **Erstellen**, und wählen Sie dann **Ok**.
1. Suchen Sie in der oberen Suchleiste nach **`Resource groups`** und wählen Sie **rg_eastus_soc**.
1. Öffnen Sie den Log Analytics-Arbeitsbereich **law-sentinel**.
1. Erweitern Sie im linken Navigationsbereich **Einstellungen** und wählen Sie **Tabellen**.
1. Suchen Sie nach **`Cisco_Umbrella_dns_CL`**.
1. Klicken Sie auf die Ellipsen (...), wählen Sie **Zugriffssteuerung (IAM)**.
1. Wählen Sie **Hinzufügen** > **Rollenzuweisung hinzufügen**.
1. Suchen Sie nach **`NOC-CiscoUmbrellaCL-Read`** und wählen Sie die benutzerdefinierte Rolle.
1. Wählen Sie **Weiter** aus.
1. Wählen Sie **Mitglieder auswählen**, suchen Sie nach **NOC**, wählen Sie es aus den Suchergebnissen aus und drücken Sie dann **Wählen**.
1. Wählen Sie erneut **Überprüfen und zuweisen** aus.

Sie haben erfolgreich ein rollenbasiertes Zugriffsmodell für die Rollenanforderungen für das Sicherheitsbetriebsteam von Contoso erstellt und eine benutzerdefinierte Rolle für das Netzwerkteam erstellt und die Rolle der spezifischen Tabelle in Ihrem Log Analytics-Arbeitsbereich zugewiesen.

### Aufgabe 4: Erstellen einer Arbeitsmappe

> [!NOTE]
> Diese Schritte sind nur zu Informationszwecken enthalten. Wenn Sie die Schritte ausführen, werden keine Daten zurückgegeben.

In dieser Aufgabe erstellen Sie eine Arbeitsmappe, um ein Dashboard mit benutzerdefinierten Ansichten und aktuellen Vorfällen und deren Warnungen zu erhalten.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
1. Suchen Sie in der Suchleiste oben nach **`Microsoft Sentinel`** und öffnen Sie es.
1. Wählen Sie **law-sentinel**.
1. Erweitern Sie im linken Navigationsbereich den Eintrag **Bedrohungsmanagement** und wählen Sie **Arbeitsmappen** aus.
1. Wählen Sie **Arbeitsmappe hinzufügen** aus.
1. Wählen Sie **Bearbeiten** aus.
1. Wählen Sie die erste Schaltfläche **Bearbeiten** auf der rechten Seite aus.
1. Wählen Sie **Hinzufügen** > **Parameter hinzufügen** aus.
1. Wählen Sie **Parameter hinzufügen** und geben Sie die folgenden Informationen ein:
     - **Parametername:** TimeRange
     - **Parametertyp:** Zeitbereichsauswahl
1. Überprüfen Sie die folgenden Einstellungen:
     - **Erforderlich?**
1. Wählen Sie **Speichern**.
1. Wählen Sie im Dropdown-Menü **TimeRange:** unten links **Letzte 7 Tage** aus.
1. Wählen Sie **Parameter hinzufügen** und geben Sie die folgenden Informationen ein:
     - **Parametername:** AlertSeverity
     - **Parametertyp:** Dropdown
1. Überprüfen Sie die folgenden Einstellungen:
     - **Erforderlich?**
     - **Mehrfachauswahl zulassen**
     - **Parameter im Lesemodus ausblenden**
1. Unter **Log Analytics-Arbeitsbereich-Protokollabfrage** fügen Sie Folgendes ein:

    ```KQL
    SecurityAlert
    | summarize Count = count() by AlertSeverity
    | order by Count desc, AlertSeverity
    | project Value = AlertSeverity, Label = strcat(AlertSeverity, ' - ', Count)
    ```

1. Wählen Sie im Dropdown-Menü **Zeitbereich** den Eintrag **TimeRange** aus.
1. Scrollen Sie nach unten zu **In Dropdown aufnehmen**, markieren Sie **Alle** und legen Sie **Standardmäßig ausgewähltes Element** auf **Alle** fest.
1. Wählen Sie **Speichern**.
1. Wählen Sie **Parameter hinzufügen** und geben Sie die folgenden Informationen ein:
     - **Parametername:** ProductName
     - **Parametertyp:** Dropdown
1. Überprüfen Sie die folgenden Einstellungen:
     - **Erforderlich?**
     - **Mehrfachauswahl zulassen**
     - **Parameter im Lesemodus ausblenden**

1. Unter **Log Analytics-Arbeitsbereich-Protokollabfrage** fügen Sie Folgendes ein:

    ```KQL
    SecurityAlert
    | summarize Count = count() by ProductName
    | order by Count desc, ProductName asc
    | project Value = ProductName, Label = strcat(ProductName, ' - ', Count)
    ```

1. Wählen Sie im Dropdown-Menü **Zeitbereich** die Option **TimeRange**.
1. Scrollen Sie nach unten zu **In Dropdown aufnehmen**, markieren Sie **Alle** und legen Sie **Standardmäßig ausgewähltes Element** auf **Alle** fest.
1. Wählen Sie **Speichern**.
1. Wählen Sie **Hinzufügen** und wählen Sie **Abfrage hinzufügen**.
1. Unter **Log Analytics-Arbeitsbereich-Protokollabfrage** fügen Sie Folgendes ein:

    ```KQL
    SecurityIncident
    | where CreatedTime {TimeRange:value}
    | summarize arg_max(TimeGenerated,*) by tostring(IncidentNumber)
    | extend IncidentID = IncidentName
    | extend Alerts = extract("\\[(.*?)\\]", 1, tostring(AlertIds))
    | mv-expand AlertIds to typeof(string)
    | join
    (
        SecurityAlert
        | extend AlertEntities = parse_json(Entities)
        | mv-expand AlertEntities
    ) on $left.AlertIds == $right.SystemAlertId
    | summarize AlertCount=dcount(AlertIds) by IncidentNumber, Status, Severity, Title, Alerts, IncidentUrl, IncidentID
    | project IncidentNumber, IncidentID, Title, Severity, Status, AlertCount, Alerts, IncidentUrl
    | order by Severity
    ```

1. Wählen Sie **TimeRange** im Dropdown-Menü „Zeitbereich“.
Sie richten dynamische Inhalte ein, um alle Warnungen für den ausgewählten Vorfall abzurufen. Warnungen werden exportiert und außerhalb dieser Abfrage verfügbar.
1. Wählen Sie die Registerkarte **Erweiterte Einstellungen** am oberen Rand des Fensters **Abfrage bearbeiten**.
1. Überprüfen Sie die folgenden Einstellungen:
    - **Parameter exportieren, wenn Elemente ausgewählt wurden** 
1. Wählen Sie **Parameter hinzufügen** aus, und geben Sie die folgenden Informationen ein:
    - **Zu exportierende Felder:** Warnungen
    - **Parametername:** Warnungen
1. Wählen Sie **Speichern**.
1. Gehen Sie zurück auf die Registerkarte **Einstellungen**.
1. Wählen Sie **Run Query** (Abfrage ausführen) aus.
1. Wählen Sie **Spalteneinstellungen** aus.
1. Wählen Sie **IncidentUrl** aus.
1. Legen Sie den Spaltenrenderer auf **Link** fest.
1. Legen Sie unter Link-Einstellungen **Zu öffnende Ansicht** auf **URL** fest.
1. Wählen Sie **Speichern und Schließen**.
1. Als Nächstes erstellen Sie die Warnungsansicht basierend auf dem ausgewählten Vorfall.
1. Wählen Sie **+ Hinzufügen** am unteren Rand des Fensters **Abfrageelement bearbeiten**. Wählen Sie **Abfrage hinzufügen** aus.
1. Einfügen der KQL in die Log Analytics-Arbeitsbereichs-Protokollabfrage

    ```KQL
    SecurityAlert
    | where SystemAlertId in ({Alerts})
    | summarize by  DisplayName, StartTime, EndTime,  SystemAlertId
    | sort by EndTime desc
    ```

1. Wählen Sie **TimeRange** im Dropdown-Menü „Zeitbereich“.
1. Wählen Sie **Bearbeitung abgeschlossen** aus.
1. Wählen Sie **Bearbeitung abgeschlossen** in der oberen Leiste des Fensters **Neue Arbeitsmappe** aus.
1. Wählen Sie einen **Vorfall**.
1. Warnungen an den verknüpften Vorfall werden unten angezeigt.
1. Speichern Sie Ihre Anfrage, indem Sie auf das Symbol „Speichern“ klicken.  
1. Geben Sie im Fenster **Speichern unter** einen Titel für Ihre neue Arbeitsmappe ein, wählen Sie die Ressourcengruppe **rg_eastus_soc** aus dem Dropdown-Menü aus und klicken Sie dann auf **Speichern unter**.

Sie haben erfolgreich ein Dashboard mit benutzerdefinierten Ansichten für Vorfälle und die zugehörigen Warnungen erstellt.
