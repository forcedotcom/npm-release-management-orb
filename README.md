# npm-release-management-orb

[![CircleCI Build Status](https://circleci.com/gh/forcedotcom/npm-release-management-orb.svg?style=shield&circle-token=7a6dcc6c02f82515aec6533ed1c7253ef38e6e13 "CircleCI Build Status")](https://circleci.com/gh/forcedotcom/npm-release-management-orb) ![Orb Version Badge](https://badges.circleci.com/orbs/salesforce/npm-release-management.svg) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/forcedotcom/npm-release-management-orb/develop/LICENSE.txt)

- [npm-release-management-orb](#npm-release-management-orb)
  - [Usage](#usage)
  - [Note on Version Bumps and Changelogs](#note-on-version-bumps-and-changelogs)
    - [Overriding Version Bump](#overriding-version-bump)
  - [Using the SF-CLI-BOT for builds](#using-the-sf-cli-bot-for-builds)
  - [Environment Variable Reference](#environment-variable-reference)
  - [Variables for Change Case Management](#variables-for-change-case-management)
  - [How To Contribute](#how-to-contribute)

## Usage

Example use-cases are provided on the orb [registry page](https://circleci.com/orbs/registry/orb/salesforce/npm-release-management#usage-examples). Source for these examples can be found within the `src/examples` directory.

This orb is designed to make releasing npm packages straightforward and with as little configuration as possible. To get started you will need to:

1. Add the orb to your config.yml

   ```yml
   orbs:
     release-management: salesforce/npm-release-management@x.y.z
   ```

   NOTE: We recommend pinning the major version (e.g. `salesforce/npm-release-management@4`) so that you automatically receive all minor and patch updates.

2. Setup the required environment variables.

   Please see the [Environment Variable Reference](#environment-variable-reference) for the required environment variables.

3. Add a user key to your SSH Keys in CircleCi

   As part of the release job we create a new git tag based on the version in the package.json. This requires that you add a user key that has the permissions to push to github. To do this, simply go to the `SSH Keys` tab in the project settings and follow the directions for adding user keys. See [Using the SF-CLI-BOT for builds](#using-the-sf-cli-bot-for-builds) section on how to use our github bot for this.

4. Follow the [examples](https://circleci.com/orbs/registry/orb/salesforce/npm-release-management#usage-examples) for how to setup your config.yml

## Note on Version Bumps and Changelogs

Version bumps and changelogs are generated based on [conventional commit messages](https://www.conventionalcommits.org/en/v1.0.0/) (We use the [standard-version](https://github.com/conventional-changelog/standard-version) library to do this).

Your plugin will enforce this style of commit messages if you created your plugin using the [plugin-template](https://github.com/salesforcecli/plugin-template-sf/). If you did not using plugin-template, you will need to add the following to your `package.json`

```json
"devDependencies": {
 "@salesforce/dev-scripts": "^2",
}
```

And add these .husky files to your project: https://github.com/salesforcecli/plugin-template-sf/tree/main/.husky

And add a `commitlint.config.js` with the following:

```javascript
module.exports = { extends: ["@commitlint/config-conventional"] };
```

### Overriding Version Bump

The default behavior of the orb is to use `standard-version` to determine the next version number. However, you can specify the version you want published by updating the version field in the `package.json` yourself. If that version does not exist, the orb will publish it. Otherwise, it will fall back to using `standard-version`

## Using the SF-CLI-BOT for builds

We've created the [SF-CLI-BOT](https://github.com/SF-CLI-BOT) bot user in github to do any github related tasks in the build (creating releases, pushing tags, merges changes back to a specific branch, etc...). Having this bot ensure that the required tokens and keys do not belong to any one person.

If you would like to use this bot for your builds, contact the CLI team and we will add the ssh keys and github token to your CircleCI pipeline.

## Environment Variable Reference

| Variable                           | Description                                                        | Required                               |
| ---------------------------------- | ------------------------------------------------------------------ | -------------------------------------- |
| AWS_ACCESS_KEY_ID                  | access key id for aws s3                                           | Yes (only if signing packages)         |
| AWS_SECRET_ACCESS_KEY              | secret access key for aws s3                                       | Yes (only if signing packages)         |
| GH_USERNAME                        | github username that will be used for creating new tags            | No                                     |
| GH_EMAIL                           | github email that will be used for creating new tags               | No                                     |
| GH_TOKEN                           | github personal access token that will be used for release         | Yes (only if creating github releases) |
| NPM_TOKEN                          | auth token for publishing to npm                                   | Yes                                    |
| SALESFORCE_KEY                     | base64 encoded cert for plugin signing                             | Yes (only if signing packages)         |
| SFDX_DEVELOPER_TRUSTED_FINGERPRINT | fingerprint from developer.salesforce.com. Used for plugin signing | No                                     |
| NPM_REGISTRY                       | url to npm registry. Used for install and publish.                 | No                                     |

## Variables for Change Case Management

Please see the docs for the CLI commands here.  The orb derives the `--location` flag from Circle's built-in environment variables, but you must supply the other environment variables (either via a context or project-level settings).

## How To Contribute

We welcome [issues](https://github.com/forcedotcom/npm-release-management-orb/issues) to and [pull requests](https://github.com/forcedotcom/npm-release-management-orb/pulls) against this repository!

To publish a new production version:

- Create a PR to the `main` branch with your changes.
- When ready, squash and merge the PR into `main`. The merge commit should include `[semver:major|minor|patch|release|skip]` to indicate the type of release. If this is not included, then a new version will not be released.
- On merge, the release will be published to the orb registry automatically.

For further questions/comments about this or other orbs, visit the Orb Category of [CircleCI Discuss](https://discuss.circleci.com/c/orbs).

