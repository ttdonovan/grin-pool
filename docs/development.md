# Development Setup [DRAFT]

The following documentation is for a Mac OS X environment setup and
contribution. Dependency package management is done by using
[Homebrew](https://brew.sh/).

## TODO

Checklist of components that need explanation:

[ ] `ansible`
[x] `grin`
[ ] `grin-py/api`
[ ] `grin-py/grinbase`
[ ] `grin-py/grinlib`
[ ] `grin-py/services`
[ ] `grin-py/webui` (is this used?)
[x] `grin-py/webui-js`
[ ] `keybase`
[ ] `logstash`
[ ] `rmp`
[ ] `splunk`
[x] `stratum`

**#TODO** Question should some this be split between "development" and "operations"?
Meaning would some of this be better suited for an "operations" guide on how to
setup and run a mining pool - fine line between Dev and Ops. The main `README.md`
starts to address some of this question.

## Components

Described below are the components used to operate the Grin mining pool. Each
will have a description of it's purpose and also include information on it's
dependencies, installation and running a development environment.

### Grin-Pool User Interface (webui-js)

The web user interface for a Grin mining pool. Found at
`grin-pool/grin-py/webui-js`. This is the UI of HTML/CSS found on
[mwgrinpool.com](https://mwgrinpool.com).

#### Dependencies

* [Node.js](https://nodejs.org) - allows for command-line execution of JavaScript
* [Yarn](https://yarnpkg.com) - JavaScript dependency manager
* [serve](https://www.npmjs.com/package/serve) - allows serving of local files

#### Installation

```
> brew install node
> brew install yarn
> yarn global add serve
```

#### Running: Steps to build & serve

```
> cd grin-pool/grin-py/webui-js
> yarn
> yarn start
```

#### Production: Serve production build

```
> yarn build
> yarn -s
```

**Note** to change production port from `5000` execute the command
`yarn serve -s build -p [portNumber]`.

See the **README.md** for more detailed information:
`grin-pool/grin-py/webui-js/README.md`

#### Grin-Pool Stratum Server

The Grin mining pool. Found at `grin-pool/stratum`. The Stratum server is the
proxy all miners connect to for mining Grin.

#### Dependencies

* [Rust](https://www.rust-lang.org/)

#### Installation

```
> curl https://sh.rustup.rs -sSf | sh
# TODO: remove the dependency of this directory path needs to be configurable
> sudo mkdir /stratum
```

#### Running: Steps to build & run (or test)

```
> cd grin-pool/stratum
> rustup update
> rustup default stable
> cargo build
# TODO: would like to change path of '/stratum' or make it configurable to remove 'sudo'
> sudo cargo run
> cargo test
```

### Grin

The Docker container build for a Grin server (and wallet?). Found at
`grin-pool/grin`. This is used by the Grin-Pool (Stratum Server) as an upstream
Grin node.
