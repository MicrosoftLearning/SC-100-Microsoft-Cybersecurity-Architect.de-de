# Lab 2 – Übung 2 – Bedingter Zugriff

Sie haben festgestellt, dass Mitarbeitende von unbekannten Standorten aus auf Microsoft 365 zugreifen, obwohl Ihre Richtlinien für den bedingten Zugriff nur den Zugriff von bestimmten Standorten und Geräten aus erlauben. Ihre Untersuchung hat ergeben, dass diese Mitarbeitenden auf Microsoft 365 zugreifen, während sie mit öffentlichen Verkehrsmitteln von ihrem Büro nach Hause fahren. Dieses Verhalten verstößt gegen die Branchenvorschriften, und Sie möchten es mit der fortlaufenden Zugriffsevaluierung verhindern. Außerdem möchten Sie die Authentifizierungsstärke implementieren, die Sie in der vorherigen Übung vorbereitet haben, um bestimmte Anwendungen zu schützen, die Kundendaten verarbeiten. 

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept zur Bewältigung der Risiken, denen Contoso Ltd. ausgesetzt ist.

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage der beschriebenen Problematik zu analysieren, die Ziele zu verstehen und die Anforderungen zu definieren.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Einschränken des Zugriffs von unsicheren/unbekannten Speicherorten
- Erfordern einer starken Authentifizierung für Apps mit vertraulichen Informationen

Im zweiten Schritt untersuchen Sie die vorhandene Umgebung von Contoso Ltd.. Microsoft Entra ID bietet Lösungen zur Verwaltung und Einschränkung des Benutzerzugriffs mit Hilfe von Entra ID Richtlinien für den bedingten Zugriff. Untersuchen Sie, welche Kontrollen bestehen und welche Richtlinien bereits eingesetzt werden. Verwenden Sie das Entra ID Portal, um die aktuellen Konfigurationen und Richtlinien zu überprüfen und festzustellen, ob Anpassungen erforderlich sind oder neue Richtlinien implementiert werden müssen.

In der dritten Phase wird das Konzept der Lösung erarbeitet. Bei der Untersuchung stellt sich heraus, dass noch kein vertrauenswürdiges Netzwerk konfiguriert ist und keine der aktuellen Richtlinien die definierten Anforderungen erfüllt. Daher ist eine neue Reihe von Richtlinien für bedingten Zugriff unerlässlich. 

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Einschränken des Zugriffs von unsicheren/unbekannten Speicherorten|Richtlinie für bedingten Zugriff einer Entra ID|Definieren sie die Netzwerke des aktuellen Unternehmens als vertrauenswürdiges Netzwerk, und beschränken Sie den Zugriff auf Geräte innerhalb dieses Netzwerks.|
|Erfordern einer starken Authentifizierung für Apps mit vertraulichen Informationen|Richtlinie für bedingten Zugriff einer Entra ID|Erstellen Sie eine neue Richtlinie für bedingten Zugriff für vertrauliche Anwendungen, die die soeben erstellte gehärtete Authentifizierungsstärke erfordern, die unsichere Authentifizierungsmethoden wie SMS und Voice ausschließt.|

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1 – Erstellen eines vertrauenswürdigen Netzwerks

In dieser Aufgabe erstellen Sie einen benannten Speicherort unter Verwendung der externen IP-Adresse Ihrer VM, um ein vertrauenswürdiges Netzwerk zu definieren, das Sie in einer Richtlinie für bedingten Zugriff in den folgenden Aufgaben verwenden können. Sie verwenden diese Adresse, da sich Ihr Computer in Ihrem Firmennetzwerk befindet.

1. Melden Sie sich am Client 1 VM (LON-Sc1) als **lon-sc1\admin**-Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
2. Öffnen Sie ein **PowerShell**-Fenster, indem Sie das Startmenü mit der rechten Maustaste auswählen und dann **Windows PowerShell** wählen.
3. Geben Sie das folgende Cmdlet ein, um Ihre aktuelle externe IP-Adresse zu überprüfen:
    ```powershell
    curl ifconfig.me | Select-String -Pattern '.'
    ```
4. Notieren Sie sich die von Powershell zurückgegebene IP-Adresse.
5. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **https://entra.microsoft.com** und melden Sie sich beim Entra ID Portal als **MOD Administrator**admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandanten-ID ist, die Sie von Ihrem Labor-Hosting-Anbieter erhalten haben). Das Passwort der administrierenden Person sollte von Ihrem Lab-Hosting-Anbieter bereitgestellt werden.
6. Aktivieren Sie im Dialogfeld Angemeldet bleiben? das Kontrollkästchen Dies nicht mehr anzeigen und wählen Sie dann Nein.
7. Schließen Sie das Dialogfeld zum Speichern des Kennworts von unten, indem Sie Nie wählen, um die Anmeldeinformationen des globalen Admins nicht in Ihrem Browser zu speichern.
8. Navigieren Sie im linken Navigationsbereich zu **Schutz** > **Bedingter Zugriff** > **Benannte Orte**.
9. Wählen Sie **+ IP-Bereiche Speicherort**.
10. Geben Sie den Namen **Vertrautenwürdiges Contoso-Netzwerk** ein.
11. Wählen Sie **Als vertrauenswürdigen Speicherort markieren** aus.
12. Wählen Sie **+**, um die IP-Adresse hinzuzufügen, die Sie in **Schritt 4 notiert haben.**
13. Die Eingabe sollte wie ``168.245.***.***/32`` aussehen (*** kann je nach Ihrem Lab-Hosting-Anbieter unterschiedlich sein).
14. Wählen Sie **Hinzufügen**.
15. Klicken Sie auf **Erstellen**.

Sie haben nun die externe IP-Adresse Ihres Unternehmens und den vertrauenswürdigen Speicherort festgelegt, mit dem Sie den Zugriff außerhalb des Unternehmensnetzes beschränken können.

### Aufgabe 2 – Erstellen einer neuen Richtlinie für bedingten Zugriff mit eingeschränktem Umfang

Nachdem Sie erfolgreich ein vertrauenswürdiges Netzwerk erstellt haben, erstellen Sie nun die Richtlinie für bedingten Zugriff, um den Zugriff außerhalb des Unternehmensnetzwerks zu beschränken, wobei der Geltungsbereich auf Ihre persönlichen Benutzenden beschränkt ist, um eine unternehmensweite Kontosperrung durch Entra ID zu testen und zu verhindern.

1. Sie sollten weiterhin im Entra ID Portal **https://entra.microsoft.com** angemeldet sein.
2. Navigieren Sie im linken Navigationsbereich zu **Schutz** > **Bedingter Zugriff** > **Richtlinien**.
3. Wählen Sie **+Neue Richtlinie erstellen** aus.
4. Geben Sie den Namen **Zugriff außerhalb des vertrauenswürdigen Netzwerks sperren** ein.
5. Wählen Sie **0 Benutzer*innen und Gruppen ausgewählt**.
6. Wählen Sie unter **Einschließen** **Benutzende und Gruppen auswählen** und markieren Sie **Benutzende und Gruppen**.
7. Wählen Sie **Allan Deyoung** als einzigen Testbenutzer für die Richtlinie aus.
8. Wählen Sie **Keine Zielressourcen ausgewählt** und unter **Einschließen** wählen Sie **Alle Cloud-Apps**.
9. Wählen Sie **0 Bedingungen ausgewählt** und unter **Speicherorte** wählen Sie **Nicht konfiguriert**.
10. Wählen Sie **Ja**, um die Speicherortbedingungen zu konfigurieren.
11. Wählen Sie unter **Einschließen** die Option **Alle Speicherorte** aus.
12. Wählen Sie unter **Ausschließen** **Alle vertrauenswürdigen Speicherorte**.
13. Unter **Zuweisung** wählen Sie **0 Kontrollen ausgewählt** und wechseln Sie von **Zugriff gewähren** zu **Zugriff sperren**.
14. Wählen Sie unter **Sitzung** **0 Kontrollen ausgewählt**.
15. Aktivieren Sie **Anpassen der fortlaufenden Zugriffsevaluierung** und wechseln Sie von **Deaktivieren** zu **Speicherort-Richtlinien strikt durchsetzen**. Wählen Sie unten **Auswählen**, um zu bestätigen.
16. Aktivieren Sie nun die Richtlinie über die Steuerleiste am unteren Rand und wählen Sie **Erstellen**.

Sie haben nun Ihre CA-Richtlinie erstellt und aktiviert, um den Zugriff außerhalb vertrauenswürdiger Netzwerke zu beschränken, was nur Ihr eigenes Testbenutzerkonto betrifft.

### Aufgabe 3 - Testen der konfigurierten Richtlinie

Da Sie eine Richtlinie für bedingten Zugriff erstellt haben, die den Zugriff auf alle Cloudanwendungen Ihres Unternehmens beschränkt, müssen Sie sicherstellen, dass der Zugriff weiterhin möglich ist.

>[!CAUTION] WARNUNG! Diese Aufgabe ist zur Veranschaulichung stark abgekürzt! In einem realen Szenario würden Sie einen längeren Testzeitraum mit einer größeren, repräsentativeren Gruppe durchführen, um sicherzustellen, dass keine unvorhersehbaren Ereignisse das Ergebnis verfälschen.

1. Öffnen Sie ein neues **InPrivate**-Fenster in Ihrem **Microsoft Edge**-Browser, indem Sie mit der rechten Maustaste auf das Symbol in der Taskleiste klicken und dann **Neues InPrivate-Fenster** wählen.
2. Wählen Sie die Adressleiste aus, navigieren Sie zu **https://portal.microsoft.com** und melden Sie sich beim M365-Portal als **Allan Deyoung**alland@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandanten-ID ist, die Sie von Ihrem Lab-Hosting-Anbieter erhalten haben). Das Passwort für die Benutzenden sollte von Ihrem Lab-Hosting-Anbieter bereitgestellt werden.
3. Aktivieren Sie im Dialogfeld Angemeldet bleiben? das Kontrollkästchen Dies nicht mehr anzeigen und wählen Sie dann Nein.
4. Schließen Sie das Dialogfeld zum Speichern des Kennworts von unten, indem Sie Nie wählen, um die Anmeldeinformationen des globalen Admins nicht in Ihrem Browser zu speichern.
5. Da die Anmeldung erfolgreich war, können Sie das Fenster **InPrivate** schließen.
6. Wechseln Sie zurück zu Ihrem Edge-Browserfenster, wo Sie immer noch beim Entra ID-Portal **https://entra.microsoft.com** angemeldet sein sollten.
7. Navigieren Sie im linken Navigationsbereich zu **Schutz** > **Bedingter Zugriff** > **Überwachung** > **Anmeldeprotokolle**.
8. Wählen Sie **Filter hinzufügen** und filtern Sie nach dem **Benutzenden** von **Allan Deyoung**.
9. Wählen Sie den neuesten Protokolleintrag von **Allan Deyoung** aus.
10. Wählen Sie unter der Registerkarte **Bedingter Zugriff** die Option **Zugriff außerhalb des vertrauenswürdigen Netzwerks sperren**.
11. Wählen Sie die Zuordnung **Benutzende** und Sie sollten sehen, dass sie **übereinstimmt** durch **Direkte Zuordnung**.
12. Wählen Sie die Zuordnung **Anwendung** und Sie sollten sehen, dass sie **übereinstimmt** durch **Alle Apps eingeschlossen**.
13. Sie sollten auch sehen, dass die **Speicherort**-Bedingung **nicht erfüllt** wurde, da sie innerhalb des vertrauenswürdigen Netzwerks liegt, das ausgeschlossen ist.
Wenn Sie versuchen würden, sich von einem Netzwerk mit einer anderen externen IP-Adresse anzumelden, würde diese Bedingung zutreffen und den Anmeldeversuch blockieren.
14. Schließen Sie die **Details zur Richtliniefür bedingten Zugriff** und die **Aktivitätsdetails: Anmeldungen**.

Sie haben nun den Zugriff auf alle Cloud-Anwendungen aus dem Unternehmensnetz heraus erfolgreich getestet und sichergestellt. Sie haben auch die Anmeldeprotokolle überprüft, um sicherzustellen, dass die Richtlinie wie beabsichtigt funktioniert und die richtigen Zuweisungen und Bedingungen verwendet, um den Zugriff auf Ihre Cloudanwendungen von außerhalb des Unternehmensnetzwerks einzuschränken.

### Aufgabe 4 – Unternehmensweites Richtlinienrollout

Nach dem erfolgreichen Test in der vorherigen Aufgabe können Sie die Richtlinie nun für das gesamte Unternehmen aktivieren. Zu diesem Zweck bearbeiten Sie den Benutzerbereich der bestehenden Richtlinie.

>[!CAUTION] WARNUNG! Die in dieser Aufgabe implementierten Aktionen können zu Kontosperrung führen!
Stellen Sie sicher, dass Sie mindestens ein Notfall-Administratorkonto haben, das in einem produktiven, realen Szenario von dieser Richtlinie ausgenommen ist. 

1. Sie sollten weiterhin im Entra ID Portal **https://entra.microsoft.com** angemeldet sein.
2. Navigieren Sie im linken Navigationsbereich zu **Schutz** > **Bedingter Zugriff** > **Richtlinien**.
3. Wählen Sie die Richtlinie **Zugang außerhalb des vertrauenswürdigen Netzwerks blockieren**.
4. Wählen Sie unter „Benutzer“ die Option **Bestimmte eingeschlossene Benutzer**.
5. Wählen Sie **Alle Benutzer**.
6. In der Warnung, die unten im Fenster erscheint, wählen Sie **Aktuellen Benutzer, admin@WWLxZZZZZZ.onmicrosoft.com, von dieser Richtlinie ausschließen**.
7. Wählen Sie **Speichern**.

Sie haben jetzt eine aktiv arbeitende Richtlinie für bedingten Zugriff konfiguriert, die verhindert, dass sich Benutzende außerhalb des vertrauenswürdigen Netzwerks anmelden, das Sie als externe IP-Adresse des Unternehmens definiert haben. Dies wurde mithilfe eines eingeschränkten Benutzerbereichs getestet, um sicherzustellen, dass alle Cloudanwendungen zugänglich bleiben. Schließlich haben Sie die CA-Richtlinie auf alle Benutzenden ausgeweitet.

Sie haben den Zugriff von außerhalb des vertrauenswürdigen Netzwerks erfolgreich eingeschränkt.

### Aufgabe 5 – Erfordern von MFA für Salesforce

In dieser Aufgabe erstellen Sie eine Zertifizierungsstellenrichtlinie, um die Authentifizierungsstärke durchzusetzen, die Sie in der vorherigen Übung bei der Anmeldung bei Salesforce erstellt haben. 

>[!IMPORTANT] Wichtig: Diese Aufgabe überspringt die Testphase. In einem realen Szenario würden Sie zuerst mit einem begrenzten Benutzerbereich testen, wie in den vorherigen Aufgaben zu sehen und nach einer erfolgreichen Testphase ein vollständiges Rollout durchzuführen.

1. Sie sollten weiterhin im Entra ID Portal **https://entra.microsoft.com** angemeldet sein.
2. Navigieren Sie im linken Navigationsbereich zu **Schutz** > **Bedingter Zugriff** > **Richtlinien**.
3. Wählen Sie **+ Neue Richtlinie** aus.
4. Geben Sie den Namen **Salesforce-Authentifizierungsstärke** ein.
5. Wählen Sie **0 Benutzer*innen und Gruppen ausgewählt**.
6. Wählen Sie unter **Einschließen** **Benutzende und Gruppen auswählen** und markieren Sie **Benutzende und Gruppen**.
7. Wählen Sie **Alex Wilber** aus „Vertrieb“ als einziger Testbenutzer für die Richtlinie aus.
8. Wählen Sie **Keine Zielressourcen ausgewählt** und unter **Einbinden** wählen Sie **Anwendungen auswählen**.
9. Wählen Sie unter **Auswahl** die Option **Keine** und suchen Sie nach **Salesforce**.
10. Bestätigen Sie Ihre Wahl mit **Auswählen**.
11. Wählen Sie unter **Zuweisung** die Option **0 Kontrollen ausgewählt** und aktivieren Sie **Authentifizierungsstärke anfordern**.
12. Wählen Sie Ihre individuell erstellte Authentifizierungsstärke **Verstärkte MFA** und bestätigen Sie mit der Schaltfläche **Auswählen**.
13. Legen Sie nun die Richtlinie auf **Ein** fest, indem Sie die Kontrollleiste unten verwenden und **Erstellen** wählen.
14. Nach einer erfolgreichen Testphase mit Ihrem begrenzten Umfang an Benutzenden wählen Sie **Salesforce-Authentifizierungsstärke**.
15. Wählen Sie unter „Benutzer“ die Option **Bestimmte eingeschlossene Benutzer**.
16. Wählen Sie **Alle Benutzer**.
17. Wählen Sie **Speichern**.

Sie haben nun eine Zertifizierungsstellenrichtlinie erstellt, um Ihre Richtlinie zur Authentifizierungsstärke in Salesforce durchzusetzen, wobei SMS-OTP ausgeschlossen ist, und somit erfolgreiche Angriffe durch das Abfangen von SMS zu verhindern. 
