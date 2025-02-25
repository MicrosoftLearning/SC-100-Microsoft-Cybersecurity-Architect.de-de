# Lab 1 – Übung 2 – Verwalten der externen Angriffsfläche

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
2. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **<https://portal.azure.com>** und melden Sie sich im Azure-Portal als benutzende Person <user1-ZZZZZZZ@LODSUATMCA.onmicrosoft.com> an. Das Passwort der administrierenden Person sollte von Ihrem Lab-Hosting-Anbieter bereitgestellt werden.
3. Aktivieren Sie im Dialogfeld Angemeldet bleiben? das Kontrollkästchen Dies nicht mehr anzeigen und wählen Sie dann Nein.
4. Schließen Sie den Dialog zum Speichern von Passwörtern von unten, indem Sie **Nie** wählen, um die Standard-Anmeldeinformationen für globale Administrierende nicht in Ihrem Browser zu speichern.
5. Suchen Sie in der oberen Suchleiste nach **Microsoft Defender EASM**.
6. Klicken Sie auf **Erstellen**.
7. Wählen Sie unter Microsoft Defender EASM-Ressource erstellen die vorhandene Ressourcengruppe **rg_eastus_soc**.
8. Geben Sie in den Instanzdetails den Namen **EASM** ein und wählen Sie **USA, Osten** als Region aus.
9. Wählen Sie **Überprüfen + erstellen** aus.
10. Klicken Sie auf **Erstellen**.

Sie haben den Defender-EASM-Arbeitsbereich erfolgreich erstellt.

### Aufgabe 2 - Erstellen von Ermittlungen

In diesem Task erstellen Sie eine Ermittlung über die nach außen gerichteten Assets von Contoso Ltd. Nachdem Sie eine Instanz erstellt haben, müssen Sie sie mit aktuellen Daten füllen. Deshalb werden Sie jetzt eine Ermittlung erstellen.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **<https://portal.azure.com>**.
2. Suchen Sie in der Suchleiste oben nach **Microsoft Defender EASM** und öffnen Sie es.
3. Wählen Sie den **EASM**-Arbeitsbereich, den Sie in der letzten Aufgabe erstellt haben.
4. Suchen Sie nach **Contoso** im Suchfeld **Suche nach einer Organisation**.
5. Wählen Sie **Contoso Ltd.**.
6. Wählen Sie **Ermittlung der Angriffsoberfläche starten**.

Sie haben die Ermittlungen zur externen Angriffsfläche von Contoso erfolgreich durchgeführt und die EASM-Instanz mit verwertbaren Daten gefüllt.

### Aufgabe 3: Einrichten des Datenkonnektors und des Arbeitsbereichs für die Protokollanalyse

In diesem Task konfigurieren Sie eine Datenverbindung von Defender EASM zu einem Arbeitsbereich für die Protokollanalyse, der für Sentinel verwendet wird. Defender EASM-Ressourceninformationen oder -Erkenntnisse können in Log Analytics verwendet werden, um vorhandene Workflows mit anderen Sicherheitsdaten zu verbessern.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **<https://portal.azure.com>**.
2. Suchen Sie in der oberen Suchleiste nach **Log Analytics-Arbeitsbereiche**.
3. Wählen Sie ihren **Law-Sentinel** -Arbeitsbereich aus der letzten Übung aus.
4. Erweitern Sie im linken Navigationsbereich die **Einstellungen** und wählen Sie **Agents** aus.
5. Lassen Sie die Seite unverändert, öffnen Sie eine weitere Registerkarte und melden Sie sich beim Azure-Portal an **<https://portal.azure.com>**.
6.  Suchen Sie in der Suchleiste oben nach **Microsoft Defender EASM** und öffnen Sie es.
7.  Wählen Sie Ihren **EASM**-Arbeitsbereich.
8.  Erweitern Sie im linken Navigationsbereich **Verwalten** und wählen Sie **Datenverbindungen**.
9.  Wählen Sie unter Log Analytics **Verbindung hinzufügen**.
10. Nennen Sie es **law-sentinel**
11. Wechseln Sie zur vorherigen Registerkarte mit dem Log Analytics-Arbeitsbereich, der geöffnet werden soll.
12. Erweitern Sie **Log Analytics agent-Anweisungen**.
13. Kopieren Sie die **Workspace-ID** und den **Primärschlüssel** in das entsprechende Feld in Defender EASM – Datenverbindung hinzufügen.
14. Wählen Sie unter Inhalt **Alle**.
15. Wählen Sie unter Häufigkeit **Täglich**.
16. Wählen Sie **Hinzufügen**.

Nachdem die Verbindung erstellt wurde, werden benutzerdefinierte Protokolltabellen im Log Analytics-Arbeitsbereich erstellt. In Sentinel können diese Daten dann verwendet werden, um Sicherheitsvorfälle zu erstellen oder zu bereichern, Untersuchungs-Playbooks zu erstellen, Machine Learning-Algorithmen zu trainieren oder Abhilfemaßnahmen auszulösen.

Sie haben die Verbindung zwischen Defender EASM und einem Log Analytics-Arbeitsbereich erfolgreich eingerichtet.

### Aufgabe 4 - Überprüfen von Dashboards und Kennzeichnen von Assets

In dieser Aufgabe überprüfen Sie die Sicherheitslage von Defender EASM und erhalten Informationen über die Ergebnisse.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **<https://portal.azure.com>**.
2. Suchen Sie in der Suchleiste oben nach **Microsoft Defender EASM** und öffnen Sie es.
3. Wählen Sie Ihren **EASM**-Arbeitsbereich.
4. Erweitern Sie im linken Navigationsbereich **Dashboards** und wählen Sie **Zusammenfassung der Angriffsfläche**.

Die Attack Surface Summary-Dashboardsstellen stellen wichtige Erkenntnisse und eine Übersicht auf hoher Stufe über die betroffenen zentralen Assets Ihrer Angriffsfläche bereit.

5. Überprüfen Sie das Dashboard **Zusammenfassung der Angriffsfläche**.
6. Wählen Sie im linken Navigationsbereich **Sicherheitsstatus**.
7. Überprüfen Sie die unterschiedlichen Kategorien für offene Schwachstellen.
8. Wählen Sie unter der Kategorie **Offene Anschlüsse** die Option **Web-Server**.
9.  Wählen Sie die gefundene IP-Adresse **34.223.124.45**.

Sie beschließen, das Asset für weitere Untersuchungen zu kennzeichnen.

10. Wählen Sie **Ressourcen ändern** aus.
11. Wählen Sie **Neue Bezeichnung erstellen**.
12. Nennen Sie es **Ports öffnen** und wählen Sie **Hinzufügen**.
13. Weisen Sie die neu erstellte Bezeichnung im Feld **Bezeichnungen** zu.
14. Wählen Sie **Aktualisieren**.

Sie haben den Sicherheitsstatus erfolgreich überprüft und eine Ressource zur weiteren Untersuchung gekennzeichnet.

### Aufgabe 5 - Verwalten von Ressourcen

In dieser Aufgabe verwalten und kategorisieren Sie die ermittelten Ressourcen.

1. Sie sollten immer noch im Azure-Portal angemeldet sein **<https://portal.azure.com>**.
2. Suchen Sie in der Suchleiste oben nach **Microsoft Defender EASM** und öffnen Sie es.
3. Wählen Sie Ihren **EASM**-Arbeitsbereich.
4. Erweitern Sie im linken Navigationsbereich **Allgemein** und wählen Sie **Inventar**.
5. Wählen Sie im Dropdownmenü unter „Suchen“ die Option **Bezeichnung** aus.
6. Wählen Sie im Dropdownmenü unten die Bezeichnung aus, die wir kürzlich in Aufgabe 4 **Offene Ports** erstellt haben.
7. Wählen Sie **Suchen** aus.
8. Öffnen Sie die gefundene Ressource **34.223.124.45**.
9. Wählen Sie die Spalte **Webkomponenten** aus.

Sie stellen fest, dass dieser Ressource auf Amazon gehostet wird. Es gibt auch offene CVEs für einige der Komponenten, aber diese sind nicht aktiv, wie Sie in den Spalten **Aktuell** und **Zuletzt online** sehen können. Diese stammen aus früheren Ermittlungsläufen.
Da diese Ressource von einem Dritten gehostet wird, aber dennoch zu Ihrer Angriffsfläche gehört, kategorisieren Sie sie auf der Grundlage ihrer Rolle in Ihrer Organisation.

10. Wählen Sie **Ressourcen ändern** aus.
11. Wählen Sie **Abhängigkeit** aus.
12. Wählen Sie **Aktualisieren**.

>[!NOTE]In diesem Fall wählen Sie Abhängigkeit, da es sich um eine Infrastruktur handelt, die sich im Besitz eines Dritten befindet, aber Teil Ihrer Angriffsfläche ist, da sie den Betrieb Ihrer eigenen Anlagen direkt unterstützt.

13. Kehren Sie zurück zum Inventar, indem Sie oben rechts **X** wählen und eine neue Suche erstellen.
14. Ändern Sie die Suchanfrage in **Webkomponentenname - enthält - Amazon**.
15. Wählen Sie **Suchen** aus.
16. Wählen Sie alle Ressourcen aus.
17. Wählen Sie **Ressourcen ändern** aus.
18. Wählen Sie **Abhängigkeit** in Status und wählen Sie **Aktualisieren**.

Nur wenn der Status auf **Genehmigtes Inventar** eingestellt ist, werden die Anlagen in Dashboard-Diagrammen dargestellt und täglich durchsucht. Aus diesem Grund ist es wichtig, neu entdeckte Ressourcen zu überprüfen und ihren Zustand entsprechend zu ändern.

Im Rahmen dieser Übung haben Sie Defender EASM eingerichtet, die Entdeckung der Außenumgebung von Contoso erstellt, einen tieferen Einblick in die Vermögenswerte und deren Konfiguration erhalten und die Vermögenswerte so verwaltet, dass die Dashboards nur Daten enthalten, für die Contoso direkt verantwortlich ist.
