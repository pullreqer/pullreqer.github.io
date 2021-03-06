# Installation

Installation steps,

1. Build the container 
2. Run the container
3. Build the client utilities
3. Client ssh setup 

## Step 1
Building the container.
---------
`pullreqr_container/mk_pullreqr_container`

## Step 2
Running the container.

`build/host_scripts/git_start.sh`

To stop it:

`build/host_scripts/git_stop.sh`

Optionally enable it to start via systemd
```
install -D -t ~/.config/systemd/user/ build/host_scripts/pullreqr.service
systemctl --user enable pullreqr.service --now
```

## Step 3
Client installation
---------

installation:
* install [rust](https://www.rust-lang.org/tools/install)
* `cargo install manifest-tool`
* install [git-repo](https://git-repo.info)

## Step 4
Client setup:
* Add keys to `~/.ssh/config`
```
cat <<"EOF" | envsubst '${PWD}' >>~/.ssh/config
Host localhost 
    HostName localhost 
    User git
    Port 2222
    IdentityFile ${PWD}/persistent/keys/user_key
EOF
```

Initial Testing
-------

Check that you can ssh into the container, and create a repository. Next We'll use this test repostory in [single repostory](./single-repo.md)

```
ssh localhost create_pr_repo test
```


