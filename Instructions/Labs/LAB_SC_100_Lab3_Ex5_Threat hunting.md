---
lab: 3
title: Übung 5 – Bedrohungssuche
---


# Lab 3 – Übung 5 – Inhaltssuche in Microsoft Purview

Ihr Unternehmen ist einer ernsthaften Bedrohung seiner Integrität und Sicherheit ausgesetzt. Eine erhebliche Anzahl bösartiger E-Mails wurde erkannt. Ihre Aufgabe besteht darin, die Absenderadressen oder Betreffzeilen dieser E-Mails zu identifizieren. Nachdem Sie diese schädlichen E-Mails identifiziert haben, müssen Sie sie massenweise löschen.

## Teil 1: Entwerfen einer Lösung (erforderlich)

### Entwurfsansatz

Der erste Schritt besteht darin, schädliche E-Mails zu identifizieren. Daher ist eine Analyse des aktuellen Nachrichtenflusses unerlässlich. Das Microsoft Defender Portal bietet eine umfassende Übersicht über alle ausgehenden und eingehenden E-Mails sowie weitere Funktionen zur Untersuchung dieses Datenverkehrs. Die Abhilfemaßnahme besteht darin, die schädlichen E-Mails zu löschen. 

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Identifizieren bösartiger E-Mails|Microsoft Defender für Office 365|Untersuchen des Nachrichtenflusses und Analysieren von E-Mail-Kopfzeilen|
|Beseitigung von Risiken, die aus bösartigen E-Mails stammen|Microsoft Defender für Office 365|Löschen bösartiger E-Mails|

### Aufgabe 1: Untersuchen bösartiger E-Mails

Sie untersuchen die eingehenden E-Mails im Microsoft Defender-Portal und identifizieren, welche E-Mails verdächtig sind und bösartige Inhalte enthalten.

1. Melden Sie sich beim Microsoft Defender-Portal **https://security.microsoft.com** als Allan Deyoung mithilfe seines Administratorkontos **MOD-Administrator** an.
1. Erweitern Sie im Microsoft-Sicherheitsportal **E-Mail und Zusammenarbeit** und wählen Sie dann **Explorer** aus.
1. Passen Sie auf der Seite **Explorer** den Zeitraum der Abfrage an, um den gesamten Mail-Flow der letzten 30 Tage anzuzeigen, und wählen Sie **Aktualisieren** aus.
1. Das Ergebnis zeigt Alle eingehenden und ausgehenden E-Mails an. Untersuchen Sie den E-Mail-Fluss und den Betreff der E-Mails.
1. E-Mails mit dem Betreff „Sie haben heute fällige Aufgaben“ erscheinen verdächtig.
1. Wählen Sie den Betreff aus, um weitere Untersuchungen zu unternehmen.
1. In der neuen Ansicht **Sie haben heute fällige Aufgaben** finden Sie die Informationen und wählen **Kopfzeile anzeigen** aus.
1. Wählen Sie im Bereich **E-Mail-Nachrichtenkopf** die Option **Nachrichtenkopf kopieren** und dann **Microsoft Message Header Analyzer**.
1. In Ihrem Browser öffnet sich eine neue Registerkarte.
1. Fügen Sie auf der Seite **Message Header Analyzer** den Nachrichtenkopf ein und wählen Sie **Nachrichtenkopf analysieren**.
1. Überprüfen Sie das Ergebnis.

Sie haben den Nachrichtenfluss im Microsoft Defender-Portal erfolgreich überprüft.

### Aufgabe 2: Durchführung der Massenlöschung bösartiger E-Mails

Sie sind zu dem Schluss gekommen, dass E-Mails mit dem Betreff „Sie haben heute fällige Aufgaben“ Phishing-Angriffe sind. Ihre Abhilfemaßnahme besteht darin, diese E-Mails mithilfe von Powershell massenweise zu löschen.

>[!NOTE] Sie sollten das Exchange Online PowerShell-Modul bereits installiert haben. Wenn das Modul fehlt, befolgen Sie die Anweisungen zum Installieren des Moduls.

1. Öffnen Sie ein erweitertes PowerShell-Fenster, indem Sie mit der rechten Maustaste auf die Schaltfläche Windows klicken und dann **Windows PowerShell (Admin)** wählen.
1. Bestätigen Sie das Fenster **Benutzerkontensteuerung** mit **Ja**.
1. Geben Sie das folgende Cmdlet ein, um die neueste Version des Exchange Online PowerShell-Moduls zu installieren:

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Bestätigen Sie den Sicherheitsdialog für das nicht vertrauenswürdige Repository mit **Y** für Ja und drücken Sie **Eingabe**.  Dieser Vorgang nimmt einige Zeit in Anspruch.
1. Öffnen Sie ein erweitertes PowerShell-Fenster, indem Sie mit der rechten Maustaste auf die Schaltfläche Windows klicken und dann **Windows PowerShell (Admin)** wählen.
1. Bestätigen Sie das Fenster **Benutzerkontensteuerung** mit **Ja**.
1. Geben Sie das folgende Cmdlet ein, um eine Verbindung mit Security & Compliance PowerShell herzustellen:

    ```powershell
    Connect-IPPSSession
    ```

1. Wenn das Fenster **Anmelden** angezeigt wird, melden Sie sich als admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandanten-ID ist, die Sie von Ihrem Lab-Hosting-Anbieter erhalten haben) und verwenden Sie das administrative Kennwort für Ihren Mandanten.
1. Geben Sie das folgende Cmdlet ein, um die Inhaltssuche auszuführen, und geben Sie den Zeitraum im Cmdlet an:

    ```powershell
    $Search=New-ComplianceSearch -Name "Purge phishing messages" -ExchangeLocation All -ContentMatchQuery '(Received:mm/dd/yyyy..mm/dd/yyyy) AND (Subject:"You have tasks due today")'
    Start-ComplianceSearch -Identity $Search.Identity
    ```
1. Geben Sie das folgende Cmdlet ein, um die Nachrichten endgültig zu löschen:

    ```powershell
    New-ComplianceSearchAction -SearchName "Purge phishing messages" -Purge -PurgeType HardDelete
    ---
You have successfully performed a mass-deletion of malicious mails.