# List Open Ports

The following command lists all open ports on the Mac:

Run

```bash
$ lsof -i -P | grep -i "listen"
```

It can be useful when a particular port is occupied and there is a need to use that particular port.

You can list the occupied port and kill the process which is using this port.