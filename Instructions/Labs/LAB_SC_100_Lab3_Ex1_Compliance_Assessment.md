---
lab: 3
title: Übung 1 – Compliancebewertung
---

# Lab 3 – Übung 1 – Compliancebewertung

Contoso Ltd. expandiert nach Europa, um den Umsatz zu steigern, hat aber Schwierigkeiten, die Anforderungen der Kundschaft an die IT-Sicherheit zu erfüllen. Kunden möchten, dass Contoso eine sichere Umgebung verwaltet, um die sichere Zusammenarbeit zu erleichtern und das Risiko von Datenlecks und kompromittierten Unternehmensressourcen zu minimieren. Viele Kunden verlangen Beweise für gut etablierte IT-Geschäftsprozesse und einen soliden Sicherheitsframework, der häufig in Form einer ISO-27001-Zertifizierung erbracht wird. Um dies zu adressieren, hat Contoso beschlossen, eine externe Überwachungsfirma zu beauftragen, die ISO-27001-Überwachung durchzuführen und die Zertifizierung zu erhalten. Es ist notwendig, den aktuellen Stand der Organisation zu bewerten und einen Aktionsplan zur Erfüllung der ISO-27001-Anforderungen zu entwickeln. Als Cybersicherheitsarchitektur entwerfende Person des Unternehmens werden Sie damit beauftragt, die vorhandenen Lücken zu identifizieren und Personen innerhalb der Organisation bestimmte Aufgaben zuzuweisen, um sie zu lösen.

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept zur Bewältigung der Herausforderungen, mit denen Contoso Ltd. konfrontiert ist.

### Entwurfsansatz

Um das beschriebene Problem wirksam zu adressieren, ist es entscheidend, ISO 27001 gründlich zu verstehen. Es ist wichtig, die Einrichtung von Contoso anhand der ISO 27001-Normen zu bewerten und etwaige Unstimmigkeiten für die Analyse aufzuzeigen. Dieser Prozess kann aufgrund der Komplexität der M365-Umgebung und der Vorschriften für 27001 zeitaufwändig sein. Die Bewertung durch den Microsoft Compliance-Manager vereinfacht diese Analyse jedoch.

Compliance-Manager-Bewertungen von Microsoft sind Gruppierungen von Kontrollen aus bestimmten Vorschriften, Standards oder Richtlinien. Sie helfen Ihnen, sicherzustellen, dass Ihre Organisation die Anforderungen verschiedener Standards, Vorschriften oder Gesetze erfüllt. Wenn Sie zum Beispiel alle Aktionen innerhalb einer Bewertung durchführen, können Sie Ihre Microsoft 365-Einstellungen nach den ISO 27001-Anforderungen ausrichten. Die Bewertungen umfassen mehrere Komponenten und bieten Vorlagen für über 360 Vorschriften, die die notwendigen Kontrollen und Schritte für eine wirksame Bewertung Ihrer Compliance enthalten. 

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Vergleich der M365-Umgebung mit den ISO 27001-Vorschriften|Grundlegendes zum Compliance-Manager für Microsoft Purview|Bewertung erstellen|
|Erstellen eines Aktionsplans|Grundlegendes zum Compliance-Manager für Microsoft Purview|Zuweisung von Aufgaben an einen technischen Ingenieur bzw. ein technische Ingenieurin|

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1: Durchführen einer ISO-27001-Bewertung

Ihr erster Schritt besteht darin, die aktuelle Umgebung des Unternehmens zu analysieren. Sie führen eine Konformitätsbewertung durch, um zu analysieren, inwieweit die Umgebung von Contoso den ISO-27001-Vorschriften entspricht.

1. Melden Sie sich beim Microsoft Purview Compliance Portal **https://compliance.microsoft.com/** als Allan Deyoung mithilfe seines Administratorkontos **MOD Administrator** an.
2. Sie werden aufgefordert, die Multifaktor-Authentifizierung einzurichten, folgen Sie den Anweisungen.
3. Wählen Sie im Microsoft Purview-Complianceportal auf der linken Navigationsseite **Compliance-Manager**.
4. Wählen Sie auf der Seite **Compliance-Manager** die Option **Bewertung**.
5. Wählen Sie auf der Seite **Compliance-Manager \|Bewertungen** die Option **+ Bewertung hinzufügen**.
6. Wählen Sie auf der Seite **Ihre Bewertung auf einer Vorschrift basieren** die Option **Vorschrift auswählen**.
7. Geben Sie in das Suchfeld **ISO-27001:2022** ein, wählen Sie die Vorschrift aus, wählen Sie **Speichern** und dann **Weiter**.
8. Auf der Seite **Namen und Gruppe hinzufügen** geben Sie in das Textfeld **Name der Bewertung** **ISO-27001 Überwachungsbewertung** ein und wählen dann **Weiter**.
9. Auf der Seite **Dienste auswählen** wählen Sie **Dienste auswählen** und wählen Sie **Microsoft 365** und wählen Sie **Hinzufügen** und dann **Weiter**
10. Beenden Sie die Konfiguration, und erstellen Sie die Bewertung.

Sie haben erfolgreich eine Bewertung basierend auf ISO-27001 erstellt.

### Aufgabe 2: Zuweisen von Aufgaben an einen technischen Ingenieur

Die Ergebnisse der Bewertung zeigen Ihnen unterschiedliche Bereiche und Maßnahmen, die für die Einhaltung der ISO-27011-Vorschriften unerlässlich sind. Sie werden Verbesserungsmaßnahmen untersuchen und einem technischen Ingenieur eine Aufgabe zuweisen.

1. Sie sollten weiterhin im Microsoft Purview-Complianceportal **https://compliance.microsoft.com/** angemeldet sein.
2. Wählen Sie im Microsoft Purview-Complianceportal auf der linken Navigationsseite **Compliance-Manager**.
3. Wählen Sie auf der Seite **Compliance-Manager** die von Ihnen erstellte Bewertung **ISO/IEC-27001:2022**.
4. Wählen Sie auf der Bewertungsseite die Klinge **Ihre Verbesserungsaktionen**.
5. Legen Sie den Filter für **Steuerelementengruppe** auf **Physisch Steuerelemente** fest.
6. Markieren Sie alle angezeigten Verbesserungsaktionen und wählen Sie dann **Benutzer zuweisen**.
7. Geben Sie auf der neuen Seite **Verbesserungsaktionen zuweisen** im Suchtextfeld **Nestor Wilke** ein.
8. Wählen Sie den Benutzenden und wählen Sie **Zuweisen**.

Sie haben eine Verbesserungsaktion erfolgreich einer technischen Ingenieurs-Fachkraft angezeigt und zugewiesen.

### Aufgabe 3: Bereitstellen des Zugriffs für eine technische Ingenieurs-Fachkraft für die Verbesserungsaktionen.

Die Benutzenden benötigen Zugriff, um die ihnen zugewiesenen Aufgaben einzusehen. Sie gewähren Nestor Wilke Zugriff auf die Bewertung.

1. Sie sollten weiterhin im Microsoft Purview-Complianceportal **https://compliance.microsoft.com/** angemeldet sein.
2. Wählen Sie im Microsoft Purview-Complianceportal im linken Navigationsbereich **Compliance-Manager**.
3. Wählen Sie auf der Seite **Compliance-Manager** den Bereich **Bewertung** und wählen Sie dann die **ISO-27001 Auditbewertung**.
4. Wählen Sie auf der Seite **ISO/IEC 27001: Beurteilung** in der oberen rechten Ecke die Option **Benutzerzugriff verwalten**.
5. Auf der neuen Seite **Benutzerzugang verwalten** wählen Sie **Begutachter** und wählen Sie **Begutachter hinzufügen**.
6. Geben Sie in das Textfeld **Nach Benutzern suchen** **Nestor Wilke** ein.
7. Markieren Sie den Benutzenden und wählen Sie dann **Speichern** aus.

Sie haben Nestor Wilke erfolgreich Zugriff auf die Bewertung gewährt.
