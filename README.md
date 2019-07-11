# Coding challenge

## Goal

The goal of this challenge is to deliver insights about a stream of data.

In this particular case, you are provided with a stream of events (each event represents a query, that ran on a database) and the insight you want to deliver is how many queries are running at the same time at a specific point in time. Lets look at an example:

**Example:**

Assuming the following events on the stream:

```javascript
[
  {
    // ...
    'executionTime': 120000, // 2 mins
    'timestamp': 1546322400 // 2019-01-01T06:00:00+00:00
  }, {
    // ...
    'executionTime': 120000, // 2 mins
    'timestamp': 1546322460 // 2019-01-01T06:01:00+00:00
  }
]
```

Your solution should yield the following result:

Time                      | Queries Running
--------------------------|----------------
2019-01-01T06:00:00+00:00 | 1
2019-01-01T06:01:00+00:00 | 2
2019-01-01T06:02:00+00:00 | 2
2019-01-01T06:03:00+00:00 | 1

## Event schema

Field           | Description
----------------|------------
`id`            | Unique query ID
`status`        | Query status (one of `Success`, `Failure`, or `Cancelled`)
`database`      | The database the query ran against
`executionTime` | Query runtime in ms
`bytesScanned`  | Amount of bytes scanned in order to fulfill the query
`timestamp`     | Unix timestamp of query execution

## Setup

In this repository you will find a prepared environment using docker containers:

- `coding-challenge_webserver`:	This will provide you with the stream of events. Once you run it, more information on how to receive the events is provided on http://localhost:8080.
- `mysql`:	A MySQL database which you **might** want to use in order to aggregate your results and as an interface for the end-user to deliver the requested insights.
- `jupyter`: A jupyter notebook with both a Scala and Python kernel. It comes with preconfigured notebooks which are already connected to both, the event stream and the MySQL server. Feel free to use this to run and share some adhoc experiments. You can find the URL including the access token in the logs of the container. Note that you need to change the hostname to `localhost` though in order to access it from your local machine.

The only container that is absolutely necessary in order to solve this challenge is obviously the `coding-challenge_webserver`. All other containers are only there to minimize the time for bootstrapping the solution but it is **absolutely not required to use any of them**. Feel free to use them if you wish and also feel free to provide an environment that **you** are comfortable with.

### Running

Run 
```
docker-compose up
```

to start the environment.

## Constraints
### User Interface

The user interface of the final application should allow
- querying for the amount of queries running in parallel on a specific point in time
- provide an overview over the number of parallel queries over time

The technical implementation of the interface is up to you. We assume a tech-savvy user, so the interface could be the provided by MySQL itself, a REPL session - via command line -, an HTTP interface or something completely different. You should provide some **minimal documentation** on how to use the interface.

## Hints

You are allowed to use auxiliary libraries if you need to (e.g. web frameworks, CLI frameworks, parsing libraries, etc.). **Feel free to make assumptions** if the description of the challenge is unclear.

A test suite should be part of your solution.

Focus on establishing a minimum viable solution first before considering any optimizations or optional features. It is more important to deliver something that works and that can be improved rather than something that doesn't work.

Once you have viable solution, feel free to incorporate your own ideas.

**Have fun!**
