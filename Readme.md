Deployment Scripts for [Share Space](https://github.com/alexjball/share-space/)
-------------------------------------------------------------------------------

This repository contains scripts for starting Share Space environments using Vagrant.


Setting Bash Variables
----------------------

Environments are defined in the [Vagrantfile](Vagrantfile).
The current environments can be selected by running one of the following:
  - `ENV=dev`
  - `ENV=staging`
  - `ENV=prod`

Environment-specific flags are expected in a file named `.${ENV}rc`.
An example that can be copied is [.example-envrc](.example-envrc).
Note that the `SHARE_SPACE_ENV` variable in the file will need to be changed.

The `PROJECT_REPO` variable must be set to the path of a local Share Space repo cloned from [here](https://github.com/alexjball/share-space/).
`PROJECT_REPO` can be set manually, or by running `source .envrc` in the cloned repo.


Vagrant Environment Commands
----------------------------

Bring up an environment:
`vagrant up ${ENV}`

Build and run the stack:
`vagrant provision $ENV --provision-with=stack-build,stack-up`

Stop the stack:
`vagrant provision $ENV --provision_with=stack-down`

On up, the environment clones the share space repo pointed to by `$PROJECT_REPO` and hands off
to the repo's install script. To edit the code in that clone, mount it with `./run-host mount-env $ENV`.
This will mount e.g. dev to ./dev using NFS.


Accessing Share Space
---------------------

Once the stack is running, you can access the Share Space with a local web browser.

Check [Vagrantfile](Vagrantfile) for the enviroment specified by ${ENV} for the corresponding IP address.
By default, the IP addresses will be set to:
  - dev: 172.28.128.10
  - staging: 172.28.128.12
  - prod: 172.28.128.11

Direct your broswer to ${IP}:3000 to access the Share Space.

The room server is ${IP}:3001 and the room code is specified in .${ENV}rc (defaults to `share-room` if .${ENV}rc is not found).
