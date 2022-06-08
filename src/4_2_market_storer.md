# Market Storer

The purpose of product "Market Storer" is to receive market data from `Market` through SBE ZMQ and put them into influxdb2. The project is actually very simple and short go scripts.

- `/main.go` contains the logic
- `/parse.go` contains some generic parsing logic
- `/env_var.go` contains the configurable env var
- `/market_definition` is the git submodule for fixing the version of sbe encoding

Thats all for the source code of this project.

For your curiousity, these are the rests.

- `/proper_market_api/` is the generated code from `market_definition`. There are some capitalization missing and does not match with golang "bigger capital = public, smaller capital = private" syntax rules, and require some manual fixings. Otherwise it is most likely ignorable.

- `/Dockerfile` generate a container image

- `/k8s.yaml` contains yaml scripts that make this a pod inside k8s.

- `/goczmq/` anchored a specific commit on the goczmq github repository. This is because there was a bug preventing this binary to compile that was fixed at newest commit but not newest release. Could get rid of this once the change is pushed into a versioned release.