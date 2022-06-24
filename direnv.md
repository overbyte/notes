# Setup

```
sudo apt install direnv
```

add the following to `.profile`

```
eval "$(direnv hook bash)"
```

or to `.zshrc`

```
eval "$(direnv hook zsh)"
```

# Usage

In the dev directory add a new `.envrc` file with the environment variables

```
echo export GIT_AUTHOR_EMAIL=allandt.bik-elliot@pulselive.com > .envrc
```

Enable the directory as a parent (from the directory)

```
dotenv allow .
```
