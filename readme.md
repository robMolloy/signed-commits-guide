Create the public key

```
gpg --full-generate-key
```

And check that it is created with

```
gpg --list-secret-keys --keyid-format=long
```

which gives the format

```
sec   rsa3072/AAABBBCCCCDDDDE 2025-05-13 [SC]
      EEEEEEFFFFFGGGGGHHHHHIIIIJJJJKKKKKLLLLLM
uid                 [ultimate] Jo Bloggs <jo.bloggs@nttdata.com>
ssb   rsa3072/NNNNNOOOOOOOPPPP 2025-05-13 [E]
```

use the key id AAABBBCCCCDDDDE and add to the git config and other keys
```
git config user.signingkey AAABBBCCCCDDDDE
git config --global user.signingkey AAABBBCCCCDDDDE

git config commit.gpgsign true
git config --global commit.gpgsign true

git config user.name "Jo Bloggs"
git config --global user.name "Jo Bloggs"

git config user.email "jo.bloggs@nttdata.com"
git config --global user.email "jo.bloggs@nttdata.com"
```

get the gpg key
```
gpg --armor --export jo.bloggs@nttdata.com
```

the output looks like

```
-----BEGIN PGP PUBLIC KEY BLOCK-----
...
-----END PGP PUBLIC KEY BLOCK-----
```

Add this output to github using your browser by going to settings then to gpg keys

You should now be able to sign commits with the following command
```
git commit -S -m "commit message"
```

If this works please push your changes to confirm that it all works - branch rules should prevent you from pushing to main without a signed commit.

Troubleshooting:
You may need the following command to be able to sign commits
```
export GPG_TTY=$(tty)
```
