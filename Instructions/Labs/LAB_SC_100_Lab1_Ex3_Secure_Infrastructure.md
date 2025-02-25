# Lab 1 – Übung 3 – Sichere Infrastruktur

Contoso Ltd. hat kürzlich Tailwind Traders übernommen, das immer noch lokale Dateiserver für die Speicherung verwendet. Als Cybersicherheitsarchitektur entwerfende Person von Contoso Ltd. möchten Sie eine Lösung auswerten, um diese Dateiserver mit Ihrer vorhandenen Cloudumgebung zu schützen. Tailwind Traders haben Ihnen einen Testserver (The Lab VM 2) zur Verfügung gestellt, den Sie für die Implementierung Ihres Proof of Concept verwenden können. In dieser Übung richten Sie den Server ein und integrieren ihn mithilfe von Azure Arc in Ihre Cloudinfrastruktur und Sicherheitsumgebung und senden Serverprotokolle an Defender for Cloud.

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept zum Sichern der lokalen Umgebung in Ihrer Cloudinfrastruktur.

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage des beschriebenen Szenarios zu analysieren, die Ziele zu verstehen und die Anforderungen zu definieren.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Aktivieren von Defender for Cloud für Ihre Abonnements
- Lokale Server müssen gesichert werden
- Protokolle sollten gespeichert werden, sodass die SIEM-Lösung von Contoso sie verarbeiten kann
- Bewerten des Konformitätszustands der eingesetzten Ressourcen

Im zweiten Schritt untersuchen Sie die vorhandene Umgebung von Contoso Ltd.. Defender for Cloud bietet Empfehlungen für die Absicherung von Cloud- undlokalen Ressourcen, indem Schritte zur Verbesserung der Konfiguration und Bereitstellung aufgezeigt werden. Durch die aktive Überwachung von Workloads wird der allgemeine Sicherheitsstatus verbessert und die Gefährdung durch Bedrohungen reduziert.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Aktivieren von Defender for Cloud für Ihre Abonnements| Defender für Cloud | Aktivieren von Defender-Plänen in Defender for Cloud |
|Lokale Server müssen gesichert werden | Azure Arc | Onboarding des lokalen Servers in die Cloudumgebung durchführen |
|Protokolle müssen gespeichert werden, sodass die SIEM-Lösung von Contoso sie verarbeiten kann |Defender for Cloud, DataCollectionRules, AzureMonitoring Agent, Log Analytics-Arbeitsbereich | Erstellen einer Datensammlungsregel zum Sammeln von Protokollen vom lokalen Server von Contoso |
|Bewerten des Konformitätszustands der eingesetzten Ressourcen | Defender for Cloud Sicherheitsrichtlinien| Aktivieren der NIST SP 800-53 Rev.5 Compliance und Bewerten des Konformitätszustands|

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1: Erstellen eines Log Analytics-Arbeitsbereichs

In dieser Aufgabe erstellen Sie einen Log Analytics-Arbeitsbereich, der erforderlich ist, um die Daten zu speichern, die aus verschiedenen Ressourcen gesendet werden.

1. Melden Sie sich an der Client 1 VM (LON-SC1) als **lon-sc1\admin** Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
2. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **https://portal.azure.com** und melden Sie sich im Azure-Portal als benutzende Person **Benutzer1-*******@LODSUATMCA.onmicrosoft.com** an (wobei ****** Ihre eindeutige Mandanten-ID ist, die Sie von Ihrem Lab-Hosting-Anbieter erhalten haben). Das Kennwort des Benutzernden sollte von Ihrem Provider für die Übung bereitgestellt werden.
3. Aktivieren Sie im Dialogfeld Angemeldet bleiben? das Kontrollkästchen Dies nicht mehr anzeigen und wählen Sie dann **Nein**.
4. Schließen Sie das Dialogfeld zum Speichern des Kennworts von unten, indem Sie Nie wählen, um die Anmeldeinformationen des globalen Admins nicht in Ihrem Browser zu speichern.
5. Bildschirm Willkommen bei Microsoft Azure abbrechen
6. Wählen Sie **Eine Ressource erstellen** und suchen Sie nach **Log Analytics-Arbeitsbereich**
7. Suchen Sie die **Kachel Log Analytics-Arbeitsbereich** und wählen Sie **Erstellen**.
8. Erstellen Sie auf der Site Log Analytics-Arbeitsbereich erstellen eine neue **Ressourcengruppe** und nennen Sie sie **ContosoRG**.
9. In den Instanzdetails geben Sie den Namen **ContosoLA** ein und wählen **USA, Osten** als Region.
10. Wählen Sie **Überprüfen & Erstellen**
11. Wählen Sie **Erstellen** aus, um die Bereitstellung zu starten.

Sie haben den Log Analytics-Arbeitsbereich erfolgreich erstellt.

### Aufgabe 2: Aktivieren von Microsoft Defender for Cloud

Bevor Defender for Cloud Schutzmaßnahmen auf Ihre Ressourcen anwenden kann, müssen Sie die Defender-Pläne für die Ressourcentypen aktivieren, die Sie schützen möchten.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
2. Suchen Sie nach **Microsoft Defender for Cloud** und öffnen Sie es.
3. Erweitern Sie im linken Navigationsbereich **Mangement** und wählen Sie **Umgebungseinstellungen**.
4. Klicken Sie auf **Alle erweitern** und wählen Sie Ihr Abonnement aus.
5. Wenn das Abonnement als **nicht registriert** angezeigt wird, laden Sie die Seite neu.
6. Wählen Sie die Auslassungspunkte (...) neben dem Abonnement aus und wählen Sie **Einstellungen bearbeiten**.
7. Stellen Sie unter **Cloud Workloadschutz** den Schieberegler **Server** auf der rechten Seite auf **Ein**.
8. Wählen Sie im oberen Bereich der Seite **Speichern** aus.
   
Wenn Sie den Plan für Server aktivieren, können Sie sehen, dass Defender for Cloud viele weitere Ressourcentypen unterstützt.

### Aufgabe 3: Aktivieren des lokalen Servers in Azure Arc

Azure Arc ist erforderlich, damit Daten an den Log Analytics-Arbeitsbereich gesendet werden können, den Defender for Cloud verwendet.

1. Wechseln Sie zur VM **LON-SC2** und melden Sie sich im Azure-Portal **https://portal.azure.com** an.
2. Suchen Sie nach **Azure Arc** und öffnen Sie es.
3. Erweitern Sie im linken Navigationsbereich **Azure Arc Ressourcen** und wählen Sie **Computer**.
4. Wählen Sie **Hinzufügen/Erstellen** > **Computer hinzufügen**.
5. Wählen Sie unter Einen einzelnen Server hinzufügen die Option **Skript generieren**.
6. Wählen Sie **ContosoRG** in der Ressourcengruppe.
7. Wählen Sie **USA, Osten** als Region.
8. Wählen Sie **Skript herunterladen und ausführen** aus.
9. Wählen Sie **Herunterladen** und führen Sie das Skript auf Ihrem zweiten Lab Client **LON-SC2** aus, um das Onboarding des lokalen Servers in Azure zu durchzuführen.
10. Führen Sie die Windows PowerShell als Administrator aus.
11. Setzen Sie die Ausführungsrichtlinie auf uneingeschränkt.
```Powershell
Set-ExecutionPolicy -ExecutionPolicy unrestricted
```
12. Führen Sie das Onboarding-Skript aus.
13. Wenn das Authentifizierungs-Popup erscheint, melden Sie sich mit demselben Konto an, das Sie für das Azure-Portal verwenden.
14. Warten Sie, bis das Skript erfolgreich abgeschlossen ist.
15. Kehren Sie zurück zu LON-SC1 und öffnen Sie Azure Arc.
16. Wählen Sie **Computer**, wählen Sie **Aktualisieren** oben auf der Seite und überprüfen Sie, ob Ihr Server erfolgreich in Azure Arc bereitgestellt wurde.

Sie haben Azure Arc erfolgreich auf dem Testserver aktiviert, und die Daten sollten nun in den Log Analytics-Arbeitsbereich fließen. Dieser Vorgang kann einige Zeit in Anspruch nehmen, bis Sie im Dashboard etwas sehen können.

### Aufgabe 4: Hinzufügen des Servers zu Defender für Cloud und Sammeln von Protokollen.

Sie stellen eine Datensammlungsregel bereit, um Ereignisprotokolle vom lokalen Server abzurufen. Die Regel wird den Überwachungsagent automatisch auf dem Server bereitstellen und Protokolle an den zuvor erstellten Log Analytics-Arbeitsbereich weiterleiten.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
2. Öffnen Sie Defender for Cloud und wählen Sie die Registerkarte **Erste Schritte** oben auf der Seite.
3. Wählen Sie unter **Nicht-Azure-Server hinzufügen** die Option **Konfigurieren**.
4. Sie finden Ihren zuvor erstellten Log Analytics-Arbeitsbereich, wählen Sie daneben **Upgrade** aus.
5. Wenn das Upgrade abgeschlossen ist, wählen Sie **+ Server hinzufügen**.
6. Wählen Sie **Datensammlungsregeln** aus
7. Klicken Sie auf **Erstellen**.
8. - Regelname: ContosoDCR
   - Ressourcengruppe: contosorg
9. Wählen Sie **Weiter: Ressourcen** aus.
10. Wählen Sie **Ressourcen hinzufügen** aus. Erweitern Sie den Bereich der Ressourcengruppe. Überprüfen Sie den zuvor integrierten Azure Arc-Computer und wählen Sie **Anwenden**.
11. Wählen Sie **Weiter: Sammeln und übermitteln** aus.
12. Wählen Sie die Option **Datenquelle hinzufügen**.
13. Wählen Sie den Datenquellentyp **Windows-Ereignisprotokolle** aus.
14. Wählen Sie alle Optionen unter **Ereignisprotokolle und zu erfassende Ebenen konfigurieren:** aus.
15. Wählen Sie **Weiter: Ziel** aus.
16. Klicken Sie auf **Ziel hinzufügen**.
17.  - Zieltyp: Azure Monitor-Protokolle
     - Konto oder Namespace: ContosoLA
18. Wählen Sie die Option **Datenquelle hinzufügen**.
19. Klicken Sie auf **Überprüfen + erstellen**.
20. Klicken Sie auf **Erstellen**.

Es kann einige Stunden dauern, bis die Ressource vollständig in Defender for Cloud integriert ist. Der nächste Schritt besteht darin, sich die Empfehlung anzusehen, die Defender for Cloud für diese Ressource generiert.

### Aufgabe 5: Hinzufügen eines Standards zur Einhaltung von Vorschriften

Auf der Grundlage der Empfehlung können Sie damit beginnen, die Ressource zu sichern und Sicherheitsrichtlinien zuzuweisen, z. B. NIST SP 800-53 Rev. 5, um sicherzustellen, dass die Ressourcen der Tailwind Traders unseren Compliance-Vorschriften entsprechen.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
2. Öffnen Sie Defender for Cloud, erweitern Sie **Verwaltung** und wählen Sie **Umgebungseinstellungen**.
3. Wählen Sie **Alle erweitern** aus.
4. Wählen Sie die Auslassungspunkte (...) neben dem Abonnement aus und wählen Sie **Einstellungen bearbeiten**.
5. Wählen Sie **Sicherheitsrichtlinien** im Navigationsmenü auf der linken Seite. Es kann eine Weile dauern, bis die Liste geladen ist.
6. Suchen Sie nach **NIST SP 800-53 Rev. 5**. Schieben Sie den Schieberegler Status auf **Ein**. 
7. Wechseln Sie zurück zu Defender for Cloud und wählen Sie **Gesetzlicher Bestimmungen**.

Aufgrund der eingeschränkten Lab-Umgebung können Sie die Ressourcen sowie die Compliance-Empfehlungen nicht sehen. Es dauert eine Weile, bis die bereitgestellten Ressourcen in Defender for Cloud sichtbar sind.

Im Dashboard zur Einhaltung gesetzlicher Vorschriften können Sie jetzt alle fehlerhaften Bewertungen überprüfen, die im Dashboard angezeigt werden, um die Details der Empfehlungen zu verstehen.
Durch die kontinuierliche Bewertung von Ressourcen anhand dieser Steuerelemente identifiziert Defender for Cloud Probleme, die das Erreichen bestimmter Compliance-Zertifizierungen behindern können. Die Einhaltung gesetzlicher Vorschriften ist entscheidend, um die Daten Ihrer Organisation zu schützen und eine sichere Cloudumgebung zu gewährleisten.
