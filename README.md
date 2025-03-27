
# BambangShop Publisher App

Tutorial and Example for Advanced Programming 2024 - Faculty of Computer Science, Universitas Indonesia

  

---

  

## About this Project

In this repository, we have provided you a REST (REpresentational State Transfer) API project using Rocket web framework.

  

This project consists of four modules:

1.  `controller`: this module contains handler functions used to receive request and send responses.

In Model-View-Controller (MVC) pattern, this is the Controller part.

2.  `model`: this module contains structs that serve as data containers.

In MVC pattern, this is the Model part.

3.  `service`: this module contains structs with business logic methods.

In MVC pattern, this is also the Model part.

4.  `repository`: this module contains structs that serve as databases and methods to access the databases.

You can use methods of the struct to get list of objects, or operating an object (create, read, update, delete).

  

This repository provides a basic functionality that makes BambangShop work: ability to create, read, and delete `Product`s.

This repository already contains a functioning `Product` model, repository, service, and controllers that you can try right away.

  

As this is an Observer Design Pattern tutorial repository, you need to implement another feature: `Notification`.

This feature will notify creation, promotion, and deletion of a product, to external subscribers that are interested of a certain product type.

The subscribers are another Rocket instances, so the notification will be sent using HTTP POST request to each subscriber's `receive notification` address.

  

## API Documentations

  

You can download the Postman Collection JSON here: https://ristek.link/AdvProgWeek7Postman

  

After you download the Postman Collection, you can try the endpoints inside "BambangShop Publisher" folder.

This Postman collection also contains endpoints that you need to implement later on (the `Notification` feature).

  

Postman is an installable client that you can use to test web endpoints using HTTP request.

You can also make automated functional testing scripts for REST API projects using this client.

You can install Postman via this website: https://www.postman.com/downloads/

  

## How to Run in Development Environment

1. Set up environment variables first by creating `.env` file.

Here is the example of `.env` file:

```bash

APP_INSTANCE_ROOT_URL="http://localhost:8000"

```

Here are the details of each environment variable:

| variable | type | description |

|-----------------------|--------|------------------------------------------------------------|

| APP_INSTANCE_ROOT_URL | string | URL address where this publisher instance can be accessed. |

2. Use `cargo run` to run this app.

(You might want to use `cargo check` if you only need to verify your work without running the app.)

  

## Mandatory Checklists (Publisher)

- [x]Clone https://gitlab.com/ichlaffterlalu/bambangshop to a new repository.

-  **STAGE 1: Implement models and repositories**

- [x] Commit: `Create Subscriber model struct.`

- [x] Commit: `Create Notification model struct.`

- [x] Commit: `Create Subscriber database and Subscriber repository struct skeleton.`

- [x] Commit: `Implement add function in Subscriber repository.`

- [x] Commit: `Implement list_all function in Subscriber repository.`

- [x] Commit: `Implement delete function in Subscriber repository.`

- [x] Write answers of your learning module's "Reflection Publisher-1" questions in this README.

-  **STAGE 2: Implement services and controllers**

- [x] Commit: `Create Notification service struct skeleton.`

- [x] Commit: `Implement subscribe function in Notification service.`

- [x] Commit: `Implement subscribe function in Notification controller.`

- [x] Commit: `Implement unsubscribe function in Notification service.`

- [x] Commit: `Implement unsubscribe function in Notification controller.`

- [x] Write answers of your learning module's "Reflection Publisher-2" questions in this README.

-  **STAGE 3: Implement notification mechanism**

- [ ] Commit: `Implement update method in Subscriber model to send notification HTTP requests.`

- [ ] Commit: `Implement notify function in Notification service to notify each Subscriber.`

- [ ] Commit: `Implement publish function in Program service and Program controller.`

- [ ] Commit: `Edit Product service methods to call notify after create/delete.`

- [ ] Write answers of your learning module's "Reflection Publisher-3" questions in this README.

  

## Your Reflections

This is the place for you to write reflections:

  

### Mandatory (Publisher) Reflections

  

#### Reflection Publisher-1

1. In the context of the BambangShop application, the `Subscriber` model is primarily used to store and transfer data related to subscribers, such as their URL and name. The current implementation uses a `struct` to define this data structure, which is perfectly adequate for the application's current needs. A `struct` in Rust is a lightweight and efficient way to group related data fields. However, if the application's requirements evolve and there's a need to support different types of subscribers with varying behaviors or data structures, then introducing a `trait` would be beneficial. For example, you might have different notification delivery mechanisms for different subscriber types (e.g., email, SMS, webhooks). In such cases, defining a `Subscriber` trait with a `notify` method would allow each subscriber type to implement its own notification logic.
2. The BambangShop application requires efficient storage and retrieval of subscriber data, as well as thread safety in a concurrent environment. The `DashMap` data structure is specifically designed to meet these requirements. The `DashMap` enforces uniqueness of keys, which is essential for ensuring that each subscriber is uniquely identified by their URL. Using a regular `Vec` (vector) would not provide the same level of efficiency or thread safety.
3. In the BambangShop application, a Singleton pattern could be used to manage the `DashMap` instance, ensuring that only one instance of the subscriber map exists throughout the application. However, the Singleton pattern itself does not provide thread safety. It merely controls the instantiation of the `DashMap`. To ensure thread-safe concurrent access to the subscriber data, the `DashMap` data structure itself is still necessary.

  

#### Reflection Publisher-2

1. The separation of "Service" and "Repository" from a monolithic Model in modern software architectures stems from adhering to design principles like the Single Responsibility Principle (SRP) and promoting loose coupling. By extracting data access logic into a dedicated Repository layer, we isolate data storage concerns, making the system more adaptable to changes in database technologies or data sources. The Service layer, on the other hand, encapsulates business logic, ensuring that the Model remains focused on data representation. This separation enhances testability, maintainability, and reusability, as each layer can be independently modified and tested, leading to a more robust and scalable application.

2. If we rely solely on the Model without Service and Repository layers, the Model classes (Program, Subscriber, Notification) would become overly complex and tightly coupled. Each Model would need to handle both data storage and business logic, leading to code duplication and increased complexity. For instance, the Program Model would manage program data while also handling subscriber management and notification triggers, making it bloated and difficult to maintain. Similarly, the Subscriber Model would need to interact with both program data and notification services, creating intricate dependencies. This interconnectedness would make the code harder to understand, test, and modify, ultimately leading to a more fragile and error-prone system.

3. Postman has proven to be an indispensable tool for testing our API endpoints. By allowing us to send various HTTP requests with custom headers and bodies, it facilitates thorough testing of our API's functionality. The ability to automate tests through collections and scripts has streamlined our testing process, ensuring consistency and efficiency. Features like environments, which enable us to manage different configurations, and monitors, which allow scheduled API health checks, are particularly useful for our group project. Furthermore, Postman's mock server capabilities could be invaluable for future projects, allowing us to test API interactions even before the backend is fully implemented, thereby accelerating development and improving collaboration.


#### Reflection Publisher-3