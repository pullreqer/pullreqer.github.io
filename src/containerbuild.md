
### Containers build process
Here is a general overview of the container building process.
There are 3 containers

*TODO* This could use a lot more explanation.


1. build_env
2. build
3. run

#### build_env
* Install development tools for git
* Install development tools for rust

#### build
* Compile git & pull_req_hook

#### run
* Generate user keys & account to push to, using git-shell.
* Copy *public* key into a mounted volume.
* installs git and the hook, and ssh daemon.
* Configures the ssh daemon