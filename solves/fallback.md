# FALLBACK

## Hope you have solved level 0,So now let's dive into  level 1

### THE EXPLOIT

The Fallback contract has a vulnerability related to the ownership transfer mechanism, specifically in the receive() function. This function allows any user who sends Ether directly to the contract to become the new owner, provided that the sender has made a contribution before. The issue arises because the receive() function does not verify the sender's contribution amount relative to the current owner's contributions; it only checks if the sender has contributed anything at all. As a result, someone can become the owner by simply sending a small amount of Ether directly to the contract using your metamask wallet, bypassing the contribute() function's contribution limits and logic.

so for this follow the commands

first we will know the contribution

```
fromWei(await contract.getContribution());
```

---> fromWei is a function commonly used in Ethereum development to convert values from Wei (the smallest unit of Ether) to Ether.1 ether = 10^18 wei.

---> We can see the contribution as 0.So we need to contribute to get our address in the contribution list

```
await contract.contribute({value:toWei("0.0001")})
```
---> Now if you give the previous command we can know that our contribution has increased

---> Now we have to increase our contribution to such a level that we can gain ownership of the contract and withdraw the contract fund

---> For this we can make use of the fallback function "receive" which also gives ownership based on some requirements.Send a small amount say 0.00001 ether and now you can be the owner

--> Now call the withdraw function

```
await contract.getBalance();
```
## KABOOOOOOMMMM !! YOU HAVE BREACHED THIS LEVEL.THANK YOU !!







