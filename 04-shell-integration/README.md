# 04 - Shell Integration and Configuration

**Time**: 45 minutes
**Level**: Intermediate

## Overview

Deep integration of GitHub Copilot CLI into your shell environment. Set up aliases, functions, and configurations for maximum productivity.

## Why Shell Integration?

Without integration:
```bash
gh copilot suggest "find large files"  # Too long to type repeatedly
```

With integration:
```bash
ghcs "find large files"  # Quick and efficient!
```

## Basic Aliases

### Bash/Zsh Configuration

Add to your `~/.bashrc` or `~/.zshrc`:

```bash
# GitHub Copilot CLI Aliases
alias ghcs='gh copilot suggest'
alias ghce='gh copilot explain'
```

Apply changes:
```bash
source ~/.bashrc  # or ~/.zshrc
```

### Fish Shell Configuration

Add to `~/.config/fish/config.fish`:

```fish
# GitHub Copilot CLI Aliases
alias ghcs='gh copilot suggest'
alias ghce='gh copilot explain'
```

Apply changes:
```fish
source ~/.config/fish/config.fish
```

### PowerShell Configuration

Add to your PowerShell profile:

```powershell
# GitHub Copilot CLI Aliases
Set-Alias -Name ghcs -Value 'gh copilot suggest'
Set-Alias -Name ghce -Value 'gh copilot explain'
```

## Enhanced Functions

### Bash/Zsh Functions

Add to `~/.bashrc` or `~/.zshrc`:

```bash
# Quick suggest with automatic execution confirmation
ghcsx() {
    local suggestion=$(gh copilot suggest "$*")
    echo "$suggestion"
    read -p "Execute this command? (y/n) " -n 1 -r
    echo
    if [[ $REPLY =~ ^[Yy]$ ]]; then
        eval "$suggestion"
    fi
}

# Explain last command from history
ghcel() {
    local last_command=$(fc -ln -1)
    gh copilot explain "$last_command"
}

# Quick git suggest
ghcsgit() {
    gh copilot suggest "git $*"
}

# Quick docker suggest
ghcsdocker() {
    gh copilot suggest "docker $*"
}

# Suggest with clipboard copy
ghcsc() {
    gh copilot suggest "$*" | tee >(pbcopy)  # macOS
    # or: | tee >(xclip -selection clipboard)  # Linux
    # or: | tee >(clip.exe)  # WSL
}
```

### Fish Functions

Create `~/.config/fish/functions/ghcsx.fish`:

```fish
function ghcsx
    set suggestion (gh copilot suggest $argv)
    echo $suggestion
    read -P "Execute this command? (y/n) " -n 1 confirm
    if test "$confirm" = "y"
        eval $suggestion
    end
end
```

## Complete Configuration Files

### Comprehensive Bash Configuration

See [configs/bashrc-copilot.sh](./configs/bashrc-copilot.sh) for a complete setup including:
- All basic aliases
- Advanced functions
- History integration
- Productivity shortcuts
- Error handling

### Comprehensive Zsh Configuration

See [configs/zshrc-copilot.sh](./configs/zshrc-copilot.sh) for Zsh-specific features:
- Oh-My-Zsh integration
- Completion support
- Custom key bindings
- Theme integration

### Fish Configuration

See [configs/config-copilot.fish](./configs/config-copilot.fish) for Fish shell setup.

## Advanced Integration

### History Integration

#### Suggest from History (Bash/Zsh)

```bash
# Add to ~/.bashrc or ~/.zshrc
ghcsh() {
    local pattern="$1"
    local cmd=$(history | grep "$pattern" | tail -1 | sed 's/^[ ]*[0-9]*[ ]*//')
    gh copilot explain "$cmd"
}
```

Usage:
```bash
ghcsh "docker"  # Explains last docker command from history
```

### Command Correction

```bash
# Suggest fix for last failed command
ghcsfix() {
    local last_cmd=$(fc -ln -1)
    echo "Last command: $last_cmd"
    echo "Getting suggestion to fix..."
    gh copilot suggest "fix this command: $last_cmd"
}
```

### Context-Aware Suggestions

```bash
# Suggest based on current directory
ghcspwd() {
    local dir_name=$(basename "$PWD")
    local file_type=$(ls | head -1 | sed 's/.*\.//')
    gh copilot suggest "$* in $dir_name directory with $file_type files"
}
```

## Key Bindings

### Bash/Zsh Key Bindings

Add to `~/.bashrc` or `~/.zshrc`:

```bash
# Ctrl+G: Open Copilot suggest with current line
bind '"\C-g": "gh copilot suggest \"\C-a\C-k\C-y\"\n"'

# Ctrl+X Ctrl+E: Explain current line
bind '"\C-x\C-e": "gh copilot explain \"\C-a\C-k\C-y\"\n"'
```

### Fish Key Bindings

Add to `~/.config/fish/config.fish`:

```fish
function fish_user_key_bindings
    # Ctrl+G: Copilot suggest
    bind \cg 'commandline -i "gh copilot suggest \""; commandline -f end-of-line; commandline -i "\""'

    # Ctrl+X Ctrl+E: Copilot explain
    bind \cx\ce 'set -l cmd (commandline); gh copilot explain "$cmd"'
end
```

## Environment Variables

```bash
# Add to shell config
export GITHUB_COPILOT_CLI_EDITOR="code"  # or vim, nano, etc.
export GITHUB_COPILOT_CLI_PAGER="less"
```

## Shell Completion

### Bash Completion

```bash
# Add to ~/.bashrc
eval "$(gh completion -s bash)"
```

### Zsh Completion

```bash
# Add to ~/.zshrc
eval "$(gh completion -s zsh)"
```

### Fish Completion

```fish
# Fish auto-generates completion
gh completion -s fish | source
```

## Integration with Other Tools

### FZF Integration

If you use [fzf](https://github.com/junegunn/fzf):

```bash
# Fuzzy search history and explain
ghcsfzf() {
    local cmd=$(history | fzf --tac --no-sort | sed 's/^[ ]*[0-9]*[ ]*//')
    if [ -n "$cmd" ]; then
        gh copilot explain "$cmd"
    fi
}
```

### Tmux Integration

Add to `~/.tmux.conf`:

```bash
# Prefix + g: Open Copilot suggest in new window
bind g new-window -n "copilot" "gh copilot suggest"
```

### Vim Integration

Add to `~/.vimrc`:

```vim
" Execute Copilot suggest on visual selection
vnoremap <leader>cs :<C-u>execute '!gh copilot suggest "' . @* . '"'<CR>
vnoremap <leader>ce :<C-u>execute '!gh copilot explain "' . @* . '"'<CR>
```

## Prompt Integration

### Show Copilot Status in Prompt

#### Bash Prompt

```bash
# Add to ~/.bashrc
COPILOT_INDICATOR="🤖"
PS1="\u@\h:\w $COPILOT_INDICATOR $ "
```

#### Zsh with Oh-My-Zsh

```bash
# Add to ~/.zshrc
PROMPT='%n@%h:%~ 🤖 $ '
```

#### Starship Prompt

Add to `~/.config/starship.toml`:

```toml
[character]
success_symbol = "[➜](bold green) 🤖"
error_symbol = "[➜](bold red) 🤖"
```

## Practical Workflow Shortcuts

### Quick Task Shortcuts

```bash
# Add to shell config

# Quick file operations
alias ghcsfind='gh copilot suggest "find"'
alias ghcsgrep='gh copilot suggest "search for"'

# Quick system operations
alias ghcsps='gh copilot suggest "show processes"'
alias ghcsdisk='gh copilot suggest "disk usage"'

# Quick git operations
alias ghcsgit='gh copilot suggest "git"'
alias ghcsglog='gh copilot suggest "git log"'

# Quick docker operations
alias ghcsdocker='gh copilot suggest "docker"'
alias ghcskube='gh copilot suggest "kubernetes"'
```

## Context Menu Integration (Linux)

### Nautilus Script

Create `~/.local/share/nautilus/scripts/copilot-suggest.sh`:

```bash
#!/bin/bash
zenity --entry --title="Copilot Suggest" --text="What do you want to do?" | xargs gh copilot suggest | zenity --text-info --width=800 --height=600
```

Make executable:
```bash
chmod +x ~/.local/share/nautilus/scripts/copilot-suggest.sh
```

## Configuration Management

### Modular Configuration

Create `~/.config/copilot-cli/`:

```bash
mkdir -p ~/.config/copilot-cli
```

Create separate files:
- `aliases.sh` - Basic aliases
- `functions.sh` - Shell functions
- `keybindings.sh` - Key bindings
- `completions.sh` - Completions

Source in your shell config:

```bash
# Add to ~/.bashrc or ~/.zshrc
for file in ~/.config/copilot-cli/*.sh; do
    source "$file"
done
```

### Version Control Your Config

```bash
cd ~/.config/copilot-cli
git init
git add .
git commit -m "Initial Copilot CLI config"
```

## Platform-Specific Tips

### macOS

```bash
# Use pbcopy for clipboard
ghcsc() {
    gh copilot suggest "$*" | pbcopy
    echo "Command copied to clipboard"
}

# Spotlight search integration (create app with Automator)
```

### Linux

```bash
# Use xclip for clipboard
ghcsc() {
    gh copilot suggest "$*" | xclip -selection clipboard
    echo "Command copied to clipboard"
}
```

### Windows (PowerShell)

```powershell
# Clipboard integration
function ghcsc {
    gh copilot suggest $args | Set-Clipboard
    Write-Host "Command copied to clipboard"
}
```

### WSL

```bash
# Use Windows clipboard
ghcsc() {
    gh copilot suggest "$*" | clip.exe
    echo "Command copied to clipboard"
}
```

## Testing Your Configuration

Run these tests after setup:

```bash
# Test aliases
ghcs "test"
ghce "ls -la"

# Test functions (if created)
ghcsx "echo hello"
ghcel  # Explain last command

# Test key bindings
# Press Ctrl+G and type something

# Test completion
gh copilot <TAB>
```

## Troubleshooting

### Aliases Not Working

```bash
# Check if alias exists
alias ghcs

# Reload configuration
source ~/.bashrc  # or ~/.zshrc

# Check for typos
cat ~/.bashrc | grep ghcs
```

### Functions Not Found

```bash
# Check if function defined
declare -f ghcsx

# Check shell type
echo $SHELL

# Ensure correct syntax for your shell
```

### Key Bindings Not Working

```bash
# Check current bindings
bind -P | grep copilot  # Bash
bindkey | grep copilot  # Zsh

# Reload configuration
source ~/.bashrc
```

## Example Configurations

Full example configurations are available in the `configs/` directory:

- [bashrc-copilot.sh](./configs/bashrc-copilot.sh) - Bash configuration
- [zshrc-copilot.sh](./configs/zshrc-copilot.sh) - Zsh configuration
- [config-copilot.fish](./configs/config-copilot.fish) - Fish configuration
- [profile-copilot.ps1](./configs/profile-copilot.ps1) - PowerShell configuration

## Next Steps

With shell integration set up:

1. [05-aliases-shortcuts](../05-aliases-shortcuts/) - Create custom productivity shortcuts
2. [06-workflows](../06-workflows/) - Apply to real-world workflows
3. [07-advanced](../07-advanced/) - Advanced power user techniques

---

**Estimated completion time**: 45 minutes
**Previous**: [03-explain-command](../03-explain-command/)
**Next**: [05-aliases-shortcuts](../05-aliases-shortcuts/)
