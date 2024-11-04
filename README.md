# PandaTool 智能合约源码
PandaTool作为全网最强的一键发币平台，在EVM链拥有最多的合约机制。每一个智能合约的玩法、写法都不尽相同，现在，我们将这些合约源码统一上传至Github。尽管PandaTool的代币合约本身就是在浏览器开源的，但考虑到很多开发者获取困难的缘故，我们现在将代码放在这里，以方便各位参考学习。

需要注意的是，这个世界上没有百分百完美的代码。尤其是Solidity这种并不是非常大众的语言，可能还会有很多未知的问题存在。管PandaTool的技术团队也一直在不断的对代码进行优化，后续所有新的合约以及更新，都会同步更新在这里

## BSC合约介绍
[stardand](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/BSC/stardand)：标准的BEP20合约，干净、无任何功能，无权限

[holdreflection](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/BSC/holdreflection)：具有持币分红本币、交易销毁等功能，无权限、合约干净

[314protocol](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/BSC/314protocol)：314协议，转账即交易，具有交易冷却防夹功能

[lpreflection](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/BSC/lpreflection)：LP分红模式，加池可以分任何代币，同时具备销毁回流、黑/白名单、交易空投等

[holdwithinviter](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/BSC/holdwithinviter)：持币复利+推荐奖励，以增发的方式实现持币生息的功能，且具有上下级

[Mint+lpburn](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/BSC/lpburn)：Mint+底池燃烧，以转账的方式实现Mint预售、底池内代币定时燃烧销毁，来提升币价

[Mint+holdothers](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/BSC/mint%2Bholdothers):Mint+持币分红，以转账的方式实现Mint预售，同时实现持币分其他币（非本币）

[lpmine](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/BSC/lpmine)：LP挖矿模式，全网独创。持有Lp开启挖矿，合约自动运行，有交易即可获得挖矿奖励

## ETH合约介绍
[stardand](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/ETH/stardand)：标准的ERC20合约，干净、无任何功能，无权限

## BASE合约介绍
[stardand](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/Base/stardand)：标准的ERC20合约，干净、无任何功能，无权限

## Arbitrum合约介绍
[stardand](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/Arbitrum/stardand)：标准的ERC20合约，干净、无任何功能，无权限

## Polygon合约介绍
[stardand](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/Polygon/stardand)：标准的ERC20合约，干净、无任何功能，无权限

## TRON合约介绍
[stardand](https://github.com/pandatoolcode/Token-Smart-Contracts/blob/main/TRON/stardand)：波场链标准的TRC20合约，干净、无任何功能，无权限
