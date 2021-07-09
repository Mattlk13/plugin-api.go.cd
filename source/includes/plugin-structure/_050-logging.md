# Logging

> An example for plugin logging:

```java
package com.example.go.testplugin;

import com.thoughtworks.go.plugin.api.*;
import com.thoughtworks.go.plugin.api.logging.Logger;
import com.google.gson.Gson;
import java.util.*;

@Extension
public class ExampleExtension implements GoPlugin {
  private static final Logger LOG = Logger.getLoggerFor(ExampleExtension.class);
  private GoApplicationAccessor accessor;

  public GoPluginApiResponse handle(GoPluginApiRequest request) throws UnhandledRequestTypeException {
    LOG.info("Request from server: " + request.requestName());
  }
}
```

Plugins can optionally log events to a log file. Plugin logging is supported by `com.thoughtworks.go.plugin.api.logging.Logger` class, the Logger class should be available on including the `go-plugin-api` dependency as mentioned earlier.

## Log location

Each plugin will have a separate log file and the name of the log file will be in the format `plugin-<plugin_id>.log`. The location of the plugin log file will be the same as the location of the GoCD server logs.

## Log level

The default log level for a plugin is `info`. The log level can be controlled using a Java system property which should be provided to the GoCD server.

The system property to control the log level is specific to each plugin and is of the format `plugin.<plugin_id>.log.level=<log_level>`. The log level can be either of `info`, `debug`, `warn`, `error`.
