# Checkpointz

A beacon chain aware Checkpoint Sync provider.

Checkpointz exists to reduce the operational burden of running a checkpoint sync endpoint. Checkpointz only serves a subset of the [beacon APIs](https://ethereum.github.io/beacon-APIs/#/) that are required for all consensus clients to checkpoint sync.

> :warning: **Checkpointz is still in heavy development** - use with caution

## Features
- Resource reduction
  - Adds HTTP cache-control headers depending on the content
- DOS protection
  - Never routes an incoming request directly to an upstream beacon node
  - Caches all requests
- Support for multiple upstream beacon nodes
  - Only serves a new finalized epoch once 50%+ of upstream beacon nodes agree
- Extensive Prometheus metrics

## Future features
- Web UI
  - Public-facing: shows information about the state of the provider, along with all state roots that the instance is aware of for cross-checking against instances.
  - Internal: shows information about the internal instance, health checks, etc.

## What is checkpoint sync?
Checkpoint sync is an operation that lets fresh beacon nodes jump to the head of the chain by fetching the state from a trusted & synced beacon node. 

More info: https://notes.ethereum.org/sWeLohipS9GdgMugYn9VkQ
## Usage
Checkpointz requires a config file. An example file can be found [here](https://github.com/samcm/checkpointz/blob/master/example_config.yaml).

```
Checkpoint sync provider for Ethereum beacon nodes

Usage:
  checkpointz [flags]

Flags:
      --config string   config file (default is config.yaml) (default "config.yaml")
  -h, --help            help for checkpointz
```
## Getting Started

### Docker
Available as a docker image at `samcm/checkpointz`

**Quick start**
```
docker run -d -it --name checkpointz -v $HOST_DIR_CHANGE_ME/config.yaml:/opt/exporter/config.yaml -p 9090:9090 -p 5555:5555 -it samcm/checkpointz --config /opt/exporter/config.yaml
```


**Building yourself (requires Go)**

1. Clone the repo
   ```sh
   go get github.com/samcm/checkpointz
   ```
2. Change directories
   ```sh
   cd ./checkpointz
   ```
3. Build the binary
   ```sh  
    go build -o checkpointz .
   ```
4. Run the exporter
   ```sh  
    ./checkpointz
   ```

## Contributing

Contributions are greatly appreciated! Pull requests will be reviewed and merged promptly if you're interested in improving the exporter! 

1. Fork the project
2. Create your feature branch:
    - `git checkout -b feat/new-metric-profit`
3. Commit your changes:
    - `git commit -m 'feat(profit): Export new metric: profit`
4. Push to the branch:
    -`git push origin feat/new-metric-profit`
5. Open a pull request

## Contact

Sam - [@samcmau](https://twitter.com/samcmau)
