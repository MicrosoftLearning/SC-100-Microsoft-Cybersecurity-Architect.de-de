---
casestudy:
  title: 'Fallstudie: Bewertung der Einhaltung von Vorschriften'
  module: 'Module 05: Design solutions for regulatory compliance'
---

Diese Fallstudienübung dient dazu, Erfahrungen bei der Durchführung einiger konzeptioneller Designaufgaben zu sammeln, die sich auf die in diesem Modul erlernten Themen beziehen.

## Fallstudie: Bewertung der Einhaltung von Vorschriften

Contoso Pharma ist ein internationales Pharmaunternehmen mit Niederlassungen in Nordamerika und Europa. Contoso Pharma hat Workloads vor Ort und in Azure. Das Ziel ist, dass in den nächsten zwei Jahren alle Arbeitslasten vollständig in Azure stattfinden und nur noch ein Minimum an Arbeitslasten vor Ort vorhanden sein wird. Nachfolgend finden Sie eine Liste ihrer wichtigsten Arbeitsaufgaben:

- VMs (Windows and Linux)
- Speicherkonten
- Key Vault
- SQL PaaS und SQL auf VMs

Contoso Pharma verfügt außerdem über ein Site-to-Site-VPN zwischen dem Hauptsitz in Redmond und der Hauptniederlassung in London. Dieses VPN wird verwendet, um die Kommunikation von Ressourcen vor Ort zu ermöglichen.

Contoso Pharma verfügt über eine Legacy-Umgebung in Redmond, die aus einigen Windows Server 2012 besteht, auf denen ein Webserver läuft, der von der Anwendung verwendet wird, die die Datenbank abfragt, um die Kundeninformationen zu überprüfen. Bei der Untersuchung wurde festgestellt, dass die Kommunikation des Legacy-Webservers mit der Datenbank über HTTP erfolgt.

### Anforderungen an das Design

Contoso Pharma hat je nach Arbeitsaufkommen unterschiedliche Compliance-Anforderungen, wie in der folgenden Tabelle dargestellt:

| **Workload** | **Datentyp** | **Konformitätsstandard** |
|:---:|:---:|:---:|
| Virtuelle Windows-Computer | Informationen zum Kreditkarteninhaber | PCI-DSS |
| SQL PaaS | Gesundheitsinformationen für Patienten | HIPAA |
| Speicherkonten | Informationen zum Kreditkarteninhaber | PCI DSS-Konten |

Um diese Standards zu erfüllen, muss Contoso Pharma in der Lage sein:

- Überwachen Sie die Fortschritte bei der Einhaltung der Vorschriften im Laufe der Zeit
- Verbieten Sie den Eigentümern von Workloads, Ressourcen bereitzustellen, die nicht mit diesen Standards übereinstimmen.
- Sicherstellen, dass neue Abonnements, die in der Umgebung bereitgestellt werden, standardmäßig die erforderlichen Standards verwenden
- Stellen Sie sicher, dass Ressourcen, die an jedem geografischen Standort bereitgestellt werden, die Daten aus Gründen der Datenhoheit in der Ursprungsregion behalten.

### Entwurfsaufgaben

* Welches Tool sollte verwendet werden, um sicherzustellen, dass Contoso Pharma seinen Compliance-Status im Laufe der Zeit analysieren kann? Wählen Sie die entsprechende Option aus:
* Welcher Dienst in Azure sollte verwendet werden, um Workload-Besitzer dazu zu zwingen, nur Ressourcen zu erstellen, die den erforderlichen Standards entsprechen?
* Welche Option sollte verwendet werden, um sicherzustellen, dass die Daten bei der Erstellung von Ressourcen an der richtigen geografischen Position gespeichert werden?
* Wie kann Contoso Pharma überprüfen, ob die bereitgestellten VMs mit dem PCI DSS konform sind, und wenn nicht, was muss getan werden, um dies zu ändern?
* Die Datenverschlüsselung ist eine unerlässliche Komponente, um Ihre Datenschutzanforderungen zu erfüllen. In welchen Phasen müssen Sie die Daten verschlüsseln?
* Welchen Azure-Dienst können Sie verwenden, um die Datenverschlüsselung über Arbeitslasten hinweg durchzusetzen?
