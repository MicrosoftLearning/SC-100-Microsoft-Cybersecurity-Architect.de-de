# Konfigurieren der Entra-ID

Sie sind Allan Deyoung, der neu beförderte IT-Sicherheitsspezialist von Contoso Ltd. Da das Unternehmen kürzlich Tailwind Traders übernommen hat, haben Sie Ihren Entra ID-Mandanten überprüft und neue Sicherheitsanforderungen festgelegt. Ihre Aufgabe ist es, die Aufgaben zu verwalten und Strategien umzusetzen, um die mit dem Unternehmenskauf verbundenen Anforderungen zu erfüllen.

Sie haben Unternehmensanwendungen überprüft und festgestellt, dass einige Benutzende einer Drittanbieteranwendung Zugriffsrechte auf ihre Postfachdaten erteilt haben. Dies stellt ein potenzielles Risiko für Datenverluste bei der E-Mail-Korrespondenz dar. Daher möchten Sie dieses Verhalten einschränken, den Benutzenden aber erlauben, sich bei von Microsoft validierten Websites anzumelden und Anmelde-IDs weiterzugeben. Außerdem möchten Sie den Benutzenden die Möglichkeit geben, unter Verwendung ihrer Entra ID-Identität spezifischen Zugriff auf die neuen SaaS-Produkten zu beantragen. 

Da eine Partnerorganisation vor kurzem durch das Abfangen von SMS angegriffen wurde, möchten Sie die Authentifizierungssicherheit gemäß NIST durchsetzen. Um dies zu erreichen, erstellen Sie eine Richtlinie zur Authentifizierungsstärke, um SMS OTP zu deaktivieren und die Verwendung von AAL1-Authentifizierungsmethoden in Ihrem Unternehmen einzuschränken. Sie werden diese Konfiguration im Entra ID Portal erstellen.

## Teil 1: Entwerfen einer Lösung (erforderlich)

In dieser Aufgabe entwerfen Sie ein Konzept zur Bewältigung der Risiken, denen Contoso Ltd. ausgesetzt ist.

### Entwurfsansatz

Der erste Schritt besteht darin, die Anforderungen auf der Grundlage der beschriebenen Problematik zu analysieren, die Ziele zu verstehen und die Anforderungen zu definieren.

Auf der Grundlage des vorliegenden Anwendungsfalls können die folgenden Anforderungen skizziert werden:

- Einschränkung des unkontrollierten Zugriffs von Drittanbieteranwendungen
- Benutzenden die gemeinsame Nutzung von Anmeldungs-IDs für geprüfte Dienste ermöglichen
- Benutzenden die Anforderung des Zugriffs auf SaaS-Produkte ermöglichen
- Verbessern der Authentifizierungsstärke

Im zweiten Schritt untersuchen Sie die vorhandene Umgebung von Contoso Ltd.. Microsoft Entra ID bietet Lösungen zur Verwaltung und Einschränkung des Zugriffs von Benutzenden und Cloudanwendungen mit Hilfe von Entra ID-Richtlinien. Untersuchen Sie, welche Kontrollen bestehen und welche Richtlinien bereits eingesetzt werden. Verwenden Sie das Entra ID Portal, um die aktuellen Konfigurationen und Richtlinien zu überprüfen und festzustellen, ob Anpassungen erforderlich sind oder neue Richtlinien implementiert werden müssen.

In der dritten Phase wird das Konzept der Lösung erarbeitet. Bei der Untersuchung ist offensichtlich, dass keine der aktuellen Richtlinien die definierten Anforderungen erfüllt. Daher sind Anpassungen an die Entra ID-Konfiguration unerlässlich.

### Vorgeschlagene Lösung

|Anforderung|Lösung|Maßnahmenplan|
|----|----|----|
|Blockieren des unkontrollierten Zugriffs von Drittanbieteranwendungen|Entra-ID-Anwendungsrichtlinie|Beschränken Sie die Zustimmung der Benutzenden auf Berechtigungen, die als „mit geringer Auswirkung“ eingestuft werden, für Apps von verifizierten Herausgebern oder für Apps, die in dieser Organisation registriert sind|
|Benutzenden die gemeinsame Nutzung von Anmeldungs-IDs für geprüfte Dienste ermöglichen|Entra-ID-Anwendungsrichtlinie|Beschränken Sie die Zustimmung der Benutzenden auf Berechtigungen, die als „mit geringer Auswirkung“ eingestuft werden, für Apps von verifizierten Herausgebern oder für Apps, die in dieser Organisation registriert sind|
|Benutzenden die Anforderung des Zugriffs auf SaaS-Produkte ermöglichen|Entra-ID-Anwendungsrichtlinie|Definition von Benutzenden, die berechtigt sind, Anwendungen zu genehmigen, die sicher zu verwenden sind|
|Einschränken der Verwendung unsicherer Authentifizierungsmethoden|Entra ID-Authentifizierungsmethoden|Erstellen einer Authentifizierungsstärke ohne SMS- und VoIP-Methoden|

## Teil 2: Implementieren der Lösung (optional)

**Hinweis:** Diese Lab-Schritte müssen im M365 Lab-Profil ausgeführt werden.

### Aufgabe 1: Einschränken der Verwendung von Drittanbieter-Apps auf überprüfte Microsoft-Dienste

In dieser Aufgabe schränken Sie die Zugriffsebene ein, die eine benutzende Person für Anwendungen gewähren kann. Außerdem fügen Sie die Funktionalität für Benutzende hinzu, um den Zugriff anzufordern, den sie nicht selbst zulassen können. 

1. Melden Sie sich am Client 1 VM (LON-Sc1) als **lon-sc1\admin**-Konto an. Das Passwort sollte von Ihrem Provider für die Übung bereitgestellt werden.
1. Öffnen Sie **Microsoft Edge**, wählen Sie die Adressleiste, navigieren Sie zu **`https://entra.microsoft.com`** und melden Sie sich beim Entra ID Portal als **MOD-Fachkraft in der IT-Verwaltung**admin@WWLxZZZZZZ.onmicrosoft.com an (wobei ZZZZZZ Ihre eindeutige Mandanten-ID ist, die Sie von Ihrem Lab-Hosting-Anbieter erhalten haben). Das Administratorpasswort sollte von Ihrem Lab-Hosting-Anbieter bereitgestellt werden.
1. Wenn Sie aufgefordert werden, die mehrstufige Authentifizierung einzurichten, befolgen Sie die Anweisungen.
1. Aktivieren Sie im Dialogfeld **Angemeldet bleiben?** das Kontrollkästchen **Dies nicht mehr anzeigen** und wählen Sie dann **Nein**.
1. Schließen Sie das Dialogfeld zum Speichern des Kennworts, indem Sie **Nicht jetzt** wählen, um die Anmeldedaten des globalen Standardadmins nicht in Ihrem Browser zu speichern.
1. Navigieren Sie im linken Navigationsbereich zu **Identität** > **Anwendungen** > **Unternehmensanwendungen** > **Sicherheit** > **Einwilligung und Berechtigungen**.
1. Navigieren Sie zu **Berechtigungsklassifizierungen**.
1. Entra schlägt die am häufigsten verwendeten Berechtigungen für **niedriges Risiko** vor.
1. Überprüfen Sie alle diese Berechtigungen und wählen Sie **Ja, ausgewählte Berechtigungen hinzufügen**, um sie als **niedriges Risiko** in Ihrem Entra ID-Mandanten einzustufen.
1. Navigieren Sie zu **Einstellungen für die Benutzerzustimmung**.
1. Wählen Sie unter **Benutzereinwilligung für Anwendungen** die empfohlene Option **Benutzereinwilligung für Apps von verifizierten Herausgebern für ausgewählte Berechtigungen zulassen** aus. Dadurch können Benutzende Berechtigungen zustimmen, die als „geringe Auswirkung“ eingestuft sind (die Sie zuvor ausgewählt haben), für Apps von verifizierten Herausgebern.
1. Wählen Sie **Speichern**.
1. Navigieren Sie zu **Administratoreinwilligung-Einstellungen** und aktivieren Sie Administratoreinwilligungsanfragen, indem Sie **Ja** auswählen, um Benutzenden zu ermöglichen, die Einwilligung eines Admins für Anwendungen anzufordern, mit denen sie nicht einverstanden sind.
1. Wählen Sie **+ benutzende Person hinzufügen**, um **`Lidia Holloway`** und **`MOD Administrator`** als Benutzende hinzuzufügen, die Administratorzustimmungsanforderungen überprüfen können.
1. Wählen Sie **Speichern** im Fenster **Einstellungen für Administratoreinwilligung**.
1. Lassen Sie diese Registerkarte für die nächste Aufgabe geöffnet.

Sie haben nun die Einstellungen für die Zustimmung zu Anwendungen konfiguriert, die den Zugriff jeder benutzendenPerson auf Anwendungen einschränken. Die Benutzenden können nach wie vor eine Genehmigung für Anwendungen beantragen, und das Anwendungs-Admin-Team kann sie nach Bewertung der Notwendigkeit und des Risikos für die jeweilige Anwendung genehmigen.

### Aufgabe 2 - Erstellen einer Authentifizierungsstärke

In dieser Aufgabe werden Sie das Entra ID Portal verwenden, um eine eigene Authentifizierungsstärke zu erstellen, um die Verwendung von SMS OTP innerhalb Ihrer Organisation zu beschränken. 

1. Sie sollten weiterhin im Entra ID Portal **https://entra.microsoft.com** angemeldet sein.
2. Navigieren Sie im linken Navigationsbereich zu **Schutz** > **Authentifizierungsmethoden** > **Authentifizierungsstärken**.
3. Wählen Sie **+ Neue Authentifizierungsstärke**.
4. Geben Sie den Namen **Hardened MFA** ein.
5. Prüfen Sie **phishing-sichere MFA**, **kennwortlose MFA** und **Multi-Faktor-Authentifizierung**.
6. Deaktivieren Sie unter Multi-Faktor-Authentifizierung die folgenden Optionen:
   - **Befristeter Zugriffspass (Mehrfachverwendung)**
   - **Kennwort + SMS**
   - **Kennwort + Stimme**
   - **Verbund Einzelfaktor + SMS**
   - **Verbund Einzelfaktor + Stimme**.
7. Wählen Sie **Weiter** aus.
8. Überprüfen Sie, dass keiner der oben genannten Faktoren in der Authentifizierungsstärke enthalten ist.
9.  Klicken Sie auf **Erstellen**.

Sie haben nun eine Authentifizierungsstärke erstellt, die die Verwendung von SMS OTP als Authentifizierungsfaktor einschränkt.
