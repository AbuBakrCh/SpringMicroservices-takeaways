# SpringMicroservices-takeaways #
## Chapter 1: Welcome to the Cloud - Spring ##
### What's a microservice?
- A microservice is a small, loosely coupled, distributed service. Microservices let you take an extensive application and decompose it into easy-to-manage components with narrowly defined responsibilities. Microservices help combat the traditional problems of complexity in a large codebase by decomposing it down into small, well-defined pieces.
- The key concepts you need to embrace as you think about microservices are decomposing and unbundling. The functionality of your applications should be entirely independent of one another.
- Application logic is broken down into small-grained components with well-defined, coordinate boundaries of responsibility.
- Each component has a small domain of responsibility and is deployed independently of the others. A single microservice is responsible for one part of a business domain.
- Microservices employ lightweight communication protocols such as HTTP and JSON (JavaScript Object Notation) for exchanging data between the service consumer and service provider.
- Because microservice applications always communicate with a technology-neutral format (JSON is the most common), the underlying technical implementation of the service is irrelevant. This means that an application built using a microservice approach can be constructed with multiple languages and technologies.
- Microservices—by their small, independent, and distributed nature—allow organizations to have smaller development teams with well-defined areas of responsibility. These teams might work toward a single goal, such as delivering an application, but each team is responsible only for the services on which they’re working.

### Why change the way we build applications? ###
- **Flexible:** Decoupled services can be composed and rearranged to quickly deliver new functionality. The smaller the unit of code that one is working with, the less complicated it is to change and the less time it takes to test (sanity testing) and deploy the code.
- **Resilient:** Decoupled services mean an application is no longer a single “ball of mud,” where a degradation in one part of the application causes the entire application to fail. Failures can be localized to a small part of the application and contained before the entire application shuts down. This also enables the application to degrade gracefully in case of an unrecoverable error.
- **Scalable:** Decoupled services can easily be distributed horizontally across multiple servers, making it possible to scale the features/services appropriately. With a monolithic application, where all the logic for the application is intertwined, the entire application needs to scale back, even if only a small part of the application is the bottleneck. With small services, scaling is localized and much more cost effective.

### Microservices are more than writing the code ###
- **Right-sized:** How you ensure that your microservices are properly sized so that you don’t have a microservice take on too much responsibility. Remember, properly sized, a service allows you to make changes to an application quickly and reduces the overall risk of an outage to the entire application.
- **Location transparent:** How you manage the physical details of service invocation. When in a microservice application, multiple service instances can quickly start and shut down.
- **Resilient:** How you protect your microservice consumers and the overall integrity of your application by routing around failing services and ensuring that you take a “fail-fast” approach.
- **Repeatable:** How you ensure that every new instance of your service brought up is guaranteed to have the same configuration and codebase as all the other service instances in production.
- **Scalable:** How you establish a communication that minimizes the direct dependencies between your services and ensures that you can gracefully scale your microservices.

### Core microservice development patterns
#### Microservice routing patterns ####
- **Service discovery:** With service discovery and its key feature, service registry, you can make your microservice discoverable so client applications can find them without having the location of the service hardcoded into their application. Remember the service discovery is an internal service, not a client-facing service.
- **Service routing:** With an API Gateway, you can provide a single entry point for all of your services so that security policies and routing rules are applied uniformly to multiple services and service instances in your microservices applications.

#### Microservice client resiliency ####
- **Client-side load balancing:** How you cache the location of your service instances on the service so that calls to multiple instances of a microservice are load balanced to all the health instances of that microservice.
- **Circuit breaker pattern:** How you prevent a client from continuing to call a service that’s failing or suffering performance problems. When a service is running slowly, it consumes resources on the client calling it. You want these microservice calls to fail fast so that the calling client can quickly respond and take appropriate action.
- **Fallback pattern:** When a service call fails, how you provide a “plug-in” mechanism that allows the service client to try to carry out its work through alternative means other than the microservice being called.
- **Bulkhead pattern:** Microservice applications use multiple distributed resources to carry out their work. This pattern refers to how you compartmentalize these calls so that the misbehavior of one service call doesn’t negatively impact the rest of the application.

#### Microservice security patterns ####
- **Authentication:** How you determine the service client calling the service is who they say they are.
- **Authorization:** How you determine whether the service client calling a microservice is allowed to undertake the action they’re trying to take.
- **Credential management and propagation:** How you prevent a service client from constantly having to present their credentials for service calls involved in a transaction. To achieve this, we’ll look at how you can use token-based security standards such as OAuth2 and JSON Web Tokens (JWT) to obtain a token that can be passed from service call to service call to authenticate and authorize the user.

#### Microservice tracing and logging pattern ####

- **Log correlation:** How you tie together all the logs produced between services for a single user transaction. With this pattern, we’ll look at how to implement a correlation ID, which is a unique identifier that’s carried across all service calls in a transaction and that can be used to tie together log entries produced from each service.
- **Log aggregation:** With this pattern, we’ll look at how to pull together all of the logs produced by your microservices (and their individual instances) into a single queryable database across all the services involved and understand the performance characteristics of the services in the transaction.
- **Microservice tracing:** We’ll explore how to visualize the flow of a client transaction across all the services involved and understand the performance characteristics of the transaction’s services.

#### Application metrics pattern ####

- **Metrics:** How you create critical information about the health of your application and how to expose those metrics
- **Metrics service:** Where you can store and query the application metrics
- **Metrics visualization suite:** Where you can visualize business-related time data for the application and infrastructure

#### Microservice build/deployment pattern ####

- **Build and deployment pipelines:** How you create a repeatable build and deployment process that emphasizes one-button builds and deployment to any environment in your organization.
- **Infrastructure as code:** How you treat the provisioning of your services as code that can be executed and managed under source control.
- **Immutable servers:** Once a microservice image is created, how you ensure that it’s never changed after it has been deployed.
- **Phoenix servers:** How you ensure that servers that run individual containers get torn down on a regular basis and re-created from an immutable image. The longer a server is running, the more opportunity there is for configuration drift [1]. A configuration drift can occur when ad hoc changes to a system configuration are unrecorded.

**[1] Note ~ Configuration Drift:** It refers to an environment in which running clusters in an infrastructure become increasingly different over time, usually due to manual changes and updates on individual clusters.


## Chapter 2: Exploring the microservices world with Spring Cloud ##

### Spring Cloud Congfig
- Spring Cloud Config handles the management of the application configuration data through a centralized service. Your application configuration data (particularly your environment-specific configuration data) is then cleanly separated from your deployed microservice. This ensures that no matter how many microservice instances you bring up, they’ll always have the same configuration. Spring Cloud Config has its own property management repository but also integrates with open source projects like Git.

### Spring Cloud Service Discovery
- With Spring Cloud Service Discovery, you can abstract away the physical location (IP and/or server name) of where your servers are deployed from the clients consuming the service. Service consumers invoke business logic for the servers through a logical name rather than a physical location. Spring Cloud Service Discovery also handles the registration and deregistration of service instances as these are started and shut down.

### Spring Cloud LoadBalancer and Resilience4j
- By using the Resilience4j libraries, you can quickly implement service client resiliency patterns such as circuit breaker, retry, bulkhead, and more.
While the Spring Cloud LoadBalancer project simplifies integrating with service discovery agents such as Eureka, it also provides client-side load balancing of calls from a service consumer. This makes it possible for a client to continue making service calls even if the service discovery agent is temporarily unavailable.

### Spring Cloud API Gateway
- Like the name says, it is a service gateway that proxies service requests and makes sure that all calls to your microservices go through a single “front door” before the targeted service is invoked. With this centralization of service calls, you can enforce standard service policies such as security authorization, authentication, content filtering, and routing rules.

### Spring Cloud Stream
- Spring Cloud Stream is an enabling technology that lets you easily integrate lightweight message processing into your micro-service. Using Spring Cloud Stream, you can build intelligent microservices that use asynchronous events as these occur in your application. You can also quickly integrate your microservices with message brokers such as RabbitMQ and Kafka.

### Spring Cloud Sleuth
- Spring Cloud Sleuth lets you integrate unique tracking identifiers into the HTTP calls and message channels (RabbitMQ, Apache Kafka) used within your application. These tracking numbers, sometimes referred to as correlation or trace IDs, allow you to track a transaction as it flows across the different services in your application. With Spring Cloud Sleuth, trace IDs are automatically added to any logging statements you make in your microservice.
The real beauty of Spring Cloud Sleuth is seen when it’s combined with logging-aggregation technology tools like the ELK Stack (Elastic Search, Logstash and Kibana Stack) and tracking tools like Zipkin. Open Zipkin takes data produced by Spring Cloud Sleuth and allows you to visualize the flow of your service calls involved for a single transaction.

### Spring Cloud Security
- Spring Cloud Security is an authentication and authorization framework that controls who can access your services and what they can do with them. Because Spring Cloud Security is token-based, it allows services to communicate with one another through a token issued by an authentication server. Each service receiving an HTTP call can check the provided token to validate the user’s identity and their access rights. Spring Cloud Security also supports JSON Web Tokens (JWT). JWT standardizes the format for creating an OAuth2 token and normalizes digital signatures for a generated token.

## Chapter 3: Building microservices with Spring Boot ##

We can see the four potential microservices based on the following elements:
* Assets
* License
* Contract
* Organization

The goal is to take these major pieces of functionality and extract them into entirely self-contained units that we can build and deploy independently of each other. **These units can optionally share or have individual databases.** However, extracting services from the data model involves more than repackaging code into separate projects. It also involves teasing out the actual database tables the services will access and only allowing each service to access the tables in its specific domain.

What is the right level of granularity?
It’s better to start broad with our microservice and refactor to smaller services -> It is easy to go overboard when you begin your microservice journey and make everything a microservice. But decomposing the problem domain into small services often leads to premature complexity because microservices devolve into nothing more than fine-grained data services.

### If a microservice is too coarse-grained, you’ll likely see the following:
**A service with too many responsibilities:**
The general flow of the business logic in the service is complicated and seems to be enforcing an overly diverse array of rules.

**A service that manages data across a large number of tables:**
A microservice is the record for the data it manages. If you find yourself persisting data to multiple tables or reaching out to tables outside of the service database, this is a clue that the service is too big. We like to use the guideline that a microservice should own no more than three to five tables. Any more, and your service is likely to have too much responsibility.

**A service with too many test cases:**
Services can grow in size and responsibility over time. If you have a service that started with a small number of test cases and ended up with hundreds of unit and integration tests, you might need to refactor.

### What about a microservice that’s too fine-grained?
**The microservices in one part of the problem domain breed like rabbits:**
If everything becomes a microservice, composing business logic out of the services becomes complex and difficult. That’s because the number of services needed to get a piece of work done grows tremendously. A common smell is when you have doz- ens of microservices in an application, and each service interacts with only a single database table.

**Your microservices are heavily interdependent on one another:**
You find that microservices in one part of the problem domain keep calling back and forth between each other to complete a single user request.

**Your microservices become a collection of simple CRUD (Create, Replace, Update, Delete) services:**
Microservices are an expression of business logic and not an abstraction layer over your data sources. If your microservices do nothing but CRUD- related logic, they’re probably too fine-grained.

### When not to use microservices
**Complexity when building distributed systems**
Because microservices are distributed and fine-grained (small), these introduce a level of complexity into your application that’s not found in more monolithic applications. Microservice architectures require a high degree of operational maturity. Don’t consider using microservices unless your organization is willing to invest in the automation and operational work (monitoring, scaling, and so on) that a highly distributed application needs to be successful.

**Server or container sprawl**
One of the most common deployment models for microservices is to have one microservice instance deployed in one container. In a large microservice-based application, you might end up with 50 to 100 servers or containers (usually virtual) that must be built and maintained in production alone. Even with the lower cost of running these services in the cloud, the operational complexity of managing and monitoring these services can be tremendous.

**Application type**
Microservices are geared toward reusability and are extremely useful for building large applications that need to be highly resilient and scalable. This is one of the reasons why so many cloud-based companies have adopted microservices. If you’re building small, departmental-level applications, or applications with a small user base, the complexity associated with building a distributed model like a microservice might generate more expense than it’s worth.

**Data transactions and consistency**
If your application needs to do complex data aggregation or transformation across multiple data sources, the distributed nature of microservices will make this work difficult. Your microservices will invariably take on too much responsibility and can also become vulnerable to performance problems.
