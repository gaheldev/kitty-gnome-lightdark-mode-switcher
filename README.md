# Track Gnome's light/dark mode with Kitty

## Installation

```bash
git clone ...
cd kitty-gnome-lightdark-mode-switcher
chmod +x install
./install
```

Uninstall by running ```./uninstall```


## Usage

### Basic usage

If you want kitty to automatically change catppuccin theme to follow Gnome's light/dark theme run:
```bash
set-kitty-theme -m system
```

It is also possible to set light or dark theme manually with:
```bash
set-kitty-theme light   # stops tracking of Gnome's theme if active
set-kitty-theme dark    # stops tracking of Gnome's theme if active
set-kitty-theme system  # use current Gnome's theme without tracking
```

### Use different themes

Currently the catpuccin themes are hardcoded in ```set-kitty-theme```. You can change them in code and run ```./install```.


### Synchronize your text editor's theme with kitty

The current theme in use is tracked by ~/.local/state/TERMINAL_THEME which contains the value 'light' or 'dark'.

For example with neovim, you can add the following code to init.vim:
```vim
" use dark theme as default
let terminal_theme = 'dark'

" use the current kitty theme from the local state file TERMINAL_THEME if it exists
" replace <user> with your actual user name
if filereadable('/home/<user>/.local/state/TERMINAL_THEME')[0]
        let terminal_theme = readfile('/home/<user>/.local/state/TERMINAL_THEME')[0]
endif

if terminal_theme == 'light'
        colorscheme catppuccin-latte
else
        colorscheme catppuccin
endif
```


## Debugging

Get the daemon status:
```bash
systemctl --user status kitty-gnome-theme-monitor.service
```

Enable the daemon to automatically run on startup:
```bash
systemctl --user enable kitty-gnome-theme-monitor.service
```

Start the daemon:
```bash
systemctl --user start kitty-gnome-theme-monitor.service
```

Stop the daemon:
```bash
kitty-gnome-theme-monitor -k
systemctl --user stop kitty-gnome-theme-monitor.service
```
