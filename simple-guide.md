---
description: Simple installation and Instructions use snapshot
---

### Public Endpoint

>- API: http://157.230.52.200:43317/
>- RPC: http://157.230.52.200:43657/
>- gRPC: http://157.230.52.200:40690/
>- gRPC Web : http://157.230.52.200:40690/
# Installation


**Chain ID**: nolus-rila | **Latest Version Tag**: v0.1.43 | **Custom Port**: 43

# Auto Installing NOLUS-RILA testnet for NOLUS
```
wget https://raw.githubusercontent.com/raflesiaa/Nolus-Testnet-Guide/main/autoinstaller.sh && chmod +x rila.sh && ./autoinstaller.sh
```
**_noted: actually the auto installer above already includes a snapshot, but if you have installed nolus and only need a snapshot, I will make a guide below_**

# Snapshot

{% hint style='info' %}
Snapshots allows a new node to join the network by recovering application state from a backup file. 
Snapshot contains compressed copy of chain data directory. To keep backup files as small as plausible, 
snapshot server is periodically beeing state-synced.
{% endhint %}


**pruning**: 100/0/19 | **indexer**: null | **version tag**: v0.1.43

| BLOCK             | AGE             | DOWNLOAD                                                                                            |
| ----------------- | --------------- | --------------------------------------------------------------------------------------------------- |
| 1278825 | 1 hours | [snapshot (1.25 GB)](http://157.230.52.200/snapshot/nolus/nolus-snapshot-latest.tar.lz4) |

## Instructions

### Stop the service and reset the data

```bash
sudo systemctl stop nolusd
cp $HOME/.nolus/data/priv_validator_state.json $HOME/.nolus/priv_validator_state.json.backup
rm -rf $HOME/.nolus/data
```

### Download latest snapshot

```bash
curl -L http://157.230.52.200/snapshot/nolus/nolus-snapshot-latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.nolus
mv $HOME/.nolus/priv_validator_state.json.backup $HOME/.nolus/data/priv_validator_state.json
```

### Restart the service and check the log

```bash
sudo systemctl start nolusd && sudo journalctl -u nolusd -f --no-hostname -o cat
```
