---
lab: 3
title: Übung 3 – Vorbereiten des Datenschutzrisikomanagements
---


# Lab 3 – Übung 3 – Vorbereiten des Datenschutzrisikomanagements

Als Fachkraft für Cybersicherheit und Architekt für Contoso wurden Sie damit beauftragt, die Compliance-Strategie des Unternehmens im Rahmen seiner europäischen Expansion zu verbessern. Insbesondere arbeiten Sie daran, die Priva Privacy Risk Management-Bewertung zu verbessern. Dazu verwenden Sie den Compliance-Manager, um Verbesserungsmaßnahmen zu identifizieren und deren Implementierung zu delegieren. Dies führt zu einer Verbesserung der Compliancebewertung des Datenschutzrisikomanagements. Außerdem fügen Sie eine neue Richtlinie für die Regionen USA und EU hinzu. 

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept, um die Anforderungen von Contoso Ltd. zu erfüllen.

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage des beschriebenen Szenarios zu analysieren, die Ziele zu verstehen und die Anforderungen zu definieren.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Admins und andere Benutzende mit Zugriff auf Berichte sollten die Namen der Benutzenden nicht sehen.
- Datenschutzrisiken müssen von einem bestimmten Team verwaltet werden.
- Richtlinien müssen für Datenschutzrisiken vorhanden sein.

Im zweiten Schritt untersuchen Sie die vorhandene Umgebung von Contoso Ltd. Microsoft Priva bietet Lösungen zum Verwalten von Datenschutzrisiken. Untersuchen Sie, welche Kontrollen bestehen und welche Richtlinien bereits eingesetzt werden. Verwenden Sie das Microsoft Purview Compliance-Portal, um aktuelle Konfigurationen zu überprüfen und zu bestimmen, welche Anpassungen implementiert werden müssen, um die Anforderungen für die Region zu erfüllen, auf die sie erweitert werden.

In der dritten Phase wird das Konzept der Lösung erarbeitet. Bei der Untersuchung ist offensichtlich, dass die Schaffung von Richtlinien zur Überwachung potenzieller Risiken die beste Möglichkeit ist, die Anforderungen zu erfüllen.  

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Admins und andere Benutzende mit Zugriff auf Berichte sollten die Namen der Benutzenden nicht sehen.|Compliance-Verbesserungsaktionen|Zuweisen und Implementieren der Verbesserungsaktion **Anonymisieren von Benutzernamen für Benutzende in bestimmten Rollen**|
|Datenschutzrisiken müssen von einem bestimmten Team verwaltet werden.|Microsoft Purview-Rollen|Erstellen einer Rollengruppe mit Berechtigungen zur Behandlung von Datenschutzrisiken und Zuweisen der festgelegten Mitarbeitenden|
|Richtlinien müssen für Datenschutzrisiken vorhanden sein.|Richtlinien zum Datenschutz-Risikomanagement|Erstellen einer Richtlinie für das Datenschutzrisikomanagement, um das Datenschutz-Risikomanagementteam über potenzielle Risiken zu informieren|

## Teil 2: Implementieren der Lösung (optional)

## Aufgabe 1: Sehen Sie sich mögliche Verbesserungsmaßnahmen des Compliance-Managers für das Datenschutzrisikomanagement an, und weisen Sie ihnen Besitzende zu.

In dieser Aufgabe erhalten Sie einen Überblick über mögliche Verbesserungsmaßnahmen im Datenschutzrisikomanagement und delegieren diese.

1. **Melden Sie sich** beim **Microsoft Purview Compliance-Portal****https://compliance.microsoft.com/** an.
2. Wählen Sie im linken Bereich **Übersicht über Datenschutzrisikomanagement**.
3. Blättern Sie nach unten zur Karte **Bleiben Sie auf dem Laufenden mit den Vorschriften und verbessern Sie Ihren Datenschutz**.
4. Wählen Sie die Schaltfläche **Verbesserungsaktionen anzeigen**.
5. Sehen Sie sich die möglichen Verbesserungsaktionen an. Überlegen Sie, welche Verbesserungsaktionen vorab konfiguriert werden können und welche an das Sicherheitsteam delegiert werden können.
6. Wählen Sie die Verbesserungsaktion **Admins für Vorgänge zum Datenschutz aktivieren, um die Erfüllung von Anfragen zu Subjektrechten zu erstellen und zu unterstützen** aus.
7. Lesen Sie die Details der Verbesserung.
8. Weisen Sie **Megan Bowen** als Besitzerin der Verbesserungsaktion mithilfe des Dropdownmenüs zu.
9. Wählen Sie oben auf der Seite **Details bearbeiten** aus.
10. Legen Sie den **Implementierungsstatus** auf **Implementiert** fest. Weil Sie **Megan Bowen** in der letzten Übung die Admin-Rollen für Subjektrechteanfragen und Datenschutzrisikomanagement zugewiesen haben.
11. Wählen Sie anschließend **Speichern und schließen** oben auf der Seite.

Sie haben einem Sicherheitsmitarbeitenden erfolgreich eine Verbesserungsaktion zugewiesen.

## Aufgabe 2 – Zuweisen und Implementieren der Verbesserungsaktion **Anonymisieren von Benutzernamen für Benutzende in bestimmten Rollen**

Sie müssen sicherstellen, dass die Benutzenden in allen Priva-Komponenten für die Verbesserungsaktion anonymisiert sind.

*Fahren Sie mit 5. fort, wenn Sie sich noch in der **Übersicht der Verbesserungsaktion befinden.***
1. **Melden Sie sich** beim **Microsoft Purview Compliance-Portal****https://compliance.microsoft.com/** an.
1. Wählen Sie **Compliance Manager** > **Verbesserungsaktionen**.
1. Wählen Sie die Verbesserungsaktion **Benutzernamen für Benutzende in bestimmten Rollen anonymisieren**.
1. Weisen Sie sich selbst **MOD-Administrator** als Besitzer für diese Verbesserungsaktion zu, indem Sie das Dropdown-Menü verwenden.
1. Wählen Sie unter **Details** den Link **Jetzt starten** am Ende der Beschreibung **Wie wird implementiert**.
1. Prüfen Sie, ob die Einstellung **Anonymisierte Versionen der Benutzernamen anzeigen** festgelegt ist. Wenn nicht, wählen Sie sie aus und wählen Sie **Speichern**.
1. Schließen Sie die Browser-Registerkarte.
1. Wählen Sie **Details bearbeiten** am oberen Rand der Verbesserungsaktion **Anonymisierte Versionen von Benutzernamen anzeigen**.
1. Legen Sie den **Implementierungsstatus** auf **Implementiert** fest und wählen Sie **Speichern**.
1. Wählen Sie anschließend **Speichern und schließen** oben auf der Seite.

Sie haben erfolgreich eine Verbesserungsaktion zugewiesen und implementiert.

## Aufgabe 3 – Erstellen einer Richtlinie für das Datenschutzrisikomanagement

Bei dieser letzten Aufgabe geht es um die Erstellung der benutzerdefinierten Datenschutzrisikomanagement-Richtlinie für die Regionen EU und USA.

1. Wechseln Sie zum **Microsoft Purview-Complianceportal****https://compliance.microsoft.com/**
2. Wählen Sie im linken Bereich **Datenschutzrisikomanagement** > **Richtlinien**.
3. Wählen Sie oben rechts **Richtlinie erstellen**.
4. Wählen Sie **Erstellen** in der **Kundenkarte**.
5. Wählen Sie die Richtlinienvorlage **Datenminimierung**.
6. Geben Sie den Namen der Richtlinie ein:**Datenminimierung USA und EU**.
7. Geben Sie die Beschreibung ein:**Diese Richtlinie soll das Risiko der Speicherung von datenschutzrelevanten Daten gemäß den Bestimmungen der USA und der EU minimieren.**
8. Wählen Sie **Weiter** aus.
9. Wählen Sie **Klassifizierungsgruppen hinzufügen**.
10. Wählen Sie Folgendes aus:
    - DSGVO erweitert
    - U. S. amerikanisches Gesetz "Gramm-Leach-Bliley Act" (GLBA) erweitert
    - U.S. Health Insurance Act (HIPAA) erweitert
    - U.S. Patriot Act Enhanced erweitert
    - U.S. Personally identifiably Information (PII) Daten erweitert
    - U.S. State Breach Notification Laws erweitert
11. Wählen Sie **Hinzufügen** und **Weiter**.
12. Markieren Sie alle Benutzenden und Gruppen und wählen Sie **Weiter**.
13. Markieren Sie alle Orte und wählen Sie **Weiter**.
14. Legen Sie die Einstellung **Eintrag wurde in den letzten (Tagen) nicht geändert** auf 120 fest.
15. Für **Wählen Sie die Häufigkeit der Benachrichtigungen**, wählen Sie **Monatlich, jeden 1**.
16. Für den **Link zum Datenschutztraining** geben Sie ein: https://learn.microsoft.com/en-us/privacy/
17. Wählen Sie **Weiter** aus.
18. Legen Sie **Warnungen erstellen** auf **Ein** fest.
19. Legen Sie **Hohes Volumen an persönlichen Daten** auf 20 Instanzen fest.
20. Wählen Sie **Weiter** aus.
21. Wählen Sie **Weiter** aus.
22. Legen Sie Ihre Einstellungen fest und wählen Sie **Übermitteln**.

Sie haben erfolgreich eine Richtlinie zum Datenschutzrisikomanagement für die Datenschutzgesetze der USA und der EU erstellt.

Sie haben erfolgreich einige Verbesserungsaktionen, Richtlinien zum Datenschutzrisikomanagement und Benutzerberechtigungen eingerichtet und delegiert. Sie können mit der nächsten Übung fortfahren.
