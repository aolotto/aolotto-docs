# 🚰 Faucet

**21,000,000 $ALT** (10% of the total supply) will be distributed to early users via the faucet. Join the official Aolotto [Discord](https://discord.com/invite/BFhkUCRjmF) to claim your free $ALT minting buff (**ALTb**). Each Discord account can only claim it once. When placing bets, the ALTb you received will be converted into $ALT based on the number of bets placed. The amount you can claim decreases linearly with the cumulative number of recipients. The earlier you claim, the more you get.

1. **Claim per account** = faucet balance \* 0.001%. The first recipient will get 2,100 ALTb. The second recipient will get (21,000,000 - 2,100) \* 0.001%, and so on.
2. If the faucet balance falls below 100,000 (expected after the 53,469th claim), the remaining ALTb will be issued at a fixed rate of 0.001% (\~10 ALTb) until the balance is exhausted and the faucet is permanently closed.

### **ALTb to $ALT Conversion**

ALTb is not a real token, but the address holding ALTb can convert it into the AO standard token, **$ALT**, during the betting process. This conversion adds $ALT to the betting rewards. The conversion method is as follows:

1. **Current minting speed** = 1 - ($ALT total circulation / $ALT maximum supply)
2. **Single bet release ($ALT)** = MIN(ALTb balance \* 0.01 \* bet amount \* minting speed, ALTb balance)
3. **Minting actual gain ($ALT)** = single bet release ($ALT) \* 0.8
4. **Minting tax ($ALT)** = single bet release ($ALT) \* 0.2

For more details on minting methods, please visit: [usdalt.md](usdalt.md "mention")

### Faucet Tutorial

1. Join **Aolotto** official [Discord](https://discord.com/invite/BFhkUCRjmF) ;
2. Enter the faucet channel;
3. Input the “/get” command to wake up the faucet robot;
4. Fill your AR wallet address;
5. After confirming, wait for the robot to transfer;

### **Testnet $ALT**

Since Aolotto's launch on the testnet in May 2024, it has attracted significant attention from enthusiastic users. During the testing phase, a total of **1,093,519.8 $ALT** was distributed to **447 addresses** via the faucet and ALT pool. These $ALT tokens were then converted into ALTb based on the balance snapshot. The release mechanism follows the process outlined above.

**$ALT balance snapshot during the testing phase:** [View Snapshot](https://www.ao.link/#/token/sdqQuIU6WNT1zVNculn814nVhol2XXhDxqgCrUpCtlA)
