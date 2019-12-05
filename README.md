# Node.js + Redis Workshop

This is a beginners workshop for Node.js engineers who would like to work with Redis.

## Pre-Requisites

Try to do the following before coming to the workshop. If not, that's okay too.

### Install Node.js

- Install the current LTS version: <https://nodejs.org/en/>

### Install Redis

#### macOS with Homebrew

If you have [Homebrew](https://brew.sh/) installed, then follow along with these instructions. If you don't already have Homebrew installed it's worth giving it a try, as it's very beneficial to installing other software on your Mac.

```shell
$ brew install redis # this installs Redis
$ redis-server # this starts the server

# switch to a new terminal window

$ redis-cli PING # this sends a command to redis
> PONG # if you get this message back then it worked

$ redis-cli # use this for an interactive Redis REPL
```

#### Linux with Apt

If you're using Ubuntu / Debian / Linux Mint, then this is for you. We can download the Redis source code and install it.

```shell
$ sudo apt-get update
$ sudo apt-get install build-essential
$ curl -O http://download.redis.io/redis-stable.tar.gz
$ tar xzvf redis-stable.tar.gz
$ cd redis-stable
$ make
$ sudo make install
$ redis-server # this starts the server

# switch to a new terminal window

$ redis-cli PING # this sends a command to redis
> PONG # if you get this message back then it worked

$ redis-cli # use this for an interactive Redis REPL
```

#### Any OS with Docker

```shell
$ docker run \
  --name nodeschool-redis \
  -p 6379:6379 \
  -d redis \
  redis-server

# switch to a new terminal window

$ docker exec -it nodeschool-redis redis-cli PING # this sends a command to redis
> PONG # if you get this message back then it worked

$ docker exec -it nodeschool-redis redis-cli PING # use this for an interactive Redis REPL
```
