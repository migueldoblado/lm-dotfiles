# Dotfiles

This repository contains all the dotfiles I use to customize my software development tools in OS X.

For the management of the files it uses [chezmoi](https://www.chezmoi.io/).
The secrets and other sensitive information is stored using [pass](https://www.passwordstore.org/)

## Prerequisites

- [chezmoi](https://www.chezmoi.io/)
- [pass](https://www.passwordstore.org/)
- [gnupg](https://gnupg.org/)
- [git](https://git-scm.com/)
- [Brew](https://brew.sh)
- My gpg keys

## How to start?

0. Install needed software
1. Import my gpg keys
2. Clone password store

    ```sh
    git@github.com:migueldoblado/$SECRETS.git ~/.password-store
    ```

3. Create `~/.config/chezmoi/chezmoi.toml` and fill it with the information

    ```toml
    [data.git]
    name = "<my name>"

    [data.git.work]
    email = "<work email>"
    signkey = "<my work gpg sign key>"
    # Used to clone my organization repositories
    company = "<company name>"
    # Used to clone my organization repositories
    repositories = "<work git repositories>" repositories
    ```

4. Finally apply

    ```sh
    chezmoi init --apply git@github.com:migueldoblado/dotfiles.git
    ```

## Included configuration

### Zsh shell

Drop-in files for `$PATH` management:

- [jenv](https://www.jenv.be/)
- [nodenv](https://github.com/nodenv/nodenv)
- [plenv](https://github.com/tokuhirom/plenv)
- [pyenv](https://github.com/pyenv/pyenv)
- `~/.local/bin`

### Git

- Set up globally my work information
- Enables company git hooks software only in specific dir

### Ssh

Basic ssh configuration with known hosts and rendering work sensitive hosts stored in the secret store.

### macOS system

- Installing automatically packages from a [Brewfile](https://github.com/migueldoblado/lm-dotfiles/blob/main/Brewfile)
- GNU coreutils and recent version of curl in `$PATH`
- Setup qtpass to find out git and gpg utlities from brew
- Enable uptimed and locate services
- Enable fingerprint for sudo

### iTerm2

- Install [Prezto](https://github.com/sorin-ionescu/prezto.git) and configuration
- Fonts powerline (https://github.com/powerline/fonts)

### vscode

- Set up projects managed by `alefragnani.project-manager` extension

### Third-party services setup

- Docker registries
- npm private registry

## Password store structure

This is the structure required to use the dotfiles. You can obtain it executing `pass`

```txt
Password Store
├── aws
│   ├── accountId -> password
│   └── region    -> passwoerd
├── docker
│   └── dockerRegistry -> password(token)
├── npm
│   └── github -> password(token)
└── ssh
    ├── hosts_list -> raw(configuration included in the file in private_dot_ssh/config.tmpl)
    └── keys
        ├── github -> raw(ssh key)
        └── id_rsa -> raw(ssh key)
```

## Acknowledgements

Big shoutout to [@ribugent](https://github.com/ribugent/dotfiles/) and [@albertvila](https://github.com/albertvila/dotfiles/) for their awesome dotfiles!
I totally borrowed a ton of ideas and configurations from their repositories. If you check out their dotfiles, you'll see what I mean. They're incredible!
