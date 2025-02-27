# Kompatibilitätsbewertung

## Lab-Szenario Einführung

Sie sind Allan Deyoung, Mitglied der IT-Abteilung von Contoso Ltd. Sie wurden kürzlich in den Geschäftsbereich IT-Sicherheit versetzt. Ihre neue Aufgabe ist es, die Zero-Trust-Bereitschaft von Contoso zu bewerten und einen Aktionsplan für die Einführung einer Zero-Trust-Initiative zu entwickeln, die den Zero-Trust-Säulen folgt. Contoso ist ein großes multinationales Unternehmen mit globaler Präsenz in mehreren Branchen. Das Unternehmen verfügt über einen großen Cloud-Speicherbedarf und eine Hybridinfrastruktur. Das Security Operations Center (SOC) von Contoso ist für die Überwachung und Reaktion auf Sicherheitsvorfälle im gesamten Unternehmen verantwortlich. Das SOC ist mit Sicherheitsanalytikern bzw. -analytikerinnen, technischen Fachkräften für Sicherheit und Netzwerktechnikern bzw. -technikerinnen besetzt. Das SOC verwendet Microsoft Sentinel als SIEM-Lösung (Security Information & Event Management). Das SOC verfügt über einen Log Analyticvs-Arbeitsbereich, in dem Sicherheitsprotokolle aus dem gesamten Unternehmen gesammelt und analysiert werden.

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

1. Melden Sie sich beim Microsoft Purview Compliance Portal **`https://purview.microsoft.com/`** als Allan Deyoung mit seinem Administratorkonto **MOD-Admin** an.
1. Wenn Sie aufgefordert werden, die mehrstufige Authentifizierung einzurichten, befolgen Sie die Anweisungen.
1. Sie gelangen zur neuen Landing Page des Microsoft Purview-Portals. Aktivieren Sie das Kästchen neben der Erklärung **Ich stimme den Bedingungen für die Offenlegung des Datenflusses und den Datenschutzerklärungen zu** und wählen Sie dann **Erste Schritte** aus.
1. Wählen Sie im linken Navigationsbereich **Lösungen** und dann **Compliance Manager**. Alternativ können Sie im Hauptfenster die Kachel **Alle Lösungen anzeigen** und dann die Kachel **Compliance-Manager** auswählen, die unter Risiko und Compliance aufgeführt ist.
1. Wählen Sie im Bereich **Compliance-Manager** auf der linken Seite **Bewertungen**.
1. Wählen Sie im Fenster **Bewertungen** die Option **+ Bewertung hinzufügen**.
1. Wählen Sie im Fenster **Bewertung auf einer Vorschrift basieren** die Option **Vorschrift auswählen**.
1. Geben Sie in das Suchfeld **`ISO/IEC 27001:2022`** ein, wählen Sie dann die Verordnung aus, wählen Sie **Speichern** und dann **Weiter**.
1. Auf der Seite **Namen und Gruppe hinzufügen** geben Sie in das Textfeld **Bewertungsname** **`ISO-27001 Audit assessment`** ein. Belassen Sie die Einstellung **Bewertungsgruppe** auf **Vorhandene Gruppe verwenden** mit der **Standardgruppe**, und wählen Sie dann **Weiter**.
1. Auf der Seite **Dienste auswählen** sollte der Dienst **Microsoft 365** bereits aufgeführt sein.  Wenn nicht, wählen Sie **Dienste auswählen** und wählen Sie **Microsoft 365** und wählen Sie **Hinzufügen**. Wählen Sie **Weiter** aus.
1. Auf der Seite **Überprüfen und beenden** wählen Sie **Bewertung erstellen**. Es dauert ein paar Sekunden, bis die Bewertung erstellt ist, dann wählen Sie **Erledigt**.
1. Sie sollten sich nun auf der neu erstellten Seite **ISO-27001-Überwachungsbewertung** befinden.
1. Lassen Sie diese Registerkarte für die nächste Aufgabe geöffnet.

Sie haben erfolgreich eine Bewertung basierend auf ISO-27001 erstellt.

### Aufgabe 2: Zuweisen von Aufgaben an einen technischen Ingenieur

Die Ergebnisse der Bewertung zeigen Ihnen unterschiedliche Bereiche und Maßnahmen, die für die Einhaltung der ISO-27011-Vorschriften unerlässlich sind. Sie werden Verbesserungsmaßnahmen untersuchen und einem technischen Ingenieur eine Aufgabe zuweisen.

1. Sie sollten immer noch auf der Seite für die soeben erstellte Bewertung **ISO-27001-Überwachungsbewertung** sein.  Falls nicht, navigieren Sie zum Microsoft Purview-Portal **`https://purview.microsoft.com/`** und wählen Sie dort **Lösungen** > **Compliance Manager** > **Bewertungen** > **ISO-27001 Überwachungsbewertung**
1. Wählen Sie auf der Seite **ISO-27001 Überwachungsbewertung** **Ihre Verbesserungsmaßnahmen**.
1. Legen Sie den Filter für **Steuerelementengruppe** auf **Physisch Steuerelemente** fest.
1. Markieren Sie das Kästchen neben **Verbesserungsmaßnahme**, um alle angezeigten Verbesserungsmaßnahmen auszuwählen, und wählen Sie dann **Benutzender zuweisen** (oberhalb der Filteroptionen).
1. Im neuen Fenster **Verbesserungsmaßnahmen zuweisen** geben Sie in das Suchtextfeld **`Nestor`** ein und drücken die Eingabetaste.
1. Wählen Sie den Benutzenden und wählen Sie **Zuweisen**.
1. Lassen Sie diese Registerkarte für die nächste Aufgabe geöffnet.

Sie haben eine Verbesserungsaktion erfolgreich einer technischen Ingenieurs-Fachkraft angezeigt und zugewiesen.

### Aufgabe 3: Bereitstellen des Zugriffs für einen technischen Ingenieur für die Verbesserungsmaßnahmen

Die Benutzenden benötigen Zugriff, um die ihnen zugewiesenen Aufgaben einzusehen. Sie gewähren Nestor Wilke Zugriff auf die Bewertung.

1. Sie sollten sich immer noch auf der Registerkarte **Ihre Verbesserungsmaßnahmen** für die Seite **ISO-27001 Überwachungsbewertung** befinden.  Falls nicht, navigieren Sie zum Microsoft Purview-Portal **`https://purview.microsoft.com/`** und wählen Sie dort **Lösungen** > **Compliance Manager** > **Bewertungen** > **ISO-27001 Überwachungsbewertung** > **Ihre Verbesserungsmaßnahmen**.
1. Wählen Sie in der oberen rechten Ecke der Seite **ISO/IEC 27001: Bewertung** die Option **Benutzerzugriff verwalten**.
1. Wählen Sie im neuen Fenster **Benutzerzugriff verwalten** die Registerkarte **Prüfer** und wählen Sie **Prüfer hinzufügen**.
1. Geben Sie in das Textfeld **Suche nach Benutzenden** **`Nestor`** ein und drücken Sie die Eingabetaste.
1. Markieren Sie den Benutzenden und wählen Sie **Anwenden**, dann **Speichern**.
1. Sie haben Nestor Wilke erfolgreich die Rolle des Prüfers für diese Beurteilung zugewiesen.
1. Sie können nun das Microsoft Purview-Portal beenden, indem Sie die Registerkarte des Browsers schließen.

Sie haben Nestor Wilke erfolgreich die Rolle des Prüfers für diese Beurteilung zugewiesen.
