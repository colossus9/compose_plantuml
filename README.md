[![Build Status](https://travis-ci.org/funkwerk/compose_plantuml.svg)](https://travis-ci.org/funkwerk/compose_plantuml)
[![](https://badge.imagelayers.io/funkwerk/compose_plantuml.svg)](https://imagelayers.io/?images=funkwerk/compose_plantuml:latest 'funkwerk/compose_plantuml')
[![PyPi downloads](https://img.shields.io/pypi/dm/compose_plantuml.svg)](https://pypi.python.org/pypi/compose_plantuml/)
[![PyPi version](https://img.shields.io/pypi/v/compose_plantuml.svg)](https://pypi.python.org/pypi/compose_plantuml/)
[![Docker pulls](https://img.shields.io/docker/pulls/funkwerk/compose_plantuml.svg)](https://hub.docker.com/r/funkwerk/compose_plantuml/)

# compose_plantuml

Generate Plantuml graphs from docker-compose files

Note that version 2 as well as the legacy version is supported.

## Usage

### Via Python

Install it via:
`pip3 install compose_plantuml`

After that use it like:
`compose_plantuml --link-graph docker-compose.yml`

### Via Docker

Use it like:
`cat docker-compose.yml | docker run -i funkwerk/compose_plantuml --link-graph`

For SVG Output, just call:

`cat docker-compose.yml | docker run -i funkwerk/compose_plantuml --link-graph | docker run -i think/plantuml > output.svg`

For PNG Output, just call:

`cat docker-compose.yml | docker run -i funkwerk/compose_plantuml --link-graph | docker run -i think/plantuml -tpng > output.png`

## Link Graph

Link Graphs provide an overview over docker-compose services.

Consider the following docker-compose.yml

```
version: '2'
services:
  first:
    links:
      - second
  second: {}
```

When calling 'compose_plantuml docker-compose.yml' it will generate the following link graph:

```
[first]
[second]
[first] --> [second]
```

Rendered it looks like:

<img src="https://cdn.rawgit.com/funkwerk/compose_plantuml/master/img/link_graph.svg">

## Boundaries

Boundaries visualize the external boundaries a system has.

Consider the following docker-compose.yml

```
version: '2'
services:
  service:
    ports:
      - 8080:80
```

When calling 'compose_plantuml --boundaries docker-compose.yml' it will generate the following plantuml:

```
rectangle system {
  [service]
}
[service] --> 8080 : 80
```

Rendered it looks like:

<img src="https://cdn.rawgit.com/funkwerk/compose_plantuml/master/img/boundaries.svg">

## Related Links

 - draw compose
   - https://github.com/Alexis-benoist/draw-compose
   - generates dot graphs from docker-compose files
   - currently just supports docker-compose version 1
   - does not read from stdin, so is not easy useable as docker container
