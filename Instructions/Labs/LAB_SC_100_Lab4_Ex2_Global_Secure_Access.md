# Übung 4 - Aufgabe 2 - Globaler sicherer Zugriff

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
<!--BITE AUSFÜLLEN-->
|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Aktivieren des sicheren Remotezugriffs für lokale Server| Globaler sicherer Zugriff auf EntraID | Aktivieren des globalen sicheren Zugriffs  |
|Integrieren in die bestehende Infrastruktur | Anwendungsproxy | Bereitstellen des Anwendungsproxys auf dem Dateiserver von Contoso |

## Teil 2: Implementieren der Lösung (optional)

## Aufgabe 1: Aktivieren des globalen sicheren Zugriffs

Der erste Schritt ist die Aktivierung von globalem sicherem Zugriff in Ihrem Mandanten. Dadurch können Sie einen Azure App Proxy verwenden, um sicheren Zugriff auf OnPremises-Ressourcen zu ermöglichen.

1. Melden Sie sich bei der **Client 1 VM** (LON-SC1) als **lon-sc1\admin** Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
2. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **https://entra.microsoft.com** und melden Sie sich im Entra Portal als **MOD Administrator**admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandant-ID ist, die von Ihrem Anbieter für das Hosting von Übungen bereitgestellt wird). Das Kennwort des Benutzernden sollte von Ihrem Provider für die Übung bereitgestellt werden.
3. Sie werden aufgefordert, die Multifaktor-Authentifizierung einzurichten. Folgen Sie den Anweisungen.
4. Aktivieren Sie im Dialogfeld Angemeldet bleiben? das Kontrollkästchen Dies nicht mehr anzeigen und wählen Sie dann **Nein**.
5. Schließen Sie das Dialogfeld zum Speichern des Kennworts von unten, indem Sie Nie wählen, um die Anmeldeinformationen des globalen Admins nicht in Ihrem Browser zu speichern.
6. Erweitern Sie im linken Navigationsbereich **Global Secure Access** und wählen Sie **Dashboard**.
7. Wählen Sie unter **Global Secure Access in Ihrem Mandanten aktivieren** **Aktivieren**.

Sie haben den globalen sicheren Zugriff erfolgreich aktiviert.

## Aufgabe 2: Bereitstellung des Anwendungsproxys

Global Secure Access basiert auf Application Proxy, mit dem Sie einen sicheren Cloud-Endpunkt für Ihre lokalen Ressourcen erstellen können. In diesem Fall erlauben Sie dem Testserver, den Sie zuvor festgelegt haben, über die Proxy-Infrastruktur zu kommunizieren.

1. Melden Sie sich bei der **Server 1-VM** (LON-SC2) als **lon-sc1\admin-Konto** an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
2. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **https://entra.microsoft.com** und melden Sie sich im Entra Portal als **MOD Administrator**admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandant-ID ist, die von Ihrem Anbieter für das Hosting von Übungen bereitgestellt wird). Das Kennwort des Benutzernden sollte von Ihrem Provider für die Übung bereitgestellt werden.
3. Erweitern Sie im linken Navigationsbereich unter **Global Secure Access** den Bereich **Connect** und wählen Sie **Connectors**.
4. Wählen Sie **Connectordienst herunterladen**.
5.  Wählen Sie **Begriffe akzeptieren & Download**.
6.  Installieren Sie den **Microsoft Azure Active Directory Application Proxy Connector**.
7.  Während des Installationsvorgangs müssen Sie sich mit dem von der Übung bereitgestellten Benutzernamen und Passwort anmelden.
8.  Öffnen Sie die **CMD** und führen Sie den Befehl **ipconfig** aus, dann beachten Sie die IP-Adresse.
9.  Gehen Sie zurück zum Entra-Portal und aktualisieren Sie die Seite Konnektoren.

Sie sollten die eingebaute VM und die zugehörige IP-Adresse sehen. Dies bedeutet, dass Sie den Konnektor erfolgreich hergestellt haben.

## Aufgabe 3: Erstellen der Freigabe auf dem Dateiserver

In dieser Aufgabe erstellen Sie eine SMB-Freigabe auf dem lokalen Dateiserver, auf die über den GSA zugegriffen wird.

1. Sie sollten weiterhin bei LON-SC2 angemeldet sein.
2. Öffnen Sie den **Explorer**, navigieren Sie zum Laufwerk C: und erstellen Sie einen Ordner mit dem Namen **Share**.
3. Wählen Sie den Ordner „Freigabe“ und öffnen Sie die **Eigenschaften**.
4. Wählen Sie **Freigeben**.
5. Wählen Sie **Freigeben...**.
6. Wählen Sie **Alle** aus dem Dropdown-Menü und wählen Sie **Hinzufügen**.
7. Wählen Sie **Teilen** aus.
8. Wählen Sie **Nein, das Netzwerk, mit dem ich verbunden bin, zu einem privaten Netzwerk machen**.

## Aufgabe 4: Einrichten des Schnellzugriffs und Zuweisen des Benutzenden

Damit Ihre Benutzenden über den GSA-Client auf den Dateiserver zugreifen können, müssen Sie den Schnellzugriff aktivieren und ihn Ihren Testbenutzenden zuweisen. Ohne diese Konfiguration kann der Benutzende keine Verbindung zum Dateiserver herstellen.

1. Erweitern Sie im linken Navigationsbereich **Anwendungen** und wählen Sie **Schnellzugriff**. Geben Sie die folgenden Informationen ein:
    - Name: **SMB to ContosoFS**
    - Konnektoren-Gruppe: **Standard**
1. Wählen Sie **Anwendungssegment Schnellzugriff hinzufügen** und geben Sie die folgenden Informationen ein:
    - Zieltyp: IP-Adresse
    - IP-Adresse: "**IHRE VM-IP**"
    - Ports: 445
1. Wählen Sie **Übernehmen**.
1. Wählen Sie **Speichern** und laden Sie das Menü Schnellzugriff neu.
1. Wählen Sie auf der linken Seite **Benutzende und Gruppen**.
1. Wählen Sie **Benutzer/Gruppe hinzufügen** aus.
1. Wählen Sie **Keine Auswahl**.
1. Fügen Sie **MOD Verwaltung** hinzu.
1. Klicken Sie auf **Auswählen** > **Zuordnen**.

Sie haben den Schnellzugriff für Ihren Testbenutzenden, in diesem Fall Ihr Administratorkonto, erfolgreich aktiviert.

## Aufgabe 5: Gerätebeitritt bei Entra-ID

Um den globalen sicheren Zugriff zu verwenden, müssen Sie den Client-Endpunkt mit Entra ID verbinden. Andernfalls wird der GSA-Client nicht funktionieren.

1. Verbinden Sie sich mit LON-SC1, öffnen Sie das Startmenü und wählen Sie **Einstellungen**.
2. Wählen Sie **Konten** > **Zugang zu Arbeit oder Schule**.
3. Um ein Arbeits- oder Schulkonto hinzuzufügen, wählen Sie **Verbinden**.
4. Klicken Sie auf **Gerät mit Entra ID verbinden**.
5. Melden Sie sich mit den vom Anbieter der Übung bereitgestellten Anmeldeinformationen für die **MOD Verwaltung** an.

Sobald Ihr Endpunkt mit Entra ID verbunden ist, können Sie den GSA-Client verwenden, um auf alle Ressourcen zuzugreifen, die Sie mit Global Secure Access schützen.

## Aufgabe 6: Aktivieren des Profils und Überprüfen der Verbindung

Der globale sichere Zugriff ist in zwei Teile unterteilt. Der Teil, an dem Sie arbeiten, wird als privater Zugriff bezeichnet und sichert Ihre lokalen und privaten Ressourcen wie Dateiserver oder OnPremises-Anwendungen. Um den Zugriff auf Ihren Dateiserver zu aktivieren, müssen Sie das private Zugriffsprofil aktivieren, das es den Benutzenden ermöglicht, auf die ihnen zugewiesenen Ressourcen über den Schnellzugriff zuzugreifen.

1. Erweitern Sie im Menü Global Secure Access im linken Bereich des Microsoft Entra Admin Centers **Verbindung** und wählen Sie **Datenverkehrsweiterleitung**.
2. Überprüfen Sie das Profil **Privater Zugriff**.
3. Wählen Sie **OK** aus.
4. Wählen Sie im linken Bereich der Navigation unter **Verbinden** die Option **Client-Download**.
5. Unter Windows 10/11 wählen Sie **Download-Client**.
6. Installieren des **Global Secure Access Client**.
7. Während des Installationsvorgangs müssen Sie sich bei Ihrem MOD-Administrator anmelden.
8. Öffnen Sie **Explorer** in Windows und navigieren Sie zu **Dieser PC** Menüleiste wählen Sie die Auslassungspunkte (...) und wählen Sie **Netzlaufwerk kartieren**.
9. Ordner: `\\IP-ADDRESS\Share` Verwenden Sie die zuvor gemerkte Ipadresse.
10. Wählen Sie **Fertig stellen**aus.
11. Geben Sie den lokalen Benutzernamen und das Passwort ein, um das Netzlaufwerk zuzuordnen.


Sie haben sich mithilfe von Global Secure Access erfolgreich mit dem Dateiserver verbunden.
