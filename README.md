# Zaptos Developer Docs
Zaptos Liquid Staking contracts allow the user to deposit stake, which is pushed to a validator to earn yield.
# Contract Addresses
`Staked Aptos Coin Contract = 0xe8f59d770be479176888276a5e658058d93e7aa6eefe272641115984951e3391::st_aptos_coin`

`Stake Contract Address = 0xe8f59d770be479176888276a5e658058d93e7aa6eefe272641115984951e3391::zaptos_stake`
# API Specs

**Stake**
`public(script) fun stake(user_account: &signer,  amount: u64  )`

	user_account == signer depositing funds
	Amount == amount of aptos coins to withdraw
This call withdraws aptos from the wallet and deposits it into the protocol. Staked Aptos is minted to the user's wallet. This call will fail if amount > number of Aptos coins in the wallet. The *exchange rate* = total aptos in Zaptos / total staked aptos outstanding.



**Unstake**

`public(script) fun stake(user_account: &signer,  amount: u64  )`

	user_account == signer depositing funds
	Amount == amount of staked aptos coins to withdraw 

This call withdraws Staked Aptos from the wallet and deposits it into the protocol.  After the unstake waiting period the coins are withdrawn and then returned to the user wallet. Please note this unstake period can take up to two weeks. This call will fail if amount > number of Staked Aptos coins in the wallet. The *exchange rate* = total aptos in Zaptos / total staked aptos outstanding.


*The following functions are still in testing but will be added soon:*


**Unstake_Immediately**

`public(script) fun stake(user_account: &signer,  amount: u64  )`

	user_account == signer depositing funds
	Amount == total staked Aptos coins to be withdrawn from the user_account 

This call withdraws money from the protocol liquidity pool to withdraw Aptos immediately. This typically costs a 0.3% - 3% fee.  Staked Aptos is withdrawn from the wallet and Aptos is deposited in the wallet. The *exchange rate* = total aptos in Zaptos / total staked aptos outstanding.


**Withdraw**

`public(script) fun unstake(  user_account: &signer,  amount: u64  )`

This call withdraws money from the protocol liquidity pool to withdraw Aptos immediately. This typically costs a 0.3% - 3% fee. The *exchange rate* = total aptos in Zaptos / total staked aptos outstanding.


## Unstaking In Aptos

Unstaking in Aptos is a two step process, after the unstake period (typically two weeks), the validator funds are unstaked. One epoch (one hour) after the funds are unstaked, the withdraw function must be called to put the funds into the user wallet.

Zaptos automates the unlock function. However, when gas fees are high or during a server outage, the user must call the withdraw function manually to retrieve their funds.
