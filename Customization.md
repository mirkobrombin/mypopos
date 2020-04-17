# GNOME
The GNOME Workflow is perfect for me, normally there are few extensions and changes I make.

## Extensions
Here is the list of extensions I use:
- **Do Not Disturb** Activate or deactivate do not disturb mode (this should be removed with GNOME 3.36)
- **KStatusNotifierItem/AppIndicator Support** Adds KStatusNotifierItem support to the Shell
- **Workspace Scroll** Just scroll anywhere in the top panel to change the workspace.

## Theme
I'm using the beautiful official Pop theme by making some local changes to make it less space-destroying.

Create new file in `~.config/gtk-3.0/gtk.css` with content:

```css
headerbar {
    min-height: 28px;
    padding-top: 2px;
    padding-left: 2px;
    padding-right: 2px;
    padding-bottom: 2px;
}

headerbar entry,
headerbar spinbutton,
headerbar button,
headerbar separator {
    margin-top: 2px;
    margin-bottom: 2px;
}

.default-decoration {
    min-height: 0; 
    padding: 2px
}

.default-decoration .titlebutton {
    min-height: 26px;
    min-width: 26px;
}

```

and restart GNOME Shell `Alt+F2`, type `r`.

A lot smaller, right?

## Terminal/Zsh
As shell I am using ZSH with oh-my-zsh and Powerlevel10K.

### ZSH
First install `zsh`package:

```bash
apt install zsh
```

move to `oh-my-zsh`:

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Powerlevel10k
This is the theme I'm using:

```bash
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```
edit `ZSH_THEME` in `~.zshrc`:

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

and add below:

```bash
POWERLEVEL9K_MODE="nerdfont-complete"
ENABLE_CORRECTION="true"
```

#### Fonts
Download and install fonts:
- [Fura Mono Nerd Font](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/FiraMono/Regular/complete/Fura%20Mono%20Regular%20Nerd%20Font%20Complete.otf?raw=true)
- [Fira Mono](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/FiraMono/Regular/complete/Fira%20Mono%20Regular%20Nerd%20Font%20Complete.otf?raw=true)

### ZSH Plugins
I'm using these plugins:
- zsh-autosuggestions
- zsh-syntax-highlighting

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```

add plugins to `~.zshrc`:

```bash
plugins=(.. zsh-autosuggestions zsh-syntax-highlighting)
```