# Tony's(aka CourtSide) Quest Submissions

## Chapter 1 - Day 1

-Q:  Explain what the Blockchain is in your own words.

A:  The Blockchain is an online database that permanently stores information strung across a timeline. It is open and available to everyone as well as decentralized ( not controlled by any single entity).

-Q:  Explain what a Smart Contract is.

A:  A Smart Contract is a digital intermediary between two parties that accomplishes a specific task within a set of guidelines. It is created by developers to ensure trust and transparency for the participating parties, but not without risks of developer mistakes.

-Q:  Explain the difference between a script and a transaction.

A:  A script is a procedure that only reads information from the blockcahin, whereas a transaction is a procedure that changes the state of the blockchain.

## Chapter 1 - Day 2
 -Q: What are the 5 Cadence Programming Language Pillars?
 
 A: 1)Safety and Security
    2)Clarity
     3)Approachability
     4)Developer Experience
     5)Resource Oriented Programming
     
  -Q: In your opinion, even without knowing anything about the Blockchain or coding, why could the 5 Pillars be useful (you don't have to answer this for #5)?
 
 A:  1- As noted previously, the biggest security risk in smart contracts is with the development of the smart contracts themselves. Keeping safety and security as a pillar for Cadence helps to prevent that inherent risk for disciplined developers.
    2- Clarity is useful for the users to understand the smart contracts that they are signing. In a physical representation, a User should be able to read the entirety of the contract they sign. It should be no different in a digital form.
    3- Approachability helps ease the transition for qualified developers and as a result promotes faster growth and rentention for the system.
    4- The developer experience helps to reduce wasted time and allows faster response rates to known issues.

## Chapter 2 - Day 1
```Cadence
pub contract JacobTucker{

pub let is: String

init(){
  self.is = "the best"
  }
}
```
![Screenshot (350)](https://user-images.githubusercontent.com/93283651/178340892-9a80e24a-43fe-4ef3-bd0c-f356c20e93d1.png)

## Chapter 2 - Day 2

-Q: Explain why we wouldn't call changeGreeting in a script.

 A: A script only reads the information on the blockchain, so we would not have the capability of changing the greeting while running a script.

 -Q: What does the AuthAccount mean in the prepare phase of the transaction?
 
  A: The AuthAccount is the address of the party that is initializing the transaction and granting permission to access data.
  
  -Q:What is the difference between the prepare phase and the execute phase in the transaction?
  
  A: The prepare phase is used to access data in the authorizers account, while the execute phase is used to call functions that change/modify the data in the
  account.

```Cadence
pub contract JacobTucker{

pub let is: String
pub var myNumber: Int

init(){
  self.is = "the best"
  self.myNumber = 0
  }

pub fun updateMyNumber(newNumber: Int){
  self.myNumber = newNumber
}
}
```
```Cadence
import HelloWorld from 0x01

transaction(myNewGreeting: String){
  prepare(signer: AuthAccount){
  
  }
  execute{
    HelloWorld.changeGreeting(newGreeting: myNewGreeting)
  }
}
```
![chp2_day2](https://user-images.githubusercontent.com/93283651/178354073-64a711bc-4149-401b-a4de-a1b7539abb45.JPG)

