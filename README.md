# knowledge-base

This is a set of best practices for development, deployment, etc.

## ssh

* Use [SSH keys](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/about-ssh) and avoid passwords.
* Use ed25519 keys for ease of sharing public key (and also because it is strong).
* Setup `.ssh/config` to avoid entering username, hostname, identity file, etc for ssh, rsync, scp, etc. [See example](https://gist.github.com/asdofindia/6ac769c1cee0459ba76db4b6b7d7962a)
* Keep a passphrase for your ssh key. [Add one if you didn't set one](https://codybonney.com/adding-passphrase-to-an-existing-private-key/)

## git

* Use [git feature branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow).
* Use [semantic commit messages](https://seesparkbox.com/foundry/semantic_commit_messages)
* [Commit Often, Perfect Later, Publish Once](https://sethrobertson.github.io/GitBestPractices/)
* If your branch diverges from the target branch (usually `master` or `main`), use `git rebase -i target-branch` to rebase your changes on the target branch. [Read a real life example](https://github.com/zhukov/webogram/blob/master/CONTRIBUTING.md)

## Deployment

### Source code

* When deploying private github repositories, use [deploy keys](https://docs.github.com/en/free-pro-team@latest/developers/overview/managing-deploy-keys)
* Alternatively use `rsync` to sync your local repository to the staging server

### pm2

* Avoid committing private data in ecosystem.config.js. If at all you do, use a [combination of .env and .gitignore](https://stackoverflow.com/a/59334216/589184) to make sure you don't commit sensitive data.
* [Generate startup script](https://pm2.keymetrics.io/docs/usage/startup/) to setup automatic restart on system reboot

### systemd

* Use `~/.config/user/systemd` to setup user units and start them with `systemctl --user start unitname`. Why run services as root unnecessarily?
