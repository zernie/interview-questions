## General
 
  
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
**Hash Table** - collisions and how to solve it (increase dynamically)


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


  * 

### Equality
`==` – Checks if the value of two operands are equal (often overridden to provide a class-specific definition of equality).

`===` – Specifically used to test equality within the when clause of a case statement (also often overridden to provide meaningful class-specific semantics in case statements).

`eql?` – Checks if the value and type of two operands are the same (as opposed to the `==` operator which compares values but ignores types). For example, `1 == 1.0` evaluates to true, whereas `1.eql?(1.0)` evaluates to false.

`equal?` – Compares the identity of two objects; i.e., returns `true` if both operands have the same object id (i.e., if they both refer to the same object). Note that this will return `false` when comparing two identical copies of the same object.

### Algorithms

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
* XSS
* Cross-Site Request Forgery (CSRF) is an attack that allows a malicious user to spoof legitimate requests to your server, masquerading ...

 
## Blockchain
 
DAO

