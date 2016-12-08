---
layout: default
title: {{ site.name }}
---

# Sorna Project

Sorna is now fully open-sourced!  
<sup>* Python 3.5.2+, Linux 64bit or macOS, Docker 1.10+ required</sup>

## Getting Started

Just do some magic:

```sh
# configure virtualenv
python3 -m venv venv
source ~/venv/bin/activate
pip install -U pip

# install
pip install sorna-client
export SORNA_ACCESS_KEY=...
export SORNA_SECRET_KEY=...
```

Then run the following Python code:

```python
import sorna.kernel import *

kid = create_kernel('lua5')
result = execute_code('<reserved>', '''print("hello world!")''')
print(result['stdout'])
# hello world!
destroy_kernel(kid)
```

Now you have executed a real Lua code without installing Lua!  
There are [many more languages you can use](http://github.com/lablup/sorna-repl).

You may run also [your own Sorna API server on your machines](https://github.com/lablup/sorna).

Note: public API key registration site is under construction!

## Server Architecture

Sorna consists of three loosely coupled components.

 * **sorna-gateway**: Provides an HTTP REST API server and routes user code snippets to agents.

 * **sorna-agent**: Executes user code snippets inside Docker containers.

 * **sorna-repl**: The Docker containers with REPL (read-evaluate-print-loop) daemons in various programming languages.

We call each code-running container *a kernel*.
All kernels have our custom-built sandbox (called "sorna-jail") that secures our infrastructure on the system-call level.

Additionally, we provide a pluggable **sorna-media** Javascript library and Python packages for front-end services to render interactive graphics and handle multi-media outputs generated from kernels.

## License

Sorna and its sub-projects are distributed under GNU Lesser Public License (LGPL) 2.0.