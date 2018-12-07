---
weight: 500
title: Developer Documentation
---

# Developer Documentation

TODO: there's platform dev, and also a need for SBAC client dev in multiple languages.

## Platform Development

You will need to the following to get Chainspace running locally:

* [Go](https://golang.org/dl/) `1.11` or above. Earlier versions won't work
* [Docker](https://docs.docker.com/install/)

To test that Docker is working run `docker run hello-world` in a shell. Fix any errors before proceeding.

With these requirements met, run `make install`. This will build and install the `chainspace` binary as well as the `httptest` load generator. You can generate a new set of shards, start the nodes, and hit them with a load test.

See the help documentation (`chainspace -h` and `httptest -h`) for each binary.

### Committing

Please use Git Flow - work in feature branches, and send merge requests to `develop`.

#### Versioning

The version of the Chainspace application is set in the `VERSION` file found in the root of the project. Please update it when creating either a `release` or `hotfix` using the installed Git hooks mentioned above.

### Adding Dependencies

Dependency management is done via `dep`. To add a dependency, do the standard `dep ensure -add <dependency>`. We attempted to use `go mod` (and will go back to it when it stabilises). Right now `mod` breaks too many of our tools.

## Client Development

TODO: we have clients already for XYZ langs, more would be nice. Here's how. 
