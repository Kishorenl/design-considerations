
![Monolithic vs SOA vs Microservices - SOA vs Microservices - Edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/03/2-5.png)


**Major Differences Between SOA and MSA**!

[Microservices vs SOA architecture - Microservices vs SOA - Edureka](https://d1jnx9ba8s6j9r.cloudfront.net/blog/wp-content/uploads/2018/03/Asset-25-1.png)
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

| **SOA** | MSA |
| --- | --- |
| Follows "**share-as-much-as-possible**" architecture approach | Follows "**share-as-little-as-possible**" architecture approach |
| Importance is on **business functionality** reuse | Importance is on the concept of "**bounded context**" |
| They have **common governance** and **standards** | They focus on **people, collaboration** and freedom of other options |
| Uses **Enterprise Service bus (ESB)** for communication | Simple messaging system |
| They support **multiple message protocols** | They use **lightweight protocols** such as **HTTP/REST** etc. |
| **Multi-threaded** with more overheads to handle I/O | **Single-threaded** usually with the use of Event Loop features for non-locking I/O handling |
| Maximizes application service reusability | Focuses on **decoupling** |
| **Traditional Relational Databases** are more often used | **Modern **Relational Databases ****are more often used |
| A systematic change requires modifying the monolith | A systematic change is to create a new service |
| DevOps / Continuous Delivery is becoming popular, but not yet mainstream | Strong focus on DevOps / Continuous Delivery |

Major Differences Between Microservices and SOA in Detail
---------------------------------------------------------

-   **Service Granularity**: Service components within a microservices architecture are generally single-purpose services that do one thing really, really well. With SOA, service components can range in size anywhere from small application services to very large enterprise services. In fact, it is common to have a service component within SOA represented by a large product or even a subsystem.
-   **Component Sharing**: Component sharing is one of the core tenets of SOA. As a matter of fact, component sharing is what enterprise services are all about. SOA enhances component sharing, whereas MSA tries to minimize on sharing through "bounded context." A bounded context refers to the coupling of a component and its data as a single unit with minimal dependencies. As SOA relies on multiple services to fulfill a business request, systems built on SOA are likely to be slower than MSA.
-   **Middleware vs API layer**: The microservices architecture pattern typically has what is known as an API layer, whereas SOA has a messaging middleware component. The messaging middleware in SOA offers a host of additional capabilities not found in MSA, including mediation and routing, message enhancement, message, and protocol transformation. MSA has an API layer between services and service consumers.
-   **Remote services**: SOA architectures rely on messaging (AMQP, MSMQ) and SOAP as primary remote access protocols. Most MSAs rely on two protocols -- REST and simple messaging (JMS, MSMQ), and the protocol found in MSA is usually homogeneous.
-   **Heterogeneous interoperability**: SOA promotes the propagation of multiple heterogeneous protocols through its messaging middleware component. MSA attempts to simplify the architecture pattern by reducing the number of choices for integration. If you would like to integrate several systems using different protocols in a heterogeneous environment, you need to consider SOA. If all your services could be exposed and accessed through the same remote access protocol, then MSA is a better option.