#### Twitter Scan Pass

[合约地址](https://etherscan.io/address/0xd9372167ef419cfbbcd6483603ad15976364e557)

[Deth地址](https://etherscan.deth.net/token/0xd9372167ef419cfbbcd6483603ad15976364e557#code)


##### 合约要点
* 1967透明代理结构
* conf.refundStarId里有指定可以退款的起始id， >6500是公售的部分； 退款在refund函数中实现
* 非721A，所以在mint多个时，gas fee成倍增长；（通常mint 2个，32w+gas）
* 可以控制nft转移开关，但没有预授权；
* 实现burn接口
* 有实现购买时退回多余的钱；
