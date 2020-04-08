# Using packages in VIM

# Overview

# System used

* Linux Ubuntu 19.10
* Vim 8

# Setup

make directory structure if it doesn't exist

```
mkdir -p ~/.vim/pack/plugins/start
```

# Steps

* Clone vim plugin repo to start directory

```
cd ~/.vim/pack/plugins/start
git clone git@github.com:octol/vim-cpp-enhanced-highlight.git 
```

* Build the helpdocs in VIM

```
:helptags ALL
```

note this gives error: `E152: Cannot open /usr/share/vim/vim81/doc/tags for
writing`
This is normal and can be tested using the more verbose

```
:100verbose :helptags ALL
```

# Links

* https://vi.stackexchange.com/questions/9522/what-is-the-vim8-package-feature-and-how-should-i-use-it
  (note: the later answer by Klaus is very helpful - https://vi.stackexchange.com/a/18526)
* https://vi.stackexchange.com/questions/17210/generating-help-tags-for-packages-that-are-loaded-by-vim-8s-package-management/17213
