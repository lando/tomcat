---
title: Configuration
description: Learn how to configure the Lando Apache Tomcat service.
---

# Configuration

Here are the configuration options, set to the default values, for this service. If you are unsure about where this goes or what this means, we *highly recommend* scanning the [services documentation](https://docs.lando.dev/core/v3/services/lando.html) to get a good handle on how the magicks work.

Also note that options, in addition to the [build steps](https://docs.lando.dev/core/v3/services/lando.html#build-steps) and [overrides](https://docs.lando.dev/core/v3/services/lando.html#overrides) that are available to every service, are shown below:

```yaml
services:
  myservice:
    type: tomcat:8
    webroot: .
    ssl: false
    config:
      server: SEE BELOW
      web: SEE BELOW
      context: SEE BELOW
      users: SEE BELOW
```

## Using custom Tomcat config files

You may need to override our [default tomcat config](https://github.com/lando/tomcat/tree/main/builders) with your own.

If you do this, you must use files that exist inside your application and express them relative to your project root as shown below:

Note that the default files may change based on how you set `ssl`.

**A hypothetical project**

Note that you can put your configuration files anywhere inside your application directory. We use a `config` directory but you can call it whatever you want such as `.lando` in the example below:

```bash
./
|-- config
   |-- server.xml
   |-- web.xml
   |-- context.xml
   |-- tomcat-users.xml
|-- index.html
|-- .lando.yml
```

**Landofile using custom tomcat config**

```yaml
services:
  myservice:
    type: tomcat
    config:
      server: config/server.xml
      web: config/web.xml
      context: config/context.xml
      users: config/tomcat-users.xml
```

**Overriding the CATALINA_OPTS environment variable/enable Tomcat debugging**

As with any Lando service, you can override almost any aspect of the service container that is built by Lando. For the Tomcat service, it is sometimes desireable to alter that CATALINA_OPTS environment variable, to, for example, [enable Tomcat application debugging](https://stackoverflow.com/questions/7677060/debugging-java-application-deployed-in-tomcat). However, CATALINA_OPTS is [used by the Tomcat plugin's builder](https://github.com/lando/tomcat/blob/main/services/tomcat/builder.js#L38) to set a few properties that Lando uses in its default configuration of Tomcat. To save yourself trouble, you'll want to include these properties in CATALINA_OPTS, if you elect to override the environment variable. See the example below:

```yaml
cmd:
  - catalina.sh jdpa start
overrides:
  ports:
    - '8000:8000'
  environment:
    JPDA_ADDRESS: "8000"
    JPDA_TRANSPORT: "dt_socket"
    CATALINA_OPTS: "-Dlando.http=80 -Dlando.https=443 -Dlando.webroot=/app/path-to-your-webroot -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:8000"
```
