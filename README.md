# link-core-gems

A GitHub Action to link a local copy of the Bullet Train core gems into an application

In Bullet Train we use this to be able to properly test across repo boundaries when there are "join PRs" that require changes to be made in more than one repo.

## Usage

```yaml
- name: Link Core Gems
  uses: bullet-train-co/link-core-gems@v1
  with:
    application_dir: tmp/starter
    core_dir: tmp/core
```

## Action Inputs

| Name | Description | Default |
| --- | --- | --- |
| `application_dir` | The directory where your application and `Gemfile` live. | N/A |
| `local_gem_dir` | The directory where the local copy of the core gems live. | N/A |

## Action Outputs

None

TODO: Maybe we should output some things?

## Reference Example

Here is an example workflow. In this example we're checking out the `bullet-train-co/bullet_train` repository at `tmp/starter`, and then
linking the gem that hosts the workflow into the starter repo.

```yaml
name: CI

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  check_out_starter_repo:
    runs-on: ubuntu-latest
    name: Bullet Train Minitest

    steps:
      - name: Checkout This Repo
        uses: actions/checkout@v4

      - name: Checkout Bullet Train Core Repo
        uses: bullet-train-co/checkout-repo-with-matching-branch@v1
        with:
          target_dir: tmp/starter
          repository: bullet-train-co/bullet_train-core

      - name: Link Core Gems
        uses: bullet-train-co/link-local-gem@v1
        with:
          application_dir: .
          core_dir: tmp/core
```
