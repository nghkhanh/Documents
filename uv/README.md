# uv

## install uv
```python
WSL/Ubuntu
- Install `mise` for managing dev tools
wget -O - https://github.com/jdx/mise/releases/download/v2025.1.6/install.sh | sh

- Activate mise
echo 'eval "$(~/.local/bin/mise activate bash)"' >> ~/.bashrc

- Restart your terminal

- Install uv via mise
mise use -g uv 

WIN
- Install winget
Add-AppxPackage -RegisterByFamilyName -MainPackage Microsoft.DesktopAppInstaller_8wekyb3d8bbwe

- Restart your terminal

- Install `uv`
winget install astral.uv --source winget
```

## install python
```python
uv python install 3.11
```
