## Docker Images For Nonstop Setup
Nonstop is a set of tools to assist in creating a continuous integration and delivery environment. It does this primarily via self-updating service hosts that pull new versions of packaged artifacts from an index.

This repository provides Docker containers for the various concerns in attempts to simplify standing up a functional environment using Nonstop and Drone. Each project provides a README that explains the intended use.

## Recommended Use
Steal this repository. Really. It's likely that you'll put credentials into some of these containers when setting them up (like the Drone container).

## Inventory
Each of these Dockerfiles has a specific role. They are arranged to show inheritence between images.

 * [Drone server](drone/README.md)
 * Baseline NodeSource Image (ubuntu 14.04 + Node version)
	 * [Drone build image - Node](drone-node/README.md)
	 * [Nonstop index](index/README.md)
	 * [Nonstop host - Node](node-host/README.md)
	 * [Nonstop host - CoffeeScript](coffee-host/README.md)
 * [Drone build image - Web](drone-web/README.md)

## Setup
You'll need:
 * A build server with Docker and
 	* a Drone container
 	* an Index container
 	* the Node and/or Web build images
 * At least one server for hosts
 	* the Node and/or Coffee images

 Technically you can put all these things on a single box but it might get a little cramped.

## Templates
To put a repository into the pipeline, you'll need to:

 * Sync Drone with your account
 * Browse to the repository
 * Activate it
 * Add a `.drone.yml`, `.nonstop.yaml` and `.boot.yaml` to the root of the repository.

### Drone File
This file controls what Docker image Drone will spin up to build your project in a container.

This template demonstrates a Node.JS project build with slack integration.

> Note: replace placeholders in the template before using ;)

```yaml
image: 'arob/drone-nonstop-node:0.12.7'
script:
  - 'ns --verbose'
deploy:
  bash:
    command: 'ns upload --latest --index [INDEX IP] --port 4444 --token [AGENT TOKEN]'
notify:
  slack:
    webhook_url: [SLACK INTEGRATION URL]
    username: 'drone'
    channel: '#drone'
    on_started: true
    on_success: true
    on_failure: true
```

### Nonstop Build File
Nonstop build files contain a sequence of shell commands to run from the root of your repository and a list of globs to tell it how to package your build output.

This template demonstrates a very simple two step build that installs NPM dependencies and then runs tests via a Gulp command (our projects tend to use [BigGulp](https://github.com/leankit-labs/biggulp)).

> Note: _always_ include the boot file in your package or the service host will not be able to start it.

```yaml
projects:
  'some-project':
    path: './'
    steps:
      npm:
        path: './'
        command: 'npm'
        arguments:
          - 'install'
      test:
        path: './'
        command: 'gulp'
        arguments:
          - 'test-behavior'
    pack:
      pattern: './node_modules/**,./bin/**,./*.json,.boot.yaml'
```

### Boot File
This is a fairly simple file that the service host requires in order to start your service after unpackaging the tarball of a build.

```yaml
boot: "node ./src/index.js"
```

## Things that may happen one day

 * Create a yo generator that generates Dockerfiles based on information
 * Create a script to handle updating containers on version changes

