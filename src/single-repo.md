# Single repository usage

Now that the server and client are built and running,
create a test repository, and commit to it, and make a pull request.

* Client setup for a single repository


[Previously](./install.md) we created an empty repository on the server which we can push to, before we can make a pull request, we need to add an initial commit.

```
git init
cd test
echo "foo" >README.md
git add README.md
git commit -m "An initial commit"
git remote add origin ssh://localhost/~/test.git
git push --set-upstream origin main
```

Now create a pull request:
```
echo "test 1" >>README.md
git add README.md
git commit -m "a test pull-request"
git pr
```

This should launch your editor, after filling in the form and exiting you should see:

```
$ git pr
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Writing objects: 100% (3/3), 252 bytes | 252.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To ssh://localhost:2222/~/test.git
 * [new branch]      master -> for/master/pr1

----------------------------------------------------------------------
```

Check out the pull-request to a local branch:
```
git fetch origin for/master/pr1:pr1
git checkout pr1
```

