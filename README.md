# Quest-Submissions

## Chapter 1 Day 1

1. What is a blockchain in own words?
A blockchain is a public database that stores information that everyone can see.  Anyone can interact with it and no one owns it.  Information on the blockchain is difficult or impossible to change or hack making it very secure.  Information is added to the chain in chronological order and creates a ledger style record.

2. Explain a smart contract
A smart contract is a set of rules or guidelines that developers create for users to interact with the blockchain.  They are fast, accurate, require no paperwork, and are extremely secure.  It might not make sense or be totally correct but I'm a gamer so I think about it like this.  If the console is the blockchain, the smart contracts are the games I use to interact and play with the system.  

3. Transaction vs Script
A transaction is a function that changes the data on the blockchain.  It is usually the only way to change the data.  Transactions can have a cost associated with it.  Scripts are ways to just view data on the chain.  They are free and do not change anything.

## Chapter 1 Day 2
1. The 5 pillars of cadence are safety and security, clairty, approachability, developer experience, and resource oriented programming.

2. The pillars are important because they speak to people who may not be familiar or experienced in this space.  Coding or learning about blockchains can be itimidating for many.  By building something that has pillars focused on secrutiy, safety, and approachability it appears less intimidating to people like me with no history in coding.  Transparency and a good user experience for developers are something that are appealing to people looking to get involved.

## Chapter 2 Day 1
1  ![Screenshot_2022-06-08 Try out this Playground project](https://user-images.githubusercontent.com/90950005/172719740-6304bcdf-05fa-449b-8423-b92dfe19ffbc.png)
2. ![Screenshot_2022-06-08 Try out this Playground project(1)](https://user-images.githubusercontent.com/90950005/172719767-424b098b-502a-4a36-adbb-6fa13aa65394.png)

## Chapter 2 Day 2
1. changeGreeting wouldn't be called in a script because a script is just a way to view the data without actually changing the smart contract.  Like a "Read Only" permission on a google doc I believe.
2. AuthAccount basically means the account owner is authorizing access to their account for the transaction to take place.  It's asking for and getting permission to access an account.
3. Prepare allows access to an account or set of data.  Execute actualy changes the data on the blockchain.
4. 
![Screenshot_2022-06-08 Try out this Playground project(2)](https://user-images.githubusercontent.com/90950005/172736832-5c9e1a20-3194-44b2-90e5-e50bd4c24738.png)

![Screenshot_2022-06-08 Try out this Playground project(3)](https://user-images.githubusercontent.com/90950005/172736851-a011c0ac-8f27-4cb7-b560-da93dd9e2c89.png)

![Screenshot_2022-06-08 Try out this Playground project(4)](https://user-images.githubusercontent.com/90950005/172736882-dfefe2d0-c289-41de-b2ba-5923783cb4c0.png)

## Chapter 2 Day 3
1. <img width="1135" alt="Screen Shot 2022-06-12 at 7 29 07 PM" src="https://user-images.githubusercontent.com/90950005/173260121-c53d59e0-e1de-4499-aadd-4536ee819d5f.png">

2. <img width="927" alt="Screen Shot 2022-06-12 at 7 36 54 PM" src="https://user-images.githubusercontent.com/90950005/173260433-851f0666-8aeb-4f2e-8aee-211832b0831a.png">


3.
```cadence
pub fun main() {

var myAccount: Int? = 8
var unwrappedmyAccount: Int = myAccount!

var myAccount2: Int? = nil
var unwrappedmyAccount2 : Int = myAccount2!
}
```
Force unwrap in the second example above would cause panic in the system because the return value would be nil.  Not sure if I am understanding this correctly.  One would want to return optionals in order to deal with any values that came back as nil.  The dev can then see if the nil option is ok, needs to be modified, or was an error they missed.  If they force unwrapped and there was a nil value where there shouldn't be, the program would have errors, not work properly, and possibly shut down.  Then the dev would have to figure out where that nil value is.  Is that sort of right?

4. The error is occuring because it's a mismatch of the return type from the declared type.  Dictionary returns optionals.  The first line of the code has String which gives the error.  A couple ways of fixing this scenario.
```cadence
pub fun main(): String {
  let thing: {Address: String} = {0x01: "One", 0x02: "Two", 0x03: "Three"}
  return thing[0x03]!
}
```
```cadence
pub fun main(): String? {
  let thing: {Address: String} = {0x01: "One", 0x02: "Two", 0x03: "Three"}
  return thing[0x03]
}
```
## Chapter 2 Day 4
```cadence
pub contract FlovatarDB {
    pub var flovatars: {Address: Flovatar}

    pub struct Flovatar{
        pub let name: String
        pub let side: String
        pub let club: String
        pub let account: Address

        init(_name: String, _side: String, _club: String, _account: Address) {
        self.name = _name
        self.side = _side
        self.club = _club
        self.account = _account
    }
}

pub fun addFlovatar(name: String, side: String, club: String, account: Address) {
    let newFlovatar = Flovatar(_name: name, _side: side, _club: club, _account: account)
    self.flovatars[account] = newFlovatar
}

init() {
    self.flovatars = {}
    }
}
```
//Transaction
```cadence
import FlovatarDB from 0x01

transaction(name: String, side: String, club: String, account: Address) {

  prepare(signer: AuthAccount) {}

  execute {
    FlovatarDB.addFlovatar(name: name, side: side, club: club, account: account)
    log("We're done")
  }
}
```
//Script
```cadence
import FlovatarDB from 0x01

pub fun main(account: Address): FlovatarDB.Flovatar {
    return FlovatarDB.flovatars[account]!

}
```

## Chapter 3 Day 1
1. Structs and Resources are different because resources cannot be copied, lost, or created whenever you want.  They tend to be more difficult to deal with than structs but also more beneficial and secure.

2. A resource is better to use than struct when you are dealing with something that's valuable or critical to the contract.  Since resources are impossibele to lose unless you actually write "destroy", it is much better to use them when dealing with something like a valuable NFT.

3. In order to make a new resource, you must use the key word "create"

4. No, resources cannot be created in a script or transaction.  It has to be within the contract.  

5. The resource is @Jacob

6. The 4 errors are: 
  - You need an @ symbol in front of the resource.  Should be @Jacob
  - Replace the = with <- symbol and add the @ in front of Jacob
  - Add <- symbol after return

## Chapter 3 Day 2
```cadence
pub contract Whiskey {

    pub var dictionaryOfBrands: @{String: Brand}
    pub var arrayOfBrands: @[Brand]

    pub resource Brand {
        pub let message: String
        init () {
        self.message = "wildTurkey"
        }
    }
    init() {
    self.arrayOfBrands <-[]
    self.dictionaryOfBrands <- {}
    }
    //Array Funtions
    pub fun addBrand(Brand: @Brand) {
        self.arrayOfBrands.append(<-Brand)
    }
    pub fun removeBrand(Index: Int): @Brand {
        return<-self.arrayOfBrands.remove(at: Index)
    }
    //Dictionary Functions
    pub fun addToDictionary(String: @Brand) {
        self.dictionaryOfBrands[String.message] <-! Brand
    }

   
}
```
