# Lesson 1: Ping Pong

In this first lesson we're going to do the most basic things we can in Redis: Send a simple request and receive a simple response.

## Doing it in the REPL

The first thing we're going to do is run the `PING` command directly using the Redis REPL. From a terminal window, issue the following commands and you should see similar feedback being presented.
```
$ redis-cli
127.0.0.1:6379> PING
PONG
127.0.0.1:6379> QUIT
```

> (Remember that if you're using Docker, run `docker exec -it nodeschool-redis redis-cli` instead of just `redis-cli`.)

The `redis-cli` program allows us to interactively run Redis commands on a Redis server. Redis commands are a lot like functions; they have a name, and a series of arguments. In this case the command we're running is `PING`, and it doesn't have any arguments. We also call the `QUIT` command, which tells the `redis-cli` program to close the connection.


## Create a new File

In the `code/` directory, create a new file called `lesson-1.js`. Then, open the file using your favorite code editor. Once that's done, we're going to start adding some code.


## Load the `ioredis` module

Add this line to the top of the file. It'll require the `ioredis` module and make it available as `Redis`.

```javascript
const Redis = require("ioredis");
```


## Define a connection

Next up, create a new instance of `Redis`, and assign the value to `redis`. This will instruct the module to start a connection at some point in the near future.

```javascript
const redis = new Redis('redis://localhost:6379');
```


## Run a command

Add the following lines to the end of the file. This tells the `ioredis` to queue up a command called `PING`. Once the connection has been established (this is happening asynchronously in the background), any of our queued commands will then be sent off to the Redis server. Once the command is received and processed, the Redis server will reply. Node.js will handle this reply and trigger the callback function.
```javascript
redis.ping((err, result) => {
  // ...
});
```


## Handle the results

Add the following lines of code into the body of the callback you added previously.

```javascript
  if (err) { // <1>
    throw err;
  }

  console.log('RESULT', result); // <2>

  redis.disconnect(); // <3>
```

1. If an error was received, the callback will throw it again. This will cause the Node.js application to quit and display a stack trace. Raise your hand if this causes your program to crash.
2. Assuming an error wasn't thrown, you should now see the message “RESULT PONG” displayed in your console. If you don't see that message, also raise your hand.
3. Finally, we tell the `ioredis` module to disconnect from the Redis server. Since the Redis connection was the final thing keeping the process running the program will gracefully quit.


## Summary

In this first lesson we ran the `PING` Redis command. It gives us a simple string reply of `PONG`. To run this in a Node.js program, we first had to require `ioredis` and establish a connection. Afterwards we called `redis.ping()` to run the command.

As we'll see in the next lesson, Redis offers many other commands. Each of these commands are provided to us by the `ioredis` by calling `redis.{commandName}`.
