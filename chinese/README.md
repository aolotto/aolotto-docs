---
layout:
  title:
    visible: false
  description:
    visible: false
  tableOfContents:
    visible: false
  outline:
    visible: true
  pagination:
    visible: true
---

# 👋 欢迎

## 欢迎来到 aolotto

**aolotto** 是首款运行在[Arweave AO](https://ao.arweave.dev/)(统称AO)上的去中心化彩票协议，简单，透明，开放。每间隔24小时开奖一次，开奖算法采用开奖时间戳，区块哈希[^1]值以及当前轮次的累积投注量作为随机因子，生成000-999之间的任意3位数作为幸运号码，数值完全匹配的投注均分当前轮次奖池总额的50%，剩余50%转移到下一轮次作为基础奖金。

当前已开放测试网版本，支持使用**aolotto**权益代币 $ALT (altoken) 购买和参与，主网版本上线后正式切换为AO原生代币 $AO 购买参与，**aolotto**协议完全开源且归社区所有**，**70%的 $ALT 面向社区公平发行，您可以通过水龙头免费获取$ALT 参与测试。

相比传统中心化的彩票发行机构，**aolotto**返奖率高达**100%**，完全由协议算法确保投注与开奖过程中的公平性与透明性，无需担心黑箱操控。**aolotto**由ao(Arweave AO的简称) + lotto(乐透简写)组成， AO是建立在Arweave永存网络上的去中心化超级并行计算机，使用**aolotto**之前您需要了解和掌握必要的AO知识和技能：

* [AO官网](https://ao.arweave.dev/) ：AO官放网站及白皮书，了解
* AO cookbook :  新手入门AO
* Arconnect ：Arweave钱包插件
* Web AOS：AOS是用户

### 1. 投注

**当前仅支持通过AOS命令行下注**，web端应用即将推出。用户的单笔最小投注额为0.001 ALT，支持手选和机选000-999之间的任意3位数号码，无投注金额和次数上限。投注异常简单，直接向**aolotto**协议地址`wqwklmuSqSPGaeMR7dHuciyvBDtt1UjmziAoWu-pKuI`发起ALT转账即可参与最新轮次的投注。

#### 1.1 机选号码

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

向ALT代币进程发起转账，Quantity代表您需要下注的数量，“1”代表最小的下注单位0.001 ALT，发送转账消息后，在进程或者钱包地址余额充足的情况下，将会一条是来自于ALT进程回复的`Debit-Notice`，和一条来自于AOLOTTO的`Lotto-Notice`, `Lotto-Notice`中包含了AOLOTTO为你随机选择的号码信息。若下注进程或钱包地址上ALT余额不足，ALT代币进程将会回复`Transfer-Error`信息，不会触发AOLOTTO投注。

#### 1.2 自选号码

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

发送转账时加入`X-Numbers`标签可以指定特定号码参与投注，号码需要符合3位数规范，非法号码系统将自动废弃并使用随机的机选号码下注。

#### 1.3 批量投注

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

#### 1.4 区间投注

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

#### 1.5 添加受益人

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

### 2. 开奖

**aolotto**逐轮持续进行，用户下注将自动计入到当前进行的轮次中。触发器每间隔5分钟触发轮次开奖，满足如下两项条件自动开奖并切换到下一轮次，否则当前轮次继续进行：

1. **间隔时间≥24小时**，触发时间比对轮次启动时间大于等于24小时，则满足开奖的时间条件；
2. **用户投注金额≥基础奖金**，启动当前轮次时会将上一轮次的50%奖池余额计入为基础奖金，当前轮次所有用户的累积投注金额大于或等于基础奖金，则满足开奖的参与度条件；

#### 2.1 幸运号码生成

轮次结束后的第5个区块高度上触发开奖算法并生成幸运号码，幸运号码基于Issac Cipher的随机数函数生成，使用开奖区块的Hash值, 轮次累积投注人数以及数量等无法提前预知因子作为随机函数的种子输入，保证幸运号码分布的随机性，可验证性和不可预测性：

1. 不可预测性：Arweave的区块Hash是基于区块全部交易内容生成的唯一性ID，采用轮次结束后的第五个区块的hash值，意味着任何人在下注时完全无法预知。
2. 可验证性：issac cipher的随机数函数在种子确定的情况下生成的结果也是确定的，意味着通过CU节点生成的幸运号码可被验证，规避CU（计算单元）节点在执行中进行黑箱操作的可能性；
3. 取值分布的随机性：3位数号码按位置单独生成，

<details>

<summary>查看算法源码</summary>

```
// Some code
```

</details>

[^1]: 区块链哈希值是一串固定长度的字符串
