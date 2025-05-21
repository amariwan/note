## 🔤 Schlagworte & ihre Bedeutung

| Abkürzung          | Ausgeschrieben                   | Bedeutung / Erklärung                                                                                                                                                                      |
| ------------------ | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **OOP**            | Objektorientierte Programmierung | Ein Programmierparadigma, bei dem Software in „Objekte“ mit Zuständen und Verhalten modelliert wird. Kernkonzepte sind Kapselung, Vererbung, Polymorphie und Abstraktion ([Wikipedia][1]). |
| **DRY**            | Don’t Repeat Yourself            | Prinzip zur Vermeidung von Redundanz: Informationen oder Logik sollen nur an einer einzigen Stelle im System definiert sein ([Wikipedia][2]).                                              |
| **KISS**           | Keep It Simple, Stupid           | Design-Prinzip, das Einfachheit fördert: Lösungen sollten so simpel wie möglich bleiben, komplexe Konstrukte vermeiden ([Wikipedia][3]).        [KISS-Prinzip (Wikipedia)](https://en.wikipedia.org/wiki/KISS_principle)                                            |
| **YAGNI**          | You Aren’t Gonna Need It         | Man implementiert keine Funktionalität vorab, die aktuell nicht erforderlich ist („You aren’t gonna need it“).        [YAGNI bei Extreme Programming](https://xp123.com/articles/yagni/)                                                                        |
| **SoC**            | Separation of Concerns           | Trennung von Verantwortlichkeiten: unterschiedliche Aspekte (z. B. Datenzugriff, UI, Geschäftslogik) werden klar voneinander abgegrenzt.    [Separation of Concerns – MDN Web Docs](https://developer.mozilla.org/en-US/docs/Glossary/SoC)                                                    |
| **Encapsulation**  | Kapselung                        | Interne Implementierungsdetails werden verborgen und nur über definierte Schnittstellen (Methoden/Properties) zugänglich gemacht.        [Encapsulation in OOP (JavaTPoint)](https://www.javatpoint.com/encapsulation)                                                    |
| **Abstraction**    | Abstraktion                      | Komplexität wird durch Interfaces oder abstrakte Klassen reduziert, um nur relevante Details offenzulegen.        [OOP: Abstraction – TutorialsPoint](https://www.tutorialspoint.com/java/java_abstraction.htm)                                                                           |
| **Modularization** | Modularisierung                  | Zerlegung des Systems in wiederverwendbare, in sich geschlossene Module mit klaren Schnittstellen.      [Clean Architecture Modularization (thoughtworks)](https://www.thoughtworks.com/en-de/insights/blog/module-boundaries-and-clean-architecture)                                                                                   |
| **Code Smell**     | Codegeruch                       | Hinweise im Code, die auf mögliche Qualitätsprobleme oder mangelnde Wartbarkeit hindeuten (z. B. zu große Klassen, Duplicate Code).      [Martin Fowler: Code Smell Catalog](https://martinfowler.com/bliki/CodeSmell.html)                                                        |
| **Zombie Code**    | Toter Code                       | Codeabschnitte, die im System vorhanden, aber nicht mehr genutzt oder veraltet sind.              [Dead Code Detection (Wikipedia)](https://en.wikipedia.org/wiki/Dead_code)                                                                                           |

[1]: https://de.wikipedia.org/wiki/Objektorientierte_Programmierung?utm_source=chatgpt.com "Objektorientierte Programmierung – Wikipedia"
[2]: https://de.wikipedia.org/wiki/Don%E2%80%99t_repeat_yourself?utm_source=chatgpt.com "Don’t repeat yourself – Wikipedia"
[3]: https://en.wikipedia.org/wiki/KISS_principle?utm_source=chatgpt.com "KISS principle - Wikipedia"

---

### 📐 Architektur & Design

| Abkürzung                        | Ausgeschrieben                                 | Bedeutung / Erklärung                                                                                      |
| -------------------------------- | ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **SOLID**                        | –                                              | Akronym für fünf Prinzipien:   [SOLID Principles – Clean Code Dev](https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english/)                                                                             |
| • **SRP**                        | Single Responsibility Principle                | Eine Klasse/Modul hat nur eine einzige Verantwortlichkeit.                                                 |
| • **OCP**                        | Open/Closed Principle                          | Offen für Erweiterung, geschlossen für Modifikation.                                                       |
| • **LSP**                        | Liskov Substitution Principle                  | Subtypen müssen sich verhalten, als wären sie der Basistyp.                                                |
| • **ISP**                        | Interface Segregation Principle                | Kleine, spezialisierte Interfaces statt großer „Alles-könner“-Interfaces.                                  |
| • **DIP**                        | Dependency Inversion Principle                 | High-Level-Module sollten nicht von Low-Level-Details abhängen; beide von Abstraktionen abhängig.          |
| **Clean Architecture**           | –                                              | Entkopplung der Geschäftslogik von Frameworks über Schichtenmodell (z. B. Entities, Use Cases, Adapters). [Robert C. Martin’s Clean Architecture](https://8thlight.com/blog/uncle-bob/2012/08/13/the-clean-architecture.html)   |
| **Hexagonal / Ports & Adapters** | –                                              | Trennung von Kernlogik und externen Details (Datenbanken, UI) über definierte Ports und Adapters.   [Alistair Cockburn: Hexagonal Architecture](https://alistair.cockburn.us/hexagonal-architecture/)           |
| **CQRS**                         | Command Query Responsibility Segregation       | Getrennte Modelle für Lese- (Queries) und Schreiboperationen (Commands).    [CQRS explained by Microsoft](https://learn.microsoft.com/en-us/azure/architecture/patterns/cqrs)                                  |
| **Event-driven**                 | –                                              | Asynchrone, entkoppelte Kommunikation über Events.   [Event-driven architecture (AWS)](https://docs.aws.amazon.com/whitepapers/latest/event-driven-architecture/event-driven-architecture.html)                                                       |
| **MVC**                          | Model-View-Controller                          | Muster zur Aufteilung in Model (Daten), View (Darstellung) und Controller (Logik). [Model-View-Controller Pattern – MDN](https://developer.mozilla.org/en-US/docs/Glossary/MVC)                         |
| **DDD**                          | Domain-Driven Design                           | Modellierung komplexer Software anhand der Fachdomäne und Domänen­logik.  [Domain-Driven Design Reference – Eric Evans](https://domainlanguage.com/ddd/reference/)                                     |
| **ACID**                         | Atomicity, Consistency, Isolation, Durability  | Eigenschaften für zuverlässige Datenbank­transaktionen.   [ACID Properties – IBM Docs](https://www.ibm.com/docs/en/informix-servers/12.10?topic=ssw_ibm_i)                                                     |
| **CAP**                          | Consistency, Availability, Partition Tolerance | Theorem: In verteilten Systemen können stets nur zwei der drei Eigenschaften garantiert werden.  [CAP Theorem – AWS Architecture Blog](https://aws.amazon.com/builders-library/the-cap-theorem/)              |
| **REST**                         | Representational State Transfer                | Architekturstil für Web-APIs auf Basis von HTTP-Methoden und Ressourcen.   [REST Architecture Guide – REST API Tutorial](https://restfulapi.net/)                                      |
| **UML**                          | Unified Modeling Language                      | Standardisierte grafische Sprache zum Spezifizieren, Visualisieren und Dokumentieren von Softwaresystemen.[UML Introduction – Lucidchart](https://www.lucidchart.com/pages/uml-diagram)                  |

---

## 🧪 Tests & Qualität

| Begriff              | Bedeutung                                                                       |
| -------------------- | ------------------------------------------------------------------------------- |
| **TDD**              | Test First: zuerst testen, dann implementieren   [Kent Beck’s TDD Primer](https://www.agilealliance.org/glossary/tdd/)                                |
| **BDD**              | Nutzerzentrierter Testansatz („describe behavior“)      [Cucumber BDD Guide](https://cucumber.io/docs/bdd/)                                |
| **Mocking**          | Fake-Objekte für z. B. Stores, APIs, Components   [Vitest Mocking Guide](https://vitest.dev/guide/mocking.html)                                      |
| **Coverage**         | Wie viel des Codes wird durch Tests ausgeführt          [Code Coverage 101 – Atlassian](https://www.atlassian.com/continuous-delivery/code-coverage)                         |
| **Kosten von Tests** | Mehr Initialaufwand – aber später besser wartbar und erweiterbar + weniger Bugs [Martin Fowler – Test Pyramid](https://martinfowler.com/bliki/TestPyramid.html)   |
| **Clean Tests**     | [Vue Test Utils Best Practices](https://test-utils.vuejs.org/guides/overview.html)           |


---

### ⚙️ Tooling & Praxis

| **Abkürzung**          | **Ausgeschrieben**                             | **Bedeutung / Erklärung**                                                                         | **Quelle**                                                                                                     |
| ---------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **CI/CD**              | Continuous Integration / Deployment            | Automatisierte Tests, Builds und Deployments                                                      | [GitLab](https://about.gitlab.com/topics/ci-cd/)                                                               |
| **Linting**            | –                                              | Automatisierte Prüfung auf Codequalität und Stil                                                  | [ESLint](https://eslint.org/docs/latest/user-guide/getting-started)                                            |
| **Refactoring**        | –                                              | Umbau von Code ohne Änderung der Funktionalität                                                   | [Refactoring Guru](https://refactoring.guru/refactoring)                                                       |
| **Pair Programming**   | –                                              | Zwei Entwickler arbeiten gleichzeitig am Code                                                     | [Agile Alliance](https://www.agilealliance.org/glossary/pairing/)                                              |
| **Version Control**    | –                                              | Verwaltung von Codeänderungen (z. B. Git)                                                         | [Atlassian](https://www.atlassian.com/git/tutorials)                                                           |
| **IaC**                | Infrastructure as Code                         | Infrastruktur wird als deklarativer Code geschrieben (z. B. Terraform)                            | [Terraform](https://developer.hashicorp.com/terraform/intro)                                                   |
| **SRE**                | Site Reliability Engineering                   | Praxis zur Steigerung von Zuverlässigkeit und Skalierbarkeit                                      | [Google SRE Book](https://sre.google/books/)                                                                   |


---

### 🚀 Moderne Konzepte

| **Abkürzung**          | **Ausgeschrieben**                             | **Bedeutung / Erklärung**                                                                         | **Quelle**                                                                                                     |
| ---------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Microservices**      | –                                              | Kleine, unabhängige Dienste mit eigener Laufzeit                                                  | [Martin Fowler](https://martinfowler.com/articles/microservices.html)                                          |
| **Monolith**           | –                                              | Alles in einer Anwendung gebündelt                                                                | [Thoughtworks](https://www.thoughtworks.com/en-de/radar/techniques/microservices-vs-monoliths)                 |
| **DevOps**             | –                                              | Verzahnung von Entwicklung & Betrieb mit Automatisierung                                          | [DevOps Handbook](https://itrevolution.com/book/the-devops-handbook/)                                          |
| **Agile**              | –                                              | Iterative Entwicklung mit Feedback-Zyklen                                                         | [Agile Manifesto](https://agilemanifesto.org/)                                                                 |
| **Containerization**   | –                                              | Isolierung von Apps in Containern (z. B. Docker)                                                  | [Docker Docs](https://docs.docker.com/get-started/)                                                            |
| **Serverless**         | –                                              | Code wird ausgeführt ohne eigene Serverwartung                                                    | [Martin Fowler](https://martinfowler.com/articles/serverless.html)                                             |
| **PWA**                | Progressive Web App                            | Webapp mit App-ähnlichem Verhalten (offline, installierbar)                                       | [Google Dev](https://developer.chrome.com/docs/workbox/understanding/pwa/)                                     |
| **SPA**                | Single Page Application                        | Webapp mit clientseitigem Routing (keine Full Page Reloads)                                       | [MDN](https://developer.mozilla.org/en-US/docs/Glossary/SPA)                                                   |
| **GraphQL**            | –                                              | Abfragesprache, bei der Client exakt Daten spezifiziert                                           | [GraphQL.org](https://graphql.org/learn/)                                                                      |
| **DevSecOps**          | –                                              | Integration von Security in DevOps-Prozesse                                                       | [GitLab](https://about.gitlab.com/topics/devsecops/)                                                           |


---

### Extras

| Kategorie             | Quelle                                                                                           |
| --------------------- | ------------------------------------------------------------------------------------------------ |
| **Vue Style Guide**   | [Vue 3 Official Style Guide](https://vuejs.org/style-guide/)                                     |
| **TypeScript Guide**  | [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)                   |
| **Design Patterns**   | [Refactoring Guru – Patterns](https://refactoring.guru/design-patterns)                          |
| **Vue Testing**       | [Vitest Guide](https://vitest.dev/guide/) • [Vue Test Utils](https://test-utils.vuejs.org/)      |
| **Best Practice Vue** | [Vue School – Best Practices](https://vueschool.io/articles/vuejs-tutorials/vue-best-practices/) |
