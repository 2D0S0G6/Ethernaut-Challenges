# LEVEL 0 HELLO ETHERNAUT

 ---> Hope you have got your metamask wallet set with sepolia ether

## So let's get started

 ---> If you want to view the functions defined in the contract you have to use

``` 
await contract.abi();
```

 --->  "await" pauses the execution of the async function until the Promise is resolved or rejected

 ---> Now give the command

 ```
await contract.info()
 ```

 ---> You can see the message "You will find what you need in info1()."

 ---> So now you have to call info1() with the command

 ```
await contract.info1()
 ```

 ---> You can see the message Try info2(), but with "hello" as a parameter.'

 --->As mentioned in the last hint message we can give

 ```
await contract.info2("hello");
 ```

 ---> You can get a message "The property infoNum holds the number of the next info method to call.".So according to this we can now call infoNum()

```
await contract.infoNum
```

 ---> So we get 42 and now we can call info42()

 ```
await contract.info42()
 ```

 -->Now you get a message called 'theMethodName is the name of the next method.'So in contract.abi we can seea function called password.We are gonna call it using 

 ```
await contract.password();
```

 --->Now you get can see the password as 'ethernaut0'.So use the authenticate function to get the level done

```
await contract.authenticate('ethernaut0');
```
---> Submit the instance.
## THANK YOU !!!
