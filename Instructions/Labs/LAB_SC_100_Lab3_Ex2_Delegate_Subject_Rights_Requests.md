---
lab: 3
title: Übung 2 – Delegieren von Anfragen zu Betroffenenrechten
---


# Lab 3 – Übung 2 – Delegieren von Anfragen zu Betroffenenrechten

Contoso Ltd. bereitet sich auf die ISO-27001-Zertifizierung vor. Im Rahmen dieser Vorbereitung müssen sie einen Prozess für Anfragen zu Betroffenenrechten der DSGVO implementieren. Das Unternehmen wird Microsoft Priva Subject Rights Requests nutzen und den neuen Workflow in seinen internen Compliance-Überprüfungsprozess integrieren. 

Als für Fachkraft für Cybersecurity-Architektur delegieren Sie die Bearbeitung europäischer DSRs und richten Leseberechtigungen für die Überwachung ein. Um sicherzustellen, dass Mitarbeitende, die DSR-Fälle bearbeiten, nicht auch die Funktion „Datenschutzrisikomanagement“ bearbeiten, erstellen Sie eine benutzerdefinierte Rollengruppe mit Lesezugriff. Die integrierten Rollengruppen gewähren zu viele Berechtigungen für die Überprüfung. 

Sie weisen den ausgewählten Mitarbeitenden die erforderlichen Rollen für die Bearbeitung von Anfragen zu Themenrechten oder Überprüfungen zu und befolgen dabei das Prinzip der geringsten Privilegien. Um das Proof of Concept abzuschließen, verwenden Sie die Microsoft Priva-Testversion und stellen sicher, dass Überprüfungsprotokolle in Ihrem Mandanten aktiviert sind. Da die Konformitätsprüfung alle zwei Monate stattfindet, sollten Sie die Aufbewahrungsdauer für Anträge auf Rechteeinräumung erhöhen, um etwaige Lücken zwischen den Überprüfungen zu schließen. 

## Teil 1: Entwerfen einer Lösung (erforderlich)

Bei dieser Aufgabe entwerfen Sie ein Konzept für die Anforderungen von Contoso Ltd. mit ihrer Expansion in Europa.

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage des beschriebenen Szenarios zu analysieren, die Ziele zu verstehen und die Anforderungen zu definieren.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Aktivieren Ihrer Umgebung zum Behandeln von Anträgen betroffener Personen.
- Ein bestimmtes Team muss Anträge betroffener Personen verarbeiten.
- Aufbewahrungsfristen von Anträgen betroffener Personen müssen geändert werden, um den Prüfzeitplan einzuhalten.

Im zweiten Schritt untersuchen Sie die vorhandene Umgebung von Contoso Ltd.. Microsoft Priva bietet Lösungen zum Verwalten von Anfragen betroffener Personen. Untersuchen Sie, welche Kontrollen bestehen und welche Richtlinien bereits eingesetzt werden. Verwenden Sie das Microsoft Purview Compliance-Portal, um aktuelle Konfigurationen zu überprüfen und zu bestimmen, welche Anpassungen implementiert werden müssen, um die Anforderungen für die Region zu erfüllen, auf die sie erweitert werden.

In der dritten Phase wird das Konzept der Lösung erarbeitet. Nach einer Untersuchung ist es offensichtlich, dass die Möglichkeit für bestimmte Mitarbeitende, DSRs zu verwalten, der beste Weg ist, um alle Anforderungen zu erfüllen.  

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Aktivieren Ihrer Umgebung zum Behandeln von Anträgen betroffener Personen.|Microsoft Purview und Admin Center|Zuweisen von Priva-Lizenzen und Überprüfen, ob das einheitliche Überwachungsprotokoll aktiviert ist|
|Ein bestimmtes Team muss Anträge betroffener Personen verarbeiten.|Microsoft Purview-Rollen|Erstellen einer Rollengruppe mit Berechtigungen zum Behandeln von DSRs und Zuweisen der vorgesehenen Mitarbeitenden|
|Aufbewahrungsfristen von Anträgen betroffener Personen müssen geändert werden, um den Prüfzeitplan einzuhalten.|Microsoft Purview-Datenschutz-Risikomanagement|Verwenden einer Verbesserungsmaßnahme zum Festlegen eines Aufbewahrungsgrenzwerts von 90 Tagen für DSRs|

## Teil 2: Implementieren der Lösung (optional)

## Aufgabe 1 – Aktivieren der Microsoft Priva-Testlizenz

In den ersten beiden Aufgaben überprüfen Sie die erforderlichen Voraussetzungen für die Verwendung der Microsoft Priva-Features. Sie müssen die Microsoft Priva-Testlizenz aktivieren und sicherstellen, dass Überwachungsprotokolle in Ihrem Mandanten aktiviert sind.

1. Melden Sie sich mit Ihren Admin-Anmeldedaten bei der **VM** an.
2. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste aus, navigieren Sie zu **https://compliance.microsoft.com** und melden Sie sich beim Microsoft Purview Compliance-Portal als **MOD Admin**admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandant-ID ist, die Sie von Ihrem Lab-Hosting-Anbieter erhalten haben). Das Kennwort für Admins** sollte Ihnen von Ihrem Lab-Hosting-Anbieter mitgeteilt werden.
3. Wenn Sie gefragt werden, ob Sie angemeldet bleiben möchten, wählen Sie **Nein** aus.
4. Wählen Sie im linken Bereich entweder **Datenschutzrisikomanagement – Übersicht** oder **Anträgen betroffener Personen** aus.
5. Wenn die Testversion nicht aktiv ist, aktivieren Sie **die Testversion** oben auf der Seite.

Wenn die Testversion bereits in Ihrem Lab aktiv ist, müssen Sie dennoch die genaue Anzahl der Anfragen an Antragstellerrechte überprüfen, die in Ihrer Lizenz im Admin Center enthalten sind.

6. **Melden Sie sich** beim **Microsoft 365 Admin Center****https://admin.microsoft.com/** an.
7. Wählen Sie im linken Bereich **Abrechnung** und **Ihre Produkte**.
8. Suchen Sie nach der Lizenz **Priva Privacy Risk Management**.
9. Achten Sie auf die Lizenz **Datenschutzmanagement - Bearbeitung von Anträgen betroffener Personen** und wie viele Fälle enthalten sind.

Sie haben erfolgreich überprüft, ob Ihr M365 Mandant über aktive Microsoft Priva-Lizenzen verfügt.

## Aufgabe 2 - Überprüfen, ob Überwachungsprotokolle aktiviert sind

Damit die Funktionen zur Verwaltung des Datenschutzrisikos funktionieren, muss die Überwachungsprotokollierung in Ihrem Mandanten aktiv sein.

1. Öffnen Sie ein erhöhtes **PowerShell**-Fenster, indem Sie das Startmenü mit der rechten Maustaste auswählen und dann **Windows PowerShell** und **als Administrator ausführen** wählen.
2. Geben Sie das folgende Cmdlet ein, um die neueste Version des Exchange Online-Moduls zu installieren:
    ```powershell
    Install-Module -Name ExchangeOnlineManagement
    ```
3. Bestätigen Sie den Nuget-Sicherheitsdialog und den Sicherheitsdialog des nicht vertrauenswürdigen Repositorys mit Y für Ja und drücken Sie die EINGABETASTE. Es kann eine Weile dauern, bis der Vorgang abgeschlossen ist.
4. Geben Sie das folgende Cmdlet ein, um eine Verbindung mit dem Exchange Online-Dienst herzustellen:
    ```powershell
    Connect-ExchangeOnline
    ```
5. Melden Sie sich im Formular **Anmelden in Ihrem Konto** mit Ihren Anmeldeinformationen als Administrator an.
6. Nach erfolgreicher Verbindung mit Exchange Online PowerShell geben Sie Folgendes ein:
    ```powershell
    Get-AdminAuditLogConfig | Format-List UnifiedAuditLogIngestionEnabled
    ```
7. Ein **True**-Wert für _UnifiedAuditLogIngestionEnabled_ wird zurückgegeben.
8. Wenn der Wert **Falsch** zurückgegeben wird, aktivieren Sie das Überwachungsprotokoll mit dem Befehl:
    ```powershell
    Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true
    ```
9. Es wird eine Warnung ausgegeben, dass es bis zu 60 Minuten dauern kann, bis die Änderung wirksam wird. Das Überwachungsprotokoll ist jetzt in Ihrem Mandanten aktiviert. Sie können dies später mit dem oben genannten Befehl erneut überprüfen.

Sie haben erfolgreich bestätigt, dass die Überwachungsprotokolle in Ihrem Mandanten aktiviert sind.

## Aufgabe 3 - Erstellen Sie eine benutzerdefinierte Rollengruppe und weisen Sie ihr die gewünschten mitarbeitenden Personen zu.

In dieser Aufgabe erstellen Sie die benutzerdefinierte, schreibgeschützte Rollengruppe für die Contoso Ltd. Konformitätsprüfung und weisen die dafür vorgesehenen mitarbeitenden Personen zu.

1. Melden Sie sich beim **Microsoft Purview Compliance Portal****https://compliance.microsoft.com/** an.
2. Wählen Sie die Registerkarte **Berechtigungen** unter der Registerkarte **Rollen & Geltungsbereiche** im linken Bereich.
3. Wählen Sie **Rollen** unter dem Element Microsoft Purview-Lösungen.
4. Erstellen Sie eine neue Rollengruppe mit den folgenden Einstellungen:
    |Einstellung|Wert|
    |----|----|
    |Name|Interne Prüfung der Konformität (Schreibgeschützt)|
    |Beschreibung|Diese Rollengruppe enthält alle Rollen, die für die zweimonatliche Prüfung der Konformität von Contoso Ltd.|
    |Rollen|Schreibgeschützte Überwachungsprotokolle, Schreibgeschützter Fall, Priva Management-Viewer|
    |Benutzer|Grady Archie|
5. Wählen Sie **Weiter** auf der Seite **Rollen zur Rollengruppe hinzufügen** und fahren Sie mit der nächsten Aufgabe fort, ohne den Dialog zu schließen.

Sie haben erfolgreich eine benutzerdefinierte Rollengruppe mit den erforderlichen Mindestberechtigungen erstellt und ihr die vorgesehenen mitarbeitenden Personen zugewiesen.

## Aufgabe 4 - Weisen Sie mitarbeitende Personen und sich selbst den integrierten Rollengruppen zu

Nun müssen Sie mithilfe der integrierten Rollengruppen die verbleibenden Berechtigungen für die Verwaltung von Anforderungen für Subjektrechte zuweisen.

*(Springen Sie zu 4., wenn Sie sich noch im Menü Rollen & Geltungsbereiche befinden)*
1. **Melden Sie sich** beim **Microsoft Purview Compliance-Portal****https://compliance.microsoft.com/** an.
2. Wählen Sie **Rollen & Geltungsbereiche** > **Berechtigungen** im linken Bereich.
3. Wählen Sie **Rollen** unter dem Element **Microsoft Purview-Lösungen**.
4. Fügen Sie **Irvin Sayers** zur Rollengruppe  **Administratoren für Antragstellerrechte anfordern** hinzu.
5. Fügen Sie **Alex Wilber** und **Joni Sherman** zur Rollengruppe **Genehmigende Antragsteller anfordern** hinzu.
6. Fügen Sie Ihr Administratorkonto **MOD-Administrator** und **Megan Bowen** zu den Rollengruppen **Administratoren für die Verwaltung der Privatsphäre** und **Administratoren für die Anforderung von Subjektrechten** hinzu.

Sie haben nun allen mitarbeitenden Personen alle erforderlichen Berechtigungen zugewiesen, um Anforderungen zu verarbeiten.

## Aufgabe 5 - Konfigurieren Sie die Höchstgrenze für die Datenspeicherung bei Anforderungen von Betroffenenrechten

Für die zweimonatliche Prüfung der Konformität müssen Sie in dieser Aufgabe die Aufbewahrungsfrist für Anforderungen zu den Rechten der Betroffenen konfigurieren.

[!NOTE] Es kann bis zu 30 Minuten dauern, bis Die Rollengruppenänderungen angewendet werden, die Sie zum Anzeigen der Funktion für Anträge betroffener Rechte benötigen. Wenn Sie sich die Berechtigungen erst in Aufgabe 4 erteilt haben, müssen Sie möglicherweise warten, bis die Änderungen wirksam werden.

1. **Melden Sie sich** beim **Microsoft Purview Compliance-Portal****https://compliance.microsoft.com/** an.
2. Wählen Sie im linken Fensterbereich **Compliance Manager** und dann die Registerkarte **Verbesserungsaktionen**.
3. Wählen Sie oben auf der Seite den Filter **Lösungen:** und markieren Sie **Priva Privacy Risk Management** und **Priva Subject Rights Requests**.
4. Wählen Sie **Datenaufbewahrung für Daten aktivieren und durchsetzen, die von einer Anfrage zu den Rechten des Betroffenen betroffen sind**.
5. Klicken Sie auf **Benutzer zuweisen** > Suchen Sie nach **MOD-Administrator** > **Zuweisen**, wodurch MOD-Admin als Besitzer der Verbesserungsaktion zugewiesen wird.
6. Lesen Sie die Details der Verbesserung.
7. Wählen Sie **Jetzt starten** unten in der Beschreibung aus, um direkt die Einstellungen für die Anforderung von Antragstellerrechten einzugeben.
8.  Wählen Sie die Registerkarte **Datenaufbewahrungsfristen**.
9.  Legen Sie den Wert **Datenerfassung und Berichte** auf 90 Tage fest und wählen Sie **Speichern**.
10. Schließen Sie die Registerkarte in Edge.
11. Wählen Sie **Details bearbeiten** am oberen Rand der Seite der Verbesserungsaktion.
12. Legen Sie den **Implementierungsstatus** auf **Implementiert** fest.
13. Wählen Sie anschließend **Speichern und schließen** oben auf der Seite.

Sie haben die Datenaufbewahrungsgrenze für Anträge betroffener Personen erfolgreich erhöht und die Verbesserungsaktionen aktualisiert.

Sie haben die Einrichtung des Features für Anträge betroffener Personen und delegierte Behandlungsfälle entsprechend abgeschlossen. Sie können mit der nächsten Übung fortfahren.
