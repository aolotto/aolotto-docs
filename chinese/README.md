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

**aolotto** 是首款运行在[Arweave AO](https://ao.arweave.dev/)(统称AO)上的去中心化彩票协议，简单，透明，开放。每间隔24小时采用随机数算法开奖，随机算法采用开奖时间戳，区块哈希[^1]值以及当前轮次的累积投注量作为随机因子，生成000-999之间的任意3位数作为幸运号码，完全匹配的投注参与均分当前轮次奖池总额的50%，剩余50%转移到下一轮次作为基础奖金。

当前已开放测试网版本，支持使用**aolotto**权益代币 $ALT (altoken) 购买和参与，主网版本上线后正式切换为AO原生代币 $AO 购买参与，**aolotto**协议归社区所有**，**70%的 $ALT 面向社区发行，您可以通过水龙头免费获取$ALT。

相比传统中心化的彩票发行机构，**aolotto**完全由协议算法确保投注与开奖过程中的公平性与透明性，无需担心黑箱操控。100%返奖率，无需承担高昂的税收损耗。**aolotto**由ao(Arweave AO的简称) + lotto(乐透简写)组成， AO是建立在Arweave永存网络上的去中心化超级并行计算机，使用**aolotto**之前您需要了解和掌握必要的AO知识和技能：

* [AO官网](https://ao.arweave.dev/) ：AO官放网站及白皮书，了解
* AO cookbook :  新手入门AO
* Arconnect ：Arweave钱包插件
* Web AOS：AOS是用户

### 1. 投注

当前仅支持通过AOS命令行下注，web端应用即将推出。用户的单笔最小投注额为0.001 ALT，支持手选和机选000-999之间的任意3位数号码，无投注金额和次数上限。机选投注异常简单，直接向**aolotto**协议地址`wqwklmuSqSPGaeMR7dHuciyvBDtt1UjmziAoWu-pKuI`发起ALT转账即可参与最新轮次的投注。

#### 1.1 机选号码

```lua
AOLOTTO = "wqwklmuSqSPGaeMR7dHuciyvBDtt1UjmziAoWu-pKuI" -- 存储aolotto代理进程为全局变量
ALT_TOKEN = "Sa0iBLPNyJQrwpTTG-tWLQU-1QeUAJA73DdxGGiKoJc" -- 存储CRED代币进程为全局变量

Send({ 
	Target = ALT_TOKEN, 
	Action = "Transfer", 
	Recipient = AOLOTTO, 
	Quantity = "1" 
})
-- 发起转账，0.001 ALT为最小下注量，若需下注1 ALT，请将Quantity设置为“1000”；
```

发送以上消息将会收到两条回信，一条是来自于CRED\_PROCESS的支付单Debit-Notice，和一条来自于AOLOTTO的Lotto-Notice, Lotto-Notice中包含了AOLOTTO为你随机选择的号码信息。需要确保下注进程拥有足够的ALT余额，余额不足的情况下将会返回一条Transfer-Error信息。

#### 1.2 自选号码

{% code title="自选号码" %}
```lua
Send({ 
	Target = ALT_TOKEN, 
	Action = "Transfer", 
	Recipient = AOLOTTO, 
	Quantity = "2",
	["X-Numbers"] = "007" -- 
})
-- 下注结果：007*2
```
{% endcode %}

发送转账时加入X-Numbers标签可以指定特定号码参与投注，号码需要符合3位数规范，输入非法号码系统将废弃并使用随机的机选号码下注。

#### 1.3 批量投注

```lua
Send({ 
	Target = ALT_TOKEN, 
	Action = "Transfer", 
	Recipient = AOLOTTO, 
	Quantity = "3",
	["X-Numbers"] = "000,001,002" -- 不同号码之间使用","间隔，若号码数量超过投注数量，自动过滤溢出号码
})
-- 下注结果：000*1，001*1, 002*1
```

#### 1.4 区间投注

```lua
Send({ 
	Target = ALT_TOKEN, 
	Action = "Transfer", 
	Recipient = AOLOTTO, 
	Quantity = "10",
	["X-Numbers"] = "000-009" -- “-”代表取值区间，讲生成起始号码和结束号码之间的序列号码，号码数量超过投注数量自动过滤溢出部分；
})
-- 下注结果：000*1，001*1, 002*1, 003*1, 004*1, 005*1, 006*1, 007*1, 008*1, 009*1   
```

通过区间投注用户可以通过一笔转账生成一个区间序列数值的投注，如上列代码所示。

#### 1.5 添加受益人

```lua
Send({ 
	Target = ALT_TOKEN, 
	Action = "Transfer", 
	Recipient = AOLOTTO, 
	Quantity = "3",
	["X-Numbers"] = "000,001,002",
	["X-Donee"] = "j0Lrrv1ltimsYnD_5f-8Fp3QKcAbUjckn7kjCZCfvhk" -- 添加受益人tag和地址，地址务必为aos process地址，AR钱包地址无法发起提取奖金的请求；
})
```

默认情况下，投注地址就是受益人，但是可以通过X-Donee标签添加其它地址作为中奖受益人，你可以将受益人设置为你朋友的地址，实现投注赠送。

### 2. 开奖

[^1]: 区块链哈希值是一串固定长度的字符串
