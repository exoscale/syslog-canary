# Canary for syslog

If you syslog daemon happens to not read messages from `/dev/log`,
most of your system will stop to work as many programs will be blocked
when trying to write to `/dev/log`. On Linux, both `SOCK_DGRAM` and
`SOCK_STREAM` are reliable and sockets using those types will
therefore block on write when the reader won't read.

This simple canary will open `/dev/log` and check if it is ready for
write. If not, it will execute the provided command to restart the
syslog daemon.
