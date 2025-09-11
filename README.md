# Debian-WSL

## Debian install

Microsoft recently updated their available Debian for WSL image to Debian 13 (Trixie).

```powershell
wsl --install Debian
```

If you eventually want that to be your default for WSL:
```powershell
wsl --set-default Debian
```

## Windows Terminal and Alacritty

Windows Terminal works pretty well with a couple tweaks.  Alacritty is also a great terminal.  

### For Windows Terminal (should be pre-installed on Windows 11:
1. Download an install a [NerdFont](https://www.nerdfonts.com/) on your Windows system<br>
   A. [MesloLG Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/Meslo.zip) is an easy choice, but use whatever you like.<br>
   B. [FiraCode Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/FiraCode.zip) is also a great choice.
3. Change your settings for your Debian -> Appearance to fit the theme and your newly installed MesloLG font. I'm fond of the One Half Dark theme.<br>
    <img width="440" height="240" alt="image" src="https://github.com/user-attachments/assets/a4bb11ce-a4db-49da-b734-1cfdbe125285" />
4. Change the icon for your Debian install to something better than what Microsoft provided.<br>
    <img width="64" height="64" alt="image" src="https://github.com/user-attachments/assets/723c63da-56b3-4693-be9f-2f0687878129" /> <br>
    <img width="452" height="97" alt="image" src="https://github.com/user-attachments/assets/ccdd2df1-2061-459f-b1eb-e7fe69a7d67a" />

### For Alacritty:
1. Install Alacritty<br>
   A. By downloading an install from their [website](https://alacritty.org/) <br>
   B. via winget (my preference), e.g. <br>
       ```powershell
       winget install Alacritty.Alacritty
       ```
2. Download an install a [NerdFont](https://www.nerdfonts.com/) on your Windows system, same as you would do for Windows Terminal<br>
   A. [MesloLG Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/Meslo.zip) is an easy choice, but use whatever you like.<br>
   B. [FiraCode Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/FiraCode.zip) is also a great choice.
4. Open this location for the config files: ```%APPDATA%\alacritty\```
5. Download my [onehalfdark.toml](https://github.com/unconfused/Debian-WSL/blob/main/onehalfdark.toml) file, if you want that style.  Put it with the other config files.
6. Edit your alacritty.toml file. Add [my alacritty.toml](https://github.com/unconfused/Debian-WSL/blob/main/alacritty.toml) as choose to.  Key changes: <br>
    ```bash
    [general]
    import = ["%APPDATA%/alacritty/onehalfdark.toml",]

    [font]
    normal.family = "MesloLGM Nerd Font"
    bold.family = "MesloLGM Nerd Font"
    italic.family = "MesloLGM Nerd Font"
    bold_italic.family = "MesloLGM Nerd Font"
    size = 11.0
    ```
7. Change the shortcut for Alacritty to point to your WSL distro: <br>
    ```
    "C:\Program Files\Alacritty\alacritty.exe" --working-directory=\\wsl$\Debian\home\<youruser> -e wsl.exe -d Debian bash
    ```


## Patch and install goodies

```bash
sudo apt update
sudo apt upgrade
sudo apt install build-essentials
sudo apt install fzf bat fd-find git acl tmux neovim 7zip zip lazygit curl wget fontconfig ripgrep tree-sitter ghostscript tree 
```

## Make bash prettier

1. Install oh-my-posh <br>
     ```bash
      curl -s https://ohmyposh.dev/install.sh | bash -s
     ```
2. Install fonts for it:<br>
     ```bash
      oh-my-posh font install Meslo
      oh-my-posh font install FiraCode
     ```
3. Check out [their list of themes](https://ohmyposh.dev/docs/themes) and pick one!
4. Add the cached theme to your .bashrc so that it loads every time: <br>
    ```nvim ~/.bashrc``` <br>
   Add this at or near the bottom (for the M365Princess theme:
    ```bash
    export EDITOR=nvim
    eval "$(oh-my-posh init bash --config /home/evan/.cache/oh-my-posh/themes/M365Princess.omp.json)"
    ``` 

## Make tmux prettier

There are tons of plugins for tmux and ways to really expand its functionality, but if all you are using are the basics with stock hotkeys...this is a way to pretty it up a little.

Here is my [~/.tmux.conf](https://github.com/unconfused/Debian-WSL/blob/main/.tmux.conf)


## Install Lazyvim and One Half Dark theme for it

1. Neovim (nvim) was installed earlier...if it wasn't, install it:  ```sudo apt install neovim```
2. Install Lazyvim using these instructions:  [https://www.lazyvim.org/installation](https://www.lazyvim.org/installation)
3. First run of 'nvim' will pull and setup all the plugins for Lazyvim
4. Edit lazy.lua, e.g. ```nvim ~/.config/nvim/lua/config/lazy.lua``` <br>
    In the section:<br>
         ```require("lazy").setup({```<br>
    Add this line appropriately:<br>
         ```{ "MarcoKorinth/onehalf.nvim", lazy = false },```
5. Add [my colorscheme.lua file](https://github.com/unconfused/Debian-WSL/blob/main/colorscheme.lua) to the ```~/.config/nvim/lua/plugins``` directory. <br>
    OR you can edit and paste in the code: <br>
        ```nvim ~/.config/nvim/lua/plugins/colorscheme.lua``` <br>
    Paste my lua code into that file:
        [my colorscheme.lua file](https://github.com/unconfused/Debian-WSL/blob/main/colorscheme.lua) 

