# BSC-contract

Lost Coin:

Through continuous wear and tear and continuous consumption in transactions, the currency will increase it's value

There are currently two wear methods available, and the team can set the parameter:

1.Linear wear: According to the percentage of the transaction volume, generally around 0.01% ~ 1%

2.Large amount of wear and tear: The larger the transaction amount, the greater the wear and tear. The maximum wear amount of a single transaction is 20%. For example, if you transfer 100 million, there will be 20% wear and tear.

We can precisely control the transfer loss, and can effectively overcome the effect of the big player. The wear and tear of the small player is smaller, allowing more people to participate.

The owner of this contract can then be transferred to a multi-signature wallet, so organization can control the wear factor together.

Lost coin has been deployed on Binance Smart Chain and add 90% of total amount liquidity has been added into [PancakeSwap](https://exchange.pancakeswap.finance/),

Contract address: 0x865514DC562579d2e93B62800AdC080A60753438

45% liquidity in USDT/LOST pair,and 45% of total amount liquidity in BNB/LOST pair.

total amount: 1 quadrillion (10^15)

Current wear mode :2, wear rate value: 100, wear starting at : 10000 LOST( >200M LOST single transaction will lost 20% max)

deployed at:

https://bscscan.com/address/0x865514DC562579d2e93B62800AdC080A60753438#code

Discord: https://discord.gg/qcyBxDFstT  

Telegram: https://t.me/lostcoin_1

-----------
Chinese:

Lost 磨损币：

通过在交易中不断磨损，不断消耗，从而使得币增值

目前提供两种磨损方式，团队可以进行设置：

1.线性磨损 ：按交易额的百分比，一般在万分之一左右

2.大额磨损：交易额越大，磨损越大，单笔交易最高为20%，例如：转账1个亿，会有20%的磨损。

Lost 币已发布在 BSC ，已经将90%部分流动性注入到 [PancakeSwap](https://exchange.pancakeswap.finance/)，

合约地址：0x865514DC562579d2e93B62800AdC080A60753438

45% 总量 USDT/LOST 交易对, 45% 总量流动性在 BNB/LOST 交易对.

总量1千万亿

当前磨损模式 2，磨损率值：100 ，磨损起始额度：10000 （单笔转账超过10000LOST开始磨损，在2亿左右达到最大值 20% 磨损率）

Discord: https://discord.gg/qcyBxDFstT

Telegram: https://t.me/lostcoin_1


main code:

```

function _transfer(address sender, address recipient, uint256 amount) internal {
    require(sender != address(0), "BEP20: transfer from the zero address");
    require(recipient != address(0), "BEP20: transfer to the zero address");
    
    _balances[sender] = _balances[sender].sub(amount, "BEP20: transfer amount exceeds balance");
    uint256 amount0 = amount;
    
    if(_lostType==1){
        if(_lostRate != 100000){
            amount = amount.mul(_lostRate).div(100000);
            require(amount0>=amount,"lost overflow");
            _totalSupply -= amount0 - amount;
        }
    }else if (_lostType==2){
        if (amount > _lostStart ){
            //_lostRate should 100 ,0.01%
            uint256 fix1000 = amount.mul( _lostRate ).div(100000);
            if (fix1000> (20000)){
                fix1000 = (20000);
            }
            amount = amount.mul(100000 - fix1000).div(100000);
            require(amount0>=amount,"lost overflow 2");
            _totalSupply -= amount0 - amount;
        }
    }
    _balances[recipient] = _balances[recipient].add(amount) ;
    emit Transfer(sender, recipient, amount);
  }
```
