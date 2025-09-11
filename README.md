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
   A. [MesloLG Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/Meslo.zip) is an easy choice, but use whatever you like.
2. Change your settings for your Debian -> Appearance to fit the theme and your newly installed MesloLG font. I'm fond of the One Half Dark theme.<br>
    <img width="440" height="240" alt="image" src="https://github.com/user-attachments/assets/a4bb11ce-a4db-49da-b734-1cfdbe125285" />
3. Change the icon for your Debian install to something better than what Microsoft provided.<br>
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
   A. [MesloLG Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/Meslo.zip) is an easy choice, but use whatever you like.
3. Open this location for the config files: ```%APPDATA%\alacritty\```
4. Download my [onehalfdark.toml](https://github.com/unconfused/Debian-WSL/blob/main/onehalfdark.toml) file, if you want that style.  Put it with the other config files.
5. Edit your alacritty.toml file. Add [my settings](https://github.com/unconfused/Debian-WSL/blob/main/alacritty.toml) as choose to.  Key changes: <br>
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
6. Change the shortcut for Alacritty to point to your WSL distro: <br>
    ```
    "C:\Program Files\Alacritty\alacritty.exe" --working-directory=\\wsl$\Debian\home\<youruser> -e wsl.exe -d Debian bash
    ```


## Patch and install goodies

```bash
sudo apt update
sudo apt upgrade
sudo apt install build-essentials
sudo apt install fzf bat fd-find git acl tmux neovim 7zip zip lazygit curl wget fontconfig ripgrep tree-sitter ghostscript
```
