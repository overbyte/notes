# rsync

## sync files from old PC to a target PC

- setup ssh (which you’ll need for git anyway)

```bash
# generate your new ssh key on your target PC
ssh-keygen
# copy your public key id_rsa.pub from ~/.ssh on your target PC to ~/ on your old PC
# and on your old PC use
touch ~/.ssh/authorized_keys                    # ensure authorized_keys is there
cat ~./id_ed25519.pub >> ~/.ssh/authorized_keys # add the public key to the list of authorized keys
```

- test the ssh connection from the target PC

```bash
ssh <username>@<ip-of-old-PC>
# you should be in the home dir of the old PC
# when you're done poking around
exit
```

- and then on the target PC run

```bash
rsync -chavzP <ip-of-old-pc>/ ~/
```

NOTE: (remember the trailing / because otherwise it will sync the `input-folder` into the `output-folder` and you'll get `./output-folder/input-folder` rather that `./output-folder/…<input-folder-contents>`)
