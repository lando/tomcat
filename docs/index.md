---
title: Apache Tomcat Lando Plugin
description: Add a highly configurable Apache Tomcat service to Lando for local development with all the power of Docker and Docker Compose
next: ./config.html
---

# Apache Tomcat

[Tomcat](https://tomcat.apache.org) The Apache Tomcat® software is an open source implementation of the Java Servlet, JavaServer Pages, Java Expression Language and Java WebSocket technologies.

You can easily add it to your Lando app by adding an entry to the [services](https://docs.lando.dev/core/v3/lando-service.html) top-level config in your [Landofile](https://docs.lando.dev/core/v3).

```yaml
services:
  myservice:
    type: tomcat
```

## Supported versions

*   [9](https://hub.docker.com/_/tomcat/)
*   [9.0](https://hub.docker.com/_/tomcat/)
*   **[8](https://hub.docker.com/_/tomcat/)** **(default)**
*   [8.5](https://hub.docker.com/_/tomcat/)
*   [custom](https://docs.lando.dev/core/v3/lando-service.html#overrides)

## Legacy versions

You can still run these versions with Lando but for all intents and purposes they should be considered deprecated (e.g. YMMV and do not expect a ton of support if you have an issue).

*   [7](https://hub.docker.com/_/tomcat/)
*   [7.0](https://hub.docker.com/_/tomcat/)

## Patch versions

::: warning Not officially supported!
While we allow users to specify patch versions for this service, they are not *officially* supported, so if you use one, YMMV.
:::

To use a patch version, you can do something as shown below:

```yaml
services:
  myservice:
    type: tomcat:7.0.91
```

But make sure you use one of the available [patch tags](https://hub.docker.com/_/tomcat/tags) for the underlying image we are using.

