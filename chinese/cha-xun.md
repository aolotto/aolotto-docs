# 🔍 查询

在AOS中向**aolotto**进程发送消息即可查询相关信息。

### 1. 查询轮次信息

```lua
Send({Target=AOLOTTO,Action="GetRoundInfo"})
```

向**aolotto**进程发送`GetRoundInfo`可查询当前进行轮次的信息,消息发送后将会收到一条Action为`Reply-RoundInfo`的回复。

```lua
Send({Target=AOLOTTO,Action="GetRoundInfo",Round="1"})
```

添加Round标签，可以查询指定轮次的信息，若指定的轮次未开始或不存在将会收到一条Action为\`Error\`的错误回复。

收到回复消息后，可通过\`Inbox\[#Inbox].Data\`打印消息正文.

<details>

<summary>消息正文示例</summary>

```
  -----------------------------------------      
  aolotto Round 1 - Ended
  ----------------------------------------- 
  * Pool Balance:      215.200 ALT
  * Estimated Prize:   160.100 ALT
  * Participants:      3
  * Bets:              110200
  * Start at:          2024/07/12 19:07 UTC
  * Lucky Number:      547
  ----------------------------------------- 
  Ends at 2024/07/14 01:17 UTC, 1 winners.
```

</details>

### 2. 查询个人信息

```lua
Send({Target=AOLOTTO,Action="UserInfo"})
```

参与过投注的用户发送以上消息可以获取最新的个人的参与信息，消息发送后将会收到Action为Reply-RoundInfo的回信，使用\`Inbox\[#Inbox].Data\`打印消息正文。

<details>

<summary>用户信息正文示范</summary>

```
 TRSgY37rCXAVmYXzKQ3pw1-lyBDASlw5GGphXVO5DJE
  -------------------------------------------
  * Number of Wins :   1
  * Rewards Balance :  0.000 ALT
  * Total Rewards :    160.100 ALT
  * Bets Amount :      407000
  * Bets Placed :      11
  -------------------------------------------
  First bet on 2024/07/14 01:17 UTC
```

</details>

### 3. 查询投注

```lua
Send({Target=AOLOTTO,Action="Bets",Round="1"})
```

发送以上消息查询个人在最新轮次中的投注信息，当收到Action为Reply-UserBets的回信后，即可通过\`Inbox\[#Inbox].Data\`打印具体的投注详情。

```lua
Send({Target=AOLOTTO,Action="Bets",Round="1"})
```

添加Round标签可以查询指定轮次的投注情况。如过查询的轮次不存在或未在该轮次下注，将会收到Error回信，\`Inbox\[#Inbox].Data\`打印具体的错误信息。

<details>

<summary>投注回信正文示范</summary>

```
You've placed 3000 bets that cover 3 numbers on Round 1 : 
----------------------------------------------------------
 782 * 1000  |  400 * 1000  |  870 * 1000  | 
```

</details>
