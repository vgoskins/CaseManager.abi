You must have ETH in your affiliate address already send a little bit to your affiliate address, if you do not have any. .02 ETH is enough.

Go here: https://www.myetherwallet.com/#contracts

make sure your "Gas Price" is acceptable, 23 Gwei should be fine. if you get out of gas errors in the final steps, increase this value and try the step again

Current Contract address is (it can change, verify first): 0x0099d8Fb5Cc46fF5b04Ee3BA2f6112ff4271A0D7

ABI / JSON Interface can be found here https://raw.githubusercontent.com/vgoskins/CaseManager.abi/master/CaseManager.abi copy and paste into box

![](https://mcmxi.media/i/l2054d46.png)

Press "Access" button
![](https://mcmxi.media/i/l2055ac7.png)

Select affiliateBalances function from the drop down and enter your affiliate address, then select READ ![](https://mcmxi.media/i/l205697d.png)

Your balance shows up in the uint256 box, copy paste this somewhere 
![](https://mcmxi.media/i/l20577f7.png)

select affiliateWithdraw
![](https://mcmxi.media/i/l205848c.png)

Paste the number returned from affiliateBalances in the weiAmount box
![](https://mcmxi.media/i/l2059fd8.png)

Open your wallet in the box below (directions depend on your wallet type)
![](https://mcmxi.media/i/l20605d8.png)

Press "Write"
![](https://mcmxi.media/i/l2061506.png)

Press "Generate Transaction". the prefilled values here should be fine. 
![](https://mcmxi.media/i/l20629e7.png)

Press "yes im sure" 
![](https://mcmxi.media/i/l206395d.png)

View your transaction on Etherscan 
![](https://mcmxi.media/i/l2064240.png)

Wait for the Transaction to confirm and you will have the Ether earned from your affiliate transactions in your wallet
