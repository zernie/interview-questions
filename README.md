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

#### JWT
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

### Data structures
**Stack** - **L**ast **I**n, **F**irst **O**ut

**Hash Table** -  hash table is a collection of items which are stored in such a way as to make it easy to find them later.
Collision Resolution
One method for resolving collisions looks into the hash table and tries to find another open slot to hold the item that caused the collision. A simple way to do this is to start at the original hash value position and then move in a sequential manner through the slots until we encounter the first slot that is empty. Note that we may need to go back to the first slot (circularly) to cover the entire hash table. This collision resolution process is referred to as **open addressing** in that it tries to find the next open slot or address in the hash table. By systematically visiting each slot one at a time, we are performing an open addressing technique called linear probing.
![image](https://user-images.githubusercontent.com/1765991/140930915-bcd0740b-c29b-4feb-93d2-228b9327325c.png)
An alternative method for handling the collision problem is to allow each slot to hold a reference to a collection (or chain) of items. Chaining allows many items to exist at the same location in the hash table. When collisions happen, the item is still placed in the proper slot of the hash table. As more and more items hash to the same location, the difficulty of searching for the item in the collection increases
![image](https://user-images.githubusercontent.com/1765991/140931652-3c19c8e3-233b-4a6b-a919-565b865e6654.png)

### Algorithms
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
 
* Web3.js
  * Ethers
* DAO
* NFT
  - Lazy Minting

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
