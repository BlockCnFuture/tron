#### 本服务基于 波场(Tron) TRC20网络

## 名词介绍
---
### 钱包
指虚拟货币钱包，又称 地址，其在区块链存在资产信息
### 归集
指将多个新地址内的U，转到指定地址，小钱汇大钱
### USDT
是一种价格稳定的虚拟货币，其价格对标美元，是主流稳定币之一
### TRC20
指TRC20提币网络，本服务只监听TRC20网络的USDT转账事件
### 能量
利用tron进行各种交易都需要消耗能量，目前，1能量=15TRX  
本服务能量不足时，则消耗TRX抵押能量，此时，基础手续费将非常高  
USDT转账操作便需要消耗能量，而本服务的归集操作需要两次转账  
一次向目标归集地址转账实现归集，一次向本服务地址转账收取手续费  
与此同时，本系统自动将U闪兑为TRX来补充转账消耗时也要能量
### TRX 
是交易能量不足时，消耗的一种虚拟货币，每次交易的消耗量都不同   
本服务进行交易时，优先消耗能量来进行交易，能量不足再消耗TRX  
当本服务能量充足时，无需消耗TRX，基础手续费将非常低

## 支持功能
---
```js
新钱包地址生成
新钱包TRC20 USDT转账监控通知
USDT自动归集
USDT手动归集
USDT归集结果通知
```
## 应用场景
---
```js
客户下单购买商品 -> 生成新地址(钱包) -> 客户由TRC20网络向新地址转U -> 本服务监听到转账事件，异步通知预设的notifyurl，并开始尝试自动归集 -> 商品平台检查客户发送U的数量是否符合要求 -> 交易完成

在上面的整个交易流程当中，每次下单都生成新地址(钱包)，每一个新地址(钱包)都对应一个客户，等待客户向地址转U
交易完成后，该地址(钱包)将被弃用，本服务将删除它的记录，整个交易过程都不会泄露个人隐私，属于匿名化交易
与此同时，USDT是一种全球化的、价格稳定的数字货币，在任何存在虚拟币交易所的国家均可使用，有利于平台的国际化
```
本服务归集功能需耗时约3-4分钟

## 归集服务
---
- 归集目标地址在生成新钱包时设置
- 服务自动计算手续费所需TRX数量，而非固定值，确保归集成功
- 若服务归集失败，可用privatekey自行归集，确保资金安全
- 归集成功消耗的TRX由本服务提供，但会收取新钱包等额的U来偿还
- 偿还TRX的U是基础手续费，具体数量取决于交易消耗，是变化的
- 本服务收到偿还TRX的U后，会自动将U闪兑为TRX，确保服务正常运行

## 手续费问题
---
### 本服务收取多少手续费
本服务手续费分为：基础手续费+额外手续费，基础手续费是动态计算的  
基础手续费在服务能量充足时，是能量不足时手续费的20%  
本服务每次归集成功，收取1U额外手续费，大于300U则收取1%额外手续费  
若新钱包无法支付手续费，则自动归集会失败，且不会收取任何费用  
用户自行归集时，本服务不消耗任何资源，因此也不收取任何相关费用

### 如何免除额外手续费
可联系我定制私人专用的服务端，自行提供手续费地址来支撑TRX消耗并固定归集地址  
整个过程只需一次智能合约：把新地址的U转账给固定的归集地址，大幅减少基础手续费  
私人定制的服务端需要商户自己购买服务器来运行，且由于只为自用，故无需额外手续费  
由于手续费地址需要向新地址转TRX，所以需要提供手续费地址的私钥，归集地址无需私钥  
定制联系方式(打开需要梯子)：[https://t.me/AutoUSDT2TRX0](https://t.me/AutoUSDT2TRX0)

## 其他项目
---
### telegram自动兑币机器人
tron网络 USDT2TRX、TRX2USDT，无需额外准备大量USDT/TRX，设置费率后，收到U/T便自动扣除手续费并调用SunSwap进行闪兑  
通过租用足够的能量以及设置足够的费率谋取差价，以量换利，定制联系方式(打开需要梯子)：[https://t.me/AutoUSDT2TRX0](https://t.me/AutoUSDT2TRX0)
