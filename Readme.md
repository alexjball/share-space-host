Run Share Space environments using Vagrant.

Environments are defined in the `Vagrantfile`, and environment-specific flags are set in `.${ENV}rc`.

Bring up an environment: `vagrant up $ENV`

Build and run the stack: `vagrant provision $ENV --provision-with=stack-build,stack-up`

Stop the stack: `vagrant provision $ENV --provision_with=stack-down`

On up, the environment clones the share space repo pointed to by `$PROJECT_REPO` and hands off
to the repo's install script. To edit the code in that clone, mount it with `./run-host mount-env $ENV`.
This will mount e.g. dev to ./dev using NFS.
