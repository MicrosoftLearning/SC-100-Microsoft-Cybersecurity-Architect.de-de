# Endpunktsicherheit

Contoso verwendet Microsoft Intune zur Verwaltung seiner Geräte und stellt seinen Mitarbeitenden Geräte mit Windows 10 und Windows 11 zur Verfügung. Das Unternehmen hat in der Vergangenheit mehrere Konfigurationsprofile implementiert. Eine unternehmensweite Infrastrukturanalyse ergab jedoch, dass die bestehenden Richtlinien unabhängig voneinander erstellt wurden, was eine ganzheitliche Betrachtung und Ablaufverfolgung erschwerte. Als Cybersicherheitsarchitektur entwerfende Person des Unternehmens haben Sie beschlossen, alle notwendigen und kritischen Konfigurationen an einem Ort zu konsolidieren. 

Darüber hinaus ergab die Analyse, dass Tailwind Traders macOS-Geräte in seiner Umgebung verwendet. Im Rahmen der bevorstehenden Fusion planen Sie, den Contoso-Mandanten auf die neuen macOS-Geräte vorzubereiten.

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept zur Bewältigung der Herausforderungen, mit denen Contoso Ltd. konfrontiert ist.

### Entwurfsansatz

In dem gegebenen Szenario können die folgenden Anforderungen skizziert werden:

- Konsolidieren Sie alle Konfigurationen für Windows-Geräte an einem Ort
- Schützen von MacOS-Geräten

Microsoft Endpoint Manager mit Sicherheits-Baselines verwaltet und sichert Endgeräte wie Desktops, Laptops, Mobilgeräte und Server zentral. Es integriert Tools wie Intune und Konfigurations-Manager und ermöglicht so eine effiziente Bereitstellung von Anwendungen, die Durchsetzung von Richtlinien, die Einhaltung von Vorschriften und die Überwachung von Geräten. 

Eine Sicherheitsbaseline-Richtlinie umfasst eine Reihe von Konfigurationseinstellungen, die von Microsoft empfohlen werden, wobei ihre Sicherheitsauswirkungen beschrieben werden. Diese Einstellungen werden auf der Grundlage von Eingaben der Sicherheitsteams von Microsoft, Produktgruppen, Partnern und Partnerinen und der Kundschaft formuliert. Diese Basispläne umfassen Gerätekonfigurationseinstellungen, die denen in verschiedenen Intune-Richtlinien ähneln. Durch das Anpassen der einzelnen bereitgestellten Baselines wird die Erzwingung der erforderlichen Einstellungen und Werte ermöglicht. Beim Einrichten eines Sicherheitsbaseline-Profils in Intune erstellen Sie im Wesentlichen eine Vorlage, die aus mehreren Gerätekonfigurationsprofilen besteht. Diese Empfehlungen müssen regelmäßig entsprechend den jeweiligen Geschäftsanforderungen überprüft und angepasst werden.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Konsolidieren Sie alle Konfigurationen für Windows-Geräte an einem Ort|Microsoft Endpunkt Manager – Endpunktsicherheit|Sicherheitsbaseline-Richtlinien bereitstellen
|Schützen von MacOS-Geräten|Microsoft Endpunkt Manager|AV-Programm auf macOS-Geräten bereitstellen|

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1: Bereitstellen von Endpunkt-Sicherheitsbaseline-Richtlinien

Ihr Gesamtziel besteht darin, Ihre Endpunkte angemessen zu sichern und so viele Richtlinien wie möglich an einem zentralen Ort zu konsolidieren. Dies erreichen Sie, indem Sie Endpunkt-Sicherheitsbaseline-Richtlinien für Windows-Geräte in Intune erstellen.

1. Melden Sie sich bei der Windows-Client-VM **LON-SC1** mit dem lokalen **Administrator**-Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Melden Sie sich im Microsoft Intune Admin Center **`https://intune.microsoft.com`** als **MOD-Fachkraft in der IT-Verwaltung**admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandanten-ID ist, die Sie von Ihrem Labor-Hosting-Anbieter erhalten haben). Das Kennwort des Benutzernden sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Wenn Sie oben rechts auf dem Bildschirm ein Informationsfeld **Multi-Faktor-Authentifizierung verwalten** sehen, schließen Sie es, indem Sie das **X** auswählen.
1. Wählen Sie im Microsoft Intune Admin Center im linken Navigationsbereich **Endpunktsicherheit**.
1. Wählen Sie auf der Seite **Endpunktsicherheit | Übersicht** unter **Übersicht** die Option **Sicherheitsbaselines**.
1. Wählen Sie auf der Seite **Endpunktsicherheit | Sicherheitsbaselines** die Option **Sicherheitsbaseline für Windows 10 und höher**.
1. Auf der Seite **Sicherheitsbaseline für Windows 10 und höher | Profile** wählen Sie **+ Profil erstellen**.
1. Überprüfen Sie die Beschreibung auf dem Blatt **Ein Profil erstellen** und wählen Sie **Erstellen**.
1. Gehen Sie auf dem Blatt **Grundlagen** Folgendes ein:
    1. Name: **`Secure Windows Endpoints`**
    1. Beschreibung: **`The Security Baseline for Windows 10 and later represents the recommendations for configuring Windows.`**
1. Wählen Sie **Weiter** aus.
1. Auf dem Blatt **Konfigurationseinstellungen** untersuchen Sie die unterschiedlichen Konfigurationsoptionen. Klicken Sie abschließend auf **Weiter**.
1. Wählen Sie auf dem Blatt **Geltungsbereich der Kategorien** **Weiter**.
1. Wählen Sie auf dem Blatt **Zuordnungen** unter **Eingeschlossene Gruppen** die Option **Alle Benutzenden hinzufügen** und wählen Sie **Weiter**.
1. Wählen Sie auf dem Blatt **Überprüfen + erstellen** die Option **Erstellen** aus.
1. Gehen Sie zurück zur Seite **Endpunktsicherheit | Sicherheits-Baselines**.
1. Wählen Sie auf der Seite **Endpunktsicherheit | Sicherheits-Baselines** die Option **Microsoft Defender for Endpoint Security Baseline**.
1. Wählen Sie auf der Seite **Microsoft Defender for Endpoint Security baseline | Profile** die Option **+ Profil erstellen**.
1. Überprüfen Sie die Beschreibung auf dem Blatt **Ein Profil erstellen** und wählen Sie **Erstellen**.
1. Gehen Sie auf dem Blatt **Grundlagen** Folgendes ein:
    1. Name: **`Defender for Endpoint Security Baseline`**
    1. Beschreibung: **`Security best practices for the Microsoft security stack on devices managed by Intune`**.
1. Wählen Sie **Weiter** aus.
1. Auf dem Blatt **Konfigurationseinstellungen** untersuchen Sie die unterschiedlichen Konfigurationsoptionen. Klicken Sie abschließend auf **Weiter**.
1. Wählen Sie auf dem Blatt **Geltungsbereich der Kategorien** **Weiter**.
1. Wählen Sie auf dem Blatt **Zuordnungen** unter **Eingeschlossene Gruppen** die Option **Alle Benutzenden hinzufügen** und wählen Sie **Weiter**.
1. Wählen Sie auf dem Blatt **Überprüfen + erstellen** die Option **Erstellen** aus.

Sie haben erfolgreich zwei Richtlinien zur Sicherheitsbaseline für Windows-Geräte erstellt.

### Aufgabe 2: Bereitstellung von Virenschutz auf macOS-Geräten

Nachdem Sie Windows-Geräte mit Richtlinien der Sicherheitsbaseline für Endgeräte gesichert haben, werden Sie Virenschutz bereitstellen und die Verschlüsselung auf macOS-Geräten aktivieren, um Ihre Umgebung für die Zusammenführung mit Trailwind Traders vorzubereiten.

1. Sie sollten immer noch im Microsoft Intune Admin Center angemeldet sein **https://intune.microsoft.com**.
1. Wählen Sie im Microsoft Intune Admin Center im linken Navigationsbereich **Endpunktsicherheit**.
1. Wählen Sie auf der Seite **Endpunktsicherheit | Übersicht** unter **Verwalten** die Option **Virenschutz**.
1. Wählen Sie auf der Seite **Endpunktsicherheit | Virenschutz** die Option **+ Richtlinie erstellen**.
1. Wählen Sie im Bereich **Profil erstellen** unter **Plattform** die Option **macOS** und unter **Profil** die Option **Microsoft Defender Antivirus**.
1. Klicken Sie auf **Erstellen**.
1. Gehen Sie auf dem Blatt **Grundlagen** Folgendes ein:
    1. Name: **`Deploy antivirus on macOS devices`**
    1. Description (Beschreibung): **`Deploy antivirus and enable encryption on macOS devices to prepare your environment for merging with Trailwind Traders.`**
1. Wählen Sie **Weiter** aus.
1. Stellen Sie auf der Registerkarte **Konfigurationseinstellungen** sicher, dass die Einstellungen wie folgt konfiguriert sind:
1. Unter **Schutzeinstellungen für die Cloud**:
    - Aktivieren/Deaktivieren des Schutzes durch die Cloud: **Aktiviert (Standard)**
    - Aktivieren/Deaktivieren automatischer Beispielübermittlungen: **Aktiviert (Standard)**
    - Diagnosesammlungsstufe: **optional (Standard)**
    - Automatisches Update der Sicherheitsinformationen: **Aktiviert (Standard)**
1. Unter **Antivirenprogramm**:
    - Aktivieren des Echtzeitschutzes: **Aktiviert (Standard)**
    - Aktivieren des passiven Modus: **Deaktiviert (Standard)**
    - Ausschluss-Zusammenführung: **admin_only**
1. Wählen Sie unter **Einstellungen für den Bedrohungstyp** **+ Hinzufügen**:
    - Geben Sie in das Textfeld für den Bedrohungstyp ein: **potenziell_unerwünschte_Anwendung**
    - Auszuführende Aktion: **Blockieren**
    - Einstellungen des Bedrohungstyps zusammenführen: **admin_only**
1. Aktivieren der Datei-Hash-Berechnung: **True****
1. Nach dem Update der Definitionen eine Überprüfung durchführen: **Aktiviert (Standard)**
1. Erzwingungsstufe: **real_time**
1. Unter **Netzwerkschutz**:
    - Erzwingungsstufe: Blockieren
1. Unter **Manipulationsschutz**:
    - Erzwingungsstufe: **Block (Standard)**
1. Unter **Benutzeroberflächeneinstellungen**
    - Steuern der Anmeldung bei der Verbraucherversion: **Aktiviert (Standard)**
    - Ein-/Ausblenden des Symbols für das Statusmenü: **Deaktiviert (Standard)**
    - Rückmeldung von Benutzenden: **Aktiviert (Standard)**
1. Wählen Sie **Weiter** aus.
1. Wählen Sie auf dem Blatt **Geltungsbereich der Kategorien** **Weiter**.
1. Auf der Registerkarte **Zuweisungen** geben Sie in das Textfeld **Alle Benutzender** ein und wählen es aus.
1. Wählen Sie **Weiter** aus.
1. Auf der Registerkarte **Review + erstellen** wählen Sie **Speichern**.

Sie haben den Virenschutz für macOS-Geräte erfolgreich konfiguriert und bereitgestellt.

### Aufgabe 3 Verschlüsseln von macOS-Geräten

In dieser Aufgabe werden Sie macOS-Geräte verschlüsseln.

1. Sie sollten immer noch im Microsoft Intune Admin Center angemeldet sein **https://intune.microsoft.com**.
1. Wählen Sie im Microsoft Intune Admin Center im linken Navigationsbereich **Endpunktsicherheit**.
1. Wählen Sie auf der Seite **Endpunktsicherheit | Übersicht** unter **Verwalten** die Option **Datenträgerverschlüsselung**.
1. Wählen Sie auf der Seite **Endpunktsicherheit | Datenträgerverschlüsselung** die Option **+ Richtlinie erstellen**.
1. Wählen Sie im Bereich **Profil erstellen** unter **Plattform** die Option **macOS** und unter **Profil** die Option **FileVault**.
1. Klicken Sie auf **Erstellen**.
1. Geben Sie auf dem Blatt **Basic** eingeben:
    1. Name: **`Encrypt macOS devices`**
    1. Description (Beschreibung): **`FileVault provides built-in Full Disk Encryption for macOS devices.`**
    1. Wählen Sie **Weiter** aus.
1. Konfigurieren Sie auf dem Blatt **Konfigurationseinstellungen** unter **Verschlüsselung** die folgenden Einstellungen:
   - Aktivieren von FileVault: **Ja**
   - Rotieren des persönlichen Wiederherstellungsschlüssel: **6 Monate**
   - Speicherortbeschreibung des persönlichen Wiederherstellungsschlüssels: **`To recover a lost or recently rotated recovery key, log in to the Intune Company Portal website using any device. Navigate to the Devices section within the portal, choose the device with FileVault enabled, and then select the option to retrieve the recovery key. The portal will display the current recovery key for that device.`**
   - Anzahl der erlaubten Umgehungen: **3**
   - Aufschub bis zur Abmeldung zulassen: **Ja**
   - Prompt beim Abmelden deaktivieren: **Ja**
   - Ausblenden des Wiederherstellungsschlüssels: **Ja**
   - Wählen Sie **Weiter** aus.
1. Wählen Sie auf dem Blatt **Geltungsbereich der Kategorien** **Weiter**.
1. Wählen Sie auf dem Blatt **Zuordnungen** unter **Eingeschlossene Gruppen** die Option **Alle Benutzenden hinzufügen** und dann **Weiter**.
1. Wählen Sie auf dem Blatt **Überprüfen + erstellen** die Option **Erstellen** aus.

Sie haben ein FileVault-Profil erfolgreich konfiguriert und bereitgestellt, um macOS-Geräte zu verschlüsseln.
