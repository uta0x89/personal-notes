# Looking at [withdrawals](https://twitter.com/barnabemonnot/status/1581686737943728129)

I have investigated on "Looking at withdrawals" in ROP-1.

The core issue to consider is the following part of [this tweet](https://twitter.com/AFDudley0/status/1581675060351275008?s=20&t=wbk-RPPmODdmdkBtEb_8-A).  
> how long it would take for 1/3+ of the currently staked validators to unbond

The simplest solution to this problem would be the following statement in [annotated-spec](https://github.com/ethereum/annotated-spec/blob/master/phase0/beacon-chain.md#churn).  
> With the above numbers, if there is more than 8,388,608 ETH staking, it will take at least 65536/3 epochs, or 10.67 eeks, for 1/3 of validators to withdraw (however, if there is no attack, then the withdrawal queue will ordinarily be short).

However, the above solution has problems in two respects.

- (1) The above solution needs to take churn limit into account.  
I made [a solution](./exit-duration.ipynb) to the above issue with this in consideration.  
- (2) Withdrawal mentioned above is processed in two steps: Exit and Withdrawal.  
Since the above solution only considers the Exit queue, it is more accurate to consider the [Withdraw queue](https://notes.ethereum.org/@launchpad/withdrawals-faq#Q-How-fast-will-I-be-able-to-make-a-partial-withdrawal-Or-when-will-I-get-access-to-the-excess-rewards-that-are-on-my-validator) as well.

## Note
[Barnabe mentions](https://twitter.com/barnabemonnot/status/1581686737943728129?s=20&t=j-c4HKzzIIobHNC2vkrYEg) the following in reference to the above issue. 
> This model(=Ethereum Economic Model) would be well suited for it  

Since the current model does not take into account exit as well as withdrawal, to solve the above issue using this model, we first need to add a module on Exit to the model.
