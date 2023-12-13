---
casestudy:
  title: 'Fallstudie: Entwerfen von Lösungen, die mit dem Cloud Adoption Framework (CAF) übereinstimmen'
  module: 'Module 02: Design solutions that align with CAF and WAF'
---
Diese Fallstudienübung dient dazu, Erfahrungen bei der Durchführung einiger konzeptioneller Designaufgaben zu sammeln, die sich auf die in diesem Modul erlernten Themen beziehen.

## Fallstudie: Entwerfen von Lösungen, die mit dem Cloud Adoption Framework (CAF) übereinstimmen

- Contoso Banking ist eine Tochtergesellschaft der Contoso Group, die in eine unabhängige Geschäftseinheit ausgegliedert wird. Contoso Banking wird ein separates Unternehmen mit eigener Infrastruktur und IT-Organisation sein. 
- Die Contoso Banking-Infrastruktur basiert vollständig auf der Microsoft Azure-Cloud. Um von Anfang an eine sichere Cloudplattform aufzubauen, müssen Sie eine sichere Azure-Zielzone entwerfen.
- Die Vereinbarung sieht vor, dass der Übergang maximal 6 Monate dauern darf.
- Contoso Banking plant, die FinTech-Lösung der nächsten Generation mit cloudnativen Lösungen zu erstellen. Die MVP 1-Veröffentlichung muss in 6 Wochen erfolgen.

### Anforderungen

Contoso Group verwendet keine Clouddienste, die Infrastruktur wird vollständig in ihrem eigenen Rechenzentrum gehostet. Die Umgebung, die Teil von Contoso Banking sein wird, umfasst:

- Umgebung 1: Kernbanksysteme: 20 Apps. Sicherheit ist von entscheidender Bedeutung.
- Umgebung 2: Next-Gen-/Fintech-Anwendung, aufgebaut auf Azure Kubernetes Service und Azure Data Lake. 100 Veröffentlichungen pro Monat

#### Geplante Änderungen

Umgebung 1: Contoso Banking plant, die gesamte Kernbankinfrastruktur in die Cloud zu verlagern. Der Ansatz muss Folgendes umfassen:

- Bereitstellen einer Zielzone, in der die Kernanwendungen gehostet werden.
- Die Benutzer*innen müssen von sicheren, cloudbasierten Arbeitsstationen aus auf die Kernanwendungen zugreifen. Die Benutzer*innen müssen über eine konsistente Benutzeroberfläche verfügen, um auf die Anwendungen zuzugreifen.
- Die Lösung muss sicherstellen, dass Best Practices in den Bereichen Identity & Access Management, Governance, Sicherheit, Netzwerk und Protokollierung eingehalten werden.

Umgebung 2 (Fintech-App) muss die folgenden Anforderungen erfüllen:

- Veröffentlichung 100 x / Monat
- Ständig auf Überprüfungen vorbereitet sein
- Einhaltung von PCI-DSS

### Entwurfsaufgaben

- Welche Komponenten müssen in der Zielzone bereitgestellt werden?
- Wie wirkt sich die Auswahl von Workloads auf die Implementierungszeit und Komplexität aus?
- Wie würden Sie den sicheren Zugriff auf Kernanwendungen implementieren?
- Welche Azure-Zielzone sollten Sie Contoso Banking für Umgebung 1 empfehlen?
- Welche Azure-Zielzone sollten Sie Contoso Banking für Umgebung 2 empfehlen?
