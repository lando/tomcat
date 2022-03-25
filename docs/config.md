---
title: Configuration
description: Learn how to configure the Lando Apache Tomcat service.
---

# Configuration

Here are the configuration options, set to the default values, for this service. If you are unsure about where this goes or what this means, we *highly recommend* scanning the [services documentation](https://docs.lando.dev/config/services.html) to get a good handle on how the magicks work.

Also note that options, in addition to the [build steps](https://docs.lando.dev/config/services.html#build-steps) and [overrides](https://docs.lando.dev/config/services.html#overrides) that are available to every service, are shown below:

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

You may need to override our [default tomcat config](https://github.com/lando/tomcat/tree/main/services/tomcat) with your own.

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
