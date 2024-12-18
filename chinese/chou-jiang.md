# 🌟 开奖 & 规则

通常情况下，每一轮投注的开放时间为24小时，该轮次的投注率需要大于等于100%才具备开奖条件，奖池的定时触发器每2分钟检查一次，具备开奖条件的轮次将会自动结束，同时启动新的投注轮次。

1. **开放时间≥24小时**，定时器时间戳和轮次启动时间戳的差值需要大于等于24小时；
2. **投注率≥100%**，每一轮投注启动时都会将前一轮预留的50%计为基础奖金，投注率 = 用户累计投注额 / 基础奖金 \* 100%；

### 轮次切换

综上所述，轮次的投注率不一定能在预期的时间内到达100%，开放时间超过24小时后，轮次切换会存在如下3种结果：

1. 开放时间超过24小时，投注率满足开奖条件将会立即启动下一轮次，并归档当前轮次的投注记录，等待开奖；
2. 开放时间超过24小时，但投注率不满足开奖条件，当前轮次将会继续开放接受新的投注，直到投注&#x7387;**≥100% ;**
3. 开放时间超过168小时，投注率依然小于100%的轮次会被强行取消，由于不满足开奖条件，本轮所有投注金将会原路退还用户，该轮次的基础奖金转移到下一轮次。

### 开奖&幸运号码

轮次结束后的第5个区块高度上开奖并生成幸运号码，幸运号码基于Issac Cipher的随机数函数生成，使用开奖区块的Hash值, 轮次累积投注人数以及数量等无法提前预知因子作为随机函数的种子输入，保证幸运号码生成具有随机性，可验证性和不可预测性：

1. 不可预测性：Arweave的区块Hash是基于区块全部交易内容生成的唯一性ID，采用轮次结束后的第5个区块的hash，意味着任何人在下注期间完全无法预知开奖算法的种子。
2. 可验证性：issac cipher的随机数函数在种子确定的情况下生成的结果也是确定的，意味着通过CU节点生成的幸运号码可被验证，规避CU（计算单元）节点在执行中进行黑箱操作的可能性；
3. 取值分布的随机性：3位数号码并非一次性生成，而是逐位调用随机函数，将统一的种子和位置编号作为输入，分别生成0-9之间的随机数值，保证了3位数号码取值分布的随机性。

<details>

<summary>幸运号码生成算法示例</summary>

```lua
--[[
  开奖算法的种子由如下信息链接在一起的字符串：
  ao.id: 奖池进程的唯一性id；
  Block.Hash: 区块hash值是基于区块全部交易内容生成的固定长度的hash字符串
  Round.no: 当前的轮次编号
  Round.TotalBets：当前轮次累积投注数量
  Round.Participator: 当前轮次累积参与投注的地址数量，
]]--
local seed = ao.id..Block.Hash..Round.no..Round.TotalBets..Round.Participator

--[[
  开奖随机算法依次计算不同位置的数值，取值范围是0-9，不同位置的数值在相同种子基础上叠加了位置编号以及前一位数的结果。
]]--
local getLuckyNumber = function(seed,len)
  local numbers = ""
  for i = 1, len or 3 do
    local n = crypto.cipher.issac.random(0, 9, tostring(i)..seed..numbers)
    numbers = numbers .. n
  end
  return numbers
end

local luckyNumber = getLuckyNumber(seed,3)

```

</details>

### 奖金分发

轮次结束后，奖池总额的50%计入下一轮次，所以实发奖金是奖池总额的50%，具体的计算公式如下：实发奖金 = （基础奖金 + 用户投注金额）\* 0.5 .幸运号码生成后，开奖器检查轮次中的投注记录，号码完全匹配的投注为中奖投注：

1. **中奖投注<1**, 当前轮次无人中奖，奖金将均分给奖池中所有轮次的参与者，按照参与者累积的投注数量占比平均分配，参与者实得奖金 = 奖金 / 累积历史投注总量 \* 个人累积投注总量。
2. **中奖投注≥1,** 拥有中奖投注的中奖者均分奖金，中奖者实得奖金 = 奖金 / 总奖投注总量 \* 个人中奖投注量。

不满足开奖条件而被强行取消的轮次，参与者投注金原路退返，不在上述描述的规则中。

### 查询开奖结果

中奖者在开奖后将会收到由奖池进程下发的Win-Notice, 使用Inbox\[#Inbox].Data打印消息正文查看具体的中奖额度。错过消息，可以通过查询指令查询轮次的开奖结果。

```lua
Send({Target=POOL,Action="Winners",Round="1"})
-- 将Round替换为您想查询的轮次编号
```

同时也可以关注Aolotto官方Discord, 实时获得最新的开奖公告。
