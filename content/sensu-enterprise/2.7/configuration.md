---
title: "Enterprise Configuration"
product: "Sensu Enterprise"
version: "2.7"
weight: 2
menu: "sensu-enterprise-2.7"
---

Sensu Enterprise service scripts make use of certain environment variable values
to configure the Java runtime environment. These settings take effect prior to
Sensu Enterprise loading configuration files from disk as described in [Sensu
Configuration][1] reference documentation.

Values for the environment variables described in this document should be set by
editing `/etc/default/sensu-enterprise`. After changing values in this file, the
sensu-enterprise service must be restarted before the new values can take effect.

## Sensu Enterprise environment variables

The Sensu Enterprise honors the following environment variables. For
configuration honored by both Sensu Enterprise and Sensu Core, see the
[Sensu configuration reference documentation][1].

HEAP_SIZE    | 
-------------|-------
description  | Java initial heap size (`Xms`) and maximum heap size (`Xmx`). Increasing heap size is a common solution to out of memory (java.lang.OutOfMemoryError) errors.
type         | String
required     | false
default      | `2048m`
example      | {{< highlight shell >}}HEAP_SIZE=4096m{{< /highlight >}}

HEAP_DUMP_PATH | 
---------------|------
description    | This value determines the file system path where Sensu Enterprise will write the contents of Java's memory heap in case of a crash. Because the size of each heap dump file is determined by the JVM heap size, it's possible to fill the underlying disk after repeated crashes.
type           | String
required       | false
default        | `/var/cache/sensu-enterprise`
example        | {{< highlight shell >}}HEAP_DUMP_PATH=/var/space/sensu-enterprise{{< /highlight >}}

JAVA_OPTS    | 
-------------|------
description  | This value is used to configure JVM runtime parameters when running Sensu Enterprise. Flags allowed here are determined by your system's Java Runtime Environment.
type         | String
required     | false
example      | {{< highlight shell >}}JAVA_OPTS="-Djava.net.preferIPv4Stack=true"{{< /highlight >}}

MAX_OPEN_FILES | 
---------------|------
description    | This value is passed to `ulimit` for configuring the upper limit on open file descriptors.
type           | Integer
required       | false
default        | `16384`
example        | {{< highlight shell >}}MAX_OPEN_FILES=32768{{< /highlight >}}

[1]: /sensu-core/1.0/reference/configuration
