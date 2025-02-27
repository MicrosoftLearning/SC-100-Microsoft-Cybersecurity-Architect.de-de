# Globaler sicherer Zugriff

Nachdem Sie den Monitor-Server eingerichtet haben, müssen Sie mithilfe von Global Secure Access (GSA) eine sichere Netzwerkverbindung zum Dateiserver herstellen. Sie möchten sicherstellen, dass der Zugriff auf diese Geräte gesichert ist, bis diese Dateiserver in einen sicheren Cloud-Speicher migriert werden können, insbesondere wenn Tailwind Traders lokale Server in die IT-Infrastruktur Ihres Unternehmens einbringt. Sie haben sich dagegen entschieden, die VPN-Infrastruktur von Tailwind Traders zu überarbeiten, um Ihren mitarbeitenden Personen den Zugriff auf die Server zu ermöglichen. 

Um ein sicheres Netzwerk aufzubauen, starten Sie mit der Erstellung eines Azure App Proxy und der Registrierung des Clients bei Entra ID, bevor Sie einen Konnektor erstellen. Danach konfigurieren Sie eine Richtlinie für den Zugriff und installieren den GSA-Client. Schließlich testen Sie die GSA-Verbindung, um sicherzustellen, dass alles ordnungsgemäß funktioniert.

## Teil 1: Entwerfen einer Lösung (erforderlich)

Bei dieser Aufgabe sichern Sie den Remotezugriff auf Ihre lokale Umgebung.

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage des beschriebenen Szenarios zu analysieren, die Ziele zu verstehen und die Anforderungen zu definieren.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Aktivieren des sicheren Remotezugriffs für lokale Server
- Integrieren in die bestehende Infrastruktur
- Verwenden Sie keine veraltete Infrastruktur von Tailwind Traders

Global Secure Access integriert sich in die bestehende Cloud-Infrastruktur von Contoso Ltd. und ermöglicht Ihren mitarbeitenden Personen einen sicheren ferngesteuerten Zugriff auf lokale Server innerhalb der lokalen Infrastruktur von Tailwind Traders. Überprüfung der GSA und Abwägung der Unterschiede zu anderen Strategien für den ferngesteuerten Zugriff auf Dienste.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Aktivieren des sicheren Remotezugriffs für lokale Server| Globaler sicherer Zugriff auf EntraID | Aktivieren des globalen sicheren Zugriffs  |
|Integrieren in die bestehende Infrastruktur | Anwendungsproxy | Bereitstellen des Anwendungsproxys auf dem Dateiserver von Contoso |

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1: Aktivieren des globalen sicheren Zugriffs

Der erste Schritt ist die Aktivierung von globalem sicherem Zugriff in Ihrem Mandanten.

1. Melden Sie sich bei der VM **LON-SC1** (dem Client-Endpunkt) als lokaler **Admin** an. Das Kennwort sollten Sie von Ihrem Lab-Hostinganbieter erhalten.
1. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **https://entra.microsoft.com** und melden Sie sich im Entra Portal als **MOD Administrator**admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandant-ID ist, die von Ihrem Anbieter für das Hosting von Übungen bereitgestellt wird). Das Kennwort des Benutzernden sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Aktivieren Sie im Dialogfeld **Angemeldet bleiben?** das Kontrollkästchen **Dies nicht mehr anzeigen** und wählen Sie dann **Nein**.
1. Wählen Sie im Dialogfeld **Kennwort speichern** die Option **Nicht jetzt**.
1. Wenn das Dialogfeld **Bei Microsoft Edge anmelden** erscheint, wählen Sie **Nein danke**.
1. Wenn Sie oben rechts auf dem Bildschirm ein Informationsfeld **Multi-Faktor-Authentifizierung verwalten** sehen, schließen Sie es, indem Sie das **X** auswählen.
1. Erweitern Sie im linken Navigationsbereich **Global Secure Access** und wählen Sie **Dashboard**.
1. Wählen Sie unter **Global Secure Access in Ihrem Mandanten aktivieren** **Aktivieren**.

Sie haben den globalen sicheren Zugriff erfolgreich aktiviert.

### Aufgabe 2: Aktivieren von TLS und Installieren des privaten Netzwerkconnectors

Der private Netzwerk-Connector ist ein leichtgewichtiger Agent, der auf einem Windows-Server in Ihrer lokalen Umgebung installiert wird, Zugriff auf die Backend-Ressourcen und -Anwendungen hat und dazu dient, die Verbindung zum globalen sicheren Zugriff zu erleichtern.  Auf dem Windows-Server, auf dem der Connector installiert werden soll, muss TLS 1.2 aktiviert sein, bevor Sie den privaten Netzwerkconnector installieren.

1. Melden Sie sich bei der Server-VM, **LON-SC2**, mit dem lokalen **Administratorkonto** an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Wenn Sie sich bei der VM anmelden, wird Server-Manager geöffnet.  Sie können dieses Fenster minimieren.
1. Bevor Sie den Connector für das private Netzwerk auf dem Server installieren, müssen Sie TLS 1.2 aktivieren.  Es gibt mehrere Möglichkeiten, dies zu tun. In dieser Übung kopieren Sie die Befehle, um die Registrierungsschlüssel in eine Datei festzulegen und dann diese Datei auszuführen.

    1. Öffnen Sie **Microsoft Edge**.
    1. Geben Sie in einem Browser-Tab die URL: **`https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors`** ein und drücken Sie die Eingabetaste auf Ihrer Tastatur, um die Produktdokumentation zu öffnen.
    1. Scrollen Sie nach unten zum Abschnitt **Transport Layer Security (TLS)-Anforderungen** und wählen Sie im Codefeld unter **Registrierungsschlüssel festlegen** die Option **Kopieren** aus.
    1. Aus dem VM heraus öffnen Sie den Editor. Geben Sie im Suchfeld der Taskleiste **`Notepad`** ein und wählen Sie dann **Editor**, um die Anwendung zu öffnen.
    1. Verwenden Sie **STRG + V**, um den Code in Notepad einzufügen.  Ändern Sie nichts im eingefügten Code. Die erste Codezeile ist erforderlich.
    1. Wählen Sie im Editor **Datei** und dann **Speichern unter**. 
    1. Wählen Sie im Feld **Als Typ speichern** die Option **Alle Dateien** aus der Dropdown-Liste und geben Sie im Feld **Dateiname** **`EnableTLS.reg`** ein und wählen Sie dann **Speichern**.  Es ist wichtig, dass Sie die Datei mit der .reg-Erweiterung speichern. Notieren Sie sich, wo das Dokument gespeichert wird, und schließen Sie dann Editor.
    1. Öffnen Sie in der Taskleiste den **Datei-Explorer** und navigieren Sie zu dem Ordner, in dem Sie die Datei gespeichert haben (die Standardeinstellung ist dieser PC > Dokumente).
    1. Doppelklicken Sie auf den Dateinamen **Enable-TLS**, um es auszuführen.  Da Sie die Registrierungsdatei ändern, werden Sie gefragt: **Sind Sie sicher, dass Sie fortfahren möchten?**  Klicken Sie auf **Ja** und anschließend auf **OK**.  
    1. Da Sie die Registrierung aktualisiert haben, müssen Sie den Server neu starten. Wählen Sie in der Taskleiste der Server-VM das **Windows-Symbol**, wählen Sie **Leistung**, wählen Sie **Neustart** und wählen Sie dann **Fortfahren**.
    1. Melden Sie sich nach dem Neustart wieder bei der Server-VM an, als lokaler **Admin**.
    1. Minimieren oder schließen Sie den Server-Manager.
1. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **`https://entra.microsoft.com`** und melden Sie sich beim Entra Portal als **MOD-Administrator**admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige, von Ihrem Lab-Hosting-Anbieter bereitgestellte Mandanten-ID ist). Das Kennwort des Benutzernden sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Schließen Sie die Dialogfelder wie bei der vorherigen Aufgabe.
1. Erweitern Sie im linken Bedienfeld **Globaler sicherer Zugriff**, erweitern Sie **Verbinden** und wählen Sie **Connectors**.
1. Wählen Sie oben auf der Seite „Connectors für privates Netzwerk“ die Option **Connector-Dienst herunterladen**.
1. Überprüfen Sie die Informationen und wählen Sie dann **AGB akzeptieren und herunterladen** aus.
1. Wählen Sie im Download-Fenster oben rechts auf der Seite nach Abschluss des Downloads die Option **Datei öffnen** aus.  Wenn das Download-Fenster geschlossen wurde, bevor Sie Datei öffnen wählen konnten, wählen Sie **Dateiexplorer** in der Taskleiste, gehen Sie zum Ordner **Downloads** und führen Sie die Datei **MicrosoftEntraPrivateNetworkConnectorInstaller** aus.
1. Markieren Sie das Kästchen neben **Ich stimme den Lizenzbedingungen zu** und wählen Sie dann **Installieren**.
1. Während des Installationsvorgangs müssen Sie sich mit dem Benutzernamen und dem Kennwort als MOD-Admin anmelden. Es kann einige Minuten dauern, bis die Installation abgeschlossen ist.
1. Sobald die Installation abgeschlossen ist, **schließen** Sie das Installationsfenster und aktualisieren Sie die Browser-Seite.  Der Connector sollte aufgelistet und aktiv sein.
1. Geben Sie in der Windows-Suchleiste in der Taskleiste **`cmd`** ein und wählen Sie dann **Eingabeaufforderung**. 
1. Im Fenster „Admin: Eingabeaufforderungsfenster“ führen Sie den Befehl **`ipconfig`** aus, notieren sich die private IP-Adresse für Ihren Server und schließen dann das Eingabeaufforderungsfenster.

Sie haben den privaten Netzwerkconnector erfolgreich auf Ihrem lokalen Server installiert.

### Aufgabe 3: Erstellen eines Ordners auf dem Dateiserver

In dieser Aufgabe erstellen Sie eine SMB-Freigabe auf dem lokalen Dateiserver, auf die über GSA zugegriffen wird.

1. Sie sollten weiterhin bei LON-SC2 angemeldet sein.
1. Öffnen Sie in der Taskleiste den **Dateiexplorer**, navigieren Sie zum Laufwerk C: und erstellen Sie einen Ordner mit dem Namen **Freigabe**.
1. Wählen Sie mit der rechten Maustaste den Ordner **Freigabe** und wählen Sie **Eigenschaften** aus.
1. Wählen Sie im Fenster „Eigenschaften der Freigabe“ die Registerkarte **Teilen**.
1. Wählen Sie **Freigeben...**.
1. Wählen Sie aus der Dropdown-Liste **Jeder** und wählen Sie **Hinzufügen**.
1. Wählen Sie **Teilen** aus.
1. Wählen Sie **Nein, das Netzwerk, mit dem ich verbunden bin, zu einem privaten Netzwerk machen**.
1. Wählen Sie **Erledigt** und dann **Schließen**.
1. Minimieren oder schließen Sie den Datei-Explorer.

Sie haben einen freigegebenen Ordner auf dem Server erstellt. Es handelt sich um diesen Ordner und dessen Inhalt, auf den Sie über GSA zugreifen.

### Aufgabe 4: Einrichten des Schnellzugriffs und Zuweisen des Benutzenden

Der Privatzugriff bietet zwei Möglichkeiten, die privaten Ressourcen zu konfigurieren, die über den Dienst getunnelt werden sollen. Schnellzugriff oder Anwendungen für den globalen sicheren Zugriff. Für diese Übung verwenden Sie den Schnellzugriff.

Der Schnellzugriff enthält die primäre Gruppe aus FQDNs und IP-Adressen, die Sie sichern möchten. Wenn Sie den Schnellzugriff konfigurieren, erstellen Sie eine neue Unternehmensanwendung, die als Container für die privaten Ressourcen dient, die Sie schützen möchten.

Damit Ihre Benutzenden über den GSA-Client auf die Ressourcen des Dateiservers zugreifen können, müssen Sie den Schnellzugriff aktivieren und ihn Ihren Testbenutzenden zuweisen.

1. Sie können für diesen Schritt in LON-SC2 bleiben.
1. Erweitern Sie im linken Navigationsbereich **Globaler sicherer Zugriff**, erweitern Sie **Anwendungen** und wählen Sie dann **Schnellzugriff**. Geben Sie die folgenden Informationen ein:
    - Name: **`SMB to ContosoFS`**
    - Konnektoren-Gruppe: **Standard**
1. Wählen Sie **Anwendungssegment Schnellzugriff hinzufügen** und geben Sie die folgenden Informationen ein:
    - Zieltyp: **IP-Adresse**
    - IP-Adresse: die private IP-Adresse Ihres Servers, die Sie im vorherigen Schritt angegeben haben, **`192.168.2.100`**.
    - Ports: **`445`**
1. Wählen Sie **Übernehmen**.
1. Wählen Sie **Speichern**. Sobald das Statusfeld für das Anwendungssegment erfolgreich angezeigt wird, aktualisieren Sie die Browserseite. Wenn Sie die Seite aktualisieren, gelangen Sie auf die Seite **Schnellzugriff | Eigenschaften des Netzwerkzugriffs**.
1. Wählen Sie auf der linken Seite **Benutzende und Gruppen**.
1. Wählen Sie **Benutzer/Gruppe hinzufügen** aus.
1. Wählen Sie **Keine Auswahl**.
1. Geben Sie in das Suchfeld **`MOD Administrator`** ein und wählen Sie es dann aus den Suchergebnissen aus.
1. Drücken Sie unten auf der Seite **Auswählen** und wählen Sie dann **Zuweisen**.

Sie haben den Schnellzugriff für Ihren Testbenutzenden erfolgreich aktiviert.

### Aufgabe 5: Gerätebeitritt bei Entra-ID

Um den globalen sicheren Zugriff nutzen zu können, müssen Sie den Client-Endpunkt, die LON-SC1 VM, mit Microsoft Entra ID verbinden. Andernfalls wird der GSA-Client nicht funktionieren.

1. Wechseln Sie zurück zur VM **LON-SC1** (dies ist Ihre Client-Endpunkt-VM).
1. Wählen Sie mit der rechten Maustaste das Windows-Symbol in der Taskleiste und wählen Sie **Einstellungen**.
1. Wählen Sie auf dem linken Bedienfeld **Konten**.
1. Wählen Sie auf der Seite „Konten“ **Zugang Arbeit oder Schule**.
1. Um ein Arbeits- oder Schulkonto hinzuzufügen, wählen Sie **Verbinden**.
1. Wählen Sie am unteren Rand des Fensters **Gerät mit Microsoft Entra ID verbinden**.
1. Melden Sie sich mit den vom Anbieter der Übung bereitgestellten Anmeldeinformationen für die **MOD Verwaltung** an.
1. Überprüfen Sie im Fenster **Stellen Sie sicher, dass dies Ihre Organisation ist** die Informationen und wählen Sie **Beitreten**.
1. Überprüfen Sie die Informationen im Fenster **Sie sind bereit** und wählen Sie **Erledigt**.
1. Nachdem Ihr Gerät mit Ihrem MOD-Administratorkonto verknüpft ist, müssen Sie sich mit diesem Konto anmelden.
    1. Wählen Sie in der Taskleiste das Symbol **Windows**, wählen Sie **Admin** und dann **Benutzer wechseln**.
    1. Wählen Sie unten links im Fenster die Option **Anderer Benutzer** und melden Sie sich dann mit Ihrem MOD-Administratorkonto Konto an.
    1. Es wird einige Minuten dauern, bis das Konto festgelegt ist. Danach erscheint ein Fenster **Weitere Informationen erforderlich**. Dadurch wird der Prozess zum Einrichten der Multi-Faktor-Authentifizierung initiiert.  Folgen Sie den Anweisungen zur Einrichtung von MFA.

Sobald Ihr Endpunkt mit der Entra-ID verbunden ist, können Sie den GSA-Client einrichten, der zum Herstellen einer Verbindung mit allen Ressourcen verwendet wird, die Sie mit dem globalen sicheren Zugriff schützen.

### Aufgabe 6: Aktivieren des Datenverkehrsweiterleitungsprofils und Herunterladen des GSA-Desktopclients

Um den Zugriff auf private Ressourcen oder Anwendungen in Ihrer lokalen Umgebung zu ermöglichen, müssen Sie das Datenverkehrsweiterleitungsprofil für privaten Zugriff aktivieren und Benutzende zuweisen.

Sie müssen auch den Client für den globalen sicheren Zugriff herunterladen und installieren.  

Datenverkehr für den privaten Zugriff kann an den Dienst weitergeleitet werden, indem eine Verbindung über den Desktopclient für globalen sicheren Zugriff hergestellt wird.

1. Sie sollten sich weiterhin auf **LON-SC1** befinden, bei dem Sie sich mit Ihrem MOD-Administratorkonto angemeldet haben.
1. Öffnen Sie **Microsoft Edge**. Sie werden aufgefordert, Microsoft Edge einzurichten.
1. Navigieren Sie in der Microsoft Edge zu **`https://entra.microsoft.com`**.
1. Erweitern Sie im linken Navigationsbereich **Global Secure Access**, erweitern Sie **Connect** und wählen Sie **Verkehrsweiterleitung**.  Möglicherweise müssen Sie das linke Bedienfeld durch Auswahl von **>>** erweitern, um eine Ansicht der Optionen zu erhalten.
1. Wählen Sie den Schieberegler neben **Privates Zugriffsprofil** und wählen Sie dann **OK**.
1. Nachdem Sie das Profil für den privaten Zugriff aktiviert haben, müssen Sie nun die Benutzenden zuweisen.
    1. Wählen Sie in der Profilkarte „Privater Zugriff“ unter **Benutzer- und Gruppenzuordnungen** die Option **Ansicht**.
    1. Wählen Sie die Stelle aus, an der **0 Benutzender, 0 Gruppen zugeordnet** steht.
    1. Wählen Sie **Benutzer/Gruppe hinzufügen** aus.
    1. Wählen Sie **Keine Auswahl**.
    1. Geben Sie in der Suchleiste **`MOD Administrator`** ein, wählen Sie **MOD Administrator**, drücken Sie **Auswählen** und wählen Sie dann **Zuweisen**.
1. Wählen Sie im linken Bereich der Navigation unter **Verbinden** die Option **Client-Download**.
1. Wählen Sie unter Windows 10/11 „**Client herunterladen**“ aus.
1. Wählen Sie im Fenster „Downloads“ die Option „**Datei öffnen**“ aus. Wenn das Download-Fenster geschlossen wurde, bevor Sie „Datei öffnen“ auswählen konnten, wählen Sie „**Datei-Explorer**“ in der Taskleiste aus, wechseln Sie zum Ordner „**Downloads**“ und führen Sie dann die Datei „**GlobalSecureAccessClient**“ aus.
1. Wählen Sie „**Ich stimme den Lizenzbedingungen zu**“ und dann „**Installieren**“ aus. Wählen Sie im daraufhin angezeigten Fenster „Benutzerkontensteuerung“ die Option „**Ja**“ aus.
1. Sobald die Installation erfolgreich abgeschlossen ist, **schließen Sie** das Fenster.
1. Wählen Sie auf der Taskleiste den Nach-oben-Pfeil aus, um ausgeblendete Symbole anzuzeigen.  Hier sehen Sie das Symbol des Global Secure Access-Clients. Wenn es kein grünes Häkchen hat, klicken Sie mit der rechten Maustaste auf das Symbol und wählen Sie „**Aktivieren“**. Es kann einige Minuten dauern, bis ein grünes Häkchen angezeigt wird, das anzeigt, dass die Verbindung hergestellt wurde.
1. Wählen Sie in der Taskleiste **Datei-Explorer** aus und navigieren Sie zu **Dieser PC**. Wählen Sie die Auslassungspunkte (**...**) und dann **Netzlaufwerk verbinden** aus.
1. Geben Sie im Feld „Ordner“ `\\192.168.2.100\Share` ein. Verwenden Sie die zuvor notierte IP-Adresse UND wählen Sie **Verbinden mit anderen Anmeldedaten**.
1. Wählen Sie **Fertig stellen**aus.
1. Verwenden Sie zum Zuordnen des Netzlaufwerks die Anmeldedaten für das lokale Administratorkonto auf LON-SC2.  
    1. E-Mail-Feld: **`Administrator`** (dies kann je nach Lab-Hoster variieren).
    1. Kennwortfeld: **`Pa55w.rd`** (Dies kann je nach Lab-Hoster variieren).
    
    >[!NOTE] Es ist bekannt, dass die Verwendung des lokalen Administratorkontos kein typisches Szenario ist. Es wird in dieser Übung aufgrund der vereinfachten lokalen Umgebung verwendet. Ein realistischeres Szenario mit einer stärker eingebundenen lokalen Umgebung würde den Benutzenden mit seinem Entra-ID-Konto auf die privaten Ressourcen zugreifen lassen.

1. Bevor Sie zur nächsten Übung wechseln, empfiehlt es sich, den Benutzenden für eine optimale Bildschirmgröße zu wechseln.
    1. Wählen Sie in der Taskleiste das Symbol **Windows**, dann **MOD-Administrator** und schließlich **Benutzender wechseln** aus.
    1. Wählen Sie unten links im Fenster „**Admin**“ aus und melden Sie sich dann mit Ihrem lokalen Administratorkonto an.

Sie haben sich mithilfe von Global Secure Access erfolgreich mit dem Dateiserver verbunden.
