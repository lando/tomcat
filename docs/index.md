---
title: Apache Tomcat Lando Plugin
description: Add a highly configurable Apache Tomcat service to Lando for local development with all the power of Docker and Docker Compose
next: ./config.html
---

# Apache Tomcat

[Tomcat](https://tomcat.apache.org) The Apache Tomcat® software is an open source implementation of the Java Servlet, JavaServer Pages, Java Expression Language and Java WebSocket technologies.

You can easily add it to your Lando app by adding an entry to the [services](https://docs.lando.dev/config/services.html) top-level config in your [Landofile](https://docs.lando.dev/config/lando.html).

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
*   [custom](https://docs.lando.dev/config/services.html#advanced)

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

But make sure you use one of the available [patch tags](https://hub.docker.com/r/library/tomcat/tags/) for the underlying image we are using.

## Custom Installation

This plugin is included with Lando by default. That means if you have Lando version `3.0.8` or higher then this plugin is already installed!

However if you would like to manually install the plugin, update it to the bleeding edge or install a particular version then use the below. Note that this installation method requires Lando `3.5.0+`.

:::: code-group
::: code-group-item LANDO 3.21+
```bash:no-line-numbers
lando plugin-add @lando/tomcat
```
:::
::: code-group-item HYPERDRIVE
```bash:no-line-numbers
# @TODO
# @NOTE: This doesn't actaully work yet
hyperdrive install @lando/tomcat
```
:::
::: code-group-item DOCKER
```bash:no-line-numbers
# Ensure you have a global plugins directory
mkdir -p ~/.lando/plugins

# Install plugin
# NOTE: Modify the "npm install @lando/tomcat" line to install a particular version eg
# npm install @lando/tomcat@0.5.2
docker run --rm -it -v ${HOME}/.lando/plugins:/plugins -w /tmp node:14-alpine sh -c \
  "npm init -y \
  && npm install @lando/tomcat --production --flat --no-default-rc --no-lockfile --link-duplicates \
  && npm install --production --cwd /tmp/node_modules/@lando/tomcat \
  && mkdir -p /plugins/@lando \
  && mv --force /tmp/node_modules/@lando/tomcat /plugins/@lando/tomcat"

# Rebuild the plugin cache
lando --clear
```
:::
::::

You should be able to verify the plugin is installed by running `lando config --path plugins` and checking for `@lando/tomcat`. This command will also show you _where_ the plugin is being loaded from.
