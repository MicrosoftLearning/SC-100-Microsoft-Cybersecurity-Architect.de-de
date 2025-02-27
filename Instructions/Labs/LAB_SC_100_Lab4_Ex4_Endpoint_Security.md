---
lab: 4
title: Übung 4 - Endpunktsicherheit
---

# Labor 4 - Aufgabe 4 - Endpunktsicherheit

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

Ihr übergeordnetes Ziel ist es, Ihre Endpunkte angemessen zu sichern und so viele Richtlinien wie möglich an einem Ort zu konsolidieren. Dies erreichen Sie, indem Sie Endpunkt-Sicherheitsbaseline-Richtlinien für Windows-Geräte in Intune erstellen.

1. Melden Sie sich im Microsoft Intune Admin Center **https://intune.microsoft.com** als Allan Deyoung mit seinem Administratorkonto **MOD Administrator** an.
2. Wählen Sie im Microsoft Intune Admin Center im linken Navigationsbereich **Endpunktsicherheit**.
3. Wählen Sie auf der Seite **Endpunktsicherheit | Übersicht** unter **Übersicht** die Option **Sicherheitsbaselines**.
4. Wählen Sie auf der Seite **Endpunktsicherheit | Sicherheitsbaselines** die Option **Sicherheitsbaseline für Windows 10 und höher**.
5. Auf der Seite **MDM Security Baseline | Profile** wählen Sie **+ Profil erstellen**.
1. Überprüfen Sie die Beschreibung auf dem Blatt **Ein Profil erstellen** und wählen Sie **Erstellen**.
1. Geben Sie auf dem Blatt **Grundlagen** einen Namen und eine Beschreibung ein.
1. Wählen Sie **Weiter** aus.
1. Auf dem Blatt **Konfigurationseinstellungen** untersuchen Sie die unterschiedlichen Konfigurationsoptionen. Klicken Sie abschließend auf **Weiter**.
1. Wählen Sie auf dem Blatt **Geltungsbereich der Kategorien** **Weiter**.
1. Wählen Sie auf dem Blatt **Zuordnungen** unter **Eingeschlossene Gruppen** die Option **Alle Benutzenden hinzufügen** und wählen Sie **Weiter**.
1. Wählen Sie auf dem Blatt **Überprüfen + erstellen** die Option **Erstellen** aus.
1. Gehen Sie zurück zur Seite **Endpunktsicherheit | Sicherheits-Baselines**.
1. Wählen Sie auf der Seite **Endpunktsicherheit | Sicherheits-Baselines** die Option **Microsoft Defender for Endpoint Security Baseline**.
1. Wählen Sie auf der Seite **Microsoft Defender for Endpoint Security baseline | Profile** die Option **+ Profil erstellen**.
1. Überprüfen Sie die Beschreibung auf dem Blatt **Ein Profil erstellen** und wählen Sie **Erstellen**.
1. Geben Sie auf dem Blatt **Grundlagen** einen Namen und eine Beschreibung ein.
1. Wählen Sie **Weiter** aus.
1. Auf dem Blatt **Konfigurationseinstellungen** untersuchen Sie die unterschiedlichen Konfigurationsoptionen. Klicken Sie abschließend auf **Weiter**.
1. Wählen Sie auf dem Blatt **Geltungsbereich der Kategorien** **Weiter**. 
1. Wählen Sie auf dem Blatt **Zuordnungen** unter **Eingeschlossene Gruppen** die Option **Alle Benutzenden hinzufügen** und wählen Sie **Weiter**.
1. Wählen Sie auf dem Blatt **Überprüfen + erstellen** die Option **Erstellen** aus.

Sie haben erfolgreich zwei Richtlinien zur Sicherheitsbaseline für Windows-Geräte erstellt.

### Aufgabe 2: Bereitstellung von Virenschutz auf macOS-Geräten

Nachdem Sie Windows-Geräte mit grundlegenden Sicherheitsrichtlinien für Endgeräte gesichert haben, werden Sie Antivirus einsetzen und die Verschlüsselung auf macOS-Geräten aktivieren, um Ihre Umgebung für die Zusammenführung mit Trailwind Traders vorzubereiten.

1. Sie sollten immer noch im Microsoft Intune Admin Center angemeldet sein **https://intune.microsoft.com**.
2. Wählen Sie im Microsoft Intune Admin Center im linken Navigationsbereich **Endpunktsicherheit**.
3. Wählen Sie auf der Seite **Endpunktsicherheit | Übersicht** unter **Verwalten** die Option **Virenschutz**.
4. Wählen Sie auf der Seite **Endpunktsicherheit | Virenschutz** die Option **+ Richtlinie erstellen**.
5. Wählen Sie im Bereich **Profil erstellen** unter **Plattform** die Option **macOS** und unter **Profil** die Option **Microsoft Defender Antivirus**.
6. Klicken Sie auf **Erstellen**.
7. Geben Sie auf dem Blatt **Grundlagen** einen Namen und eine Beschreibung ein.
8. Wählen Sie **Weiter** aus.
9. Stellen Sie sicher, dass die Einstellungen auf dem Blatt **Konfigurationseinstellungen** wie folgt konfiguriert sind:

#### Präferenzen für den Schutz aus der Cloud

- **Aktivieren / Deaktivieren des Schutzes bei Cloud-Lieferung**: Aktiviert (Standard)
- **Aktivieren/Deaktivieren automatischer Beispielübermittlungen**: Aktiviert (Standard)
- **Diagnosesammlungsstufe**: optional (Standard)
- **Automatische Aktualisierung der Sicherheitsinformationen**: Aktiviert (Standard)

#### Antivirenprogramm

- **Aktivieren des Echtzeitschutzes**: Aktiviert (Standard)
- **Aktivieren des passiven Modus**: Deaktiviert (Standard)
- **Ausschluss Zusammenführung** : admin_only
- Unter **Einstellungen für Bedrohungstypen** wählen Sie **+ Hinzufügen**.
  - **Bedrohungstyp**: potentiell_unerwünschte_Anwendung
  - **Auszuführende Aktion**: blockieren
- **Zusammenführen der Einstellungen für den Bedrohungstyp**: admin_only
- **Dateihashberechnung** aktivieren: True
- **Durchführen einer Überprüfung, nachdem die Definitionen aktualisiert wurden**: Aktiviert (Standard)
- **Erzwingungsstufe**: real_time

#### Netzwerkschutz

- **Erzwingungsstufe**: Blockieren
  
#### Manipulationsschutz

- **Erzwingungsstufe**: blockieren (Standard)

#### Benutzeroberflächeneinstellungen

- **Steuern der Anmeldung bei der Verbraucherversion**: aktiviert (Standard)
- **Ein-/Ausblenden des Symbols für das Statusmenü**: Deaktiviert (Standard)
- **Rückmeldung von Benutzenden**: aktiviert (Standard)

1.  Wählen Sie **Weiter** aus.
2.  Wählen Sie auf dem Blatt **Geltungsbereich der Kategorien** **Weiter**.
3.  Auf dem Blatt **Zuweisungen** in das Textfeld **Alle Benutzende** eingeben und auswählen.
4.  Wählen Sie **Weiter** aus.
5.  Wählen Sie auf dem Blatt **Überprüfen und erstellen** die Option **Speichern** aus.

Sie haben den Virenschutz für macOS-Geräte erfolgreich konfiguriert und bereitgestellt.

### Aufgabe 3 Verschlüsseln von macOS-Geräten

In dieser Aufgabe werden Sie macOS-Geräte verschlüsseln.

1. Sie sollten immer noch im Microsoft Intune Admin Center angemeldet sein **https://intune.microsoft.com**.
2. Wählen Sie im Microsoft Intune Admin Center im linken Navigationsbereich **Endpunktsicherheit**.
3. Wählen Sie auf der Seite **Endpunktsicherheit | Übersicht** unter **Verwalten** die Option **Datenträgerverschlüsselung**.
4. Wählen Sie auf der Seite **Endpunktsicherheit | Datenträgerverschlüsselung** die Option **+ Richtlinie erstellen**.
5. Wählen Sie im Bereich **Profil erstellen** unter **Plattform** die Option **macOS** und unter **Profil** die Option **FileVault**.
6. Klicken Sie auf **Erstellen**.
7. Auf dem Blatt **Grundlagen** geben Sie einen Namen und eine Beschreibung ein. Wählen Sie **Weiter** aus.
8. Konfigurieren Sie auf dem Blatt **Konfigurationseinstellungen** unter **Verschlüsselung** die folgenden Einstellungen:
   - **Aktivieren von FileVault**: Ja
   - **Rotieren des persönlichen Wiederherstellungsschlüssels**: 6 Monate
   - **Speicherortbeschreibung des persönlichen Wiederherstellungsschlüssels**: Um einen verloren gegangenen oder kürzlich gedrehten Wiederherstellungsschlüssel wiederherzustellen, melden Sie sich mit jedem Gerät bei der Intune-Unternehmensportal-Website an. Navigieren Sie im Portal zum Abschnitt Geräte, wählen Sie das Gerät aus, auf dem FileVault aktiviert ist, und wählen Sie dann die Option zum Erhalten des Wiederherstellungsschlüssels. Das Portal zeigt den aktuellen Wiederherstellungsschlüssel für dieses Gerät an.
   - **Anzahl der erlaubten Umgehungen**: 3
   - **Aufschub bis zur Abmeldung zulassen**: Ja
   - **Prompt beim Abmelden deaktivieren**: Ja
   - **Wiederherstellungsschlüssel ausblenden**: Ja
  
9.  Wählen Sie **Weiter** aus.
10. Wählen Sie auf dem Blatt **Geltungsbereich der Kategorien** **Weiter**.
11. Wählen Sie auf dem Blatt **Zuordnungen** unter **Eingeschlossene Gruppen** die Option **Alle Benutzenden hinzufügen**.
12. Wählen Sie **Weiter** aus.
13. Wählen Sie auf dem Blatt **Überprüfen + erstellen** die Option **Erstellen** aus.

Sie haben ein FileVault-Profil erfolgreich konfiguriert und bereitgestellt, um macOS-Geräte zu verschlüsseln.