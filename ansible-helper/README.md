# Custom Python Docker Image

This Docker image is derived from the official [cimg/python:3.11.11-node](https://hub.docker.com/r/cimg/python/) image. 
It includes additional tools and dependencies such as [Poetry](https://python-poetry.org/) for managing Python packages, and `ansible` for automation tasks.
tf_env 3.0.0 for activating terraform exists, but in not-activated state.

## Features

- **Base Image**: Derived from `cimg/python:3.11.11-node`, which provides Python 3.11 with Node.js support.
- **Poetry**: Installed using the official installation script to manage Python dependencies.
- **Ansible**: Included for configuration management, deployment, and task automation.

## Usage

### Building the Image

To build use:

```sh
make build
```

To push:

```sh
make push
```

### Using in circleci

In your `.circleci/config.yml` file, you can follow ideas from examples below:

```yaml
defaults: &defaults
  docker:
    - image: softasap/circleci-helper-images:cimg_py311_ansible_latest
  environment:
    ANSIBLE_HOST_KEY_CHECKING: False
    BOX_DEPLOY_USER: ubuntu
    ANSIBLE_VAULT_IDENTITY_LIST: "/tmp/vault.txt"
```
