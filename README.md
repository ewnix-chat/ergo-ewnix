# Oragono

Oragono is an IRC daemon written in Go. It's an early, experimental fork of the [Ergonomadic](https://github.com/edmund-huber/ergonomadic) IRC daemon.

Also see the [mammon](https://github.com/mammon-ircd/mammon) IRC daemon for a similar project written in Python instead.

---

[![Go Report Card](https://goreportcard.com/badge/github.com/DanielOaks/oragono)](https://goreportcard.com/report/github.com/DanielOaks/oragono)

---

This project adheres to [Semantic Versioning](http://semver.org/). For the purposes of versioning, we consider the "public API" to refer to the configuration files, CLI interface and database format.

*NOTE: Things are probably very broken right now. The `THEATER` command does not work, and I'm currently most of the way through rearchitecting the command handling. It should be finished apart from the `THEATER` command, but things are probably still broken.*

## Features

* UTF-8 nick and channel names
* [yaml](http://yaml.org/) configuration
* native TLS/SSL support
* server password (`PASS` command)
* channels with most standard modes
* IRC operators
* ident lookups for usernames
* passwords stored in [bcrypt][go-crypto] format
* channels that [persist][go-sqlite] between restarts (+P)
* IRCv3 support

### What about TLS/SSL?

There is inbuilt TLS support using the Go TLS implementation. However,
[stunnel](https://www.stunnel.org/index.html) version 4.56 with haproxy's
[PROXY protocol](http://haproxy.1wt.eu/download/1.5/doc/proxy-protocol.txt)
may also be used. This will allow the server to get the client's original
addresses for hostname lookups.

## Installation

```sh
go get
go install
cp oragono.yaml ircd.yaml
vim ircd.yaml  # modify the config file to your liking
oragono initdb
oragono mkcerts
```

**Note:** This installation will give you unsigned certificates only suitable for teting purposes.
For real crets, look into [Let's Encrypt](https://letsencrypt.org/).

## Configuration

See the example [`oragono.yaml`](oragono.yaml). Passwords are stored using bcrypt. You can generate encrypted password strings for use in the config with the `genpasswd` subcommand.

```sh
oragono genpasswd
```

## Running the server

```sh
oragono run
```

## Credits

* Jeremy Latt, creator of Ergonomadic, <https://github.com/jlatt>
* Edmund Huber, maintainer of Ergonomadic, <https://github.com/edmund-huber>
* Niels Freier, added WebSocket support to Ergonomadic, <https://github.com/stumpyfr>
* Daniel Oakley, maintainer of Oragono, <https://github.com/DanielOaks>
* apologies to anyone I forgot.

[go-crypto]: https://godoc.org/golang.org/x/crypto
[go-sqlite]: https://github.com/mattn/go-sqlite3
