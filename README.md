# Automatic setup of user identity on git clone

![Screenshot of a git clone](/about.png)

Whenever a repository is cloned, author information (`user.email`, `user.name`) is set according defined patterns. No longer pushing commits with your corporate email address by accident.
Optionally, also `user.signingkey` and `commit.gpgsign` can be configured independently. Corresponding variablels `gpgid` and `gpgsign` might be set or omitted.

## Installation

In case you do not already have a git template directory, create and register one:

```bash
mkdir -p ~/.config/git/templates/hooks
git config --global init.templatedir ~/.config/git/templates
```
Copy the file "post-checkout" to your registered git template directory:
```bash
git clone https://github.com/DrVanScott/git-clone-init.git /tmp/git-clone-init
cp /tmp/git-clone-init/post-checkout ~/.config/git/templates/hooks/
```
Copy a configuration template:
```bash
cp /tmp/git-clone-init/git-clone-init ~/.config/git/templates/
```
## Configuration

You can use the file `git-clone-init` as a starting point. Keep in mind to create a pattern for each protocol you are using, normally ssh and https.

Example:
```bash
case "$url" in
  *@github.com:*  ) email="my-public@email";    name="public name";;
  *//github.com/* ) email="my-public@email";    name="public name";;
  *@corp.com:*    ) email="my-corporate@email"; name="real name"; gpgid="GPG ID"; gpgsign="true/false";;
  *//corp.com/*   ) email="my-corporate@email"; name="real name"; gpgid="GPG ID"; gpgsign="true/false";;
esac
```

## Usage

Just do a normal "git clone" as usual.

## Known issues

git-clone-init won't work if you clone using "-n" or clone an empty repository.

