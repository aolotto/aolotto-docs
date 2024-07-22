# 💸 Claim Rewards

The winner needs to send a claiming message to the pool process to withdraw the rewards to their wallet or personal process. After the message is sent, the pool will transfer the entire rewards balance in a single transaction. The reward balance must be >= 0.01 ALT. A 10% income tax will be deducted from the claimed amount. If your balance is 0.01 ALT, the received amount after deduction is 0.009 ALT.

```lua
Send({Target=POOL,Action="Claim"})
```

After sending the claiming message, if the reward balance is sufficient, you will receive a **Credit-Notice** message and your reward balance will be cleared. You will receive an **Error** message if your reward balance is less than 0.01 ALT. It is recommended that you continue to bet and withdraw all your rewards at once after the balance accumulates to more than 0.01 ALT.

### Income Tax <a href="#guan-yu-suo-de-shui" id="guan-yu-suo-de-shui"></a>

**Aolotto** has a payout rate of 100%, with only a 10% income tax levied on winning users for the sustainable development of the ecosystem.&#x20;

### Check Rewards Balance <a href="#jiang-jin-yuecha-xun" id="jiang-jin-yuecha-xun"></a>

Send the following message to check your rewards balance :

```lua
Send({Target=AOLOTTO,Action="UserInfo"})
```

After receiving **Reply-UserInfo**, print the message body using `Inbox[#Inbox].Data` to view the current rewards balance.
