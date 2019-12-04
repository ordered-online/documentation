![header icon](/assets/header-dark-background.jpg)

The core idea of the ordered.online application is to order online at restaurants, bars, cafés and more.

See our

- [admuc kickoff presentation](/kickoff-admuc.html),
- [scc kickoff presentation](/kickoff-scc.html),
- [admuc checkpoint presentation](/checkpoint-admuc.html)
  as well for more visual impressions.

## Use Cases

![use case diagram](/assets/use-cases.png)

## Trust Problems

The concept of this application comes with some serious trust problems:

1. How can location owners confirm, that an order was placed by a real client?
2. How can a client confirm, that he orders at the right location (i.e., not at a fake location)?
3. How can a location owner confirm, that the client actually payed?

We assessed these trust problems and came to the following solutions:

- We offer a way for the waiter to open a session and generate a scannable (i.e., QR) code to that session.
- This code can be scanned by the user, by which the ordering is made available. The user is now interlocked with the generated session.
- We plan to exclude any payment process from our application at first.

## Project Architecture

![architecture](/assets/project-architecture.png)

Because the application will offer both web user interfaces and native mobile application(s), it is of great importance, that the biggest part of this application is interoperable.
We present an architecture, which is devided into two parts:

1. The microservice based backend API layer
2. The web/native frontend application layer

### Microservice Based Backend API Layer

#### Architecture

To cover our use cases, we assessed the following service architecture:

- [`codes` (click here for its documentation)](codes.md) is our microservice to generate unique, discardable codes, which can also be rendered to a qr code representation.
- [`verification` (click here for its documentation)](verification.md) is our authentication microservice, which handles registration, login, session key based verification and logout.
- [`products` (click here for its documentation)](products.md) is our microservice to create, fetch and edit location based products.
- [`locations` (click here for its documentation)](locations.md) is our microservice to create, fetch and edit locations, i.e. bars, restaurants or cafes.
- [`orders` (click here for its documentation)](orders.md) is our microservice to place and fetch orders.

### Web/Native Frontend Application Layer

[`apps` (click here for the documentation)](apps.md) is our frontend layer and consists of a multi-platform, react native based application.

## Continous Integration

As a continuous integration service we use [Travis](https://travis-ci.org/).
We use Travis as an automated service to build our developer documentation. On commit, travis pushes README changes of microservices to our documentation repository.

## Containerization and Deployment Concepts

Because of our microservice based architecture, it is hard during deployment to interweave all services correctly, since some services depend on other services (e.g., verification) etc. We solve this issue by stringent containerization with [Docker](https://docs.docker.com/).
Each microservice is packed into an own Docker container and interlinked with [Docker networks](https://docs.docker.com/network/). Each microservice obtains its own url scheme. To avoid connections via arbitrary port numbers, we use the built-in url resolving of Docker.
As a high performance load balancer and webserver we use [NGINX](https://www.nginx.com/). NGINX accesses our containerized microservices via their Docker provided url schemes and combines all together to an accessible REST API. Note that the NGINX service itself is again containerized by Docker, which makes it possible to build the complete infrastructure out of the box with Docker.
