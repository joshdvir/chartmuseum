# Chartmuseum.cr

[![Docs](https://img.shields.io/badge/docs-available-brightgreen.svg)](https://devops-israel.github.io/chartmuseum.cr/)
[![GitHub release](https://img.shields.io/github/release/devops-israel/chartmuseum.cr.svg)](https://github.com/devops-israel/chartmuseum.cr/releases)
[![Build Status](https://travis-ci.org/devops-israel/chartmuseum.cr.svg?branch=master)](https://travis-ci.org/devops-israel/chartmuseum.cr)


[Chartmuseum.cr](https://github.com/devops-israel/chartmuseum.cr) is a [Chartmuseum API](https://chartmuseum.com/) wrapper writes with [Crystal](http://crystal-lang.org/) Language.

Inspired from [gitlab](https://github.com/icyleaf/gitlab.cr).

## Installation

1. Add the dependency to your `shard.yml`:

```yaml
dependencies:
  chartmuseum:
    github: devops-israel/chartmuseum.cr
```

2. Run `shards install`

## Usage

```crystal
require "chartmuseum"

# configuration
endpoint = "https://charts.example.com" # No tailing forward slash
username = "<username>"
password = "<password>"

# initialize a new client with user and password for basic auth
chartmuseum_client = Chartmuseum.client(endpoint, username, password)
# => #<Chartmuseum::Client:0x101653f20 @endpoint="https://charts.example.com", @username="xxx", @password="xxx>

# server health
chartmuseum_client.available?
# true

# get all charts and their versions
charts = chartmuseum_client.charts
# => {"application-1":[{"name":"application-1","version":"6410","description":"application-1 Chart","apiVersion":"v1","appVersion":"6410","urls":["charts/application-1-6410.tgz"],"created":"2019-01-27T08:43:46Z","digest":"10abe509f97a8ca20d7be48459cc3cd5190a9800783744b751cb98e98263ed09"},...]}

# get specific chart and its versions
charts = chartmuseum_client.chart("application-1")
# => [{"name":"application-1","version":"6410","description":"application-1 Chart","apiVersion":"v1","appVersion":"6410","urls":["charts/application-1-6410.tgz"],"created":"2019-01-27T08:43:46Z","digest":"10abe509f97a8ca20d7be48459cc3cd5190a9800783744b751cb98e98263ed09"},...]

# get specific version of a chart
charts = chartmuseum_client.version("application-1", "6412")
# => {"name":"application-1","version":"6412","description":"application-1 Chart","apiVersion":"v1","appVersion":"6412","urls":["charts/application-1-6412.tgz"],"created":"2019-01-27T08:43:46Z","digest":"10abe509f97a8ca20d7be48459cc3cd5190a9800783744b751cb98e98263ed09"}
```

## Implemented API

#### Completed

##### Chart Manipulation
- `GET /api/charts` - list all charts
- `GET /api/charts/[name]` - list all versions of a chart
- `GET /api/charts/[name]/[version]` - describe a chart version

### Server Info
- `GET /health` - returns 200 OK

#### TODO:

##### Chart Manipulation
- `POST /api/charts` - upload a new chart version
- `POST /api/prov` - upload a new provenance file
- `DELETE /api/charts/[name]/[version]` - delete a chart version (and corresponding provenance file)

## Development

### Prerequisites

* [Docker](https://www.docker.com/products/docker-desktop)

### Commands

* From inside the root of the project run `docker-compose up`
* The container is configured to run tests every time a file is changed so just start developing.

## Contributing

1. Fork it (https://github.com/devops-israel/chartmuseum.cr/fork)
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request

## Contributors

- [Josh Dvir](https://github.com/devops-israel) - creator and maintainer

## License

[MIT License](https://github.com/devops-israel/chartmuseum.cr/blob/master/LICENSE) © devops-israel