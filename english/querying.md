# 🔍 Querying

List commonly used query commands below. Simply enter the following command in AOS for your querying. You can print the results by `Inbox[#Inbox].Data` after receiving responses.

### Round Info

```lua
Send({Target=POOL,Action="GetRoundInfo"}
```

g information about the current round, reply identifier is `Reply-RoundInfo`

```lua
Send({Target=POOL,Action="GetRoundInfo",Round="1"})
```

### User Info

```lua
Send({Target=POOL,Action="UserInfo"})
```

### Your Bets

```lua
Send({Target=POOL,Action="Bets"})
```

```lua
Send({Target=POOL,Action="Bets",Round="1"})
```

### The Pool Info

```lua
Send({Target=POOL,Action="Info"})
```

### The winners

```lua
Send({Target=POOL,Action="Winners",Round="1"})
```

```lua
Send({Target=POOL,Action="Winners",Round="1"})
```
