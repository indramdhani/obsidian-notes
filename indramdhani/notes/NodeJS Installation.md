### Using Snap ( if the snap is available in the server )

```bash
sudo snap install node --classic --channel=14
```

```bash
sudo snap refresh node --channel=15
```

### Manual install

```bash
curl --silent --location <https://rpm.nodesource.com/setup_8.x> | sudo bash -
sudo yum install nodejs
```

### Using nvm

[](https://github.com/nvm-sh/nvm#install--update-script)[https://github.com/nvm-sh/nvm#install--update-script](https://github.com/nvm-sh/nvm#install--update-script)

Install the nvm

```bash
curl -o- <https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh> | bash
#or
wget -qO- <https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh> | bash
```

Run the script below to add the source lines to correct profile

```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \\. "$NVM_DIR/nvm.sh" # This loads nvm
```

Install the node

```bash
#install the latest version
nvm install node
#install specific version 
nvm install 12 #version number
#install lts version
nvm install --lts
```

Use the node

```bash
#use the lts version
nvm use lts
#use the specific version
nvm use 12
#use the latest version
nvm use node
```

### Using n

[](https://github.com/tj/n)[https://github.com/tj/n](https://github.com/tj/n)

#server #nodejs