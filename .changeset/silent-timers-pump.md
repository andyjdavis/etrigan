---
'@etrigan/logging': major
---

Express logging middleware now will escalate log levels when a warn or an error occurs

It will _buffer_ log messages of a request, when the request is complete it will set an appropriate log level before flushing the logs to the logger.

This means you can set the level to warn or error by default, then if a warn gets logged at the end of the request info level logs will also be logged. On error debug level logs will be logged.

-   Breaking: Removed log scrubbing test helpers, pino can be configured to not log the random information which is more reliable than scrubbing after the fact
-   Note: Due to buffering log messages, requests may use slightly more memory