# npm-release-management-orb
[![CircleCI Build Status](https://circleci.com/gh/forcedotcom/npm-release-management-orb.svg?style=shield&circle-token=7a6dcc6c02f82515aec6533ed1c7253ef38e6e13 "CircleCI Build Status")](https://circleci.com/gh/forcedotcom/npm-release-management-orb) [![CircleCI Orb Version](https://img.shields.io/badge/endpoint.svg?url=https://badges.circleci.io/orb/salesforce/npm-release-management)](https://circleci.com/orbs/registry/orb/salesforce/npm-release-management)

## Usage

Example use-cases are provided on the orb [registry page](https://circleci.com/orbs/registry/orb/salesforce/npm-release-management#usage-examples). Source for these examples can be found within the `src/examples` directory.

## How To Contribute

We welcome [issues](https://github.com/forcedotcom/npm-release-management-orb/issues) to and [pull requests](https://github.com/forcedotcom/npm-release-management-orb/pulls) against this repository!

To publish a new production version:
* Create a PR to the `develop` branch with your changes. This will act as a "staging" branch.
* When ready to publish a new production version, create a PR from `develop` to `master`. The Git Subject should include `[semver:major|minor|patch|release|skip]` to indicate the type of release.
* On merge, the release will be published to the orb registry automatically.

For further questions/comments about this or other orbs, visit the Orb Category of [CircleCI Discuss](https://discuss.circleci.com/c/orbs).
