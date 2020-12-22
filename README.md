# knowledge-base

This is a set of best practices for development, deployment, etc.

## ssh

* Use ed25519 keys because for ease of sharing public key
* Setup `.ssh/config` to avoid entering username, hostname, identity file, etc
* Keep a passphrase for your ssh key

## git

* Use [git feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow).
* Use [semantic commit messages](https://seesparkbox.com/foundry/semantic_commit_messages)
* Commit often
* If your branch diverges from the target branch (usually `master` or `main`), use `git rebase -i target-branch` to rebase your changes on the target branch

## Deployment

### Source code

* When deploying private github repositories, use [deploy keys](https://docs.github.com/en/free-pro-team@latest/developers/overview/managing-deploy-keys)
* Alternatively use `rsync` to sync your local repository to the staging server

### pm2

* Avoid committing private data in ecosystem.config.js. If at all you do, use a [combination of .env and .gitignore](https://stackoverflow.com/a/59334216/589184) to make sure you don't commit sensitive data.
* [Generate startup script](https://pm2.keymetrics.io/docs/usage/startup/) to setup automatic restart on system reboot

### systemd

* Use `~/.config/user/systemd` to setup user units and start them with `systemctl --user start unitname`. Why run services as root unnecessarily?
