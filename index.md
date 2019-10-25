![header icon](/assets/header-dark-background.jpg)

The core idea of the ordered.online application is to substitute redundant work of waiters in bars/restaurants/cafes ("locations") and to offer a live interactive interface for incoming orders. Furthermore:
- It should be possible for location owners to register an account and their locations with relevant information.
- Users should be able to find locations, at least based on their location or based on the name of the location.
- Orders should be made available without login.
- Orders should be streamed directly to a UI of the location owner.
- The app should handle user/order verification swiftly, so users are not bothered by it.

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
- [`codes`](codes.md) is our microservice to generate unique, discardable codes, which can also be rendered to a qr code representation.
- [`verification`](verification.md) is our authentication microservice, which handles registration, login, session key based verification and logout.
- [`menus`](menus.md) is our microservice to create, fetch and edit location based menus.
- [`locations`](locations.md) is our microservice to create, fetch and edit locations, i.e. bars, restaurants or cafes.
- [`orders`](orders.md) is our microservice to place and fetch orders.

#### Containerization and Deployment Concepts

`TODO`

### Web/Native Frontend Application Layer

`TODO`

