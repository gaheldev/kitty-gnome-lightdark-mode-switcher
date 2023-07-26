# Track Gnome's light/dark mode with Kitty 🌓

![export](https://github.com/ZelvStudio/kitty-gnome-lightdark-mode-switcher/assets/78329601/e5848341-2a87-49d6-bedc-b033aa4c87bf)

## 🛠️ Installation

```bash
git clone https://github.com/ZelvStudio/kitty-gnome-lightdark-mode-switcher.git
cd kitty-gnome-lightdark-mode-switcher
chmod +x install
./install
```

Uninstall by running ```./uninstall```


## 📝 Usage

### ➡️ Basic usage

If you want kitty to automatically change catppuccin theme to follow Gnome's light/dark mode run:
```bash
set-kitty-mode -m system
```

It is also possible to set light or dark mode manually with:
```bash
set-kitty-mode light   # stops tracking of Gnome's mode if active
set-kitty-mode dark    # stops tracking of Gnome's mode if active
set-kitty-mode system  # use current Gnome's mode without tracking
```

### ➡️ Use different themes

Currently the catpuccin themes are hardcoded in ```set-kitty-mode```. You can change them in code and run ```./install```.


### ➡️ Synchronize your text editor's mode with kitty

The current mode in use is tracked by ~/.local/state/TERMINAL_MODE which contains the value 'light' or 'dark'.

For example with neovim, you can add the following code to init.vim:
```vim
" use dark mode as default
let terminal_mode = 'dark'

" use the current kitty mode from the local state file TERMINAL_MODE if it exists
" replace <user> with your actual user name
if filereadable('/home/<user>/.local/state/TERMINAL_MODE')[0]
        let terminal_mode = readfile('/home/<user>/.local/state/TERMINAL_MODE')[0]
endif

if terminal_mode == 'light'
        colorscheme catppuccin-latte
else
        colorscheme catppuccin
endif
```


## 🧯 Debugging

Get the daemon status:
```bash
systemctl --user status kitty-gnome-mode-monitor.service
```

Enable the daemon to automatically run on startup:
```bash
systemctl --user enable kitty-gnome-mode-monitor.service
```

Start the daemon:
```bash
systemctl --user start kitty-gnome-mode-monitor.service
```

Stop the daemon:
```bash
kitty-gnome-mode-monitor -k
systemctl --user stop kitty-gnome-mode-monitor.service
```
