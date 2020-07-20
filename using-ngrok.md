# Using NgRok to create a tunnel to local webserver

## Setup

In development, a server is usually provided - something along the lines of
`http-server` or the framework CLI development servers. This will usually be on
port `8080` but may be on something different.

If a webserver isn't running, run one. If you don't have anything, install node
and run 

```
npm i -g http-server
```

to install `http-server` globally.

## Installation

Install link:

* https://ngrok.com/download

## Running the tunnel

The following will work for most cases:

```
ngrok http 8080
```

Notes

* `http` is the protocol
* `8080` is the port number

In some cases (ie when using the react or vue dev server), you may have to
supply the host header.

```
ngrok http 8080 -host-header="localhost:8080"
```

