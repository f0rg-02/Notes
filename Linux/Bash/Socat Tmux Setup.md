---
Name: Socat Tmux Setup
Platform: Linux
tags: Resources
---
Create and handle multiple connections using socat and tmux. ^63a416

Bash script to start with socat.

**NOTE: Tmux needs to be started before running socat**

```ruby
#!/bin/bash

SOCKDIR=$(mktemp -d)
SOCKF=${SOCKDIR}/usock

# Start tmux, if needed
tmux start
# Create window
tmux new-window "socat UNIX-LISTEN:${SOCKF},umask=0077 STDIO"
# Wait for socket
while test ! -e ${SOCKF} ; do sleep 1 ; done
# Use socat to ship data between the unix socket and STDIO.
exec socat STDIO UNIX-CONNECT:${SOCKF}

```

Socat command:

```
socat OPENSSL-LISTEN:4443,cert=bind.pem,reuseaddr,verify=0,fork EXEC:./socat_tmux.sh
```

nce a connection is made and established... the bash script is run to send the connection to another tmux window in tmux session.

To see and go to connection press Ctrl-A (Or B if default) + S. **You need to do Ctrl-A/B and release it before pressing S**