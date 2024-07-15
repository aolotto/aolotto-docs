# 🤟 投注指南

**当前仅支持通过AOS命令行下注**，web端应用即将推出。用户的单笔最小投注额为0.001 ALT，支持手选和机选000-999之间的任意3位号码，无投注金额和次数上限。投注异常简单，直接向**aolotto**协议地址`wqwklmuSqSPGaeMR7dHuciyvBDtt1UjmziAoWu-pKuI`发起$ALT转账即可参与最新轮次的投注。

### 1. 机选投注

{% code fullWidth="false" %}
```lua
-- 1. 在AOS中将aolotto 和 altoken进程ID分别设置为全局变量方便后续调用
AOLOTTO = "wqwklmuSqSPGaeMR7dHuciyvBDtt1UjmziAoWu-pKuI" 
ALT = "dzkRvtoLH6mtIW893eJSO4vdJBc-JT8N1fnBmcDVWdY" 

-- 2. 发起转账，0.001 ALT为最小下注量，若需下注1 ALT，请将Quantity设置为“1000”；
Send({ 
	Target = ALT, 
	Action = "Transfer", 
	Recipient = AOLOTTO, 
	Quantity = "1" 
})
```
{% endcode %}

向ALT代币进程发起转账，Quantity代表您需要下注的数量，“1”代表最小的下注单位0.001 ALT，发送转账消息后，在进程或者钱包地址余额充足的情况下，将会一条是来自于ALT代币进程回复的`Debit-Notice`，和一条来自于AOLOTTO进程的`Lotto-Notice`, `Lotto-Notice`中包含了AOLOTTO为你随机选择的号码信息。若下注进程或钱包地址上ALT余额不足，ALT代币进程将会回复`Transfer-Error`信息，不会触发AOLOTTO投注。

### 2. 手选投注

```lua
Send({ 
	Target = ALT, 
	Action = "Transfer", 
	Recipient = AOLOTTO, 
	Quantity = "2",
	["X-Numbers"] = "007" -- 000-999之间的任意3位数字
})
-- 下注结果：007*2
```

发送转账时加入`X-Numbers`可以手动指定号码参与投注，号码需要符合3位数规范，非法号码系统将自动废弃并使用随机的机选号码下注。

### 3 批量投注

```lua
Send({ 
	Target = ALT, 
	Action = "Transfer", 
	Recipient = AOLOTTO, 
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
	Recipient = AOLOTTO, 
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
	Recipient = AOLOTTO, 
	Quantity = "3",
	["X-Numbers"] = "000,001,002",
	["X-Donee"] = "j0Lrrv1ltimsYnD_5f-8Fp3QKcAbUjckn7kjCZCfvhk" -- 添加受益人tag和地址，地址务必为aos process地址，AR钱包地址无法发起提取奖金的请求；
})
-- 以上投注中奖后，奖金将会分配给受益人，但投注量将会叠加到购买人信息中。
```

默认情况下，购买地址就是受益人，但是可以通过X-Donee标签添加其它地址作为中奖受益人，你可以将受益人设置为你朋友的地址，实现投注赠送。



### 6. 投注查询
