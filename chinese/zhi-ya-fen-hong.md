# 质押分红

Aolotto协议总销售额的20%（即累计利润的50%）用于质押分红，每日Aolotto协议的销售新增将于次日00:00(GMT)按照质押者的锁仓$ALT(veALT)占比进行分配，veALT是一种不具备转账属性，并线性衰减的权益性代币，veALT参照veCRV设计，它是一种为**协调治理激励而创建的概念，**&#x8FD9;和普通的流通性代币略有不&#x540C;**。**

用户锁定ALT获得veALT, 不仅可以赚取协议的持续分红，同时还能获得去中心化治理中的投票权益， 当用户参与链上提案的投票时，veALT的数量直接代表了投票权重。

## veALT — 锁仓$ALT

用户将$ALT存入质押合约（CA：）后会得到相应比例的锁仓ALT(veALT, vote-escrowed ALT), 锁仓周期最短为1周(7天)，最长为4年(1440天)，锁定周期越长，得到的veALT就越多，具体参照锁仓公式, 以下举例帮助你简单理解：

* 1 ALT 锁仓 4 年 = 1 veALT
* 1 ALT锁仓 3 年 = 0.75 veALT
* 1 ALT 锁仓 2 年 = 0.5 veALT
* 1 ALT 锁仓 1 年 = 0.25 veALT

#### 锁仓公式

$$veALT = ALT * min(LockDaysLeft / 1440 days,1)$$

1. 锁定周期最长为4年（1440天），超过最长锁定周期的汇率会保持为1ALT : 1veALT;
2. 最短锁定周期为1周（7天），协议不接受小于最小锁定周期的质押申请；

#### veALT衰减

用户拥有的 veCRV 数量将随着时间的推移而逐日衰减，对应锁仓公式中的`lockDaysLeft` , 衰减算法每日运行一次，每日分红是按照衰减前的veALT数量进行计算，具体的流程为质押合约每日GMT 00:00（实际执行时间可能存在几分钟的偏差，但计算依据为每日的整点时间）结算分红，分红完成后执行衰减函数，用户的veALT数量将被算法更新。以下以1枚ALT质押7天进行说明：

* 1枚ALT锁仓剩余7天 = 0.00486 veALT
* 1枚ALT锁仓剩余6天 = 0.00417 veALT
* ...
* 1枚ALT锁仓剩余1天 = 0.0007 veALT
* 1枚ALT锁仓剩余0天 = 0 veALT

#### 延长锁仓

用户可以延长锁仓从而增加结算时的锁仓的剩余时间，如果 Bob 锁定了 100 ALT 4 年，那么 3 年后她就只剩下 25 veALT，因为她的锁仓剩余时间是 1 年。如果她在 3 年后再次将锁定时间延长至 4 年，她将再次拥有 100 veALT：

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

#### 增加锁仓数量

将 ALT 添加到锁仓意味着解锁日期将保持不变，但锁定的ALT的数量提升，意味着更多的 veALT。例如Bob 锁定了 100 ALT 4 年，但 2 年后又将 200 ALT 添加到她的锁定中，她将获得 150 veALT（2 年内总共锁定 300 CRV）。在接下来的 2 年里，这个 veALT 将继续衰减至 0

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

#### 解除质押

ALT一旦锁仓为veALT，只能在锁定时间到期后才能解除质押，用户发起质押解除后质押协议将按照用户实际的质押数量退还ALT。



质押受益人

通常情况下，用户添加锁仓时，所获得的veALT为用户自己, 即质押者 = 受益人，但用户可以更改受益人为其他人，veALT将添加到受益人账户。衰减

## 通过ALC提升锁仓汇率

ALC(AolottoLuckyClover)是由AolottoFoundation发行的系列NFTs，ALC NFT在Aolotto生态中不仅是身份象征，还能解锁特殊权益，当用户在质押ALT的基础上叠加一枚ALC，可以获得更高的锁仓汇率，例如Bob锁仓100枚ALT 4年，获得100veALT, 叠加一枚ALC即可获得120veALT;

不同类型的ALC对应的提升比例不同，参照下表：

<table><thead><tr><th>ALC类型</th><th width="181.43359375">CA</th><th data-type="number">发行总量</th><th width="111.7109375">提升比率</th><th>获取方式</th></tr></thead><tbody><tr><td>AolottoLuckyClover - OG Edition</td><td>PURLGdY5k7ujpBM_j_5XkKbnE9Rv9ta8cr7EOPWYRqk</td><td>5000</td><td>0.2</td><td>aopump, bazar</td></tr></tbody></table>



## 每日分红

分红是按照用户最新的veALT数量与veALT总量的占比进行分配，例如Bob最新的veALT余额为100，veALT总量为10000，Bob占据总量的1%， 当日分红金额为100美金，Bob当日所获得的分红为1美金；

### 分红来源

分红来源于彩票协议的销售利润，及协议累计销售额的20%，以及未来LottoFi生态产生的额外收益，分红以美金结算，分发的资产为AOX发行的跨链USDC （wUSDC）, CA：

### 提现

每日结算后的分红将会自动添加的质押受益人的账户中，用户需手工提取到钱包，单次最下提取金额不小于$1美金；



## 质押驱动LottoFi

## 链上治理

* veALT 余额代表用户在 Aolotto DAO 中的投票权，这使得他们能够**对链上提案进行投票**。
* 此外，Aolotto 治理的一个关键部分是**权重投票**。未来LottoFi生态中的。通过成功通过的 DAO 投票，Curve 上的流动性池可以添加到 GaugeController，使其有资格接收 CRV 代币发行。权重决定每个池收到多少 CRV。每周**四 00:00 UTC**都会应用更新后的权重。有关[投票](https://resources.curve.fi/governance/voting/)和[权重的更多信息](https://resources.curve.fi/reward-gauges/gauge-weights/)





