# 🤟 投注

**当前仅支持通过AOS命令行下注**，Web端应用即将推出，最小投注金额为0.001 ALT，支持手选和机选000-999之间的3位号码，无投注金额和次数上限。投注AOLOTTO\*ALT异常简单，直接向奖池进程发起$ALT转账即可参与最新轮次。

### 1. 机选投注

{% code fullWidth="false" %}
```lua
--[[
	在AOS中将Aolotto Pool和altoken进程ID分别设置为全局变量POOL和ALT,以便后续调用。
]]--
POOL = "wqwklmuSqSPGaeMR7dHuciyvBDtt1UjmziAoWu-pKuI" 
ALT = "dzkRvtoLH6mtIW893eJSO4vdJBc-JT8N1fnBmcDVWdY" 

--[[
	在AOS中发起转账，Recipient填写为设置好的全局变量POOL;
	请将Quantity设置为你希望投注的金额,ALT精度为3位，1意味着实际的投注金额为0.001ALT；
	如果你希望投注1ALT，请将Quantity设置为'1000';
]]--
Send({ 
	Target = ALT, 
	Action = "Transfer", 
	Recipient = POOL, 
	Quantity = "1" 
})
```
{% endcode %}

直接向ALT代币进程发起转账，在账户余额充足的情况下，您将成功参与到最新的投注轮次中，由于转账消息中不包含任何的号码信息，系统会自动为您随机选择号码，投注成功后您将收到一条Action为`Lotto-Notice`的回信，输入Inbox\[#Inbox].Data即可打印Lotto-Notice的正文内容，包含了随机算法帮您选择的号码信息。若私人进程或钱包地址上$ALT余额不足将会收到一条`Transfer-Error`信息，投注失败。

### 2. 手选投注

```lua
Send({ 
	Target = ALT, 
	Action = "Transfer", 
	Recipient = POOL, 
	Quantity = "2",
	["X-Numbers"] = "007" -- 000-999之间的任意3位数字
})
-- 下注结果：007*2
```

如果您希望在投注时自己选择心仪的号码，发送转账时加入`X-Numbers`即可，号码需要遵循3位数规范，非法号码系统将自动过滤并采用算法生成的随机号码。

### 3 批量投注

```lua
Send({ 
	Target = ALT, 
	Action = "Transfer", 
	Recipient = POOL, 
	Quantity = "3",
	["X-Numbers"] = "000,001,002" -- 号码之间使用","间隔
})
-- 下注结果：000*1，001*1, 002*1
```

可以一次性输入多个号码进行批量投注，Quantity数量需要大于或等于号码的数量，输入的号码数量若超过投注数量，将自动废弃多余号码。若投注数量大于号码数量，系统将会按照号码顺序循环叠加。确保总投注数量与转账的Quantity相等。

### 4 区间投注

```lua
Send({ 
	Target = ALT, 
	Action = "Transfer", 
	Recipient = POOL, 
	Quantity = "10",
	["X-Numbers"] = "000-009" -- 使用“-”代表取值区间；
})
-- 下注结果：000*1，001*1, 002*1, 003*1, 004*1, 005*1, 006*1, 007*1, 008*1, 009*1   
```

通过区间投注用户可以通过一笔转账生成一组序列数值的投注，取值的范围若超过Quantity总量，将会自动废除多余部分取值。例如Quantity=2，取值范围为“000-010”，最终生成的投注结果为000\*1，001\*1。

### 5 添加受益人

```lua
Send({ 
	Target = ALT, 
	Action = "Transfer", 
	Recipient = POOL, 
	Quantity = "3",
	["X-Numbers"] = "000,001,002",
	["X-Donee"] = "j0Lrrv1ltimsYnD_5f-8Fp3QKcAbUjckn7kjCZCfvhk" -- 添加受益人tag和地址，地址务必为aos process地址，AR钱包地址无法发起提取奖金的请求；
})
-- 以上投注中奖后，奖金将会分配给受益人，但投注量将会叠加到购买人信息中。
```

默认情况下，购买地址就是受益人，中奖奖金默认分发到购买地址上。但是可以通过X-Donee标签添加其它地址作为中奖受益人，你可以将受益人设置为你朋友或家人的地址，赠送投注。

### 6. 投注查询

如果想查看最新轮次的投注结果，直接向奖池进程发起查询即可：

```lua
Send({Target=POOL, Action="Bets"})
```

[点击这里](cha-xun-zhi-ling.md)，学习更多的查询指令。
