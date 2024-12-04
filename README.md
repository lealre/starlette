<p align="center">
  <a href="https://www.starlette.io/"><img width="420px" src="https://raw.githubusercontent.com/encode/starlette/master/docs/img/starlette.svg" alt='starlette'></a>
</p>
<p align="center">
    <em>✨ The little ASGI framework that shines. ✨</em>
</p>

---

[![Build Status](https://github.com/encode/starlette/workflows/Test%20Suite/badge.svg)](https://github.com/encode/starlette/actions)
[![Package version](https://badge.fury.io/py/starlette.svg)](https://pypi.python.org/pypi/starlette)
[![Supported Python Version](https://img.shields.io/pypi/pyversions/starlette.svg?color=%2334D058)](https://pypi.org/project/starlette)

---

**Documentation**: <a href="https://www.starlette.io/" target="_blank">https://www.starlette.io</a>

**Source Code**: <a href="https://github.com/encode/starlette" target="_blank">https://github.com/encode/starlette</a>

---

# Starlette

Starlette is a lightweight [ASGI][asgi] framework/toolkit,
which is ideal for building async web services in Python.

It is production-ready, and gives you the following:

* A lightweight, low-complexity HTTP web framework.
* WebSocket support.
* In-process background tasks.
* Startup and shutdown events.
* Test client built on `httpx`.
* CORS, GZip, Static Files, Streaming responses.
* Session and Cookie support.
* 100% test coverage.
* 100% type annotated codebase.
* Few hard dependencies.
* Compatible with `asyncio` and `trio` backends.
* Great overall performance [against independent benchmarks][techempower].

## Installation

```shell
$ pip install starlette
```

You'll also want to install an ASGI server, such as [uvicorn](https://www.uvicorn.org/), [daphne](https://github.com/django/daphne/), or [hypercorn](https://hypercorn.readthedocs.io/en/latest/).

```shell
$ pip install uvicorn
```

## Example

```python title="example.py"
from starlette.applications import Starlette
from starlette.responses import JSONResponse
from starlette.routing import Route


async def homepage(request):
    return JSONResponse({'hello': 'world'})

routes = [
    Route("/", endpoint=homepage)
]

app = Starlette(debug=True, routes=routes)
```

Then run the application using Uvicorn:

```shell
$ uvicorn example:app
```

For a more complete example, see [encode/starlette-example](https://github.com/encode/starlette-example).

## Dependencies

Starlette only requires `anyio`, and the following are optional:

* [`httpx`][httpx] - Required if you want to use the `TestClient`.
* [`jinja2`][jinja2] - Required if you want to use `Jinja2Templates`.
* [`python-multipart`][python-multipart] - Required if you want to support form parsing, with `request.form()`.
* [`itsdangerous`][itsdangerous] - Required for `SessionMiddleware` support.
* [`pyyaml`][pyyaml] - Required for `SchemaGenerator` support.

You can install all of these with `pip install starlette[full]`.

## Framework or Toolkit

Starlette is designed to be used either as a complete framework, or as
an ASGI toolkit. You can use any of its components independently.

```python
from starlette.responses import PlainTextResponse


async def app(scope, receive, send):
    assert scope['type'] == 'http'
    response = PlainTextResponse('Hello, world!')
    await response(scope, receive, send)
```

Run the `app` application in `example.py`:

```shell
$ uvicorn example:app
INFO: Started server process [11509]
INFO: Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
```

Run uvicorn with `--reload` to enable auto-reloading on code changes.

## Modularity

The modularity that Starlette is designed on promotes building re-usable
components that can be shared between any ASGI framework. This should enable
an ecosystem of shared middleware and mountable applications.

The clean API separation also means it's easier to understand each component
in isolation.

---

<p align="center"><i>Starlette is <a href="https://github.com/encode/starlette/blob/master/LICENSE.md">BSD licensed</a> code.<br/>Designed & crafted with care.</i></br>&mdash; ⭐️ &mdash;</p>

[asgi]: https://asgi.readthedocs.io/en/latest/
[httpx]: https://www.python-httpx.org/
[jinja2]: https://jinja.palletsprojects.com/
[python-multipart]: https://multipart.fastapiexpert.com/
[itsdangerous]: https://itsdangerous.palletsprojects.com/
[sqlalchemy]: https://www.sqlalchemy.org
[pyyaml]: https://pyyaml.org/wiki/PyYAMLDocumentation
[techempower]: https://www.techempower.com/benchmarks/#hw=ph&test=fortune&l=zijzen-sf
