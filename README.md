# runtime.js

[![npm](https://img.shields.io/npm/v/runtimejs.svg)](https://www.npmjs.com/package/runtimejs)

__runtime.js__ is an open-source library operating system (unikernel) for the cloud that runs JavaScript, can be bundled up with an application and deployed as a lightweight and immutable VM image.

It's built on [V8 JavaScript engine](https://code.google.com/p/v8/) and uses event-driven and non-blocking I/O model inspired by [Node.js](https://nodejs.org/). At the moment [KVM](http://www.linux-kvm.org/page/Main_Page) is the only supported hypervisor.

It tries to be compatible with npm module ecosystem and supports some of the Node.js API.

_WARNING: project is in development and not ready for production use._

### Project goals

#### Short term
- Update documentation for both the C++ kernel and the JS API and
  modules
- Get Tests for the JS portion working
- Maintain what's currently here
- Maintain build tooling for easy development

#### Long term
- Upgrade v8 to a more modern version
- Implement threads with v8 Isolates

### Installation

First thing is the command line tool `runtime-cli`, it will add `runtime` command to the shell. Type `runtime` to get full usage help.

```
npm install runtime-cli -g
```

Make sure QEMU is installed, it enables running applications locally.

```
brew install qemu           # OSX
sudo apt-get install qemu   # Ubuntu
```

### Getting Started

Create new project and add `index.js` entry point file:

```
mkdir project
cd project
npm init
npm install runtimejs --save
echo "console.log('ok')" > index.js
```

Run project locally in QEMU:

```
runtime start
```

That's it, it should start and print `ok` in the console.

Optionally you can let it watch directory for changes and restart QEMU automatically:

```
runtime watch
```

## How does it work?

There are two main components: operating system kernel and a <a href="https://www.npmjs.com/package/runtimejs"><nobr>JavaScript library</nobr></a>.

The kernel is written in C++ and manages low-level resources like CPU and memory, runs JavaScript using embedded V8 engine. Library drives the entire system and manages hardware devices (usually virtualized by hypervisor).

## Building the Kernel

Build the initial Docker image used for building the kernel, and build
the kernel.
```
npm run build
```

To build the kernel in stages, assemble the Docker image used for
building.
```
npm run prebuild
```

The kernel can be built without needing to run the prebuild step every
time now.
```
npm run scons
```

## Docs

[API docs](https://github.com/runtimejs/runtime/wiki/API-docs)

## Community

[Modules and projects developed by the community for runtime.js](https://github.com/runtimejs/runtime/wiki/Community)

License
----
Apache License, Version 2.0
