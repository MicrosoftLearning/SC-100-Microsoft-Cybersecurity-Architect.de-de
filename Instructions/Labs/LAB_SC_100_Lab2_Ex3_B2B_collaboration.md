# Lab 2 – Übung 3 – Mandantenübergreifende Synchronisierung

Contoso hat kürzlich Tailwind Traders übernommen, und es war schwierig festzustellen, welche Gäste zur Kundschaft oder Partnerschaft gehören und welche Mitarbeitende des übernommenen Unternehmens sind. Ihre Aufgabe ist es, eine erste gemeinsame Adressliste von Tailwind Traders an Contoso zu übermitteln. Außerdem muss Ihr Mandant zulassen, dass nur bekannte Domainnamen als Gastbenutzende zu Entra ID hinzugefügt werden können. Sie möchten die Personen, die Gäste in die Organisation einladen können, auf interne Benutzende beschränken. Sie beschränken den externen Zugriff auf nur eine Domäne. Sie werden auch eine B2B-Zusammenarbeit und eine mandantenübergreifende Synchronisation von Tailwind Traders zu Contoso erstellen.

Als Fachkraft für Cybersicherheitsarchitektur müssen Sie sicherstellen, dass alle Anforderungen erfüllt sind und die erforderlichen Änderungen an entra ID implementieren, um Zero Trust-Prinzipien anzuwenden. In dieser Übung arbeiten Sie mit einem Lab-Partner zusammen, um eine mandantenübergreifende Synchronisierung zu erstellen. 

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept, um die Anforderungen von Contoso Ltd. und Tailwind Traders zu erfüllen.

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage des beschriebenen Szenarios zu analysieren, die Ziele zu verstehen und die Anforderungen zu definieren.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Synchronisieren der Benutzenden beider Unternehmen
- Externe Benutzende als externe Benutzende identifizierbar machen
- Einschränken von Einladungsrechten nur auf interne Mitarbeitende 
- Einschränken des externen Zugriffs auf vertrauenswürdige Unternehmensdomänen

Im zweiten Schritt untersuchen Sie die vorhandene Umgebung von Contoso Ltd.. Microsoft Entra ID bietet Lösungen, um die externe Zusammenarbeit zu aktivieren. Untersuchen Sie, welche Kontrollen bestehen und welche Richtlinien bereits eingesetzt werden. Verwenden Sie das Entra ID-Portal, um die aktuellen Konfigurationen und Richtlinien zu überprüfen und festzustellen, welche Anpassungen vorgenommen werden müssen, um die Anforderungen für das Carve-in zu erfüllen.

In der dritten Phase wird das Konzept der Lösung erarbeitet. Die Untersuchung hat ergeben, dass die mandantenübergreifende Synchronisierung der beste Weg ist, um eine Zusammenarbeit zu ermöglichen, die allen Anforderungen gerecht wird.  

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Einschränken von Einladungsrechten nur auf interne Mitarbeitende|Einstellungen für externe Zusammenarbeit|Einschränken von Einladungsrechten auf die Mitgliedschaft des Mandanten und bestimmte Admin-Einladungsrollen|
|Einladungen von allen außer der Liste der vertrauenswürdigen Domänen blockieren|Einstellungen für externe Zusammenarbeit|Erstellen einer Einladungs-Whitelist, einschließlich nur vertrauenswürdiger Domänen|
|Synchronisieren der Benutzenden beider Unternehmen|Entra-ID Mandantenübergreifende Synchronisierung|Einrichten der Zugriffsvertrauensstellung zwischen Entra-ID-Mandanten und Erstellen einer Konfiguration, die Benutzende mit dem anderen Mandanten synchronisiert|
|Externe Benutzende als externe Benutzende identifizierbar machen|Mandantenübergreifende Attributzuordnung|Bearbeiten Sie das Attribut displayName jeder synchronisierten benutzenden Person, indem Sie einen benutzerdefinierten Ausdruck mithilfe der Attribut-Zuordnungsfunktion der mandantenübergreifenden Synchronisationskonfiguration erstellen|

## Teil 2: Implementieren der Lösung (optional)

### Aufgabe 1 - Teamup und Vorbereitungen

In dieser Aufgabe überprüfen Sie die Voraussetzungen für eine mandantenübergreifende Synchronisierung und das Team mit einem Lab-Partner.

1. Melden Sie sich am Client 1 VM (LON-Sc1) als **lon-sc1\admin**-Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
2. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **https://entra.microsoft.com** und melden Sie sich beim Entra ID Portal als **MOD Administrator**admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandanten-ID ist, die Sie von Ihrem Labor-Hosting-Anbieter erhalten haben). Das Passwort der administrierenden Person sollte von Ihrem Lab-Hosting-Anbieter bereitgestellt werden.
3. Aktivieren Sie im Dialogfeld **Angemeldet bleiben?** das Kontrollkästchen **Dies nicht mehr anzeigen** und wählen Sie dann **Nein**.
4. Schließen Sie das Dialogfeld zum Speichern des Kennworts von unten, indem Sie Nie wählen, um die Anmeldeinformationen des globalen Admins nicht in Ihrem Browser zu speichern.
5. Navigieren Sie im linken Navigationsbereich zu **Identität** > **Übersicht**.
6. Notieren Sie sich die **Mandanten-ID** und die **Primärdomäne**, die auf der Registerkarte **Übersicht** angezeigt werden.
7. Tauschen Sie Ihre **Mandanten-ID** und **Primärdomäne** mit Ihrem Lab-Partner aus.

Sie sollten einen Plan haben, welche Topologie Sie verwenden möchten, welche Benutzenden für den ersten Synchronisierungstest in Frage kommen und wie Sie sie dem Entra ID-Mandanten von Contoso zuordnen möchten.

### Aufgabe 2 - Konfigurieren des mandantenübergreifenden Zugriffs

Da Sie nun die Informationen vorbereitet haben, die Sie für die Implementierung der mandantenübergreifenden Synchronisierung benötigen, führen Sie nun die notwendigen Schritte durch, damit Ihr Mandant auf den Mandanten Ihres Partners zugreifen kann und umgekehrt.

1. Sie sollten weiterhin im Entra ID Portal **https://entra.microsoft.com** angemeldet sein.
2. Navigieren Sie im linken Navigationsbereich zu **Identität** > **External Identities** > **Mandantenübergreifende Zugriffseinstellungen**.
3. Wählen Sie die Registerkarte „** Organisationseinstellungen**“ und dann **Organisation hinzufügen** aus.
4. Füllen Sie das Feld **Mandanten-ID oder Domänenname** mit der von Ihrem Lab-Partner bereitgestellten Mandanten-ID aus und wählen Sie **Hinzufügen** aus.
5. Wählen Sie unter **Eingangs-Zugriff** für Contoso die Option **Von Standard geerbt**, um auf die mandantenübergreifenden Synchronisierungseinstellungen für diesen bestimmten Mandanten zuzugreifen.
6. Aktivieren Sie unter den **Vertrauenseinstellungen** die Option **Einladungen automatisch beim Mandanten Contoso einlösen**.
7. Wählen Sie **Speichern**.
8. Aktivieren Sie unter **Mandantenübergreifende Synchronisierung** die Option **Benutzersynchronisierung in diesen Mandanten erlauben**.
9. Wählen Sie **Speichern** und schließen Sie den Dialog mit dem **X** in der oberen rechten Ecke.
10. Wählen Sie unter **Ausgangs-Zugriff** für Contoso die Option **Vom Standard geerbt**, um auf die mandantenübergreifenden Synchronisierungseinstellungen für diesen speziellen Mandanten zuzugreifen.
11. Aktivieren Sie unter **Vertrauenseinstellungen** die Option **Einladungen automatisch beim Mandanten Contoso einlösen**.
12.  Wählen Sie **Speichern** und schließen Sie den Dialog mit dem **X** in der oberen rechten Ecke.

Sie haben Ihren Mandanten aktiviert, beide Möglichkeiten mit dem Mandanten Ihres Partners zu synchronisieren, ohne dass Benutzende ihre Einladungen manuell einlösen müssen. 

### Aufgabe 3 - Einschränken des externen Zugriffs

In dieser Aufgabe schränken Sie die Möglichkeit ein, neue Gastbenutzende in Ihre Organisation einzuladen, indem Sie den Umfang der Benutzenden mit der Berechtigung zum Senden von Einladungen steuern. Sie beschränken den Bereich der Domänen, die als Gäste zur Mandantendomäne Ihres Partners eingeladen werden können.

1. Sie sollten weiterhin im Entra ID Portal **https://entra.microsoft.com** angemeldet sein.
2. Navigieren Sie im linken Navigationsbereich zu **Identität** > **External Identities** > **Einstellungen für externe Zusammenarbeit**.
3. Wählen Sie im Abschnitt **Einstellungen für Gasteinladungen** die Option **Mitgliedsbenutzende und Benutzende, die bestimmten Administrierendenrollen zugewiesen sind, können Gastbenutzende einladen, einschließlich Gäste mit Mitgliedsberechtigungen**.
4. Wählen Sie unter **Einschränkungen für die Zusammenarbeit** die Option **Einladungen nur für die angegebenen Domänen zulassen**.
5. Fügen Sie die Domäne Ihres Partners **WWLxZZZZZZ.onmicrosoft.com** hinzu (wobei ZZZZZZ die eindeutige Mandanten-ID Ihres Partners ist, die Sie von Ihrem Lab-Hosting-Anbieter erhalten haben).
6. Wählen Sie **Speichern**.

Sie haben nun eingeschränkt, wer einladen kann und wer zu Ihrem Mandanten eingeladen werden kann. 

### Aufgabe 4 - Erstellen einer Konfiguration

In dieser Aufgabe erstellen Sie eine grundlegende Konfiguration und testen die Verbindung mit dem anderen Mandanten.

1. Sie sollten weiterhin im Entra ID Portal **https://entra.microsoft.com** angemeldet sein.
2. Navigieren Sie im linken Navigationsbereich zu **Identität** > **Externe Identitäten** > **Mandantenübergreifende Synchronisierung** > **Konfigurationen**.
3. Erstellen Sie eine **Neue Konfiguration**.
4. Geben Sie den Namen **Mandantenübergreifende Synchronisierung** ein und wählen Sie **Erstellen**.
5. Unter **Bereitstellung** ändern Sie den **Bereitstellungsmodus** auf „Automatisch“.
6. Geben Sie in das Feld **Mandanten-ID** die Mandanten-ID Ihres Partners ein, die Sie in Aufgabe 1 notiert haben.
7. Wählen Sie **Verbindung testen** aus.
8. Wählen Sie **Speichern**.

Wenn Sie die Zugriffseinstellungen korrekt konfiguriert haben, sollten Sie eine Meldung sehen, dass die angegebenen Anmeldeinformationen autorisiert sind, die Bereitstellung zu aktivieren. Wenn die Testverbindung fehlschlägt, überprüfen Sie, ob Ihr Partner die richtige Domäne in Aufgabe 3 eingegeben und die mandantenübergreifende Synchronisierung wie in Aufgabe 2 beschrieben konfiguriert hat.

### Aufgabe 5 - Definieren des Benutzerbereichs

In dieser Aufgabe legen Sie fest, wer für die erste Synchronisierung in Frage kommt. 

1. Sie sollten immer noch im Entra ID-Portal **https://entra.microsoft.com** in den Bereitstellungs-Einstellungen Ihrer gerade erstellten Konfiguration angemeldet sein. Wenn nicht, befolgen Sie diese 3 Schritte, um wieder dorthin zu gelangen:
   1. Navigieren Sie im linken Navigationsbereich zu **Identität** > **Externe Identitäten** > **Mandantenübergreifende Synchronisierung** > **Konfigurationen**.
   2. Wählen Sie **Mandantenübergreifende Synchronisierung**
   3. Navigieren Sie zur **Bereitstellung**.
2. Erweitern Sie den Abschnitt **Einstellungen**.
3. Bestätigen Sie dass der Bereich Dropdown auf **Nur zugewiesene Benutzende und Gruppen synchronisieren** eingestellt ist.
4. Wenn Sie diese Einstellung ändern mussten, wählen Sie **Speichern**.
5. Wählen Sie im Navigationsbereich **Benutzende und Gruppen**.
6. Wählen Sie **Benutzer/Gruppe hinzufügen** aus.
7. Wählen Sie auf der Seite **Zuordnung hinzufügen** die Option **Keine ausgewählt**.
8. Suchen Sie nach **Rechtliches** und markieren Sie das **Rechtsteam** mithilfe des Kontrollkästchens, dann wählen Sie **Auswählen**.
9. Wählen Sie **Zuweisen**, um das aus zwei Benutzenden bestehende Team dem Geltungsbereich hinzuzufügen.

Sie haben nun Ihren ersten Geltungsbereich von Benutzenden für die Synchronisierung mit dem Mandanten Ihres Partners definiert.

### Aufgabe 6 - Überprüfung der Attributzuordnungen

In diesem Task überprüfen Sie die Attributzuordnungen und stellen sicher, dass die synchronisierten Benutzenden in der globalen Adressliste von Contoso angezeigt werden.

1. In den **Benutzende und Gruppen** Einstellungen Ihrer mandantenübergreifenden Synchronisationskonfiguration sollten Sie noch im Entra ID Portal **https://entra.microsoft.com** angemeldet sein. Falls nicht, folgen Sie diesen 2 Schritten, um zur Konfigurationsseite zurückzukehren:
   1. Navigieren Sie im linken Navigationsbereich zu **Identität** > **Externe Identitäten** > **Mandantenübergreifende Synchronisierung** > **Konfigurationen**.
   2. Wählen Sie **Mandantenübergreifende Synchronisierung**.
2. Navigieren Sie zu **Bereitstellung** und erweitern Sie den Abschnitt **Zuordnungen**.
3. Wählen Sie **Microsoft Entra ID-Benutzer bereitstellen** aus.
4. Unter dem Attribut **showInAddressList** wählen Sie Bearbeiten.
5. Stellen Sie sicher, dass der Zuordnungstyp auf **Konstant** und sein Wert auf **True** festgelegt ist.
6. Klicken Sie auf **OK**.
7. Unter dem Attribut **displayName** wählen Sie **Bearbeiten**.
8. Ändern Sie den Zuordnungstyp in **Ausdruck**.
9. Entfernen Sie den bereits vorhandenen Ausdruck.
10. Wählen Sie **Verwenden Sie die Ausdruckserstellung**.
11. Wählen Sie die Funktion **Anhängen**.
12. Wählen Sie das Attribut **[displayName]** aus.
13. Geben Sie **„ (Contoso)“** ein, einschließlich des Leerzeichens vor der Klammer, aber ohne Anführungszeichen.
14. Wählen Sie **Ausdruck hinzufügen**.
    -  Ihr Ausdruck auf der rechten Seite sollte wie `Append([displayName], " (Contoso)")` aussehen
15. Sie können Ihren Ausdruck testen, indem Sie einen Benutzenden auswählen.
16. Wählen Sie **Ausdruck anwenden** und wählen Sie **Ok**, um den Bearbeitungsdialog zu verlassen.
17. Wählen Sie **Speichern**.
18. Schließen Sie die Seite „ Zuordnen von Attributen “, indem Sie das **X** in der oberen rechten Ecke auswählen.

Sie haben nun sichergestellt, dass alle synchronisierten Benutzenden in der globalen Adressliste des anderen Mandanten auftauchen. Außerdem haben Sie dem angezeigten Benutzernamen jedes synchronisierten Benutzenden im anderen Mandanten einen (Contoso)-Ausdruck hinzugefügt.

### Aufgabe 7 - Aktivieren Sie die Bereitstellung und testen Sie mit Ihrem Übungspartner

Mit dieser Aufgabe aktivieren Sie die Bereitstellung und testen, ob Ihre Benutzenden im anderen Mandanten so angezeigt werden, wie Sie es benötigen. Da die automatische Bereitstellung einige Zeit dauern kann, werden wir eine manuelle Bereitstellung auslösen.

1. Sie sollten noch im Entra ID Portal **https://entra.microsoft.com** in den Provisioning-Einstellungen Ihrer mandantenübergreifenden Synchronisationskonfiguration angemeldet sein. Falls nicht, folgen Sie diesen 2 Schritten, um zur Konfigurationsseite zurückzukehren:
   1. Navigieren Sie im linken Navigationsbereich zu **Identität** > **Externe Identitäten** > **Mandantenübergreifende Synchronisierung** > **Konfigurationen**.
   2. Wählen Sie **Mandantenübergreifende Synchronisierung**
2. Navigieren Sie zu **Bereitstellung bei Bedarf**.
3. Suchen Sie nach **Grady Archie** als Mitglied des **Rechtsteams**.
4. Wählen Sie **Bereitstellen** aus.
    - Sie erhalten eine Bestätigung, sobald die Bereitstellung abgeschlossen ist.
5. Schließen Sie die Seite Aktion durchführen, indem Sie das **X** in der oberen rechten Ecke wählen.

Sie haben soeben Ihren ersten Benutzenden manuell eingerichtet, und wenn Sie die Benutzerliste Ihres Partner-Mandanten überprüfen, sehen Sie den Benutzer Grady Archie (Contoso).

### Aufgabe 8 - Ausführen der vollständigen Synchronisierung

Da die erste Benutzerbereitstellung erfolgreich testet wurde, stellen Sie nun die restliche Benutzerliste für den anderen Mandanten bereit.

1. Sie sollten weiterhin im Entra ID Portal **https://entra.microsoft.com** auf der Seite **Bereitstellung bei Bedarf** Ihrer mandantenübergreifenden Synchronisationskonfiguration angemeldet sein. Falls nicht, folgen Sie diesen 2 Schritten, um zur Konfigurationsseite zurückzukehren:
   1. Navigieren Sie im linken Navigationsbereich zu **Identität** > **Externe Identitäten** > **Mandantenübergreifende Synchronisierung** > **Konfigurationen**.
   2. Wählen Sie **Mandantenübergreifende Synchronisierung**
2. Wählen Sie **Benutzer und Gruppen** aus.
3. Wählen Sie **Benutzer/Gruppe hinzufügen** aus.
4. Wählen Sie auf der Seite **Zuordnung hinzufügen** die Option **Keine ausgewählt**.
5. Wählen Sie die Gruppe **Alle mitarbeitenden Personen**, da diese Gruppe **alle mitarbeitenden Personen von Contoso** enthält.
6. Bestätigen Sie Ihre Auswahl.
7. Wählen Sie **Zuweisen** aus.

Sie haben nun erfolgreich eine mandantenübergreifende Synchronisation zwischen Ihrem Mandanten und einem anderen Mandanten erstellt. Sie sollten in der Lage sein, alles, was Sie in Ihrem Demo-Mandanten gemacht haben, an das produktive System von Tailwind Traders anzupassen und ihnen bei der Integration in Contoso zu helfen.
