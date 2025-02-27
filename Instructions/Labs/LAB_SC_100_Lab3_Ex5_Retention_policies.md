---
lab: 3
title: Übung 5 – Aufbewahrungsrichtlinien
---

# Lab 3 – Übung 5 – Aufbewahrungsrichtlinien

Die deutsche Regierung hat kürzlich bestimmte Gesetze über die Aufbewahrungsfristen für Unternehmen geändert. Eine wichtige Änderung besteht darin, dass alle Finanzunterlagen nun 11 Jahre lang aufbewahrt werden müssen, statt wie bisher 10 Jahre. Eine weitere Änderung besteht darin, dass Handels- oder Geschäftskorrespondenz, einschließlich Kopien von versandter Handels- oder Geschäftskorrespondenz, nun 5 statt 7 Jahre aufbewahrt werden kann. Derzeit gelten in Ihrem Unternehmen Aufbewahrungsrichtlinien, nach denen alle Dokumente 7 Jahre lang aufbewahrt werden. Contoso Ltd. sah sich jedoch in den letzten Jahren mit Herausforderungen konfrontiert, die sich aus der Anhäufung einer großen Datenmenge in seiner Umgebung ergaben. Dies hat zu erhöhten Wartungskosten und einem erheblichen Speicherplatzbedarf geführt. Ihre Aufgabe ist es, die Aufbewahrungsrichtlinie in Ihrem Unternehmen so zu optimieren, dass sie den gesetzlichen Vorschriften entspricht und gleichzeitig die Anforderungen an die Datenspeicherung minimiert. Die Unternehmensrichtlinie schreibt vor, dass alle Daten mindestens fünf Jahre nach der Erstellung aufbewahrt werden müssen, in strikter Einhaltung aller anwendbaren Gesetze zur Datenaufbewahrung.

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept zur Bewältigung der Herausforderungen, mit denen Contoso Ltd. konfrontiert ist.

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage des beschriebenen Problems zu analysieren und die Ziele zu verstehen

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Aufbewahren aller Finanzdaten für 11 Jahre
- Aufbewahren jeglicher Geschäftskorrespondez für 5 Jahre
- Minimierung des Datenspeicherungsaufwands

In einem zweiten Schritt wird die bestehende Umgebung von Contoso Ltd. untersucht. Contoso verfügt über mehrere Lösungen, um seine Daten für eine bestimmte Zeit aufzubewahren. Ihre Aufgabe ist es, die aktuelle Einrichtung zu analysieren und zu entscheiden, ob sie den gesetzlichen Anforderungen entspricht. 

Die dritte Phase umfasst das Erstellen des Lösungskonzepts. Nach eingehender Untersuchung stellt sich heraus, dass keine der bestehenden Maßnahmen die vorgegebenen Kriterien erfüllt. Daher ist eine neue Reihe von Richtlinien unerlässlich.

Basierend auf dem obigen Szenario kann die Microsoft Purview-Datenlebenszyklusverwaltung verwendet werden, um die Daten angemessen aufzubewahren.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Aufbewahren aller Finanzdaten für 11 Jahre| Microsoft Purview-Datenlebenszyklusverwaltung|Erstellen Sie eine automatisch angewendete Aufbewahrungsbezeichnung.|
|Aufbewahren jeglicher Geschäftskorrespondez für 5 Jahre| Microsoft Purview-Datenlebenszyklusverwaltung|Bereitstellen einer Aufbewahrungsrichtlinie|


## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1: Analysieren der aktuellen Struktur der Aufbewahrungsrichtlinie

In dieser Aufgabe machen Sie sich mit der vorhandenen Aufbewahrungsrichtlinie Ihres Unternehmens vertraut. Sie erhalten einen Einblick in verschiedene Aufbewahrungsrichtlinien, Bezeichnungen und Bezeichnungsrichtlinien. Sie werden das Security & Compliance PowerShell-Modul verwenden und die vorhandenen Richtlinien anzeigen. Sie untersuchen die derzeitige Situation und entscheiden, ob die bestehenden Aufbewahrungsrichtlinien für Contoso Ltd. ausreichend sind, um die gesetzlichen Anforderungen zu erfüllen. 

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
1. Geben Sie das folgende Cmdlet ein, um vorhandene Aufbewahrungsrichtlinien und -einstellungen anzuzeigen:

    ```powershell
     Get-ComplianceTag | Format-Table -Auto Name,Priority,RetentionAction,RetentionDuration,Workload
    ```
1. Nehmen Sie sich etwas Zeit, um die resultierende Tabelle zu bewerten.

>[!NOTE] Sie können auch auf das Microsoft Purview Compliance-Portal zugreifen, um die Aufbewahrungsrichtlinien einzusehen, aber Sie müssen sich jede Richtlinie einzeln ansehen, anstatt einen Überblick über alle Ihre Richtlinien auf einen Blick zu erhalten.

Sie haben die vorhandenen Bezeichnungen und Einstellungen erfolgreich angezeigt, um zu entscheiden, ob sie den gesetzlichen Anforderungen entsprechen.

### Aufgabe 2: Eine Aufbewahrungsrichtlinie erstellen

Sie haben die Aufbewahrungsrichtlinien von Contoso Ltd. effektiv bewertet und eine veraltete Einrichtung aufgedeckt, die nicht den gesetzlichen Standards entspricht. Ihre Untersuchung ergab, dass fünf Aufbewahrungsrichtlinien mit identischen Einstellungen und nur einer Aufbewahrungsbezeichnung angewandt wurden, von denen keine den gesetzlichen Anforderungen entsprach.

Ihr Plan umfasst die Implementierung einer neuen unternehmensweiten Aufbewahrungsrichtlinie mit einem Aufbewahrungszeitraum von fünf Jahren. Nach Ablauf dieses Zeitraums können die Daten aufbewahrt werden, müssen aber nicht zwingend gelöscht werden. Mit dieser Anpassung werden die gesetzlichen Anforderungen an die Mindestaufbewahrungsfristen erfüllt und der Daten-Mehraufwand verringert.

1. Melden Sie sich beim Microsoft Purview Compliance Portal **https://compliance.microsoft.com/** als Allan Deyoung mithilfe seines Administratorkontos **MOD Administrator** an.
1. Wählen Sie **Datenlebenszyklusverwaltung** > **Microsoft 365**.
1. Wählen sie auf der Seite **Datenlebenszyklusverwaltung** die Registerkarte **Aufbewahrungsrichtlinien** und dann **+ Neue Aufbewahrungsrichtlinie**.
1. Geben Sie auf der Seite **Benennen Sie Ihre Aufbewahrungsrichtlinie** die folgenden Informationen ein:
    - **Name**: Allgemeine Aufbewahrungsrichtlinie
    - **Beschreibung**: Diese Richtlinie ist die Standardaufbewahrungsrichtlinie für die gesamte Organisation. Alle Daten müssen mindestens 5 Jahre lang aufbewahrt werden. 
1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Richtlinienbereich** **Weiter** aus.
1. Wählen Sie auf der Seite **Typ der zu erstellenden Aufbewahrungsrichtlinie auswählen** die Option **Statisch** und wählen Sie **Weiter**.
1. Aktivieren Sie auf der Seite **Auswählen, wo diese Richtlinie angewendet werden soll** die folgenden Orte:

    - Exchange-Postfächer
    - Klassische SharePoint- und Communciation-Websites
    - OneDrive Konten
    - Microsoft 365-Gruppenpostfächer und -Websites

1. Wählen Sie**Weiter** aus.
1. Auf der Seite **Entscheiden Sie, ob Sie Inhalte aufbewahren, löschen oder beides möchten**. Geben Sie die folgenden Einstellungen ein:

    - **Elemente für einen bestimmten Zeitraum aufbewahren**: 5 Jahre
    - **Beginnen Sie die Aufbewahrungsfrist auf der Grundlage von**: Wann die Objekte erstellt wurden
    - **Am Ende des Aufbewahrungszeitraums**: Nichts tun

1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Überprüfen und beenden** die Option **Absenden** aus.

Sie haben erfolgreich eine Aufbewahrungsrichtlinie erstellt. Sie können nun alle verbleibenden Aufbewahrungsrichtlinien löschen, da sie nicht den Anforderungen des Unternehmens entsprechen.

### Aufgabe 3: Erstellen einer Aufbewahrungsbezeichnung

Um die deutschen Vorschriften einzuhalten, erstellen Sie nun eine Aufbewahrungsbezeichnung mit einem Aufbewahrungszeitraum von 11 Jahren und wenden es automatisch auf alle Dokumente an, die deutsche Finanzdaten enthalten.

1. Sie sollten weiterhin im Microsoft Purview-Complianceportal **https://compliance.microsoft.com/** angemeldet sein.
1. Erweitern Sie im Microsoft Purview-Complianceportal auf der linken Navigationsseite **Datenlebenszyklusverwaltung** und wählen Sie **Microsoft 365** aus.
1. Wählen Sie auf der Seite **Datenlebenszyklusverwaltung** die Registerkarte **Bezeichnungen** auswählen und **+ Bezeichnung erstellen** auswählen.
1. Auf der Seite **Geben Sie Ihre Aufbewahrungsbezeichnung ein** geben Sie die folgenden Informationen ein:

    - **Name**: Deutsche Finanzdaten
    - **Beschreibung für Benutzende**: Mit dieser Bezeichnung werden alle deutschen Finanzdaten für 11 Jahre aufbewahrt.
    - **Beschreibung für Admins**: Die Bezeichnung speichert alle Finanzdaten für 11 Jahre und wird automatisch angewendet.

1. Wählen Sie **Weiter** aus.
1. Auf der Seite **Bezeichnungseinstellungen definieren** wählen Sie **Aktionen nach einem bestimmten Zeitraum erzwingen** und wählen Sie **Weiter**.
1. Auf der Seite **Definieren Sie den Zeitraum** geben Sie die folgenden Informationen ein:

    - **Wie lange ist der Zeitraum?**: 11 Jahre
    - **Wann sollte der Zeitraum beginnen?**: Bei Erstellung der Elemente

1. Wählen Sie **Weiter** aus.
1. Auf der Seite **Auswählen, was nach dem Zeitraum passiert** wählen Sie **Elemente automatisch löschen**.
1. Auf der Seite **Prüfen und fertigstellen** wählen Sie **Bezeichnung erstellen**.
1. Auf der Seite **Ihre Aufbewahrungsbezeichnung wird erstellt** **Automatische Anwendung dieser Bezeichnung auf einen bestimmten Inhaltstyp** auswählen und **Fertig** auswählen.
1. Geben Sie auf der Seite **Erste Schritte** die folgenden Informationen ein:

    - **Name**: Automatisch alle deutschen Finanzdaten 11 Jahre lang aufbewahren
    - **Beschreibungen**: Diese Richtlinie wendet automatisch die Bezeichnung **Deutsche Finanzdaten** an.

1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf der Seite **Wählen Sie die Typ des Inhalts, auf den Sie diese Bezeichnung anwenden möchten** die Option **Bezeichnung auf Inhalt anwenden, der vertrauliche Informationen enthält** und wählen Sie **Weiter**.
1. Setzen Sie auf der Seite **Inhalt, der sensible Daten enthält** den Filter auf **Deutschland** und wählen Sie **Finanzen** und dann **Deutschland Finanzdaten** und wählen Sie dann **Weiter**.
1. Wählen Sie auf der Seite **Definieren Sie Inhalte, die vertrauliche Informationen enthalten** **Weiter**.
1. Wählen Sie auf der Seite **Richtlinienbereich** **Weiter**.
1. Auf der Seite **Wählen Sie den Typ der zu erstellenden Aufbewahrungsrichtlinie** wählen Sie **Statisch**.
1. Aktivieren Sie auf der Seite „**Wählen Sie aus, wo die Bezeichnung automatisch angewendet werden soll** folgende Orte:

    - Exchange-Postfächer
    - Klassische SharePoint- und Kommunikationswebsites
    - OneDrive Konten
    - Microsoft 365-Gruppenpostfächer und -Websites

1. Wählen Sie **Weiter** aus.
1. Auf der Seite **Wählen Sie eine Bezeichnung für die automatische Anwendung** wählen Sie **Weiter**.
1. Wählen Sie auf der Seite **Entscheiden Sie, ob Sie Ihre Richtlinie testen oder ausführen möchten** die Option **Richtlinie einschalten** und wählen Sie dann **Weiter**.
1. Wählen Sie auf der Seite **Überprüfen und beenden** die Option **Absenden** aus.

Sie haben erfolgreich eine Aufbewahrungsbezeichnung erstellt und automatisch angewendet.
