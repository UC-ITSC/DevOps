# Install NodeJS on new server

1. `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash` or if zsh is installed, `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | zsh`
1. Send `exit` command and re-ssh the server
1. `nvm install --lts` to install the newest long-term supported version of node (optionally `nvm install (version)` where version is the version of node you want installed)
1. `sudo ln -sf $(which npm) /usr/bin/npm`
1. `sudo ln -sf $(which node) /usr/bin/node`


# Important to note

Make sure that any existing NodeJS installations were done through NVM, not through the SUSE packages.

* `sudo yast`
* Go to Software > Software Management
* Search `nodejs`
* Ensure any node packages have a `[ ]` next to them, not a `[x]` or `[-]`
