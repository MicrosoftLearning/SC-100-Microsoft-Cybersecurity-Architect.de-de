---
lab: 3
title: Übung 4 – Vertraulichkeitsbezeichnungen
---

# Lab 3 – Übung 4 – Vertraulichkeitsbezeichnungen

Contoso Ltd. ist dabei, Tailwind Traders zu übernehmen. Die Geschäftsführung hat beschlossen, alle Dokumente in diesem Prozess streng vertraulich zu behandeln, um das Risiko eines Datenlecks zu minimieren.

Sie haben die folgenden Sicherheitsanforderungen für das Etikett erhalten:

- Inhalte dürfen nur an interne mitarbeitende Personen von Contoso Ltd. weitergegeben werden.
- Inhalte müssen verschlüsselt werden.
- Dateien und E-Mails werden möglicherweise nicht weitergeleitet.
- Der Zugriff auf Inhalte von Nicht-Unternehmensgeräten ist verboten.
- Der Geltungsbereich dieses Etiketts ist das Management.

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept, um die Probleme zu beheben, denen Contoso Ltd. gegenübersteht.

### Entwurfsansatz

Contoso hat mehrere Lösungen zum Schutz seiner Daten im Einsatz. Ihr initialer Ansatz wäre, die momentane Einrichtung zu analysieren und zu entscheiden, ob sie den erforderlichen Anforderungen entspricht. 

Basierend auf dem obigen Szenario kann Microsoft Purview Information Protection verwendet werden, um die erforderlichen Anforderungen zu erfüllen und die Daten angemessen zu schützen. Die Vertraulichkeitsbezeichnungen von Microsoft Purview Information Protection stärken Sie bei der Klassifizierung und dem Schutz der Daten Ihres Unternehmens und stellen gleichzeitig sicher, dass die Produktivität der Benutzenden und die Funktionen zur Zusammenarbeit nicht beeinträchtigt werden. 

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Verschlüsseln von Dokumenten und Mails|Microsoft Purview Information Protection|Bereitstellen einer Vertraulichkeitsbezeichnung|
|Einschränkung des Zugriffs auf Daten von nicht verwalteten Geräten|Microsoft Purview Information Protection|Bereitstellung einer Vertraulichkeitsbezeichnung|
|Zugriff nur auf interne Benutzender beschränken|Microsoft Purview Information Protection|Bereitstellung einer Vertraulichkeitsbezeichnung

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1: Untersuchung der bestehenden Vertraulichkeitsbezeichnungen

In dieser Aufgabe werden Sie bestehende Vertraulichkeitsbezeichnungen untersuchen und entscheiden, ob eine neue Kennzeichnung erstellt werden muss.

>[!NOTE] Sie sollten das Exchange Online PowerShell-Modul bereits installiert haben. Wenn das Modul fehlt, befolgen Sie die Anweisungen zum Installieren des Moduls.

1. Öffnen Sie ein erweitertes PowerShell-Fenster, indem Sie mit der rechten Maustaste auf die Schaltfläche Windows klicken und dann **Windows PowerShell (Admin)** wählen.
1. Bestätigen Sie das Fenster **Benutzerkontensteuerung** mit **Ja**.
1. Geben Sie das folgende Cmdlet ein, um die neueste Version des Exchange Online PowerShell-Moduls zu installieren:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Bestätigen Sie den Sicherheitsdialog für das nicht vertrauenswürdige Repository mit **Y** für Ja und drücken Sie **Eingabe**.  Dieser Vorgang nimmt einige Zeit in Anspruch.
1. Geben Sie das folgende Cmdlet ein, um eine Verbindung mit Security & Compliance PowerShell herzustellen:

    ```powershell
    Connect-IPPSSession
    ```
1. Wenn das Fenster **Anmelden** angezeigt wird, melden Sie sich als `admin@WWLxZZZZZZ.onmicrosoft.com` an (wobei ZZZZZZ Ihre eindeutige, von Ihrem Labor-Hosting-Anbieter bereitgestellte Mandanten-ID ist) und verwenden Sie das administrative Kennwort für Ihren Mandanten.
1. Geben Sie das folgende Cmdlet ein, um eine Liste aller bereitgestellten Vertraulichkeitsbezeichnungen abzurufen

    ```powershell
    Get-Label | Format-Table -wrap ParentLabelDisplay,DisplayName,LabelActions
    ```
Dieses Cmdlet zeigt Ihnen alle bereitgestellten Vertraulichkeitsbezeichnungen und die entsprechenden Aktionen an. Prüfen Sie die Kennzeichnungen. Entscheiden Sie, ob die vorhandenen Kennzeichnungen den geschäftlichen Anforderungen entsprechen oder ob eine neue Kennzeichnung erforderlich ist. Wenn Sie das beendet haben, fahren Sie mit der nächsten Aufgabe fort.

### Aufgabe 2: Aktivieren der Unterstützung von Vertraulichkeitsbezeichnungen für Gruppen und Websites

In einer früheren Aufgabe haben Sie die vorhandenen Kennzeichnungen überprüft und sind zu dem Schluss gekommen, dass die derzeit vorhandenen Kennzeichnungen nicht den erforderlichen Anforderungen des Unternehmens entsprechen. Um Vertraulichkeitsbezeichnungen auf Gruppen und Standorte anzuwenden, müssen Sie den Kundendienst für Vertraulichkeitsbezeichnungen in PowerShell aktivieren.

1. Öffnen Sie ein erweitertes PowerShell-Fenster, indem Sie das Startmenü mit der rechten Maustaste auswählen und dann Windows PowerShell auswählen und als Administrator ausführen wählen.
1. Bestätigen Sie das Fenster Benutzerkontensteuerung mit Ja.
1. Zuerst müssen wir das Microsoft Graph PowerShell SDK installieren. Da es in zwei Modulen, Microsoft.Graph und Microsoft.Graph.Beta, enthalten ist, müssen wir beide installieren. Geben Sie das folgende Cmdlet ein, um die neueste Version von Microsoft.Graph zu installieren:

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```
1. Bestätigen Sie den Nuget-Sicherheitsdialog und den Sicherheitsdialog des nicht vertrauenswürdigen Repositorys mit Y für Ja und drücken Sie die EINGABETASTE. Es kann eine Weile dauern, bis der Vorgang abgeschlossen ist.
1. Geben Sie das folgende Cmdlet ein, um Microsoft.Graph.Beta zu installieren:

```powershell
Install-Module Microsoft.Graph.Beta -Scope CurrentUser
```
1. Bestätigen Sie das Fenster Benutzerkontensteuerung mit Ja.
1. Verbinden Sie sich mit dem Mandanten:

```powershell
Connect-MgGraph -Scopes "Directory.ReadWrite.All"
```

1. Melden Sie sich in dem Formular Anmelden bei Ihrem Konto als admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandant-ID ist, die Sie von Ihrem Anbieter des Labor-Hostings bereitstellen). Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Im Fenster **Angeforderte Genehmigungen** wählen Sie **Zustimmung im Namen Ihrer Organisation** und wählen Sie **Annehmen**. Wählen Sie nach der Anmeldung das PowerShell-Fenster.
1. Geben Sie das folgende Cmdlet ein, um Vertraulichkeitsbezeichnungen zu aktivieren:

```powershell
$params = @{
     Values = @(
        @{
            Name = "EnableMIPLabels"
            Value = "True"
        }
     )
}

Update-MgBetaDirectorySetting -DirectorySettingId $grpUnifiedSetting.Id -BodyParameter $params
```

1. Schließen Sie das PowerShell-Fenster.

Sie haben erfolgreich den Kundendienst für Vertraulichkeitsbezeichnungen für Gruppen und Standorte aktiviert.

### Aufgabe 3: Erstellen und Bereitstellen einer Vertraulichkeitsbezeichnung mit hohem Sicherheitsniveau

Sie werden eine neue Vertraulichkeitsbezeichnung erstellen, um die erforderlichen Anforderungen zu erfüllen.

1. Melden Sie sich beim Microsoft Purview Compliance Portal **https://compliance.microsoft.com/** als Allan Deyoung mithilfe seines Administratorkontos **MOD Administrator** an.
1. Erweitern Sie im Microsoft Purview-Portal im linken Navigationsbereich **Informationsschutz** und wählen Sie dann **Kennzeichnungen**.
1. Auf der Seite **Kennzeichnungen** wählen Sie **+ Eine Kennzeichnung erstellen**.
1. Auf der Seite **Basisdetails für diese Kennzeichnung bereitstellen** geben Sie die folgenden Informationen ein:

    - **Name**: Vertraulich - Akquisitionsprozess
    - **Name anzeigen**: Vertraulich - Akquisitionsprozess
    - **Beschreibung für Benutzende**: Streng vertrauliche Daten im Zusammenhang mit einem Akquisitionsprozess.
    - **Beschreibung für Administratoren**: Diese Kennzeichnung stellt einen Schutz für alle Daten bereit, die im Zusammenhang mit einem Erwerb von Contoso stehen.

1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Definieren Sie den Geltungsbereich für diese Kennzeichnung** die Option **Elemente** und wählen Sie **Dateien**, **E-Mails** und **Gruppen & Sites**. Wenn andere Optionen auf dieser Seite ausgewählt sind, heben Sie die Auswahl dieser Optionen auf.
1. Wählen Sie auf der Seite **Schutzeinstellungen für bezeichnete Elemente festlegen** die Option **Verschlüsselung applizieren oder entfernen**.
1. Auf der Seite **Verschlüsselung** wählen Sie **Verschlüsselungseinstellungen konfigurieren**.
1. Geben Sie die folgenden Informationen in die Verschlüsselungseinstellungen ein: 
    - **Berechtigungen jetzt zuweisen oder die Benutzenden entscheiden lassen?**: Lassen Sie die Benutzenden die Berechtigungen zuweisen, wenn sie die Kennzeichnung applizieren.
    - **Erzwingen Sie in Outlook eine der folgenden Einschränkungen**: Nicht weiterleiten.
1. Wählen Sie **Benutzende in Word, PowerPoint und Excel zur Angabe von Berechtigungen auffordern** und wählen Sie dann **Weiter**.
1. Wählen Sie auf der Seite **Automatische Bezeichnung für Dateien und E-Mails** **Weiter**.
1. Wählen Sie auf der Seite **Schutzeinstellungen für Gruppen und Sites festlegen** die Optionen **Datenschutz und Zugriff externer Benutzender** und **Externe Freigabe und bedingter Zugriff** aus und wählen Sie dann **Weiter** aus.
1. Auf der Seite **Einstellungen für Datenschutz und Zugriff externer Benutzender** wählen Sie **Privat** und dann **Weiter**.
1. Wählen Sie auf der Seite **Einstellungen für externe Freigabe und bedingten Zugriff definieren** die Optionen **Externe Freigabe von gekennzeichneten SharePoint-Sites kontrollieren** und **Microsoft Entra Conditional Access verwenden, um gekennzeichnete SharePoint-Sites zu schützen** und legen Sie die Konfiguration wie folgt fest:
    - **Inhalt kann freigegeben werden für**: Nur Personen in Ihrer Organisation
    - **Ermitteln, ob Benutzende von nicht verwalteten Geräten auf SharePoint-Sites zugreifen können**: Zugriff blockieren
1. Wählen Sie **Weiter** aus.
1. Auf der Seite **Automatische Kennzeichnung für schematisierte Assets (Vorschau)** wählen Sie **Weiter**.
1. Wählen Sie auf der Seite **Überprüfen Sie Ihre Einstellungen und beenden Sie** die Option **Kennzeichnung erstellen**.
1. Auf der Seite **Ihre Vertraulichkeitsbezeichnung wurde erstellt** wählen Sie als nächsten Schritt **Kennzeichnung in den Apps der Benutzenden veröffentlichen**.
1. Wählen Sie **Fertig** aus.
1. Wählen Sie auf der Seite **Kennzeichnung veröffentlichen** die Option **Erstellen Sie eine neue Bezeichnungsrichtlinie**.
1. Auf der Seite **Wählen Sie die zu veröffentlichende Vertraulichkeitsbezeichnung** wählen Sie die soeben erstellte Kennzeichnung aus und wählen **Weiter**.
1. Auf der Seite **Admineinheiten zuweisen** wählen Sie **Weiter**.
1. Auf der Seite **Benutzende und Gruppen veröffentlichen** wählen Sie **Benutzende und Gruppen** und wählen Sie **Bearbeiten**.
1. Wählen Sie auf der Seite **Geltungsbereich für Benutzende und Gruppen** die Option **Spezifische Benutzende und Gruppen** aus und wählen Sie **+ Benutzende und Gruppen einbeziehen** aus. Wählen Sie dann **Führungskräfte** und **Führung** aus und wählen Sie **Erledigt** aus, bis die Benutzerzuweisung beendet ist.
1. Wählen Sie **Weiter** aus.
1. Auf der Seite **Richtlinieneinstellungen** wählen Sie **Benutzende müssen eine Begründung bereitstellen, um eine Kennzeichnung zu entfernen oder ihre Klassifizierung herabzusetzen** und **Benutzende müssen eine Kennzeichnung auf ihre E-Mails und Dokumente anwenden**.
1. Wählen Sie **Weiter** aus.
1. Legen Sie auf der Seite **Standardeinstellungen für Dokumente** die Option **E-Mail erbt Kennzeichnung für höchste Priorität von Anhängen** fest und wählen Sie **Weiter**.
1. Wählen Sie auf der Seite **Standardeinstellungen für Besprechungen und Kalenderereignisse** die Option **Weiter**.
1. Wählen Sie auf der Seite **Standardeinstellungen für Standorte und Gruppen** **Weiter**.
1. Auf der Seite **Standardeinstellungen für Fabric- und Power BI-Inhalte** wählen Sie **Weiter**.
1. Geben Sie auf der Seite **Benennen Sie Ihre Richtlinie** die folgenden Informationen ein:
    - **Name**: Richtlinie über Vertraulichkeitsbezeichnungen für die Verwaltung
    - **Beschreibung**: Diese Richtlinie dient dem Schutz der Unternehmensleitung im Zusammenhang mit dem Erwerb von Unternehmen
1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Überprüfen und beenden** die Option **Absenden** aus.

Sie haben erfolgreich eine Vertraulichkeitsbezeichnung erstellt und veröffentlicht.