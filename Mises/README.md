<p align="center">
  <img width="300" height="auto" src="https://user-images.githubusercontent.com/108969749/203468600-bd337c5d-70b2-46bd-8a56-bcc001a447db.jpeg">
</p>

### Minimum Hardware :
NODE  | CPU     | RAM      | SSD     |
| ------------- | ------------- | ------------- | -------- |
| Mainnet | 4          | 32         | 1TB  |

### Auto Install
```
wget -O mises.sh https://raw.githubusercontent.com/an-node/NODE-MAINNET/main/Mises/mises.sh && chmod +x mises.sh && ./mises.sh
```
### Load Variable
```
source $HOME/.bash_profile
```
### Statesync
```
sudo systemctl stop misestmd
SNAP_RPC="https://e1.mises.site:443"

LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.misestm/config/config.toml

sudo systemctl restart misestmd && sudo journalctl -u misestmd -f --no-hostname -o cat | grep chunk
```
### Information Node

   * cek sync node
```
misestmd status 2>&1 | jq .SyncInfo
```
   * Check Log Node
```
journalctl -fu misestmd -o cat
```
   * Check Node Info
```
misestmd status 2>&1 | jq .NodeInfo
```
   * Check validator Info
```
misestmd status 2>&1 | jq .ValidatorInfo
```
  * Check Node Id
```
misestmd tendermint show-node-id
```

### Create Wallet
   * New Wallet
```
misestmd keys add $WALLET
```
   * Recover Wallet
```
misestmd keys add $WALLET --recover
```
   * List wallet
```
misestmd keys list
```
   * Delete Wallet
```
misestmd keys delete $WALLET
```
### Save Wallet
```
MISES_WALLET_ADDRESS=$(misestmd keys show $WALLET -a)
MISES_VALOPER_ADDRESS=$(misestmd keys show $WALLET --bech val -a)
echo 'export MISES_WALLET_ADDRESS='${MISES_WALLET_ADDRESS} >> $HOME/.bash_profile
echo 'export MISES_VALOPER_ADDRESS='${MISES_VALOPER_ADDRESS} >> $HOME/.bash_profile
source $HOME/.bash_profile
```

### Create Validator
 * Check Balance
```
misestmd query bank balances $MISES_WALLET_ADDRESS
```
 * Create Validator
```
misestmd tx staking create-validator \
  --amount 1000000umis \
  --from $WALLET \
  --commission-max-change-rate "0.01" \
  --commission-max-rate "0.2" \
  --commission-rate "0.07" \
  --min-self-delegation "1" \
  --pubkey  $(misestmd tendermint show-validator) \
  --moniker $NODENAME \
  --fees 250umis \
  --chain-id $MISES_CHAIN_ID
```
 * Edit Validator
```
misestmd tx staking edit-validator \
  --moniker="nama-node" \
  --identity="<your_keybase_id>" \
  --website="<your_website>" \
  --details="<your_validator_description>" \
  --chain-id=$MISES_CHAIN_ID \
  --fees 250umis \
  --from=$WALLET
```
 ° Unjail Validator
```
misestmd tx slashing unjail \
  --broadcast-mode=block \
  --from=$WALLET \
  --chain-id=$MISES_CHAIN_ID \
  --fees=250umis
```
### Voting
```
misestmd tx gov vote 1 yes --from $WALLET --chain-id=$MISES_CHAIN_ID
```
### Delegate & Rewards
  * Delegate
```
misestmd tx staking delegate $MISES_VALOPER_ADDRESS 1000000umis --from=$WALLET --chain-id=MISES_CHAIN_ID --fees=250umis
```
  * Withdraw Reward
```
misestmd tx distribution withdraw-all-rewards --from=$WALLET --chain-id=$MISES_CHAIN_ID --fees=250umis
```
  * Withdraw Reward & Commission
```
misestmd tx distribution withdraw-rewards $MISES_VALOPER_ADDRESS --from=$WALLET --commission --chain-id=$MISES_CHAIN_ID
```

### Delete Node
```
sudo systemctl stop misestmd && \
sudo systemctl disable misestmd && \
rm /etc/systemd/system/misestmd.service && \
sudo systemctl daemon-reload && \
cd $HOME && \
rm -rf mises-tm && \
rm -rf mises.sh && \
rm -rf .misestm && \
rm -rf $(which misestmd)
```
