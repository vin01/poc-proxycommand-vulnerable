## RCE via insecure `~/.ssh/config`

Use of tokens like %h, %p in `ProxyCommand` is quite popular to use tunnels and connection proxying using SSH.

### Vulnerable config

```
host *.example.com
  ProxyCommand /usr/bin/nc -X connect -x 192.0.2.0:8080 %h %p
```

Use of tokens as it is without single quotes, allows code execution. 

### Secure version

```
host *.example.com
  ProxyCommand /usr/bin/nc -X connect -x 192.0.2.0:8080 '%h' '%p'
```

Taken from: https://man.openbsd.org/ssh_config#ProxyCommand

### What is in this reposiotry

A submodule which would exploit this vulnerability to pop a calculator on OSX.

Try it out using: `git clone https://github.com/vin01/poc-proxycommand-vulnerable --recurse-submodules`
