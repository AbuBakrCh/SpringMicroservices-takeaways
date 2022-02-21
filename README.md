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
