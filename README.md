## General
### 1
Hey there! With 7 years under my belt as a fullstack developer and product manager, I've had the chance to work on some pretty cool projects that have even brought in millions in investments.
I've mostly worked with North American startups, so I'm no stranger to remote and fast-paced work environments.

One thing you should know about me is that I'm a huge fan of TypeScript.
In fact, I had the opportunity to tackle a massive refactoring project for busbud.com (the world's largest bus ticket marketplace) using it.
And if you want to check out something I built just for fun, I created a Hearthstone card game clone using TypeScript, React & Redux on my GitHub.

I'd love to chat more and see how I can bring my skills to your team.

### 2
Hey! I have 7 years of experience as a fullstack developer, built a few successful projects that have raised 3.000.000+ millions in investments.

Most of my employers have been a North American-based startups, so I'm very comfortable with working in remote, fast-paced environment.

I love TypeScript, that is why I was tasked with refactoring thousands lines of legacy codebase in busbud.com, the world's largest bus tickets marketplace. And I built a Hearthstone card game clone in TS, React & Redux that you can find on my GitHub.

In the future, I'd like to move to into some managerial position, or perhaps even have my own startup. That is 've been trying to improve my soft skills recently. This year, I got hired as a CTO of a local online recruitment agency and won a free entrepreneurship exchange program from U.S. State Dept.

Would love to have a chat with you!

### 2
Hey! I have 7 years of experience as a fullstack developer. I built a few successful projects from scratch; one of them, a blockchain startup, for which I solo developed a web dashboard, have raised 3.000.000+ millions in investments during its ICO.

Most of my employers have been a North American-based startups, so I'm very comfortable with working in remote, fast-paced environment.

I love TypeScript, that is why I was tasked with refactoring thousands lines of legacy codebase in busbud.com, the world's largest bus tickets marketplace. And I built a Hearthstone card game clone in TS, React & Redux that you can find on my GitHub.


Would love to have a chat with you!

### My pros
Taking responsibility
Full Stack

### My Cons
Security
Algorithms

### Company Culture
### Startup Pros
### Startup cons
  
### Protocols
**HTTP** 80

**HTTPS** 443
Handshake -> 
Request:
```
GET /doc/ HTTP/1.1
Host: www.test.com

```
Response:
```
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
```

### Data structures
**Stack** - **L**ast **I**n, **F**irst **O**ut
**Queue** - **F**irst-**i**n **F**irst-**o**ut
**Hash Table** -  hash table is a collection of items which are stored in such a way as to make it easy to find them later.
Collision Resolution
One method for resolving collisions looks into the hash table and tries to find another open slot to hold the item that caused the collision. A simple way to do this is to start at the original hash value position and then move in a sequential manner through the slots until we encounter the first slot that is empty. Note that we may need to go back to the first slot (circularly) to cover the entire hash table. This collision resolution process is referred to as **open addressing** in that it tries to find the next open slot or address in the hash table. By systematically visiting each slot one at a time, we are performing an open addressing technique called linear probing.
![image](https://user-images.githubusercontent.com/1765991/140930915-bcd0740b-c29b-4feb-93d2-228b9327325c.png)
An alternative method for handling the collision problem is to allow each slot to hold a reference to a collection (or chain) of items. Chaining allows many items to exist at the same location in the hash table. When collisions happen, the item is still placed in the proper slot of the hash table. As more and more items hash to the same location, the difficulty of searching for the item in the collection increases
![image](https://user-images.githubusercontent.com/1765991/140931652-3c19c8e3-233b-4a6b-a919-565b865e6654.png)
**Tree** - 
  **Binary Tree** - A tree whose elements have at most 2 children is called a binary tree. Since each element in a binary tree can have only 2 children, we typically name them the left and right child.



### Algorithms
<details>
	const _ = require('lodash');

// ## https://gist.github.com/andrew6666/3fca1f95f5d0302584846343ea65dc38
// Description
// Write a program that sorts a list of comma separated products.

// Each input row looks like "TITLE,POPULARITY,PRICE". Meaning "Selfie Stick,98,29" says we sold 98 "Selfie Stick"s at 29 dollars each. 
// All numbers are integers. The input will be provided in a hardcoded array so no file I/O is needed.

// The list should be sorted by:
// - By most popular first.
// - If products are equally popular, sort by cheapest price (lower is better).
// - You don't need to write your own sorting algorithm. It's recommended to use a built-in sorting library.

// Example

const example = ["Selfie Stick,98,29",
"iPhone Case,90,15",
"Fire TV Stick,48,49",
"Wyze Cam,48,25",
"Water Filter,56,49",
"Blue Light Blocking Glasses,90,16",
"Ice Maker,47,119",
"Video Doorbell,47,199",
"AA Batteries,64,12",
"Disinfecting Wipes,37,12",
"Baseball Cards,73,16",
"Winter Gloves,32,112",
"Microphone,44,22",
"Pet Kennel,5,24",
"Jenga Classic Game,100,7",
"Ink Cartridges,88,45",
"Instant Pot,98,59",
"Hoze Nozzle,74,26",
"Gift Card,45,25",
"Keyboard,82,19"]


// const correctAnswer = ["Jenga Classic Game",
// "Selfie Stick"
// Instant Pot
// iPhone Case
// Blue Light Blocking Glasses
// Ink Cartridges
// Keyboard
// Hoze Nozzle
// Baseball Cards
// AA Batteries
// Water Filter
// Wyze Cam
// Fire TV Stick
// Ice Maker
// Video Doorbell
// Gift Card
// Microphone
// Disinfecting Wipes
// Winter Gloves
// Pet Kennel
// ]

// 1. Extract data from string
// 2. Sory by popularity
// 3. Sort by cheapest price
// 4. Return the resulting array

function sortProducts(arr) {
  const info = arr.map(item => {
    const parsed =  item.match(/(.+)+,(\d+),(\d+)/);
    const [_, product, popularity, price] = parsed;
    
    return {
      product,
      price: +price,
      popularity: +popularity
    }
  });

  const sortedInfo = info.sort((a, b) => {
    if (a.popularity === b.popularity) {
      return a.price < b.price ? -1 : 1;

      return 0;
    }
    return a.popularity > b.popularity ? -1 : 1: 
 });
  
  
  return sortedInfo.map(({product, popularity}) => product);
}

console.log(sortProducts(example));


</details>

<details>
	<summary>Sort a multi dimensional array by one of the sub-elements.</summary>

	```
	  var arr = [.....]
	  arr.sort((function(index){
	    return function(a, b){
	      return (a[index] === b[index] ? 0 : (a[index] < b[index] ? -1 : 1));
	    };
	  })
	```
</details>
	
<details>
  <summary>Secret Santa</summary>

```js
	var people = ['aaa', 'bbb', 'ccc', 'ddd', 'eee'];

var pair = function(arr) {
  var result = [];
  var recipients = arr.slice();
  var len = arr.length;
  for (var i = 0; i < len; i++) {
    var sender = arr[i];		
    var recipientIndex = Math.floor(Math.random() * recipients.length);
    while (recipients[recipientIndex] === sender) {
    	// Can't send gift to myself
      recipientIndex = Math.floor(Math.random() * recipients.length);
    }
    var recipient = recipients.splice(recipientIndex, 1)[0];
    result.push({
      sender: sender,
      receiver: recipient
    });
  }
  return result;
};

// 
console.log(pair(people));

```

```js
	var names = ["Sean","Kyle","Emily","Nick","Cotter","Brian","Jeremy","Kimmy","Pat","Johnny"];

	if (names.length % 2 != 0) {
	    alert("You must have an even number of names. You currently have " + names.length + " names.");
	} else {
	    var arr1 = names.slice(), // copy array
		arr2 = names.slice(); // copy array again

	    arr1.sort(function() { return 0.5 - Math.random();}); // shuffle arrays
	    arr2.sort(function() { return 0.5 - Math.random();});

	    while (arr1.length) {
		var name1 = arr1.pop(), // get the last value of arr1
		    name2 = arr2[0] == name1 ? arr2.pop() : arr2.shift();
		    //        ^^ if the first value is the same as name1, 
		    //           get the last value, otherwise get the first

		console.log(name1 + ' gets ' + name2);
	    }
	}
```

```python
		import random
	import pandas as pd

	def compare(list_of_names, list_of_emails):
	    zipped_lists = list(zip(list_of_emails, list_of_names))
	    random.shuffle(zipped_lists)  # shuffle list of emails and names
	    result = []
	    shuffled_emails = [i[0] for i in zipped_lists]
	    for i, _ in enumerate(shuffled_emails):
		result.append(zipped_lists[i-1][1])  # shift email relatively one position to the right
	    return list(zip(result, shuffled_emails))

	def main():
	    names  = ["John", "Bob", "Alice"]
	    emails = ["John@gmail.com", "Bob@gmail.com", "Alice@outlook.com"]

	    print(compare(names,emails))

	if __name__ == '__main__':
	    main()
```

</details>

<details>
	
```
	function convertArrayToTree(arr: number[], left: number?, right: number?) {
	  if (!left && !right) {
	   convertArrayToTree(arr, 0, arr.length - 1);
	  }

	  if (left > right) return null;

	  const medium = Math.ceil(left + right) / 2;
	  const node = new TreeNode(arr[medium], );
	  node.left = convertArrayToTree(arr, left, medium - 1);
	  node.right = convertArrayToTree(arr, medium +1, right );


	  return  node
	}

	TC - O(N)
	SC - O(logN)

	[-10,-3,0,5,9]
	// left=0, right=4, medium=(0 + 4)/2=2
	  // left=0, right=1, medium=(0 + 1)/2=1
	    // medium = (0+1)/1, left = 0,right=1
	  // left= 3, right=4
```

</details>



<details>
	
```
	Convert to different base
	calculate remainder
	add remainder to sum
	return sum
	https://leetcode.com/problems/sum-of-digits-in-base-k/


	function calculate(n, k) {
	  let sum = 0;

	  while(n > 0) {
	    const remainder = n % k;
	    sum += remainder;
	    n = Math.floor(n / k);
		}


		return sum;
	}

	n= 34, k = 6
	sum = 0; remainder = 34 % 6 = 4, sum = 4, n = 34 / 6 = 5 
	sum = 4; remainder = 5 % 6 = 5; sum = 4+5=9; n=⅚=0

	TC - O(log(k)N)

	34 % 6 = 34 - 6*5 = 4
	1 % 6 = 1 - 6*0 = 1
```

</details>

### Event Sourcing
123

### SOLID

The SOLID design principle includes these five principles:
#### Single Responsibility Principle
In addition to keeping classes small and focused it also makes them easier to understand.
	
#### Open/Closed Principle
The Open/Closed Principle states that classes or methods should be open for extension, but closed for modification. This tells us we should strive for modular designs that make it possible for us to change the behavior of the system without making modifications to the classes themselves. This is generally achieved through the use of patterns such as the strategy pattern. Let’s look at an example of some code that is violating the Open/Closed Principle:
#### Liskov Substitution Principle
The principle says that objects of a superclass should be replaceable with objects of its subclasses without breaking the application. That requires the objects of your subclasses to behave in the same way as the objects of your superclass. 
An overridden method of a subclass needs to accept the same input parameter values as the method of the superclass. That means you can implement less restrictive validation rules, but you are not allowed to enforce stricter ones in your subclass. Otherwise, any code that calls this method on an object of the superclass might cause an exception, if it gets called with an object of the subclass.

Similar rules apply to the return value of the method. The return value of a method of the subclass needs to comply with the same rules as the return value of the method of the superclass. You can only decide to apply even stricter rules by returning a specific subclass of the defined return value, or by returning a subset of the valid return values of the superclass.

#### Interface Segregation Principle
**Clients should not be forced to depend upon interfaces that they do not use.**

#### Dependency Inversion Principle
High level modules (or classes) should not depend upon low level modules. Both should depend on abstractions.
Abstractions should not depend upon details. Details should depend upon abstractions.

### SLAP
Single Level of Abstraction Principle

### Parallelism and Concurrency
Threads
Threads are useful for IO bound applications: DB, API, File system
Wait for thread – thread.join	
GIL  thread-safety

## Ruby
* Inheritance
* Composition
  * Include
  * Extends
  * Prepend
* Polymorphism - when objects of different classes have access to the same interface, they are polymorphic
* Encapsulation - Protecting access to data and functionality so that these are unavailable to certain parts of the codebase is how we ensure data is only intentionally accessed and correctly manipulated. The data is thus encapsulated, or shielded.
* Duck typing - If objects A and B are of different classes but they can both respond to a quack instance method, for example, then we can treat both as ducks (hence the name). If it quacks like a duck,…


## Rails

![image](https://user-images.githubusercontent.com/1765991/140758550-803f72d0-160a-494b-82e5-522b9dbd8b1f.png)

* [Design pattern](https://longliveruby.com/articles/rails-design-patterns-the-big-picture)
  * Service objects - class that is responsible for doing only one thing
  * Presenter -  responsible for isolating more advanced logic that is used inside the views
  * Value objects - plain Ruby class that will be responsible for providing methods that return only values
  * Decorator - it alters the original class without affecting the original class’s behavior
  * Policy object 
  * Builder / adapter - returning a given class or instance depending on the case.
  * Form objects - useful when you have to check multiple conditions before performing a given action
  * Query object - isolates the logic for querying the database. We can keep the simple queries inside the model, but we can put more complex queries or group of similar queries inside one separated class
  * Observer - allows performing a given action each time an event is called on a model. 
  * Interactor - performs a set of actions one by one. When one of the actions is stopped, then other actions should not be performed. Interactions are similar to transactions, as the rollback of previous actions is also possible.
  * Null object - provide a value for non-existing records.

  * Fat models 
  * Skinny controllers

* N+1
  * `preload` loads the association data in a separate query
  * `Include` is smart. It switches from using two separate queries to creating a single LEFT OUTER JOIN to get the data.
  * `eager_load` uses LEFT OUTER JOIN.
* Sidekiq
	  

### Equality
`==` – Checks if the value of two operands are equal (often overridden to provide a class-specific definition of equality).

`===` – Specifically used to test equality within the when clause of a case statement (also often overridden to provide meaningful class-specific semantics in case statements).

`eql?` – Checks if the value and type of two operands are the same (as opposed to the `==` operator which compares values but ignores types). For example, `1 == 1.0` evaluates to true, whereas `1.eql?(1.0)` evaluates to false.

`equal?` – Compares the identity of two objects; i.e., returns `true` if both operands have the same object id (i.e., if they both refer to the same object). Note that this will return `false` when comparing two identical copies of the same object.

### Algorithms

<details>
<summary>Binary Search</summary>
```
    function binarySearch(arr, val) {
	  let start = 0;
	  let end = arr.length - 1;

	  while (start <= end) {
	    let mid = Math.floor((start + end) / 2);

	    if (arr[mid] === val) {
	      return mid;
	    }

	    if (val < arr[mid]) {
	      end = mid - 1;
	    } else {
	      start = mid + 1;
	    }
	  }
	  return -1;
	}
	Recursive:
	function binarySearch(arr, val, start = 0, end = arr.length - 1) {
	  const mid = Math.floor((start + end) / 2);

	  if (val === arr[mid]) {
	    return mid;
	  }

	  if (start >= end) {
	    return -1;
	  }

	  return val < arr[mid]
	    ? binarySearch(arr, val, start, mid - 1)
	    : binarySearch(arr, val, mid + 1, end);
	}
```

</details>

<details>
<summary>QuickSort</summary>

```ruby
   def   quicksort(arr, first, last)
	  if first < last
	    p_index = partition(arr, first, last)
	    quicksort(arr, first, p_index - 1)
	    quicksort(arr, p_index + 1, last)
	  end
	
	  arr
	end
	
	def partition(arr, first, last)
	  # first select one element from the list, can be any element. 
	  # rearrange the list so all elements less than pivot are left of it, elements greater than pivot are right of it.
	  pivot = arr[last]
	  p_index = first
	
	  i = first
	  while i < last
	    if arr[i] <= pivot
	      temp = arr[i]
	      arr[i] = arr[p_index]
	      arr[p_index] = temp
	      p_index += 1
	    end
	    i += 1
	  end
	  temp = arr[p_index]
	  arr[p_index] = pivot
	  arr[last] = temp
	  return p_index
	end
```
			     
</details>

### Fault tolerance

*	CDN (Cloudflare, Fastly)
*	Nginx
*	Server optimization
*	Puma / Passenger / Unicorn
*	Caching
*	DB optimization
*	Proper database structure
*	Indexes
*	Views / materialized views
 

## DB
#### Postgres
* Locks
* Transactions
* Indexes (Hash, B-Tree, GiN, GisT)
* Replication (read, write)
* Sharding and partitioning are both about breaking up a large data set into smaller subsets. Sharding implies the data is spread across multiple computers while partitioning does not. Partitioning is about grouping subsets of data within a single database instance. In many cases, the terms sharding and partitioning are even used synonymously, especially when preceded by the terms “horizontal” and “vertical.” Thus, “horizontal sharding” and “horizontal partitioning” can mean the same thing.
	There are a several principle reasons to partition a table:
	1.	When a table grows so big that searching it becomes impractical even with the help of indexes (which will invariably become too big as well).
	2.	When data management is such that the target data is often the most recently added and/or older data is constantly being purged/archived, or even not being searched anymore (at least not as often).
	3.	If you are loading data from different sources and maintaining it as a data warehousing for reporting and analytics.
	4.	For a less expensive archiving or purging of massive data that avoids exclusive locks on the entire table.
	When should we resort to sharding?
	Here are a couple of classic cases:

	1.	To scale out (horizontally), when even after partitioning a table the amount of data is too great or too complex to be processed by a single server.
	2.	Use cases where the data in a big table can be divided into two or more segments that would benefit the majority of the search patterns. A common example used to describe a scenario like this is that of a company whose customers are evenly spread across the United States and searches to a target table involves the customer ZIP code. A shard then could be used to host entries of customers located on the East coast and another for customers on the West coast.
 
 
## Security
* **XSS**
* **Cross-Site Request Forgery (CSRF)** is an attack that allows a malicious user to spoof legitimate requests to your server, masquerading as an authenticated user. Rails protects against this kind of attack by generating unique tokens and validating their authenticity with each submission.
<details>
	There are two components to CSRF. First, a unique token is embedded in your site's HTML. That same token is also stored in the session cookie. When a user makes a POST request, the CSRF token from the HTML gets sent with that request. Rails compares the token from the page with the token from the session cookie to ensure they match.
</details>
			  
## Blockchain
 
* Web3.js
  * Ethers
* DAO
* NFT
  - Lazy Minting
  - SFT
* Diamond Standard
* Degraph
* TreeBox
	
	
<details>

	1. What differentiates a common transaction from a contract deployment transaction?
	The “to” field is missing and the “data” one is present.

	2. What web3 function helps you convert between different Ether denominations (and what’s the smallest one)?
	`web3.fromWei` and `web3.toWei`. Wei is the smallest denomination.

	3. What action(s) do you need to do to be able to send Ether from your account?
	Unlock your private key or account.

	4. What’s the difference between Bitcoin and Ethereum when it comes to finding out the account balance?
	Bitcoin scans your unspent transaction outputs (UTXO) to find out your balance; while Ethereum stores your account balance in the latest state.

	5. What’s the most commonly used Ethereum development framework? What features does it have?
	Truffle; it makes it easier to compile, deploy, build, test, and run console commands.

	6. What extra properties/functions does the “address” type have?
	If it’s marked as “payable”; .balance, .transfer, .send.

	7. What happens when a transaction runs out of gas?
	All state changes are reverted and the miner gets the gas consumed up to the point where the gas ran out.

	8. What is a fallback function? How do you make a contract reject Ether payments?
	A fallback function is called when you call a function that doesn’t exist or you send Ether. You can make a contract reject Ether by omitting the fallback function (depending on the compiler version), not mark it with “payable”, or make it always revert.

	9. How many values can you return from a function?
	14 values max (that’s a function of the stack depth).

	10. Which types can be assigned “memory” or “storage” locations?
	Only reference types (i.e. structs and arrays).

	Level: Medium

	1. What Geth startup option allows client applications to interact remotely with Solidity contracts? What parts of it can make this interaction secure?
	Start Geth with “--rpc” and specify which api’s can be called (-- rpcapi “eth, net, web3”).

	2. What are hash functions? Can you mention 2 of their properties? How are they used in Ethereum?
Hash functions are mathematical algorithms that map arbitrary size input data to fixed size output bit string; they are deterministic (the same input always gives the same output), have an avalanche effect (small change in input; causes a big change in output). It’s used to link blocks to each other (among many other things).

	3. What are Merkle tries? How can they be used? How many are there in a block?
Merkle tries are a data structure that stores data in the leaves and the hashes in the nodes, each node is the hash of the hash of the 2 nodes below it. They can be used to compare large and complex data structures just by comparing the roots. Blocks have 3 Merkle trees: Transactions, receipts, and state.

	4. What do you need to start your own Ethereum network? How do you insure that 2 nodes are on the same network?
You need a network id and a genesis block. To insure that 2 nodes are on the same network; get the latest block hash from the first node; go to the second node and get the same block number then compare the hashes.

	5. What transaction parameter protects Ethereum from denial of service attacks?
The “gas” parameter; execution stops and changes are reverted when the transaction runs out of gas.

	6. What goes inside a genesis block?
Chain ID, difficulty, coinbase, preallocated Ether to some accounts, a nonce.

	7. What transaction attributes/values let you know that it hasn’t’ been mined yet?
Its blockHash, blockNumber, and transactionIndex are all zeros.

	8. What costs more gas to save in storage, `uint8` or `uint256`, and why?
Uint8 costs more because the EVM works with 32 bytes stack elements and 32 bytes storage slots so when you have `uint8` (1 byte) then further operations are required to downscale and optimize storage.

	9. What’s better to use for a short text? `Bytes32` or string, and why?
Bytes32 because it fits in a single word in the EVM, while string is a dynamic array which consumes more gas for initial storage allocation and further expansions.

	10. Mention some of the functions that a contract should have to be an ERC-20 token contract.
BalanceOf, approve, transferFrom.
	
Level: Hard
	

	1. What is GHOST protocol? What benefits did it give to Ethereum? How does fast block generation affects the network security?
Greedy Heaviest Observed Subtree protocol takes in consideration the weights of the sub-trees at the current block (as opposed to just one block) when deciding which branch to consider as the “longest” (and most secure). The benefits were that uncle blocks are no longer discarded and the hash rate that was consumed while mining them is part of the calculation to choose the longest (heaviest) branch, consequently miners are rewarded for uncle blocks; so slower miners (for various reasons) are not sidelined which makes mining more decentralized. If block generation is too fast; network latency will cause block propagation uneven and slower nodes will always be too late and mine on blocks that are already discarded or deeper in the past than the most current block, so they will always lose the mining race and never get rewarded leading to mining centralization and concentration of wealth in the fastest nodes.

	2. How is the new contract address calculated? And why is the deployed contract code shorter than the compiled code?
It’s calculated from a hash of the sender’s address and the transaction nonce.
The deployed code is shorter because the constructor is only run on deployment and we don’t need to store it; plus there is the piece of code that unpacks and directs the EVM to the final bytecode.

	3. In which circumstances would you use the new `CREATE2` opcode to deploy a contract?
When you need to know the address that the future contract with a certain bytecode will use before actually deploying it.

	4. If your contract is inheriting from 2 contracts that have the same function; which contract wins (i.e. when you call that function by name; from which parent contract will it be called)?
The right most contract in the mentioned inheritance list (e.g. contract child is parent1, parent2; parent2 wins).

	5. If you want to use delegateCall to call an interface function; how do you calculate the function signature?
It’s the first 4 bytes of the `keccak256` hash of its canonical signature, or `theInstance.theFunction.selector`.

	6. Why should tx.origin be avoided?
An attacking contract can trick the victim contract to send it some Ether, then inside its fallback function they can call the victim’s function that uses tx.origin as a check; and it will pass that check because in this case the tx.origin is the victim contract that sent the Ether in the first place which in turn called that function!

	7. When to mark a function as “external”? What benefits would that give you if you called it from inside a contract? Can you cite one common application of this concept.
For external calls the compiler doesn’t expect internal calls so it doesn’t copy arguments to memory; instead it allows to read them directly from calldata which is cheaper. Calling external functions internally creates an internal transaction which allows the calling contract to pass transaction parameters such as “value” and “gas”. It is for instance used in MultiSig contracts when changing the list of owners.

	8. Which struct consumes more space, and why?

MyStructB consumes more space because structs are packed tightly meaning their attributes are packed into 32 byte words in sequence so in MyStructA `param1 + param2` fit into one word (i.e. 32 bytes) so the entire struct (param1+param2+param3) fits into 2 words, while in `MyStructB` `param1+param2` takes 2 words so the total (`param1+param2+param3`) takes 3 words.

	9. How can you send Ether to a contract that doesn’t accept Ether (i.e. there is no fallback function or the fallback function always reverts)?
Use selfdestruct, because it doesn’t execute the fallback function.

	10. How is extcodesize used, and why it should be avoided?

	If your function relies on calling extcodesize; you can have another contract call this function from their constructor. When the attacking contract is being deployed and the constructor is called; the address of the contract at that stage still doesn’t have any bytecode attached to it so extcodesize will return 0.
</details>

## Backend
	
### RabbitMQ

### Redis
 - Caching
 - TTL

### Apollo
- Apollo Server
- Apollo Client
- Apollo Foundation

	
### Aws
  - S3
  - Lambda
  - SQS

### Microservices
- Pros
- Cons
- How to do it
	
	
## Frontend
## JS
- Event loop (FIFO)
  - 1. Dequeue and run the oldest task from the macrotask queue (e.g. “script”).
    2. Execute all microtasks:
    3. While the microtask queue is not empty:
    4. Dequeue and run the oldest microtask.
    5. Render changes if any.
    6. If the macrotask queue is empty, wait till a macrotask appears.
    7. Go to step 1.
  - Microtasks 
  - Macrotasks
    - `queueMicrotask`
    - `Promise`
      - Always executed asynchronously
  - Example:
    ```
    console.log(1);
    
    setTimeout(() => console.log(2));
    
    Promise.resolve().then(() => console.log(3));
    
    Promise.resolve().then(() => setTimeout(() => console.log(4)));
    
    Promise.resolve().then(() => console.log(5));
    
    setTimeout(() => console.log(6));
    
    console.log(7);
    // The console output is: 1 7 3 5 2 6 4.
    ```

- `this`
  - arrow functions
  - `bind(this, [])` - creates new function
  - `apply(this, [args]) `
  - `call(this, ...args) `
- Promises
	- `resolve`
	- `reject`
	- `then`
	- `catch`
- Iterators
Iterators are rather strictly defined: they are object (the iterators) which contains a next (and possibly a few other) function. Every time the next function is called, it is expected to return an object with two properties:

value: the current value of the iterator
done: is the iterator finished?
An iterable on the other hand is an object which has a property with a `Symbol.iterator` key (which represents the well know symbol `@@iterator`). That key contains a function, which when called, returns a new iterator. An example of an iterable:
```js
const list = {
    entries: { 0: 'a', 1: 'b' },
    [Symbol.iterator]: function(){
        let counter = 0;
        const entries = this.entries;
        return {
            next: function(){
                return {
                    value: entries[counter],
                    done: !entries.hasOwnProperty(counter++)
                }
            }
        }
    }
};
Their main purpose, as their name suggests, is to provide an interface which can be iterated:

for (let item of list) { console.log(item); }
// 'a'
// 'b'
```
- Generators - Generators are functions that can be paused and resumed.

While they can be iterated (their iterables provide a `next` method), they can implement much more sophisticated procedures and provide a input/output communication through their next method.

A simple generator:
```js
function *mygen () {
   var myVal = yield 12;
   return myVal * 2;
}

const myIt = mygen();

const firstGenValue = myIt.next().value;
// Generator is paused and yields the first value

const result = myIt.next(firstGenValue * 2).value;

console.log(result); // 48
```
- Proxy
  - Immer
  

### Prototypes
  <img width="804" alt="Screenshot 2023-01-13 at 23 37 27" src="https://user-images.githubusercontent.com/1765991/212414669-ea25cb6b-1560-4edb-9667-4ea8d5fc8eae.png">

- Values `null` and `undefined` have no object wrappers
As we remember, they are not objects. But if we try to access their properties, temporary wrapper objects are created using built-in constructors String, Number and Boolean. They provide the methods and disappear.

- `strings, numbers and booleans` - These objects are created invisibly to us and most engines optimize them out, but the specification describes it exactly this way. Methods of these objects also reside in prototypes, available as String.prototype, Number.prototype and Boolean.prototype.



### Redux
- Thunk
- Saga
-
### JWT
JSON Web Token (JWT) — содержит три блока, разделенных точками: заголовок(header), набор полей (payload) и сигнатуру. Первые два блока представлены в JSON-формате и дополнительно закодированы в формат base64. Набор полей содержит произвольные пары имя/значения, притом стандарт JWT определяет несколько зарезервированных имен (iss, aud, exp и другие). Сигнатура может генерироваться при помощи и симметричных алгоритмов шифрования, и асимметричных. Кроме того, существует отдельный стандарт, отписывающий формат зашифрованного JWT-токена.

Пример подписанного JWT токена (после декодирования 1 и 2 блоков):

{ alg: "HS256", typ: "JWT" }.{ iss: "auth.myservice.com", aud: "myservice.com", exp: 1435937883, userName: "John Smith", userRole: "Admin" }.S9Zs/8/uEGGTVVtLggFTizCsMtwOJnRhjaQ2BMUQhcY
Токены предоставляют собой средство авторизации для каждого запроса от клиента к серверу. Токены(и соответственно сигнатура токена) генерируются на сервере основываясь на секретном ключе(который хранится на сервере) и payload'e. Токен в итоге хранится на клиенте и используется при необходимости авторизации какого-либо запроса. Такое решение отлично подходит при разработке SPA.

При попытке хакером подменить данные в header'ре или payload'е, токен станет не валидным, поскольку сигнатура не будет соответствовать изначальным значениям. А возможность сгенерировать новую сигнатуру у хакера отсутствует, поскольку секретный ключ для зашифровки лежит на сервере.

access token - используется для авторизации запросов и хранения дополнительной информации о пользователе (аля user_id, user_role или еще что либо, эту информацию также называет payload). Все поля в payload это свободный набор полей необходимый для реализации вашей частной бизнес логики. То бишь user_id и user_role не являются требованием и представляют собой исключительно частный случай. Сам токен храним не в localStorage как это обычно делают, а в памяти клиентского приложения.

refresh token - выдается сервером по результам успешной аутентификации и используется для получения новой пары access/refresh токенов. Храним исключительно в httpOnly куке.

Каждый токен имеет свой срок жизни, например access: 30 мин, refresh: 60 дней

Поскольку токены(а данном случае access) это не зашифрованная информация крайне не рекомендуется хранить в них какую либо sensitive data (passwords, payment credentials, etc...)

	Роль рефреш токенов и зачем их хранить в БД. Рефреш на сервере хранится для учета доступа и инвалидации краденых токенов. Таким образом сервер наверняка знает о клиентах которым стоит доверять(кому позволено авторизоваться). Если не хранить рефреш токен в БД то велика вероятность того что токены будут бесконтрольно гулять по рукам злоумышленников. Для отслеживания которых нам придется заводить черный список и периодически чистить его от просроченных. В место этого мы храним лимитированный список белых токенов для каждого юзера отдельно и в случае кражи у нас уже есть механизм противодействия(описано ниже).

	Пользователь логинится в приложении, передавая логин/пароль и fingerprint браузера (ну или некий иной уникальный идентификатор устройства если это не браузер)

	Сервер проверят подлинность логина/пароля

	В случае удачи создает и записывает сессию в БД { userId: uuid, refreshToken: uuid, expiresIn: int, fingerprint: string, ... } (схема таблицы ниже)

	Создает access token
Отправляет клиенту access и refresh token uuid (взятый из выше созданной сессии)
Set-Cookie: refreshToken='c84f18a2-c6c7-4850-be15-93f9cbaef3b3'; HttpOnly // для браузера
{
  body: { 
    accessToken: 'eyJhbGciOiJIUzUxMiIsI...',
    refreshToken: 'c84f18a2-c6c7-4850-be15-93f9cbaef3b3' // для мобильных приложений
  }
}

Куки подвержены CSRF: https://habr.com/ru/company/oleg-bunin/blog/412855 https://www.youtube.com/watch?v=x5AuK_IbJlg

	Нативыным приложениям для сматфонов удобнее работать с токенами. Да есть хаки для работы с куки, но это не нативная поддержка

	Куки в микросерисной архитектуре использовать не вариант. Напомню зачастую микросервисы раскиданы на разных доменах, а куки не поддерживают кросc-доменные запросы

	В микросерисной архитектуре JWT позволяет каждому сервису независимо от сервера авторизации верифицировать access токен (через публичный ключ)

	При использовании cookie sessions программист зачастую надеется на то, что предоставил фреймворк и оставляет как есть

	При использовании jwt мы видим проблему с безопасностью и стараемся предусмотреть механизмы контроля в случае каржи авторизационных данных. При использовании cookie сессий программист зачастую даже не задумывается что сессия может быть скомпрометирована

	На каждом запросе использование JWT избавляет бекенд от одного запроса в БД(или кеш) за данными пользователя(userId, email, etc.)

	В итоге:

	access токены храним исключительно в памяти клиентского приложения. Не в глобально доступной переменной аля window.accessToken а в замыкании

	refresh токен храним исключительно в httpOnly куке

	Механизмы контроля при угоне sensitive data в наличии

	Взяли лучшее из обеих технологий, максимально обезопасились от CSRF/XSS

	Добавьте в компанию ко всему CSP заголовки и SameSite=Strict флаг для кук и ждите прихода злодеев

### React
  - VirtualDOM
  - Hooks
  - Shallow comparison
  - SSR
  - When re-render
    - `memo`
  - hooks pros&cons
  - CSS
	- CSS Modules
	- styles-components
  - Libs 
    - `redux`
	- `redux-toolkit`
	- `redux-thunk`
	- `redux-saga`
    - `effector`
    - `immer`
    - `react-spring`

### Caching

**CPU**:
L1
L2
L3

Kafka - retention policy
	
	
## Project management
* Agile -  framework that takes an iterative approach towards the completion of a project. Continuous involvement with the client is necessary to ensure that the expectations are aligned and to allow the project manager to adapt to changes throughout the process. 
  * Scrum - project team, led by the project manager, consists of a product owner, Scrum master, and other cross-functional team members. The product owner is responsible for maximizing the value of the product, while the Scrum master is accountable for ensuring that the project team follows the Scrum methodology.
The Scrum methodology is characterized by short phases or “sprints” when project work occurs. During sprint planning, the project team identifies a small part of the scope to be completed during the upcoming sprint, which is usually a two to four week period of time. 

At the end of the sprint, this work should be ready to be delivered to the client. Finally, the sprint ends with a sprint review and retrospective—or rather, lessons learned. This cycle is repeated throughout the project lifecycle until the entirety of the scope has been delivered.
  * Kanban - type of Agile methodology that seeks to improve the project management process through workflow visualization using a tool called a Kanban board. A Kanban board is composed of columns that depict a specific stage in the project management process, with cards or sticky notes representing tasks placed in the appropriate stage. As the project progresses, the cards will move from column to column on the board until they are completed.
* Agile vs Scrum
	* Agile is a philosophy, whereas Scrum is a type of Agile methodology
        * Scrum is broken down into shorter sprints and smaller deliverables, while in Agile everything is delivered at the end of the project
        * Agile involves members from various cross-functional teams, while a Scrum project team includes specific roles, such as the Scrum Master and Product Owner
* Waterfall

Canary release
CI/CD
