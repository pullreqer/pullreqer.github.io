# Multi repository

After successfully testing everything works with a single repository
we'll mirror a `repo` manifest, and set up a mirror so that our pull-requests will go our local system.

It is best to do this on a repository with *no review url*  to ensure that you aren't accidentally sending bogus pull-requests upstream.

-----

mirroring a multi-repository `repo` checkout

Has a few steps,
1. Setting up a local mirror 
   * Download the repositories `git repo` using the `--mirror` flag.
   * Create repositories for these on our local server
   * Push the downloaded repositories to our local server
2. Using the local mirror with `git repo`
   * Repo init the repository again *without* the `--mirror` flag.
   * Make a modified manifest, putting that in the `local_manifests` directory.
   * Use `git repo sync` to make a clone which fetches and pulls from out local repository.
3. Using `git repo upload`, to make changes
`manifest-tool` is a tool which helps with the above steps *2* and *4*.

# Configuring manifest-tool for step 1.

Add the following to your `~/.config/manifest-tool/projects/default.env`
```
ssh localhost create_pr_repo ${remote_name}/${project_name} </dev/null
GIT_DIR="$(basename -s .git ${project_name}).git" git remote add mine ssh://localhost/~/${remote_name}/${project_name}
GIT_DIR="$(basename -s .git ${project_name}).git" git push mine --mirror
```

Rather than performing a checkout into a work tree, `--mirror` will just download the repositories.  We use manifest-tool to:
* Create a repo for the local mirror
* Add a remote the cloned repository `git repo`
* Push the repository to our mirror.

We want to run this for every *project* in the manifest.

# Step 1

Setting up a local mirror:
```
mkdir mirror
cd mirror
git repo init -u https://example.com/foo/example.git --mirror
git repo sync
manifest-tool --projects | sh
```


# Configuring manifest-tool for step 2.

  Add the following to `~/.config/manifest-tool/convert/default.env`
```
push_url=ssh://localhost/~git/${remote_name}/
review_url=ssh://localhost/~/
fetch_url=ssh://localhost/~git/${remote_name}/
review_proto=agit
```

Unlike `--projects` which just emitted a shell script,
the `--convert` flag, reads the manifest performs substitutions,
and then writes a new manifest to the `local_manifests` directory.

We run manifest tool in between `git repo init`, and `git repo sync`.  In the process `git repo sync` should now be checking out from and pushing to localhost.

# Step 2

Using the local mirror with `git repo`:

```
mkdir work
cd work
git repo init -u https://example.com/foo/example.git
manifest-tool --convert
git repo sync
```

# Step 3
 Using `git repo upload`, to make changes:

```
cd test/
git repo start pull-test
echo "test" > test.txt
git add test.txt
git commit -m "test commit for multi-repo"
git repo upload
```