# Step-by-Step Guide to Running the Initia Node

## Prerequisites

```
CPU: 4 cores
Memory: 16GB
Disk: 1000GB
```

I am using a Contabo VPS 3 instance for this setup.

## Installation

### 1. Create Screen Session (Optional but Recommended)

    I highly recommend creating a screen session to run the script as it takes a while.

```
apt install screen
screen -S initia
```

To connect to the same session later, use:

```
screen -r -d initia
```

### 2. Download and Run the Script

     Download the script, make it executable, and then run it with your moniker.

   ```
   curl -OJL https://raw.githubusercontent.com/pvsairam/initia-guide/main/initia_installer.sh
   chmod +x initia_installer.sh
   ./initia_installer.sh <moniker>
   ```

### 3. Create Wallet and Get Some Tokens

```
source .bashrc
initiad keys add <key-name>
```

  Don't forget to backup the seed at this point.
  You can get tokens from the faucet.
  
Example Command:

```
initiad keys add xtestnet
```

### 4. Check Logs

 ```
journalctl -fu initiad
 ```
  For node status:
```
source .bashrc
initiad status | jq .sync_info
```
  Wait until Catching Up: false
  
### 5.  Create Validator

```
initiad tx mstaking create-validator \
    --amount="1000000uinit" \
    --pubkey=$(initiad tendermint show-validator) \
    --moniker="<moniker>" \
    --chain-id="initiation-1" \
    --from="<key_name>" \
    --commission-rate="0.10" \
    --commission-max-rate="0.20" \
    --commission-max-change-rate="0.01" \
    --fees 30000uinit
```
    You can check your validator from the explorer.

  Example Command:

```
initiad tx mstaking create-validator \
--amount="1000000uinit" \
--pubkey=$(initiad tendermint show-validator) \
--moniker="xtestnet" \
--chain-id="initiation-1" \
--from="xtestnet" \
--commission-rate="0.05" \
--commission-max-rate="0.20" \
--commission-max-change-rate="0.01" \
--fees 30000uinit
```

