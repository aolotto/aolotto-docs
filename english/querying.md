# 🔍 Querying

List commonly used query commands below. Simply enter the following command in AOS for your query. You can print the results by `Inbox[#Inbox].Data` after receiving responses.

### Get Round Information

```lua
Send({Target=POOL,Action="GetRoundInfo"}
```

Get information about the current round, it will reply to a message with `Reply-RoundInfo`

```lua
Send({Target=POOL,Action="GetRoundInfo",Round="1"})
```

If you wish to get information about a target round, you need to add a Round tag.

<details>

<summary>The example of Response data </summary>

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

### User Info

```lua
Send({Target=POOL,Action="UserInfo"})
```

Users who have participated in betting can send the above message to get the latest user information. After sending the message, you will receive a reply message with Action as **Reply-UserInfo**. Use `Inbox[#Inbox].Data` to print the message body.

### Fetching Bets

```lua
Send({Target=POOL,Action="Bets"})
```

Send the above message to query your betting information in the latest round. When you receive a reply with Action as **Reply-UserBets** , you can print the betting details using `Inbox[#Inbox].Data`.

```lua
Send({Target=POOL,Action="Bets",Round="1"})
```

Add the Round tag to query your betting details in the target round.

### The information of the pool

```lua
Send({Target=POOL,Action="Info"})
```

Send the above message to get the summary of the pool.

### Fetching winners

```lua
Send({Target=POOL,Action="Winners",Round="1"})
```

Query the Winners of the completed round. The Round tag must be specified when querying, otherwise no information will be returned.
