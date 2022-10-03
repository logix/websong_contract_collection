### 生气猫合约

[etherscan地址](https://etherscan.io/address/0xdcf68c8ebb18df1419c7dff17ed33505faf8a20c) 

[DETH链接](https://etherscan.deth.net/address/0xdcf68c8ebb18df1419c7dff17ed33505faf8a20c#code)

##### 要点
* 合约为通用合约，symbol在Constructor中定义可以看出；测试时可使用不同名字，避免被搜索到；
* nft合约中有预授权处理
* 通过 mintByBcn 来实现蓝筹持有主动提交蓝筹信息进行mint的操作；（该合约最大的特色）
```Solidity
function mintByBcn(uint256 tokenId, address bcn, uint256 bcnTokenId) external override{
        require(block.timestamp > uint256(_startTimes[2]), "Cat:not open");
        address to = IERC721(bcn).ownerOf(bcnTokenId);
        require(to != address(0), "ERC721W:bcnTokenId not exists");
        require(!_isTokenMintByBcn[bcn][bcnTokenId], "ERC721W:bcnTokenId is used");
        require(_supportedBcns.contains(bcn), "ERC721W:not supported bcn");
        _isTokenMintByBcn[bcn][bcnTokenId] = true;
        _remaingOfBcn[bcn]--;
        emit MintByBCN(totalSupply(), to, bcn, bcnTokenId);
        _safeMint(to, 1);
    }
```
* 开图部分使用了VRF
* 开图函数里增加了id判断
```Solidity
return _boxOffset < 10000 ? string(abi.encodePacked(_tokenUri, Strings.toString((tokenId+_boxOffset) % 10000))) : _boxUri;
```

* 他这里还有个nest的实现，是另外一个合约地址，用来控制nft转移；

