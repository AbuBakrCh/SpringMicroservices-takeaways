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
