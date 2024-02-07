---
casestudy:
  title: 'Fallstudie: Ransomware-Strategie'
  module: 'Module 13: Recommend a ransomware strategy by using Microsoft Security Best Practices'
---
Diese Fallstudienübung dient dazu, Erfahrungen bei der Durchführung einiger konzeptioneller Designaufgaben zu sammeln, die sich auf die in diesem Modul erlernten Themen beziehen.

## Fallstudie: Empfehlung einer Ransomware-Strategie mithilfe der Best Practices von Microsoft Security
 
CONTOSO ist ein Dienstleistungsunternehmen im Gesundheitswesen mit Hauptsitzen in Chicago und London, Vereinigtes Königreich.  
Das Unternehmen bietet in seinen Einrichtungen in Chicago und im Großraum London Gesundheitsdienstleistungen für seine Kundschaft an.  In den Einrichtungen von Contoso gibt es viele Krankenhäuser mit Ärzt*innen, Krankenschwestern und anderen medizinischen Fachkräften. Contoso hat eine unternehmensweite Migration aller kritischen Dienste zur Cloud veranlasst. Diese Migration umfasst Server vor Ort, VMs und die unterstützenden Management- und Überwachungsgeräte.

Contoso hat seine Cloudmigration eingeleitet, mit Ausnahme einiger Daten und Anwendungen, die aufgrund von Compliance- und gesetzlichen Anforderungen weiterhin lokal gehostet werden müssen. Contoso verfügt über einen Azure Active Directory-Mandanten (Azure AD). Diese Azure AD-Instanz wird mit Active Directory Domain Services (AD DS) synchronisiert, das auf lokalen Domänencontrollern verwaltet wird. Während der Migration werden zusätzliche Azure-Abonnements nach Bedarf für jede Abteilung einschließlich SaaS-Anwendungen erstellt. Um ihre tägliche Arbeit zu erleichtern, haben die meisten Mitarbeiter*innen Zugriff auf Microsoft 365-Anwendungen.  
 
In jüngster Zeit gab es mehrere aufsehenerregende Ransomware-Fälle, in die Contosos Konkurrenz auf dem Gesundheitsmarkt verwickelt war. Der CEO und der CISO sind besorgt, dass Contoso noch keinen Plan hat, um das Risiko eines Ransomware-Angriffs zu mindern. Der CISO hat Sie persönlich gebeten, einen Plan zur Reaktion auf Ransomware und zur Schadensbegrenzung zu entwerfen, der in zwei Wochen den Führungskräften des Unternehmens vorgestellt werden soll. Einige der leitenden IT-Mitarbeiter*innen haben sich dahingehend geäußert, dass die Ransomware-Bedrohung übertrieben wird und dass das Unternehmen eigentlich nur gute Backups und eine solide Perimetersicherheit braucht.
 
### Anforderungen

* Der Plan zur Reaktion auf Ransomware und zur Schadensbegrenzung muss nicht nur die lokale kritische Infrastruktur und die Clouddienste einbeziehen, sondern auch die Unternehmensdaten, die auf Firmenlaptops und mobilen Geräten gespeichert sind, die von Mitarbeiter*innen im Außendienst verwendet werden
* Der CEO und der CISO haben eine harte Haltung eingenommen: Sie werden niemals mit Ransomware-Hacker*innen verhandeln oder sie bezahlen. Sie haben erklärt, dass im Falle eines Ransomware-Angriffs ihr Ziel darin besteht, kritische Systeme innerhalb von 12 Stunden wieder betriebsbereit zu machen und die volle Funktionalität innerhalb von 48 Stunden wiederherzustellen.
* Die Strategien für den Umgang mit Daten müssen den Anforderungen des Datenschutzes entsprechen, einschließlich HIPAA in den USA und allen damit verbundenen Standards im Vereinigten Königreich.
* Ihr Plan muss auch darlegen, warum eine gute Datensicherung nicht ausreicht, um die Bedrohung durch Ransomware zu mindern.

### Einstiegsfragen

* Welche Abteilungen und Mitarbeiter*innen müssen an der Erstellung des Plans zur Eindämmung von Ransomware beteiligt sein? 
* Welche Dienste und Infrastrukturelemente müssen durch den Plan adressiert werden? 
* Was sind realistische Fristen für die Erstellung eines robusten Ransomware-Reaktionsplans?
* Was sind die wichtigsten Erfolgsfaktoren für die Umsetzung Ihres Plans zum Schutz vor Ransomware?

### Entwurfsaufgaben

* Die Auflistung der Azure- und M365-Dienste ist entscheidend für die Sicherung und den Schutz Ihrer Daten. Erläutern Sie, warum jeder Dienst ein wichtiger Bestandteil der Ransomware-Reaktion ist und welche Nachteile jeder Dienst mit sich bringt.
* Notieren Sie sich die besonderen Anforderungen, die Ihr Unternehmen hat, die nicht von vorhandenen Azure- und M365-Lösungen erfüllt werden.
* Führen Sie die Dienstleistungen und Infrastrukturelemente auf, die in dem Plan berücksichtigt werden müssen.
* Schätzen Sie einen realistischen Zeitrahmen für die Erstellung eines robusten Ransomware-Reaktionsplans und die anschließende Ausführung dieses Plans. 