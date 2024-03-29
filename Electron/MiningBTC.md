
![images](https://github.com/an-node/NODE-MAINNET/assets/96678356/c1e4377f-f056-4444-b5e7-6e13e9370725)


### Minimum Hardware :
OS  | CPU     | RAM      | SSD     | 
| ------------- | ------------- | ------------- | -------- |
| Ubuntu 20.04 LS | 6          | 16         | 400 GB  | 


# Install Git
```
sudo apt install git
```
# Install Node.js
```
sudo apt-get update
```
```
sudo apt-get install -y ca-certificates curl gnupg
```
```
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/nodesource.gpg
NODE_MAJOR=16
echo "deb [signed-by=/usr/share/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x focal main" | sudo tee /etc/apt/sources.list.d/nodesource.list
```
```
sudo apt-get update
```
```
sudo apt-get install nodejs -y
```
# Install Screen
```
sudo apt-get install screen -y
```
# Install NPM
```
sudo apt-get install npm -y
```
```
sudo npm install -g typescript
```
# Clone Repository Git
```
git clone https://github.com/atomicals/atomicals-js.git
cd atomicals-js
```
# Create Sesion
```
screen -S btc
```
# Build Project
```
npm run build
```
# Install Yarn
```
sudo npm install -g yarn
```
# Install Dependencies with Yarn
```
yarn install
```
# Create Wallet
```
yarn cli wallet-init
```
# Run Project
```
yarn cli mint-dft electron --satsbyte 50
```
# Deposit BTC
```
Deposit BTC
```
# DONE MINNING


# NOTE : 
- [SAVE] Find Folder : atomical-js > file wallet.json > save > Download to PC

![Capture](https://github.com/an-node/NODE-MAINNET/assets/96678356/63706a0b-b560-4c6f-8be7-7c822a77ee3a)

- [Wallet] Import Pharse Wallet BTC in : https://atomicalswallet.com
- Exit Sesion Screen : CTRL A + D
- Back Sesion Screen : screen -r btc

# Delete 
```
sudo apt remove git -y
```
```
sudo apt-get remove nodejs -y
```
```
sudo rm /etc/apt/sources.list.d/nodesource.list
```
```
sudo rm /etc/apt/keyrings/nodesource.gpg
```
```
rm -rf atomicals-js
```
```
sudo apt-get remove screen
```
```
npm uninstall -g typescript -y
```
```
npm uninstall -g yarn -y
```
