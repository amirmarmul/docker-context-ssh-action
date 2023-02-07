[![GitHub release](https://img.shields.io/github/v/release/amirmarmul/docker-context-ssh-action.svg?style=flat-square)](https://github.com/amirmarmul/docker-context-ssh-action/releases/latest)
[![GitHub marketplace](https://img.shields.io/badge/marketplace-docker--context--over--ssh-blue?logo=github&style=flat-square)](https://github.com/marketplace/actions/docker-context-over-ssh)

## About 

[Github Action](https://github.com/features/actions) for creating docker context over SSH authentication.

## Input variables 

See [action.yml](./action.yml) for more detailed information.

* `ssh-host` - ssh host 
* `ssh-port` - ssh port, default 22
* `ssh-username` - ssh username
* `ssh-private-key` - content of ssh private key. ex raw content of ~/.ssh/id_rsa
* `ssh-passphrase` - passphrase for ssh private key. no default.
* `ssh-socket` - ssh socket, default /tmp/ssh-auth.sock
* `context-name` - name of docker context. default: remote
* `context-use` - indicate which this context is set as docker current context. default: false

## Usage 

```yaml
on: [push]

jobs:
  docker_context_over_ssh_job: 
    runs-on: ubuntu-latest
    steps:
      - name: Set up docker context over SSH authentication
        uses: amirmarmul/docker-context-ssh-action@v1
        with:
          ssh-host: ${{ secrets.SSH_HOST }}
          ssh-username: ${{ secrets.SSH_USERNAME }}
          ssh-private-key: ${{ secrets.SSH_PRIVATE_KEY }}
          ssh-passphrase: ${{ secrets.SSH_PASSPHRASE }}
      
      - name: Inspect docker context  
        run: docker context ls -q
```