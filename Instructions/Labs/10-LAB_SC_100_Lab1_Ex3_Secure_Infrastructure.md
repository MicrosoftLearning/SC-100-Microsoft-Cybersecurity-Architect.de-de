# Sichere Infrastruktur

Contoso Ltd. hat kürzlich Tailwind Traders übernommen, das immer noch lokale Dateiserver für die Speicherung verwendet. Als Cybersicherheitsarchitektur entwerfende Person von Contoso Ltd. möchten Sie eine Lösung auswerten, um diese Dateiserver mit Ihrer vorhandenen Cloudumgebung zu schützen. Tailwind Traders haben Ihnen einen Testserver (The Lab VM 2) zur Verfügung gestellt, den Sie für die Implementierung Ihres Proof of Concept verwenden können. In dieser Übung richten Sie den Server ein und integrieren ihn mithilfe von Azure Arc in Ihre Cloudinfrastruktur und Sicherheitsumgebung und senden Serverprotokolle an Defender for Cloud.

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept zum Sichern der lokalen Umgebung in Ihrer Cloudinfrastruktur.

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage des beschriebenen Szenarios zu analysieren, die Ziele zu verstehen und die Anforderungen zu definieren.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Aktivieren von Defender for Cloud für Ihre Abonnements
- Lokale Server müssen gesichert werden
- Protokolle sollten gespeichert werden, sodass die SIEM-Lösung von Contoso sie verarbeiten kann
- Bewerten des Compliancestatus der Bereitstellungsressourcen

Im zweiten Schritt untersuchen Sie die vorhandene Umgebung von Contoso Ltd.. Defender for Cloud bietet Empfehlungen für die Absicherung von Cloud- undlokalen Ressourcen, indem Schritte zur Verbesserung der Konfiguration und Bereitstellung aufgezeigt werden. Durch die aktive Überwachung von Workloads wird der allgemeine Sicherheitsstatus verbessert und die Gefährdung durch Bedrohungen reduziert.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Aktivieren von Defender for Cloud für Ihre Abonnements| Defender für Cloud | Aktivieren von Defender-Plänen in Defender for Cloud |
|Lokale Server müssen gesichert werden | Azure Arc | Onboarding des lokalen Servers in die Cloudumgebung durchführen |
|Protokolle müssen gespeichert werden, sodass die SIEM-Lösung von Contoso sie verarbeiten kann |Defender for Cloud, DataCollectionRules, AzureMonitoring Agent, Log Analytics-Arbeitsbereich | Erstellen einer Datensammlungsregel zum Sammeln von Protokollen vom lokalen Server von Contoso |
|Bewerten des Compliancestatus der Bereitstellungsressourcen | Defender for Cloud Sicherheitsrichtlinien| Aktivieren der NIST SP 800-53 Rev. 5 Compliance und Bewerten des Konformitätszustands|

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1: Erstellen eines Log Analytics-Arbeitsbereichs

In dieser Aufgabe erstellen Sie einen Log Analytics-Arbeitsbereich, der erforderlich ist, um die Daten zu speichern, die aus verschiedenen Ressourcen gesendet werden.

1. Melden Sie sich an der Client 1 VM (LON-SC1) als **lon-sc1\admin** Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **`https://portal.azure.com`** und melden Sie sich beim Azure-Portal als benutzende Person **User1-*******@LODSUATMCA.onmicrosoft.com** an (wobei ****** Ihre eindeutige, von Ihrem Lab-Hosting-Anbieter bereitgestellte Mandant-ID ist). Das Kennwort des Benutzernden sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Aktivieren Sie im Dialogfeld Angemeldet bleiben? das Kontrollkästchen Dies nicht mehr anzeigen und wählen Sie dann **Nein**.
1. Schließen Sie das Dialogfeld zum Speichern des Kennworts von unten, indem Sie Nie wählen, um die Anmeldeinformationen des globalen Admins nicht in Ihrem Browser zu speichern.
1. Bildschirm Willkommen bei Microsoft Azure abbrechen
1. Wählen Sie **Eine Ressource erstellen** und suchen Sie nach **Log Analytics-Arbeitsbereich**
1. Suchen Sie die **Kachel Log Analytics-Arbeitsbereich** und wählen Sie **Erstellen**.
1. Erstellen Sie auf der Site Log Analytics-Arbeitsbereich erstellen eine neue **Ressourcengruppe** und nennen Sie sie **`ContosoRG`**.
1. In den Details der Instanz geben Sie den Namen **`ContosoLA`** ein und wählen als Region **USA, Osten**.
1. Wählen Sie **Überprüfen & Erstellen**
1. Wählen Sie **Erstellen** aus, um die Bereitstellung zu starten.

Sie haben den Log Analytics-Arbeitsbereich erfolgreich erstellt.

### Aufgabe 2: Aktivieren von Microsoft Defender for Cloud

Bevor Defender for Cloud Schutzmaßnahmen auf Ihre Ressourcen anwenden kann, müssen Sie die Defender-Pläne für die Ressourcentypen aktivieren, die Sie schützen möchten.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
1. Suchen Sie nach **Microsoft Defender for Cloud** und öffnen Sie es.
1. Erweitern Sie im linken Navigationsbereich **Verwaltung** und wählen Sie **Umgebungseinstellungen** aus.
1. Wählen Sie **Alles erweitern** und wählen Sie Ihr Abonnement aus.
1. Wenn das Abonnement als **nicht registriert** angezeigt wird, laden Sie die Seite neu.
1. Wählen Sie die Auslassungspunkte (...) neben dem Abonnement aus und wählen Sie **Einstellungen bearbeiten**.
1. Stellen Sie unter **Cloud Workloadschutz** den Schieberegler **Server** auf der rechten Seite auf **Ein**.
1. Wählen Sie im oberen Bereich der Seite **Speichern** aus.

Wenn Sie den Plan für Server aktivieren, können Sie sehen, dass Defender for Cloud viele weitere Ressourcentypen unterstützt.

### Aufgabe 3: Aktivieren des lokalen Servers in Azure Arc

Azure Arc ist erforderlich, damit Daten an den Log Analytics-Arbeitsbereich gesendet werden können, den Defender for Cloud verwendet.

1. Wechseln Sie zur VM **LON-SC2** und melden Sie sich im Azure-Portal **`https://portal.azure.com`** an.
1. Suchen Sie nach **`Azure Arc`** und öffnen Sie es.
1. Erweitern Sie im linken Navigationsbereich **Azure Arc Ressourcen** und wählen Sie **Computer**.
1. Wählen Sie **Hinzufügen/Erstellen** > **Computer hinzufügen**.
1. Wählen Sie unter Einen einzelnen Server hinzufügen die Option **Skript generieren**.
1. Wählen Sie im Feld „Ressourcengruppe“ über das Dropdown-Menü **ContosoRG** aus.
1. Wählen Sie im Feld „Region“ über das Dropdown-Menü **USA, Osten** aus.
1. Wählen Sie **Skript herunterladen und ausführen** aus.
1. Wählen Sie **Herunterladen** und führen Sie das Skript auf Ihrem zweiten „Lab Client“ **LON-SC2** aus, um den lokalen Server in Azure einzubinden.
1. Führen Sie die Windows PowerShell als Administrator aus. Verwenden Sie dazu die rechte Maustaste, um das Windows-Symbol in der unteren rechten Ecke des Fensters auszuwählen, und wählen Sie **Windows PowerShell (Administrator)** aus.
1. Setzen Sie die Ausführungsrichtlinie auf uneingeschränkt.

    ```Powershell
    Set-ExecutionPolicy -ExecutionPolicy unrestricted
    ```

1. Wählen Sie in den PowerShell-Fenstern „Y“ aus.
1. Führen Sie das Onboarding-Skript aus. Wählen Sie dazu den Datei-Explorer aus. Sie sollten zum Downloadordner auf dem lokalen C-Laufwerk der Server-VM gelangen. Wählen Sie mit der rechten Maustaste die Datei **OnboardingScript** aus und wählen Sie „**Ausführen mit **PowerShell**“.
1. Wenn das Authentifizierungs-Popup erscheint, melden Sie sich mit demselben Konto an, das Sie für das Azure-Portal verwenden.
1. Warten Sie, bis das Skript erfolgreich abgeschlossen ist.
1. Kehren Sie zurück zu LON-SC1 und öffnen Sie Azure Arc.
1. Wählen Sie **Computer**, wählen Sie **Aktualisieren** oben auf der Seite und überprüfen Sie, ob Ihr Server erfolgreich in Azure Arc bereitgestellt wurde.

Sie haben Azure Arc erfolgreich auf dem Testserver aktiviert, und die Daten sollten nun in den Log Analytics-Arbeitsbereich fließen. Dieser Vorgang kann einige Zeit in Anspruch nehmen, bis Sie im Dashboard etwas sehen können.

### Aufgabe 4: Hinzufügen des Servers zu Defender für Cloud und Sammeln von Protokollen.

Sie stellen eine Datensammlungsregel bereit, um Ereignisprotokolle vom lokalen Server abzurufen. Die Regel wird den Überwachungsagent automatisch auf dem Server bereitstellen und Protokolle an den zuvor erstellten Log Analytics-Arbeitsbereich weiterleiten.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
1. Öffnen Sie Defender for Cloud.
1. Erweitern Sie im linken Navigationsbereich **Verwaltung** und wählen Sie **Umgebungseinstellungen** aus.
1. Wählen Sie **Alle erweitern** aus.
1. Der zuvor erstellte Log Analytics-Arbeitsbereich **ContosoLA** wird angezeigt.  
1. Wählen Sie die Ellipsen (...) für die **ContosoLA**-Zeile aus und wählen Sie dann **Einstellungen bearbeiten** aus.
1. Legen Sie den Plan für **Server** fest, indem Sie den Schieberegler rechts auf **Ein** stellen.
1. Wählen Sie im oberen Bereich der Seite **Speichern** aus.
1. Verwenden Sie die Suchleiste oben, um nach **Regeln für die Datenerfassung** zu suchen, und wählen Sie sie dann aus den Suchergebnissen aus.
1. Klicken Sie auf **Erstellen**.
1. - Regelname: **`ContosoDCR`**
   - Ressourcengruppe: **ContosoRG**
1. Wählen Sie **Weiter: Ressourcen** aus.
1. Wählen Sie **Ressourcen hinzufügen** aus. Erweitern Sie den Bereich der Ressourcengruppe. Überprüfen Sie den zuvor integrierten Azure Arc-Computer und wählen Sie **Anwenden**.
1. Wählen Sie **Weiter: Sammeln und übermitteln** aus.
1. Wählen Sie die Option **Datenquelle hinzufügen**.
1. Wählen Sie den Datenquellentyp **Windows-Ereignisprotokolle** aus.
1. Wählen Sie alle Optionen unter **Ereignisprotokolle und zu erfassende Ebenen konfigurieren:** aus.
1. Wählen Sie **Weiter: Ziel** aus.
1. Klicken Sie auf **Ziel hinzufügen**.
   - Zieltyp: **Azure Monitor-Protokolle**
   - Konto oder Namespace: **ContosoLA**
1. Wählen Sie die Option **Datenquelle hinzufügen**.
1. Klicken Sie auf **Überprüfen + erstellen**.
1. Klicken Sie auf **Erstellen**.

Es kann einige Stunden dauern, bis die Ressource vollständig in Defender for Cloud integriert ist. Der nächste Schritt besteht darin, sich die Empfehlung anzusehen, die Defender for Cloud für diese Ressource generiert.

### Aufgabe 5: Hinzufügen eines Standards zur Einhaltung von Vorschriften

Auf der Grundlage der Empfehlung können Sie damit beginnen, die Ressource zu sichern und Sicherheitsrichtlinien zuzuweisen, z. B. NIST SP 800-53 Rev. 5, um sicherzustellen, dass die Ressourcen der Tailwind Traders unseren Compliance-Vorschriften entsprechen.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
1. Öffnen Sie Defender for Cloud, erweitern Sie **Verwaltung** und wählen Sie **Umgebungseinstellungen** aus.
1. Wählen Sie **Alle erweitern** aus.
1. Wählen Sie die Auslassungspunkte (...) neben dem Abonnement aus und wählen Sie **Einstellungen bearbeiten**.
1. Wählen Sie **Sicherheitsrichtlinien** im Navigationsmenü auf der linken Seite. Es kann eine Weile dauern, bis die Liste geladen ist.
1. Suchen Sie nach **`NIST SP 800-53 Rev. 5`**. Schieben Sie den Schieberegler Status auf **Ein**.
1. Gehen Sie zurück zu Defender for Cloud, erweitern Sie **Cloud-Sicherheit** und wählen Sie dann **Einhaltung gesetzlicher Vorschriften** aus.

Aufgrund der Einschränkung der Lab-Umgebung können Sie die Ressourcen sowie die Compliance-Empfehlungen nicht sehen. Es dauert eine Weile, bis die bereitgestellten Ressourcen in Defender for Cloud sichtbar sind.

Im Dashboard zur Einhaltung gesetzlicher Vorschriften können Sie jetzt alle fehlerhaften Bewertungen überprüfen, die im Dashboard angezeigt werden, um die Details der Empfehlungen zu verstehen.

Durch die kontinuierliche Bewertung von Ressourcen anhand dieser Steuerelemente identifiziert Defender for Cloud Probleme, die das Erreichen bestimmter Compliance-Zertifizierungen behindern können. Die Einhaltung gesetzlicher Vorschriften ist entscheidend, um die Daten Ihrer Organisation zu schützen und eine sichere Cloudumgebung zu gewährleisten.
