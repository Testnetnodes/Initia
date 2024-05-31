sudo systemctl stop initiad
wget https://snapshots.tienthuattoan.com/testnet/initia/initia_latest.tar.lz4 -O latest_snapshot.tar.lz4
cp $HOME/.initia/data/priv_validator_state.json $HOME/.initia/priv_validator_state.json.backup
initiad tendermint unsafe-reset-all --home $HOME/.initia --keep-addr-book
lz4 -d -c ./latest_snapshot.tar.lz4 | tar -xf - -C $HOME/.initia
mv $HOME/.initia/priv_validator_state.json.backup $HOME/.initia/data/priv_validator_state.json
sudo systemctl restart initiad && sudo journalctl -u initiad -f -o cat
