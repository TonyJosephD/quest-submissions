# Tony(aka CourtSide) Quest Submissions

## Chapter 1 - Day 1

-Q:  Explain what the Blockchain is in your own words.

A:  The Blockchain is an online database that permanently stores information strung across a timeline. It is open and available to everyone as well as decentralized ( not controlled by any single entity).

-Q:  Explain what a Smart Contract is.

A:  A Smart Contract is a digital intermediary between two parties that accomplishes a specific task within a set of guidelines. It is created by developers to ensure trust and transparency for the participating parties, but not without risks of developer mistakes.

-Q:  Explain the difference between a script and a transaction.

A:  A script is a procedure that only reads information from the blockcahin and is free, whereas a transaction is a procedure that changes the state of the blockchain and costs a fee(gas).

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
import JacobTucker from 0x03

transaction(myNewNumber: Int){
prepare(signer: AuthAccount){

}
execute{
    JacobTucker.updateMyNumber(newNumber: myNewNumber)
}

}
```
![chp2_day2](https://user-images.githubusercontent.com/93283651/178354073-64a711bc-4149-401b-a4de-a1b7539abb45.JPG)

## Chapter 2 - Day 3

Q1: In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.
Q2: In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!

A1+2:

```Cadence
pub fun main(){

var favPeople: [String] = ["Me", "Myself", "I"]
var socialMedia: {String : UInt64} = {"Twitter" : 1, "YouTube" : 2, "LinkedIn" : 3, "Facebook" : 4, "Instagram" : 5} 

log(favPeople)
}
```
Q3: Explain what the force unwrap operator ! does, with an example different from the one I showed you (you can just change the type).

A3: 

```Cadence
// Declare an Optional Type. This type can either be UInt64 or Nil. All optional types can be either Nil or the
// type that we specify. In this case we specify a UInt64
var myNumber: UInt64? = 5 

// The force unwrap operator "!" indicates that we want the specified type(that's not Nil) from the
// optional.
var whoseNumber: UInt64 = myNumber! 
```

Q4: Explain from image
What the error message means
Why we're getting this error
How to fix it

A4: The error message "mismatched types. expected String got String?" means that you are indicating you are going to return a String type, but are actually returning an optional type. You get this error for two reasons: 1) You have accessed an element inside a dictionary and dictionaries will always return an optional type. 2) After accessing the dictionaries optional type, you have not used the force unwrap operator "!". You can fix it in one of two ways: 1) Use the force unwrap operator "!", after the element in the return statement. 2) Change the return type to "String?" in the function declaration.

## Chapter 2 - Day 4

Questions: 
 
Deploy a new contract that has a Struct of your choosing inside of it (must be different than Profile).

Create a dictionary or array that contains the Struct you defined.

Create a function to add to that array/dictionary.

Add a transaction to call that function in step 3.

Add a script to read the Struct you defined.

Answers:

```Cadence
pub contract info {

  pub var families: {String: Family}

  init(){
  self.families = {}
  }

  pub struct Family {

    pub let lastName: String
    pub let sisters: UInt64
    pub let brothers: UInt64
    pub let children: UInt64
    pub let spouse: Bool

    init(lastName: String, sisters: UInt64, brothers: UInt64, children: UInt64, spouse: Bool){
    self.lastName = lastName
    self.sisters = sisters
    self.brothers = brothers
    self.children = children
    self.spouse = spouse
    }
  }
 
 pub fun addFamily(lastName: String, sisters: UInt64, brothers: UInt64, children: UInt64, spouse: Bool){
  let newFamily = Family(lastName: lastName, sisters: sisters, brothers: brothers, children: children, spouse: spouse)
  self.families[lastName] = newFamily
 }


}
```

```Cadence
import info from 0x02

transaction(lastName: String, sisters: UInt64, brothers: UInt64, children: UInt64, spouse: Bool){
    prepare(signer: AuthAccount){
    
    }

    execute{
        info.addFamily(lastName: lastName, sisters: sisters, brothers: brothers, children: children, spouse: spouse)
    }

}
```

```Cadence
import info from 0x02

pub fun main(lastName: String): info.Family {
    return info.families[lastName]!

}
```
