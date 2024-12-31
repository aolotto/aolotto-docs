# 🎲 Betting

The betting process is very simple, similar to traditional games like Pick3. You can choose any 3-digit number (000-999), set the bet amount, and pay with $wUSDC to place the bet.

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

1. The game progresses in rounds, and participants will automatically place their bets on the latest ongoing round.
2. The payment token used is [$wUSDC](https://ao.link/#/token/7zH9dlMNoxprab9loshv3Y7WG45DOny_Vrq9KrXObdQ), transferred cross-chain via AOX. The minimum bet amount is $1, and the maximum is $100. No gas fees are required (though once the AO mainnet is live, there may be negligible gas fees, with the gas cost in $AO not included in the bet amount). Once the payment is confirmed, the bet is successfully placed.
3. Each bet generates a permanent ticket stored on Arweave, similar to a traditional lottery ticket. These tickets stored on Arweave are atomic assets, discoverable like NFTs, and have collectible value. \[[Example of a chain-based lottery ticket](https://kmu4rbzchrloqp3ypunbd4y345hrhritxwufx7dg5ymkbce6anhq.arweave.net/UynIhyI8Vug_eH0aEfMb508TxRO9qFv8Zu4YoIieA08)]
4. Minting rewards and ALTb release are tied to the Bet2Mint mechanism. Minting rewards are the basic $ALT given after a bet is placed, while ALTb release is a bonus added on top of the basic reward. Minting buffs are additional rewards for early users, and not all participants will have access to them. \[[Learn more about Bet2Mint](https://docs.aolotto.com/en/usdalt#bet2mint)]

After placing your bet, you’ll need to wait for the drawing. The results will be posted in real-time on Aolotto’s [official X](https://x.com/aolotto_dao) (formerly Twitter) and [Discord](https://discord.gg/BFhkUCRjmF). You can also check your win status or view past drawings in your personal center or the [Draws](https://dev.aolotto.com/#/draws) page.

## **Recommended Betting Strategy**

Aolotto offers 1000 possible numbers to choose from, so your odds of winning with each bet are 1/1000. The Bet2Mint mechanism is also applied, adding extra rewards. Generally, the earlier you bet in a round, the higher the $ALT reward you’ll earn. The later you bet, the higher your chances of winning (the last person to bet has at least a 50% higher chance of winning). Based on these rules, we recommend the following strategy:

* **For earlier bets**, when the minting rewards ($ALT) are higher, we recommend placing a bet of $100. For example, if Player A places a bet and the Bet2Mint reward for that round is 200 $ALT, Player A would earn 200 $ALT for a $1 bet, or 20,000 $ALT for a $100 bet. As the round progresses, the Bet2Mint reward decreases for subsequent participants based on the remaining minting balance, calculated as: (this round's minting balance - 20,000) \* 0.0001.
* **For later bets**, it’s often beneficial to place the minimum bet of $1 to compete for the higher chances of winning as the last bettor.
