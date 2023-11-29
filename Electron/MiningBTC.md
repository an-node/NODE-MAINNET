# Install Git
```
sudo apt install git
```
# Install Node.js
```
sudo apt-get update && sudo apt-get install -y ca-certificates curl gnupg
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
NODE_MAJOR=20
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
sudo apt-get update && sudo apt-get install nodejs -y
```
# Install Git
```
git clone https://github.com/atomicals/atomicals-js.git
```
# Install Screen
```
sudo apt-get install screen -y
```

# Install NPM
```
npm install -g typescript
```
```
cd atomicals-js
```
```
screen -S btc
```
```
npm run build
```
```
npm install -g yarn
```
```
yarn install
```
```
yarn cli wallet-init
```
# SAVE Data Wallet
```
yarn cli mint-dft electron --satsbyte 50
```
# Deposit 
```
Deposit BTC
```
Done

# NOTE : 
- [SAVE] Find Folder : atomical-js > file wallet.json > save > Download to PC
- [Wallet] Import Pharse Wallet BTC in : https://atomicalswallet.com
- Exit Sesion Screen : CTRL A + D
- Back Sesion Screen : screen -r btc

# Delete 
Uninstall Git:
```
sudo apt remove git
```
Uninstall Node.js:
```
sudo apt-get remove nodejs
sudo rm /etc/apt/sources.list.d/nodesource.list
sudo rm /etc/apt/keyrings/nodesource.gpg
Remove the cloned Git repository:
```
Remove the cloned Git repository:
```
rm -rf atomicals-js
```
Uninstall Screen:
```
sudo apt-get remove screen
```
Uninstall NPM and TypeScript:
```
npm uninstall -g typescript
```
Remove Yarn:
```
npm uninstall -g yarn
```
