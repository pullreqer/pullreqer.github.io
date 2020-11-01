# Notice

Beta quality stuff, which hasn't seen production use, and is pretty hackily thrown together.

# Introduction & Installation

Pull Reqer is grab bag of tools, both client and server side
for setting implementing a pull request like feature usable on the command line
and conversion of `repo` manifests to locally hosted repositories.

**Important** this project works with the alibaba `git-repo` client **not** the google `repo-tool`.


After setting everything up you'll have a locally hosted repository to which you can make pull requests to.
usable either the normal git checkouts, or a git-repo multi-repository manifest.

Most of this is driven by the alibaba `git-repo` client utility
 
Pull Reqer provides the needed hooks, and some utilities for converting git-repo checkouts into locally
usable variants.
 

