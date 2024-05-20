# Hardwave requirements
4 Cores, 16G Ram,  160G SSD, Ubuntu 22.04
# Auto install (Source NodeSync.Top)
```bash
sudo apt install curl -y && wget https://nodesync.top/alignedlayer_auto && chmod +x alignedlayer_auto && ./alignedlayer_auto
```
# Wallet Command
Create wallet
```bash
alignedlayerd keys add wallet
```
Recover existing key
```bash
alignedlayerd keys add wallet --recover
```
Query Wallet Balance
```bash
alignedlayerd q bank balances $(alignedlayerd keys show wallet -a)
```
# Check Sync
```bash
alignedlayerd status 2>&1 | jq .sync_info
```
False is synced
# Create Validator
Obtain your validator public key by running the following command:
```bash
alignedlayerd comet show-validator
```
The output will be similar to this (with a different key):

{"@type":"/cosmos.crypto.ed25519.PubKey","key":"lR1d7YBVK5jYijOfWVKRFoWCsS4dg3kagT7LB9GnG8I="}

Then, create a file named validator.json with the following content:
```bash
nano $HOME/validator.json
```
Change your info, from "pubkey" to "details"  and Save them
```bash
{    
    "pubkey": {"@type":"/cosmos.crypto.ed25519.PubKey","key":"lR1d7YBVK5jYijOfWVKRFoWCsS4dg3kagT7LB9GnG8I="},
    "amount": "1000000stake",
    "moniker": "your-node-moniker",
    "identity": "eqlab testnet validator",
    "website": "optional website for your validator",
    "security": "optional security contact for your validator",
    "details": "optional details for your validator",
    "commission-rate": "0.1",
    "commission-max-rate": "0.2",
    "commission-max-change-rate": "0.01",
    "min-self-delegation": "1"
}
```
Finally, we're ready to submit the transaction to create the validator:
```bash
alignedlayerd tx staking create-validator $HOME/validator.json \
--from wallet --chain-id alignedlayer \
--fees 50stake
```







