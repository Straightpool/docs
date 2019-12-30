# The problem
Early on information was circulating that you would need an account type wallet to pledge to your pool. A number of operators used the JCLI to create an account type address and sent their funds from the restored shelley wallet with cardano-wallet to this new account address before Daedalus ITN was available. 

The issues:
- An account type address created with the JCLI does have a private key but no mnemonic, thus it is uncertain if you can transfer rewards on this wallet back to mainnet
- The only way to delegate from this address is using the command line, e.g. using the delegate-account.sh script

People have tried to use the [send-money.sh script](https://raw.githubusercontent.com/input-output-hk/jormungandr-qa/master/scripts/send-money.sh) to send their balance from the account wallet to a Daedalus rewards wallet with no success.

Error shown:
error: Invalid value for '<account-id>': account parameter '<A daedalus rewards wallet address>' isn't an account address, found: 'Group(<Daedalus rewards wallet group)'

