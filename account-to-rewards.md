# The problem
Early on information was circulating that you would need an account type wallet to pledge to your pool. A number of operators used the JCLI to create an account type address and sent their funds from the restored shelley wallet with cardano-wallet to this new account address before Daedalus ITN was available. 

The issues:
- An account type address created with the JCLI does have a private key but no mnemonic, thus it is uncertain if you can transfer rewards on this wallet back to mainnet
- The only way to delegate from this address is using the command line, e.g. using the delegate-account.sh script

People have tried to use the [send-money.sh script](https://raw.githubusercontent.com/input-output-hk/jormungandr-qa/master/scripts/send-money.sh) to send their balance from the account wallet to a Daedalus rewards wallet with no success.

Error shown:
error: Invalid value for '<account-id>': account parameter '<A daedalus rewards wallet address>' isn't an account address, found: 'Group(<Daedalus rewards wallet group)'
  
After seeing this error no balance has left the account wallet.

# The solution
The error at the end is meaningless, this is just an account balance check. The transaction fails because it was attempted to send the whole balance of the account wallet not accounting for the transaction fee.

First check the available balance on the account wallet you want to send to a Daedalus rewards wallet:
```
jcli rest v0 account get $(cat ~/files/account.addr) -h http://127.0.0.1:${REST_PORT}/api
```

Now subtract 400000 lovelaces from this amount, this is the value you want to send to deplete the account balance.

Use the send-money.sh script as usual:
```
./send-money.sh <A daedalus rewards wallet address> <account balance - 400000)> <REST port> <Private key of account wallet>
```

Now the transaction will go through and you can see the funds in the Daedalus rewards wallet. The error in the end does not matter.

When you delegate from Daedalus rewards wallet the address used will be the one you sent your account balance to, so the pledge address from now on is the one Daedalus rewards wallet you selected for <A daedalus rewards wallet address>.
