# Automatic setup of user identity on git clone

![Screenshot of a git clone](/about.png)

Whenever a repository is cloned, author information (user.email, user.name) is set according defined patterns. No longer pushing commits with your corporate email address by accident.

## Installation

In case you do not already have a git template directory, create and register one:

```bash
mkdir -p ~/.git-templates/hooks
git config --global init.templatedir ~/.git-templates
```
Copy the file "post-checkout" to your registered git template directory:
```bash
cp post-checkout ~/.git-templates/hooks/
```

## Configuration

You can use the file ".git-clone-init" as a starting point. Keep in mind to create a pattern for each protokoll you are using, normally ssh and https.

Example:
```bash
case "$url" in
  *@github.com:*  ) email="my-public@email";    name="public name";;
  *//github.com/* ) email="my-public@email";    name="public name";;
  *@corp.com:*    ) email="my-corporate@email"; name="real name";;
  *//corp.com/*   ) email="my-corporate@email"; name="real name";;
esac
```

## Usage

Just do a normal "git clone" as usual.

## Known issues

git-clone-init won't work if you clone using "-n".

