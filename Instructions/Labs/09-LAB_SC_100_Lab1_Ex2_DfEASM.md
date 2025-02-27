# Verwalten externer Angriffsflächen

## Überblick über die Übung

Contoso möchte seine Cybersicherheit durch die Identifizierung und Verwaltung seiner externen Angriffsfläche verbessern. Diese Oberfläche umfasst Assets, die bei unterschiedlichen Cloud-Anbietern gehostet werden. Um dieses Ziel zu erreichen, möchte Contoso seine Angriffsflächendaten in Sentinel, seine Cloud-native SIEM-Lösung, integrieren. Diese Integration wird die Funktionen zur Überwachung der Sicherheit und zur Reaktion auf Incidents verbessern. 

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept, um sich einen Überblick über Ihre nach außen gerichteten Assets und deren Angriffsfläche zu verschaffen.

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage des beschriebenen Szenarios zu analysieren, die Ziele zu verstehen und die Anforderungen zu definieren.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Die nach außen gerichteten Assets von Contoso müssen überwacht und gesichert werden
- Entdecken Sie alle Assets, die Contoso zugeordnet sind
- Integrieren sie Daten in die SIEM-Lösung von Contoso.
- Assets müssen verwaltet und gekennzeichnet werden

In einem zweiten Schritt wird die bestehende Umgebung von Contoso Ltd. untersucht. Microsoft Defender External Attack Surface Management (EASM) überwacht kontinuierlich Ihre digitale Angriffsfläche und stellt eine externe Ansicht der Online-Infrastruktur eines Unternehmens bereit. Er identifiziert angezeigte Ressourcen, priorisiert Risiken und erweitert die Kontrolle von Schwachstellen und Risiken über die Firewall hinaus.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Die nach außen gerichteten Assets von Contoso müssen überwacht und gesichert werden| Defender EASM | Erstellen einer Microsoft Defender EASM-Ressource|
|Ermitteln aller Assets, die Contoso zugeordnet sind | Defender EASM |Erstellen eines Ermittlungsauftrags für die Assets von Contoso  |
|Integrieren Sie Daten in die SIEM-Lösung von Contoso |Defender EASM, Log Analytics Workspace | Verbinden von Log analytics workspace mit Defender EASM |
|Assets müssen verwaltet und gekennzeichnet werden | Defender EASM | Verwalten von abrechenbaren Assets und Tags |


## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1 - Defender EASM einrichten

In dieser Aufgabe erstellen Sie einen Defender EASM-Arbeitsbereich.

1. Melden Sie sich am Client 1 VM (LON-Sc1) als **lon-sc1\admin**-Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **`https://portal.azure.com`** und melden Sie sich im Azure-Portal als Benutzender <user1-ZZZZZZZ@LODSUATMCA.onmicrosoft.com> an. Das Passwort der administrierenden Person sollte von Ihrem Lab-Hosting-Anbieter bereitgestellt werden.
1. Aktivieren Sie im Dialogfeld Angemeldet bleiben? das Kontrollkästchen Dies nicht mehr anzeigen und wählen Sie dann Nein.
1. Schließen Sie den Dialog zum Speichern von Passwörtern von unten, indem Sie **Nie** wählen, um die Standard-Anmeldeinformationen für globale Administrierende nicht in Ihrem Browser zu speichern.
1. Suchen Sie in der oberen Suchleiste nach **`Microsoft Defender EASM`**.
1. Klicken Sie auf **Erstellen**.
1. Wählen Sie unter Microsoft Defender EASM-Ressource erstellen die vorhandene Ressourcengruppe **rg_eastus_soc**.
    >[!NOTE] Wenn die Ressourcengruppe rg_eastus_soc nicht aufgeführt ist, müssen Sie sie erneut erstellen, da beim Öffnen einer neuen Übungs-Instanz keine vorherige Arbeit erhalten bleibt.
1. In den Details der Instanz geben Sie den Namen **`EASM`** ein und wählen als Region **East US**.
1. Wählen Sie **Überprüfen + erstellen** aus.
1. Klicken Sie auf **Erstellen**.

Sie haben den Defender-EASM-Arbeitsbereich erfolgreich erstellt.

### Aufgabe 2 - Erstellen von Ermittlungen

In diesem Task erstellen Sie eine Ermittlung über die nach außen gerichteten Assets von Contoso Ltd. Nachdem Sie eine Instanz erstellt haben, müssen Sie sie mit aktuellen Daten füllen. Deshalb werden Sie jetzt eine Ermittlung erstellen.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
1. Suchen Sie in der Suchleiste oben nach **`Microsoft Defender EASM`** und öffnen Sie es.
1. Wählen Sie den **EASM**-Arbeitsbereich, den Sie in der letzten Aufgabe erstellt haben.
1. Suchen Sie nach **Contoso** im Suchfeld **Suche nach einer Organisation**.
1. Wählen Sie **Contoso Ltd.**.
1. Wählen Sie **Ermittlung der Angriffsoberfläche starten**.

Sie haben die Ermittlungen zur externen Angriffsfläche von Contoso erfolgreich durchgeführt und die EASM-Instanz mit verwertbaren Daten gefüllt.

### Aufgabe 3: Einrichten des Datenkonnektors und des Arbeitsbereichs für die Protokollanalyse

In diesem Task konfigurieren Sie eine Datenverbindung von Defender EASM zu einem Arbeitsbereich für die Protokollanalyse, der für Sentinel verwendet wird. Defender EASM-Ressourceninformationen oder -Erkenntnisse können in Log Analytics verwendet werden, um vorhandene Workflows mit anderen Sicherheitsdaten zu verbessern.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
1. Suchen Sie in der oberen Suchleiste nach **`Log Analytics Workspaces`**.
1. Wählen Sie ihren **Law-Sentinel** -Arbeitsbereich aus der letzten Übung aus.
    >[!NOTE] Wenn der Law-Sentinel-Arbeitsbereich nicht aufgelistet ist, müssen Sie ihn erneut erstellen, da beim Öffnen einer neuen Übungs-Instanz keine vorherige Arbeit erhalten bleibt. Siehe die Übung Security Operations Center, Teil 2, Aufgabe 1.
1. Lassen Sie die Seite unverändert, öffnen Sie eine weitere Registerkarte und melden Sie sich beim Azure-Portal an **`https://portal.azure.com`**.
1. Suchen Sie in der Suchleiste oben nach **`Microsoft Defender EASM`** und öffnen Sie es.
1. Wählen Sie Ihren **EASM**-Arbeitsbereich.
1. Erweitern Sie im linken Navigationsbereich **Verwalten** und wählen Sie **Datenverbindungen**.
1. Wählen Sie unter Log Analytics **Verbindung hinzufügen**.
1. Nennen Sie es **law-sentinel**
1. Wechseln Sie zur vorherigen Registerkarte mit dem Log Analytics-Arbeitsbereich, der geöffnet werden soll.
1. Erweitern Sie **Log Analytics agent-Anweisungen**.
1. Kopieren Sie die **Workspace-ID** in das entsprechende Feld des Fensters Datenverbindung hinzufügen.
1. Kopieren Sie den ** **Primärschlüssel** in das Feld API-Schlüssel des Fensters Datenverbindung hinzufügen.
1. Wählen Sie unter Inhalt **Alle**.
1. Wählen Sie unter Häufigkeit **Täglich**.
1. Wählen Sie **Hinzufügen**.
1. Die Log Analytics-Karte der Seite Datenverbindungen sollte nun law-sentinel unter Connected (1) aufgeführt sein.

Nachdem die Verbindung erstellt wurde, werden benutzerdefinierte Protokolltabellen im Log Analytics-Arbeitsbereich erstellt. In Sentinel können diese Daten dann verwendet werden, um Sicherheitsvorfälle zu erstellen oder zu bereichern, Untersuchungs-Playbooks zu erstellen, Machine Learning-Algorithmen zu trainieren oder Abhilfemaßnahmen auszulösen.

Sie haben die Verbindung zwischen Defender EASM und einem Log Analytics-Arbeitsbereich erfolgreich eingerichtet.

### Aufgabe 4 - Überprüfen von Dashboards und Kennzeichnen von Assets

In dieser Aufgabe überprüfen Sie die Sicherheitslage von Defender EASM und erhalten Informationen über die Ergebnisse.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
1. Suchen Sie in der Suchleiste oben nach **`Microsoft Defender EASM`** und öffnen Sie es.
1. Wählen Sie Ihren **EASM**-Arbeitsbereich.
1. Erweitern Sie im linken Navigationsbereich **Dashboards** und wählen Sie **Zusammenfassung der Angriffsfläche**. Die Attack Surface Summary-Dashboardsstellen stellen wichtige Erkenntnisse und eine Übersicht auf hoher Stufe über die betroffenen zentralen Assets Ihrer Angriffsfläche bereit.
1. Überprüfen Sie das Dashboard **Zusammenfassung der Angriffsfläche**.
1. Wählen Sie im linken Navigationsbereich **Sicherheitsstatus**.
1. Überprüfen Sie die unterschiedlichen Kategorien für offene Schwachstellen.
1. Wählen Sie unter der Kategorie **Offene Anschlüsse** die Option **Web-Server**.
1. Wählen Sie die gefundene IP-Adresse **34.223.124.45**.
1. Sie beschließen, das Asset für weitere Untersuchungen zu kennzeichnen.
1. Wählen Sie **Ressourcen ändern** aus.
1. Wählen Sie **Neue Bezeichnung erstellen**.
1. Nennen Sie es **Ports öffnen** und wählen Sie **Hinzufügen**.
1. Weisen Sie die neu erstellte Bezeichnung im Feld **Bezeichnungen** zu.
1. Wählen Sie **Aktualisieren**.

Sie haben den Sicherheitsstatus erfolgreich überprüft und eine Ressource zur weiteren Untersuchung gekennzeichnet.

### Aufgabe 5 - Verwalten von Ressourcen

In dieser Aufgabe verwalten und kategorisieren Sie die ermittelten Ressourcen.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **https://portal.azure.com**.
1. Suchen Sie in der Suchleiste oben nach **`Microsoft Defender EASM`** und öffnen Sie es.
1. Wählen Sie Ihren **EASM**-Arbeitsbereich.
1. Erweitern Sie im linken Navigationsbereich **Allgemein** und wählen Sie **Inventar**.
1. Auf der Seite EASM | Inventar ist die Registerkarte Suche ausgewählt (unterstrichen). Wählen Sie im Suchfeld aus dem Dropdownmenü **Bezeichnungen**
1. Wählen Sie im Dropdownmenü unten die Bezeichnung aus, die Sie kürzlich erstellt haben: **Ports öffnen**.
1. Wählen Sie **Suchen** aus.
1. Öffnen Sie die gefundene Ressource **34.223.124.45**.
1. Wählen Sie die Registerkarte **Webkomponenten**.
1. Sie stellen fest, dass dieser Ressource auf Amazon gehostet wird. Es gibt auch offene CVEs für einige der Komponenten, aber diese sind nicht aktiv, wie Sie in den Spalten **Aktuell** und **Zuletzt online** sehen können. Diese stammen aus früheren Ermittlungsläufen.
Da diese Ressource von einem Dritten gehostet wird, aber dennoch zu Ihrer Angriffsfläche gehört, kategorisieren Sie sie auf der Grundlage ihrer Rolle in Ihrer Organisation.
1. Wählen Sie **Ressourcen ändern** aus.
1. Verwenden Sie im Fenster Asset ändern das Dropdown-Feld **Status**, um **Abhängigkeit** auszuwählen.
1. Wählen Sie **Aktualisieren**.
    >[!NOTE]In diesem Fall wählen Sie Abhängigkeit, da es sich um eine Infrastruktur handelt, die sich im Besitz eines Dritten befindet, aber Teil Ihrer Angriffsfläche ist, da sie den Betrieb Ihrer eigenen Anlagen direkt unterstützt.
1. Kehren Sie zurück zum Inventar, indem Sie oben rechts **X** wählen und eine neue Suche erstellen.
1. Ändern Sie die Suchanfrage in **Webkomponentenname - enthält - Amazon**.
1. Wählen Sie **Suchen** aus.
1. Wählen Sie alle Ressourcen aus.
1. Wählen Sie **Ressourcen ändern** aus.
1. Wählen Sie **Abhängigkeit** in Status und wählen Sie **Aktualisieren**.

Nur wenn der Status auf **Genehmigtes Inventar** eingestellt ist, werden die Anlagen in Dashboard-Diagrammen dargestellt und täglich durchsucht. Aus diesem Grund ist es wichtig, neu entdeckte Ressourcen zu überprüfen und ihren Zustand entsprechend zu ändern.

Im Rahmen dieser Übung haben Sie Defender EASM eingerichtet, die Erkennung der nach außen gerichteten Umgebung von Contoso erstellt, einen tieferen Einblick in die Ressourcen und ihre Konfiguration erhalten und die Ressourcen so verwaltet, dass die Dashboards nur Daten enthalten, für die Contoso direkt verantwortlich ist.
