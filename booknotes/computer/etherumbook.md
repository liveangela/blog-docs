---
description: 以太坊入门书籍，涉及所有概念，小白必备
---

# 《Ethereumbook》

线上阅读：[地址](https://github.com/ethereumbook/ethereumbook)

### 摘抄节选

#### 06 transactions

交易本身才是整个以太坊的触发器。[引自](https://github.com/ethereumbook/ethereumbook/blob/develop/06transactions.asciidoc#transactions)

> Another way to look at `transactions` is that they are the only things that can trigger a change of state, or cause a contract to execute in the EVM.

以太坊就是个全局单例的状态机，通过交易来触发状态变更。引自（同上）

> Ethereum is a `global singleton state machine`, and `transactions` are what make that state machine "tick," changing its state.

以太坊无法验证目标地址正确性，以太币被允许发给错误/无效的地址，从而消耗掉以太币，原因是目标地址没有对应的私钥和数字签名来使用所获得的这些币。[引自](https://github.com/ethereumbook/ethereumbook/blob/develop/06transactions.asciidoc#transaction-recipient)

> The Ethereum protocol does not validate recipient addresses in transactions. You can send to an address that has no corresponding private key or contract, thereby "burning" the ether, rendering it forever unspendable.

对交易采用数字签名的作用有三点：证明拥有该私钥、证明是自己干的，无法抵赖、无法串改。[引自](https://github.com/ethereumbook/ethereumbook/blob/develop/06transactions.asciidoc#the-elliptic-curve-digital-signature-algorithm)

> A digital signature serves three purposes in Ethereum
>
> 1. First, the signature proves that the owner of the private key, who is by implication the owner of an Ethereum account, has authorized the spending of ether, or execution of a contract. 
> 2. Secondly, it guarantees non-repudiation: the proof of authorization is undeniable.
> 3. Thirdly, the signature proves that the transaction data has not been and cannot be modified by anyone after the transaction has been signed.

#### 07 smart-contracts

智能合约没有私钥，一旦部署就进入自我管理模式。[引自](https://github.com/ethereumbook/ethereumbook/blob/develop/07smart-contracts-solidity.asciidoc#life-cycle-of-a-smart-contract)

> You certainly don’t receive the private key for the contract account, which in fact does not exist—we can say that smart contract accounts own themselves.

智能合约不能并发，因为以太坊是单线程状态机的缘故。引自（同上）

> It is also worth noting that smart contracts are not executed "in parallel" in any sense—the Ethereum world computer can be considered to be a single-threaded machine.

### 理解

{% hint style="info" %}
一个txn的全生命周期，主要包括：

1. creation
2. signature
3. transmission/propagation
4. validation
5. record on the blockchain
{% endhint %}

{% hint style="info" %}
智能合约一旦部署，无法修改，运行逻辑展示在大家眼前（明牌式打法），所以可以使得赌博、博彩等更加公平。唯一的问题来源于赌博的标的是否受人控制，如赌BTC的涨跌，实际上庄家是可以操控的
{% endhint %}

{% hint style="info" %}
要安全完善地开发智能合约，最好地办法就是复用已有的、充分测试的开源合约，比如[openzeppelin](https://openzeppelin.com/contracts/)
{% endhint %}

### 答疑

* [ ] 虚拟币交易所生成的公私钥是否安全？
  * 比如在huobi上获取了一个公钥地址，然后进行一次交易，成功，这时私钥在哪里？
  * 每次需要转入时，都要获取一次公钥地址，如果变更，会导致之前给别人的地址无效？
  * 由于不知道私钥，如果该交易所关停，那么里面的钱全拿不出来来？
* 解答：



* [ ] EVM是跑在每个以太坊的节点上的，如何保证不被节点人为篡改？
  * 是不是改了之后计算获得的结果和其他节点都不一样，所以无法被接受，改了也白改？
  * 如果51%的节点都做同样的修改了呢？
* 解答：



* [x] 如何开发并发布一个合约？
* 最简单的是纯线上的方式，大概分为以下几个步骤：
  1. 去github上抄一个想要的类似功能的合约，尽量用openzeppelin等第三方作为代码基础
  2. 去remix上在线编辑一下，并编译好（remix中可直接import远程文件，如[这样](https://github.com/OpenZeppelin/openzeppelin-contracts/contracts/access/Ownable.sol)）
  3. 通过metamask发布出去
* 如果是本地开发，则貌似需要用到很多npm包，考虑使用truffle team的全家桶

