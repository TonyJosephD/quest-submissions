# Tony(aka CourtSide) Quest Submissions

## Chapter 1 - Day 1

- Q:  Explain what the Blockchain is in your own words.

A:  The Blockchain is an online database that permanently stores information strung across a timeline. It is open and available to everyone as well as decentralized ( not controlled by any single entity).

- Q:  Explain what a Smart Contract is.

A:  A Smart Contract is a digital intermediary between two parties that accomplishes a specific task within a set of guidelines. It is created by developers to ensure trust and transparency for the participating parties, but not without risks of developer mistakes.

- Q:  Explain the difference between a script and a transaction.

A:  A script is a procedure that only reads information from the blockcahin and is free, whereas a transaction is a procedure that changes the state of the blockchain and costs a fee(gas).

## Chapter 1 - Day 2
- Q: What are the 5 Cadence Programming Language Pillars?
 
 A: 1)Safety and Security
    2)Clarity
     3)Approachability
     4)Developer Experience
     5)Resource Oriented Programming
     
- Q: In your opinion, even without knowing anything about the Blockchain or coding, why could the 5 Pillars be useful (you don't have to answer this for #5)?
 
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

- Q: Explain why we wouldn't call changeGreeting in a script.

 A: A script only reads the information on the blockchain, so we would not have the capability of changing the greeting while running a script.

- Q: What does the AuthAccount mean in the prepare phase of the transaction?
 
 A: The AuthAccount is the address of the party that is initializing the transaction and granting permission to access data.
  
- Q:What is the difference between the prepare phase and the execute phase in the transaction?
  
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

- Q1: In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.
- Q2: In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!

A1+2:

```Cadence
pub fun main(){

var favPeople: [String] = ["Me", "Myself", "I"]
var socialMedia: {String : UInt64} = {"Twitter" : 1, "YouTube" : 2, "LinkedIn" : 3, "Facebook" : 4, "Instagram" : 5} 

log(favPeople)
}
```
- Q3: Explain what the force unwrap operator ! does, with an example different from the one I showed you (you can just change the type).

A3: 

```Cadence
// Declare an Optional Type. This type can either be UInt64 or Nil. All optional types can be either Nil or the
// type that we specify. In this case we specify a UInt64
var myNumber: UInt64? = 5 

// The force unwrap operator "!" indicates that we want the specified type(that's not Nil) from the
// optional.
var whoseNumber: UInt64 = myNumber! 
```

- Q4: Explain from image
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

## Chapter 3 - Day 1

- Q: In words, list 3 reasons why structs are different from resources.

A: Resources can NOT be copied, they MUST be accounted for (moved or removed), they are overly explicit in communication and therefore easy to keep track of/ difficult to ever lose.

- Q: Describe a situation where a resource might be better to use than a struct.

A: When you want to provide a unique instance of something, and certain that it can not be copied or misrepresented.

- Q: What is the keyword to make a new resource?

A: create

-Q: Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?

A: No, it can only be created in a contract.

- Q: What is the type of the resource below?

A: it is a resource type @Jacob

- Q: Fix the 4 errors in the code

A:

```Cadence
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): @Jacob { // there was 1 here
        let myJacob <- create Jacob() // there were 2 here
        return <- myJacob // there was 1 here
    }
}
```

## Chapter 3 - Day 2

- Q: Write your own smart contract that contains two state variables: an array of resources, and a dictionary of resources. Add functions to remove and add to each of them. They must be different from the examples above.

A:

```Cadence
pub contract myPets{

//Array of dogs
pub let myDogs: @[dog]

//Dictionary of Cats
pub let myCats: @{String: cat}

//Resources (Pets)
pub resource dog{
  pub let name: String
  init(){
    self.name = "GoodDog"
  }
}

pub resource cat{
  pub let name: String
  init(){
    self.name = "BadCat"
  }
}

//Functions
pub fun addDog(dog: @dog){
  self.myDogs.append(<- dog)
}

pub fun removeDog(index: Int): @dog{
  return <- self.myDogs.remove(at: index)
}

pub fun addCat(cat: @cat){
  let catName = cat.name
  self.myCats[catName]<-! cat
}

pub fun removeCat(catName: String): @cat{
  let myCat <- self.myCats.remove(key: catName)!
  return <- myCat
}

//Constructor
init(){
  self.myDogs <- []
  self.myCats <- {}
}

}
```

## Chapter 3 - Day 3
- Q: Define your own contract that stores a dictionary of resources. Add a function to get a reference to one of the resources in the dictionary.

A: 

```Cadence
pub contract athletes{

pub var players: @{String: Sport}

pub resource Sport{

  pub var playerSport: String

  init(playerSport: String){
    self.playerSport = playerSport 
  }
}

  pub fun getSportReference(key: String): &Sport{
  return (&self.players[key] as &Sport?)!
  }

  init(){
self.players <- {"Tiger Woods" : <- create Sport(playerSport: "Golf"), 
                  "Lebron James" : <- create Sport(playerSport: "BasketBall")}
}
}
```

- Q: Create a script that reads information from that resource using the reference from the function you defined in part 1.

A:

```Cadence
import athletes from 0x01

pub fun main(): String {
  let ref = athletes.getSportReference(key: "Tiger Woods")
  return ref.playerSport

}
```

- Q: Explain, in your own words, why references can be useful in Cadence.

A: references are useful since resources are so well protected in Cadence. If we just want to get information from a resource, we do not have to worry about moving it around which could be dangerous. Instead we just get the reference which will not harm the resource in any way and we do not have to keep track of where we are moving it in order to put it back in the right place when we are done.

## Chapter 3 - Day 4

- Q: Explain, in your own words, the 2 things resource interfaces can be used for (we went over both in today's content)

A: 1) It acts as a "check list" of characteristics(attributes) and actions(functions) that a resource must have.

 2) It can provide limited functionality to others when you want to be able to provide access to some elements of a resource, but still want to keep some elements of that resource private/secure.

- Q: Define your own contract. Make your own resource interface and a resource that implements the interface. Create 2 functions. In the 1st function, show an example of not restricting the type of the resource and accessing its content. In the 2nd function, show an example of restricting the type of the resource and NOT being able to access its content.

A: 
```Cadence
pub contract interfaces{

  pub resource interface IPractice {
    pub let number: Int64
  }

  pub resource Practice: IPractice{

    pub let number: Int64
    pub let moment: String
    init(){
      self.number = 69420
      self.moment = "KD Seeing Stars (IYKYK)"
    }
  }

  pub fun practiceNoInterface() {
    let moment: @Practice <- create Practice()
    log(moment.moment)
    destroy moment
  }

  pub fun practiceWithInterface() {
    let moment: @Practice{IPractice} <- create Practice()
    log(moment.moment) //member of restricted type is not accessible
    destroy moment
  }

}
```

- Q: How Could we fix this code?
```Cadence
pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}
```

A: For the frist error, we need to add the variable "favouriteFruit" to our resource "Test" itself because it is in the interface so we must implement it.
For the second error, we must add the function "changeGreeting" to the interface if we want to allow the function to be accessed(and in this case fix the error).

## Chapter 3 - Day 5

- Q: For today's quest, you will be looking at a contract and a script. You will be looking at 4 variables (a, b, c, d) and 3 functions (publicFunc, contractFunc, privateFunc) defined in SomeContract. In each AREA (1, 2, 3, and 4), I want you to do the following: for each variable (a, b, c, and d), tell me in which areas they can be read (read scope) and which areas they can be modified (write scope). For each function (publicFunc, contractFunc, and privateFunc), simply tell me where they can be called.

Answers Below:

Variables 
- a) pub(set): can be read and wrote in All 4 Areas
- b) pub var: can be read in all 4 areas, but can only be written in Area 1
- c) access(contract): can be read in only areas 1-3 (but not 4), and can only be written in area 1
- d) accesss(self): can only be read and wrote in Area 1

Functions
- pub fun publicFunc() - Can be called in any area (Except Area 4 which is a Script. If area 4 was a transaction it could be called there)
- access(contract) fun contractFunc() - Can be called anywhere within the contract (In this case Areas 1-3)
- access(self) fun privateFunc() - Can only be called within the current and inner scope (In this case only Area 1)

## Chapter 4 - Day 1
- Q: Explain what lives inside of an account.

A: An account is a container of two categories, Contracts and Paths. You can have 0-Many different smart contracts inside an account, and there are 3 Paths inside an account. There is a path to storage which holds all the data within an account and paths to public and private account data.

- Q: What is the difference between the /storage/, /public/, and /private/ paths?

A:
1) /storage contains all the data within an account and is only accessbile by the account owner.
2) /public grants access to the account's data to everyone
3) /private grants access to the account owner and anyone else they choose to grant access to.

- Q: What does .save() do? What does .load() do? What does .borrow() do?

A:
1) .save() will actually store data to the account
2) .load() will move data out of the account
3) .borrow() will just look at data inside an account

- Q: Explain why we couldn't save something to our account storage inside of a script.

A: Saving something to our account would require changing the block chain. Therefore we need a transaction in order to take in our account name and use it as a "permission slip" to add data to our account (and therefore change the blockchain).

- Q: Explain why I couldn't save something to your account.

A: Each Transaction takes in an AuthAccount Parameter which is going to represent the account address responsible for making the transaction. Saving requires access to an accounts storage, and only the account owner has access to their storage. Therefore the only storage an account could save anything to is their own.

- Q: Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:


A: 

```Cadence
access(all) contract coins {

   access(all) resource Bitcoin {
    
        access(all) var price: UInt64

        init(){
            self.price = 23000
        }

   }

   access(all) fun createBitcoin(): @Bitcoin {
    return <- create Bitcoin()
   }

    
    init() {

    }

}
```
A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.

```Cadence
import coins from 0x01

transaction {

  prepare(acct: AuthAccount) {
    let newCoin <- coins.createBitcoin()
    acct.save(<- newCoin, to: /storage/myNewCoin)
    let loadCoin <- acct.load<@coins.Bitcoin>(from: /storage/myNewCoin) ?? panic("You have no Bitcoin!")
    log(loadCoin.price)
    destroy loadCoin
    
    }
  execute {
    
  }
}

```
A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.
```Cadence
import coins from 0x01

transaction {

  prepare(acct: AuthAccount) {
    let newCoin <- coins.createBitcoin()
    acct.save(<- newCoin, to: /storage/myNewCoin)
    let borrowedCoin = acct.borrow<&coins.Bitcoin>(from: /storage/myNewCoin) ?? panic("You have no Bitcoin!")
    log(borrowedCoin.price)
    
    }
  execute {
    
  }
}
```

## Chapter 4 - Day 2

- Q: What does .link() do?

A: .link() will "map" a resource that is in account storage to a public or private path so that others can access it.

- Q: In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.

A: When we link a resource to the /public path we can restrict the resource we are sharing to an interface that it implements. We can choose to include as much or little in the interface that we want others to access. This way others will only have access to the interface and therefore only the elements we have pre-selected.

- Q: Deploy a contract that contains a resource that implements a resource interface. Then, do the following:

```Cadence
access(all) contract coins {

    access(all) resource interface IBitcoin{
        access(all) var price: UInt64
    }

   access(all) resource Bitcoin: IBitcoin {
    
        access(all) var price: UInt64
        access(all) let owned: Bool

        init(){
            self.price = 23000
            self.owned = false
        }

   }

   access(all) fun createBitcoin(): @Bitcoin {
    return <- create Bitcoin()
   }

    
    init() {

    }

}
```
In a transaction, save the resource to storage and link it to the public with the restrictive interface.

```Cadence
import coins from 0x01

transaction {

  prepare(acct: AuthAccount) {
    let newCoin <- coins.createBitcoin()
    acct.save(<- newCoin, to: /storage/myNewCoin)
    acct.link<&coins.Bitcoin{coins.IBitcoin}>(/public/myNewCoin, target: /storage/myNewCoin)
    
    }
  execute {
    
  }
}
```

Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.

![failed_script](https://user-images.githubusercontent.com/93283651/180036518-07e43722-37bf-4ba0-b4b3-b1c1393c2578.PNG)

Run the script and access something you CAN read from. Return it from the script.

```Cadence
import coins from 0x01

pub fun main(account: Address): UInt64 {
  let myCapability: Capability<&coins.Bitcoin{coins.IBitcoin}> = getAccount(account).getCapability<&coins.Bitcoin{coins.IBitcoin}>(/public/myNewCoin)
  let checkOwnership: &coins.Bitcoin{coins.IBitcoin} = myCapability.borrow() ?? panic("You do not have Capability.")

  return checkOwnership.price
}

```

## Chapter 4 - Day 3

- Q: Why did we add a Collection to this contract? List the two main reasons.

A: We added a collection so we can easily store all our NFTs in one storage path, and so that Other people are able to give us more NFTs

- Q: What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")

A: You must define a destroy function that destroys the nested resources.

- Q: Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.

Idea #1: Do we really want everyone to be able to mint an NFT? 🤔.
- A: We could add an NFT Interface that restricts the creatNFT function. Obviously we then change the NFT resource to implement the Interface and we will 
then update the NFT resource in the Collection to be restricted to the Interface functionality.

Idea #2: If we want to read information about our NFTs inside our Collection, right now we have to take it out of the Collection to do so. Is this good?
- A: No, this is not safe. We want our NFTs to stay put until we want to do something meaningful with them. We should create a new function that returns a reference to any NFT in our collection. This way if we want to read information about one inside our Collection we can just give out the reference instead.

Additional Idea
- We might only want certain NFTs to be minted up to a certain amount in order to keep them scarce and valuable. In our NFT resource we should add a new field for totalMinted and initialize it to 0 in our init() function. Then in our createNFT function we should specify that IF totalMinted < our desired maximum amount then we can create a new NFT, but if the totalMinted is == to our desired maximum amount then do not create a new NFT. (Using this logic, I do not know how we could execute this function if it specifies that it returns an @NFT but then we prevent it from creating an NFT and therefore can not return anything.)
