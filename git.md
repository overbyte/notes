# Using GIT

Some extra techniques for using GIT

# using git add -p

* `y` adds a block
* `n` ignores a block
* `q` ends this `-p` session
* `e` allows the dev to edit the current block (will give instructions when the
  dev does this)
  * delete lines beginning `+` to stop them being added to the commit
  * remove the `-` from lines to stop them being deleted

# switching keys

set up a `config` file in the `~/.ssh` folder:

```
Host git@github.com:darkest-star/site.git
  IdentityFile ~/.ssh/id_rsa_darkeststar
  IdentitiesOnly yes
# fix for virgin from https://stackoverflow.com/a/52817036/617603
Host github.com
   Hostname ssh.github.com
   Port 443
   PreferredAuthentications publickey
   IdentityFile ~/.ssh/id_rsa_overbyte
```

# switching users per project

use `git config user.email='my@email.com'` within a project to change the user
email for that project. If that email is associated to another account, the
commit will be credited to them

# clearing branches

use

```
git for-each-ref --format '%(refname:short)' refs/heads | grep -v "master\|main\|develop" | xargs git branch -D
```

notes:

* `for-each-ref` allows a loop over all of the branches
* `'%(refname:short)'` gives the terse branch name
* this is piped into `grep -v` (inverted search) to remove any references in the
  list (`master`, `main` or `develop` in this case)
* the result is piped into `xargs` to execute a delete on the git branch name
