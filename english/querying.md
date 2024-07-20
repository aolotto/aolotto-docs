# 🔍 Querying

List commonly used query commands below. Simply enter the desired command in AOS for your querying. You can print the results by `Inbox[#Inbox].Data` after receiving responses.

### Round Info

```lua
Send({Target=POOL,Action="GetRoundInfo"})
```

### User Info

```lua
Send({Target=POOL,Action="UserInfo"})
```

### Your Bets

```lua
Send({Target=POOL,Action="Bets"})
```

### The Pool Info

```lua
Send({Target=POOL,Action="Info"})
```

### The winners

```lua
Send({Target=POOL,Action="Winners",Round="1"})
```
