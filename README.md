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

## Development

### General

* Use meaningful names for variables, methods, files, and everything. As a corollary, do not use acronyms, single letters, etc.
* Write code such that you won't have to add comments. Abstract complicated logic into a function and give it an intuitive name. Don't have surprises in functions. A function named `sum` should only do sum. Use comments to explain reasons outside of code. For example `// we've to do this first because of performance issues`
* Don't mix concerns. Separate concerns. API/database calls should never be in the same file as UI/business logic code.

### Java

* Newer java versions are significantly more powerful than older Java versions. Use them. [This ain't your parents' Java](https://www.youtube.com/watch?v=hx5sloAYW-s)
* [Modern web development in Java](https://asd.learnlearn.in/java-web/) has grown by leaps and bounds. Use JAX-RS, etc. Use frameworks like Spring/Quarkus/Micronaut where possible. [Here's a starter repository for jersey + weld](github.com/Metastring/jaxrs-starter)
* Use [dependency injection and inversion of control](https://martinfowler.com/articles/injection.html).

### React

* Avoid using context. ([Official warning](https://reactjs.org/docs/context.html#before-you-use-context))
* Use [custom hooks](https://reactjs.org/docs/hooks-custom.html) for encapsulating logic.
* Keep your UI components clean of business logic.
* Recommended libraries:
  * [react-query](https://react-query.tanstack.com/) for network requests
  * [chakra-ui](https://chakra-ui.com/) for UI components
