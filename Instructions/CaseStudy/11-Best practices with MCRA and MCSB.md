---
casestudy:
  title: 'Fallstudie: Best Practices mit MCRA und MCSB'
  module: 'Module 11: Recommend security best practices with MCRA and MCSB'
---

Diese Fallstudienübung dient dazu, Erfahrungen bei der Durchführung einiger konzeptioneller Designaufgaben zu sammeln, die sich auf die in diesem Modul erlernten Themen beziehen.

## Fallstudie: Best Practices mit MCRA und MCSB
 
CONTOSO ist ein Dienstleistungsunternehmen im Gesundheitswesen mit Hauptsitzen in Chicago und London, Vereinigtes Königreich.  
Das Unternehmen bietet in seinen Einrichtungen in Chicago und im Großraum London Gesundheitsdienstleistungen für seine Kundschaft an.  In den Einrichtungen von Contoso gibt es viele Krankenhäuser mit Ärzt*innen, Krankenschwestern und anderen medizinischen Fachkräften. Contoso hat eine unternehmensweite Migration aller kritischen Dienste zur Cloud veranlasst. Diese Migration umfasst Server vor Ort, VMs und die unterstützenden Management- und Überwachungsgeräte.

Contoso hat seine Cloudmigration eingeleitet, mit Ausnahme einiger Daten und Anwendungen, die aufgrund von Compliance- und gesetzlichen Anforderungen weiterhin lokal gehostet werden müssen. Contoso richtet einen Azure Active Directory-Mandanten (Azure AD) ein. Diese Azure AD-Instanz wird mit Active Directory Domain Services (AD DS) synchronisiert, das auf lokalen Domänencontrollern verwaltet wird. Während der Migration werden zusätzliche Azure-Abonnements nach Bedarf für jede Abteilung einschließlich SaaS-Anwendungen erstellt. Um ihre tägliche Arbeit zu erleichtern, haben die meisten Mitarbeiter*innen Zugriff auf Microsoft 365-Anwendungen.  
 
Um die kontinuierliche Konnektivität zu unterstützen, wurden für die meisten Mitarbeiterkategorien,  
wie z. B. Kundenbetreuer*innen, Support-Mitarbeiter*innen und Mitarbeiter*innen aus den Bereichen  
Wirtschaft, Finanzen und Personal, grundlegende Tests der VDI (Virtual Desktop Infrastructure) eingeleitet. Sichere Konnektivität wird über ein VPN-Gateway (Virtual Private Network)  
für eine begrenzte Anzahl von Benutzer*innen und Geräten unterstützt. Außerdem wurde  
eine Firewall eines Drittanbieters zum Schutz der virtuellen Server-VLANs  
(Virtual Local Area Networks) eingesetzt.  
 
Während sie bei den Kund*innen vor Ort sind, verwenden Ärzt*innen mobile Geräte mit lokal  
gespeicherten Tracking- und Überwachungsdaten. Diese Daten werden durch eine proprietäre Speicherverschlüsselung  
geschützt, und die Mitarbeiter*innen des Gesundheitswesens müssen sich vor dem Zugriff auf die Daten mit lokal gespeicherten Anmeldeinformationen bei ihrem Gerät anmelden. 
 
### Anforderungen

Während die Cloudmigration fortgesetzt und ausgeweitet wird, plant Contoso, alle lokalen  
Daten und Anwendungen in die Cloud zu verlagern, mit Ausnahme der Anwendungen, die nicht in den Anwendungsbereich fallen. 

* Bereitstellen von Microsoft 365 Defender und Defender für Cloud zur Verbesserung des Sicherheitsstatus von Contoso gegenüber Gegnern 
* Microsoft Compliance-Richtlinie MCSB muss auf das Azure-Abonnement angewendet werden 
* Contoso möchte proaktiv nach möglichen Bedrohungen suchen und die Angriffsfläche aktiv verwalten 
* Contoso möchte Identitäten sowohl für externe Auftragnehmer als auch für Patient*innen und interne Mitarbeiter*innen zentral verwalten 
* Alle Endpunktgeräte müssen zentral verwaltet und kontinuierlich hinsichtlich Compliance ausgewertet werden. 
* Geschützte Gesundheitsinformationen (Protected Health Information, PHI), die auf mobilen Geräten gespeichert sind, die von Gesundheitsexperten verwendet werden, werden nach der Data Residency-Richtlinie in die Cloud verschoben, um regionale Vorschriften einzuhalten. 
* Zugriff auf mobile Geräte im Außendienst sollte durch Geolocation eingeschränkt werden und erfordert Biometrie als Multi-Faktor-Authentifizierung  
* Die Datenfreigabe zwischen Apps auf demselben Gerät muss gesteuert werden.  
* Einhaltung der Anforderungen des Health Insurance Portability and Accountability Act (HIPAA) und des National Health Service (NHS). 
* Contoso möchte Berechtigungsadministratoren nach dem Prinzip der geringsten Rechte verwalten und nur in Zeitzugriffsrichtlinien erzwingen. 
* Contoso möchte ihre Daten im Notfall wiederherstellen und diese Sicherungsdaten auch an einem sicheren Ort aufbewahren. Im Falle einer Katastrophe in ihrer primären Region möchte Contoso ein Failover auf die sekundäre Region durchführen. 
* Contoso möchte sicherstellen, dass sie dem Zero Trust-Ansatz zur Überprüfung des gesamten eingehenden Zugriffs folgen.
* Da die Daten und die Verarbeitung nach Azure verlagert werden, muss das VPN-Gateway so konfiguriert werden,  
dass es sichere P2S-Verbindungen von Geräten unterstützt, auf denen eine Vielzahl von Desktop- und mobilen Betriebssystemen  
wie Windows, macOS, Android und andere laufen.  

### Entwurfsaufgaben

* Welcher Defender-Plan wird von Contoso benötigt, um ihre Geschäfts- und Sicherheitsanforderungen zu erfüllen? 
* Was kann Contoso tun, um den gesamten eingehenden Zugriff zu überprüfen und gleichzeitig der Zero Trust-Strategie zu folgen? 
* Wie kann Contoso NHS- und HIPAA-Richtlinien in ihrer Cloudumgebung anwenden? 
* Was sollte Contoso für die Sichtbarkeit aller vorhandenen Bedrohungen und Sicherheitsrisiken verwenden? 
* Wie sollte Contoso die Sicherheitskonfiguration auf den Endpunktgeräten bereitstellen und pflegen? 
* Wie kann Contoso Sichtbarkeit für die verwendeten Cloudanwendungen und Daten haben, die extern freigegeben werden? 
