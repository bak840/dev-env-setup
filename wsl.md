# WSL Setup

## Install WSL

1. Open PowerShell as Administrator and run:  

    ```bash
    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
    ```

2. Restart your computer when prompted

3. Open the Microsoft Store and download Ubuntu

4. Open Ubuntu in the Start menu, set up a new account and run :  

    ```bash
    sudo apt update && sudo apt upgrade
    ```

## WSL setup VS Code

[Developing in WSL](https://code.visualstudio.com/docs/remote/wsl)

## Install Node

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash
```

```bash
command -v nvm
```

```bash
nvm ls
```

```bash
nvm install node --lts
```

```bash
node --version
npm --version
```
