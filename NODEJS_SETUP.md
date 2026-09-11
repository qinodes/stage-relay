# Install Node.js and npx

Install Node.js before installing Stage Relay. `npx` is included with Node.js.

## Windows

Run in PowerShell:

```powershell
winget install --id OpenJS.NodeJS.LTS --exact
```

Close and reopen PowerShell after installation.

## Linux

For Debian or Ubuntu, run:

```bash
sudo apt update
sudo apt install -y curl
curl -fsSL https://deb.nodesource.com/setup_24.x | sudo -E bash -
sudo apt install -y nodejs
```

For other Linux distributions, follow the [official npm installation guide](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm/).

## macOS

Install Homebrew if it is not already installed:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the PATH instructions shown by the installer, then run:

```bash
brew install node
```

## Verify

```bash
node --version
npx --version
```
