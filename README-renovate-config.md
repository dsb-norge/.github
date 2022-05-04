# Common configuration for Renovate

Renovate is an Open Source tool to automate:

- Detecting dependencies in a repository (Open Source and private/closed source)
- Checking if there are dependency updates
- Creating commits and Merge/Pull Requests to update dependencies
- Showing the release notes

Renovate is installed as a Github App in the github organization `dsb-norge`. It automates dependency updates for all
repositories it is given access to.

This repository contains `renovate-config.json` which contains common configuration for Renovate (DRY principle).

## Making changes
Changes to the config file in this repo takes immediate effect on all repositories referring to this common config.

To validate the config before commit, install the validator with `npm i -g renovate` and then check the config:

    cp renovate-config.json renovate.json && renovate-config-validator && rm renovate.json

### Need to configure a secret?
__DO NOT COMMIT PLAIN TEXT SECRETS TO THIS REPO!__

If you have to include a secret, encrypt it as described here:
https://docs.renovatebot.com/getting-started/private-packages/#encrypting-secrets

## Usage from other repos
When the Renovate github app gets access to a new repository, it will automatically create an "onboarding PR" which
refers to this central configuration. The PR contains a file `renovate.json` and its text body explains what
will be done when the PR is merged (e.g. how many pull requests will be created right after merge).

The generated file `renovate.json` should look like this (can be edited before merge):

    {
        "$schema": "https://docs.renovatebot.com/renovate-schema.json",
        "extends": [
            "local>dsb-norge/.github:renovate-config"
        ]
    }

The file can be edited (e.g. for overrides) before merge. To validate the config before commit, install the validator
with `npm i -g renovate` and then check the config with the command `renovate-config-validator`.

## References
- Documentation: https://docs.renovatebot.com/
- Configuration: https://docs.renovatebot.com/configuration-options/
- Encrypting secrets: https://docs.renovatebot.com/getting-started/private-packages/#encrypting-secrets
- How to use presets: https://docs.renovatebot.com/config-presets/#how-to-use-preset-configs