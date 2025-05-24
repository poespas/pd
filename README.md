# Personal Drafts

_Some would say the acronym `pd` stands for poespas diaries_

A simple note-taking system with automatic synchronization and command-line tools.

## Features

- Command-line interface for quick note access
- Automatic file creation with date-based organization
- Git-based synchronization
- Bash and Zsh completion support
- Automatic hourly synchronization
- Configurable markdown editor support

## Installation

1. Clone or create the repository:
   ```bash
   git clone git@github.com:<yourname>/notes.git ~/notes
   ```

2. Install the scripts and services:
   ```bash
   # Copy scripts to /usr/local/bin
   sudo cp bin/* /usr/local/bin/
   sudo chmod +x /usr/local/bin/pd*

   # Install Bash completion
   sudo cp share/bash-completion/completions/pd /etc/bash_completion.d/

   # Install Zsh completion
   sudo mkdir -p /usr/local/share/zsh/site-functions
   sudo cp share/zsh/site-functions/_pd /usr/local/share/zsh/site-functions/

   # Install systemd service and timer
   sudo cp etc/systemd/system/personal-drafts-sync.* /etc/systemd/system/
   ```

3. Configure the systemd service user:
   ```bash
   # Replace the User directive in the service file with your username
   sudo sed -i "s/User=.*/User=$USER/" /etc/systemd/system/personal-drafts-sync.service
   ```

4. Enable and start the sync service:
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable --now personal-drafts-sync.service
   ```

## Usage

### Basic Commands

- `pd` - Open today's note or create it if it doesn't exist
- `pd <path>` - Open a specific note or create it if it doesn't exist
- `pd-pull` - Pull latest changes from the repository
- `pd-push` - Push local changes to the repository

### Environment Variables

- `PD_DIR` - Set a custom location for your notes (default: ~/notes)
- `PD_EDITOR` - Set your preferred markdown editor (default: $EDITOR or nano)

### Editor Configuration

You can use any editor by setting the `PD_EDITOR` environment variable. Some examples:

```bash
# Use VS Code
export PD_EDITOR="code"

# Use Vim
export PD_EDITOR="vim"

# Use Nano
export PD_EDITOR="nano"

# Use Apostrophe Flatpak
export PD_EDITOR="flatpak run org.gnome.gitlab.somas.Apostrophe"
```

Add the export to your shell configuration file (`.bashrc`, `.zshrc`, etc.) to make it permanent.

### File Organization

Notes are organized by date in the following structure:
```
notes/
└── day/
    └── YYYY/
        └── MM/
            └── DD.md
```

## Requirements

- Git
- Your preferred markdown editor
- Bash or Zsh
- systemd (for automatic sync)

## License

MIT

## Author

Poespas 
