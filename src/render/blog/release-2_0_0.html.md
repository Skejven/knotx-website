---
title: Knot.x 2.0 released!
description: We have just released a major release Knot.x 2.0.
author: skejven
keywords: release
order: 1
date: 2019-08-22
knotxVersions:
    - 2.0.0
---
# Knot.x 2.0
Hurray,

Knot.x 2.0 - the open-source integrations framework is finally here!
It comes with the HTTP server, distribution and platform for building backend APIs.

Before we go throught new modules and features, we would like to thank all the contributors. Your participation has been essential to this achievement!

The main changes and features of the second version are:

- `Design First approach`: We get rid of custom routing definitions in favour of using standards. The [Open API v3](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.2.md) specification is language-agnostic, and human readable way a routing is defined.
> The Design First approach advocates for designing the API's contract first before writing any code.
>
> -- https://swagger.io/blog/api-design/design-first-or-code-first-api-development/

  It addresses distributed systems orchestration challenges, in which fine-grained services define their API's objectives consumed by all your local and distributed teams that can be validated during design definition, before writing any code.
- `Configurable integrations`: we completely redesigned Fragments processing (a Fragment is a piece of any kind of document that can be processed independently, e.g. an HTML snippet that represents the shopping cart or a JSON containing person's bookshelf). Now, building custom
logic for integrating the data is as easy as defining a [graph of actions](https://github.com/Knotx/knotx-fragments#how-does-it-work). Read more [here](/blog/configurable-integrations/).
- `Stability patterns`: We know, that when it comes to integrating multiple services over the network, not all the things go smooth. That's why Knot.x 2 brings patters such as *Circuit breaker*, *Timeouts*, *Bulkhead* and more out of the box.

With 2.0 we bring completely new experience for building any kind of backend API such as:
- Gateway API: a logic combining data from different sources, introducing caches or fallbacks
- Backend For Frontend: meets SPA challenges and allows to introduce RESTful or GraphQL contracts between your frontend and backend applications
- HTTP / Web API: exposes any kind of datasource with HTTP-based API

## Evolution but not revolution
Instead of developing all new features exclusively in Knot.x 2, we introduced some of these features in the 1.x versions. The Knot.x 2 development focus on more fundamental changes that cannot be done without breaking some compatibility. Read more [here](/blog/evolution-of-knotx/).

![knotx-evolution](/img/blog/release-2_0_0/evolution-diagram.png)

Instead of pointing each change,
we introduce all the modules (old and new ones) with a brief description of their potential and purpose.
You can find all the modules under https://github.com/Knotx. There is one special module (which was previously holding the `core`): https://github.com/Knotx/knotx. Currently, it keeps the overview of all official Knot.x modules and high-level vision
(e.g. changes that require implementation at multiple modules).

### `knotx-core` is gone
Microservice solutions fit better with the microservice repository structure. There is no such thing as `knotx-core` anymore. What we started in the latest Knot.x `1.X` versions
(extracting parts of `core` to databridge, template engine modules) was a prelude
to the major Knot.x structure reorganization in `2.0`. Modules presented below
to replace the `core` concept with smaller, well-defined responsibilities.

### [knotx-server-http](https://github.com/Knotx/knotx-server-http)
The server is essentially a "heart" of Knot.x. It's scalable (vertically and horizontally), pluggable (easy to extend), fault-tolerant and highly efficient reactive HTTP server based on Vert.x.
It handles all incoming HTTP requests and routes the traffic using OpenAPI specs.

### [knotx-fragments](https://github.com/Knotx/knotx-fragments)
While Knot.x HTTP Server is a "hearth" of Knot.x, Fragments processing is its "brain".
Knot.x Fragments is a Swiss Army knife for integrating with dynamic data sources. It comes with distributed systems stability patterns such as a circuit breaker to handle different kinds of network failures. Thanks to those build-in mechanisms developers can focus more on delivering business logic and make the solution ready to handle any unexpected integration problems.

### [knotx-stack](https://github.com/Knotx/knotx-stack)
Stack is a way of distributing fully functional bootstrap project for Knot.x-based solutions.
It does not require any external dependencies so it is used to build a Knot.x Docker images and
to setup an instance with Chef. Read more about how to start building Knot.x solution with [Getting Started with Knot.x Stack](https://knotx.io/tutorials/getting-started-with-knotx-stack/) tutorial.

### [knotx-commons](https://github.com/Knotx/knotx-commons)
Simple util classes that do not depend on other Knot.x modules.

### [knotx-cookbook](https://github.com/Knotx/knotx-cookbook)
Cookbook for automated Knot.x deployment.

### [knotx-dashboard](https://github.com/Knotx/knotx-dashboard)
The dashboard provides an online Knot.x instance monitoring. You may use it to monitor Knot.x
instance performance in real-time.

### [knotx-data-bridge](https://github.com/Knotx/knotx-data-bridge)
Data Bridge is an integration module that enriches Fragments with the data from external sources.
It comes with HTTP Action that connects to the external WEB endpoint that responds with JSON.

### [knotx-dependencies](https://github.com/Knotx/knotx-dependencies)
Dependencies define the versions of Knot.x components and required dependencies (in BOM fashion).

### [knotx-docker](https://github.com/Knotx/knotx-docker)
Knot.x Docker base image. The image is intended to be used by extension using the Docker `FROM` directive. Knot.x comes with standard and *alpine* (~`84 MB`) distributions.

### [knotx-gradle-plugins](https://github.com/Knotx/knotx-gradle-plugins)
Gradle plugins that help manage Knot.x modules build. Most of the Knot.x 2 modules
are built and deployed with Gradle 5 using Kotlin DSL.

### [knotx-junit5](https://github.com/Knotx/knotx-junit5)
JUnit 5 support and extensions for Vert.x projects.

### [knotx-launcher](https://github.com/Knotx/knotx-launcher)
Launcher provides a way to configure and run bare Knot.x instance. It can be used
as a microservice platform build on top of Vert.x using HOCON syntax for configuration
and [modules management](https://github.com/Knotx/knotx-launcher#modules-configuration).

### [knotx-repository-connector](https://github.com/Knotx/knotx-repository-connector)
Repository connector delivers template from external repositories like CMS or file system

### [knotx-starter-kit](https://github.com/Knotx/knotx-starter-kit)
Knot.x Starter Kit is a template project that you can use when creating some Knot.x extensions.
It enables easy and fast start for the Knot.x-based solutions.
Read more about how to start with Knot.x and Docker in the [Getting Started with Docker](https://knotx.io/tutorials/getting-started-with-docker/) tutorial.

### [knotx-template-engine](https://github.com/Knotx/knotx-template-engine)
Template Engine processes Fragment's data and template into the final markup. Knot.x
comes with implemented [Handlebars](http://handlebarsjs.com/) engine out of the box,
but creating any custom template engine is [very easy](https://github.com/Knotx/knotx-template-engine#how-to-create-a-custom-template-engine-strategy).
