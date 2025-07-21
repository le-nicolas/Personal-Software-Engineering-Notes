Amazon Relational Database Service(RDS), can get you a database server with 24 TB of Ram, e.g. stackoverflow in 2013 had over 10 million monthly unique visitor, but it only had 1 master database. Woah!
_____________________________________________________________________________________

<img width="1280" height="720" alt="1719946058232" src="https://github.com/user-attachments/assets/75644f7a-badd-4ec2-bfd2-c6c428a62141" />



## Memory units(American orders of magnitude)

|Power|	Approx value|	Short name|	Numeric Rep. (bytes)|	Number of 0s|
|-----|-------------|-------------|-------------------------|---------------|
|10|	1 thousand |	1 KB|	1000|	3|
|20|	1 million|	1 MB|	1000000|	6|
|30|	1 billion|	1 gb|	1000000000|	9|
|40|	1 Trillion|	1 tb|	1000000000000|	12|
|50|	1 Quadrillion|	1 Pb|	1000000000000000|	15|

Big data = Tb or Petabytes

Item	Size
1 Byte	8 bits
1 IPv4 Address	4 Bytes
1 Unix Timestamp	4 Bytes
1 IPv6 Address	16 Bytes

Size of commonly used resources

Item	Size/Unit	Notes
ASCII character	1 byte	Standard ASCII uses 7 bits, but 1 byte is common
UTF-8 character	1 to 4 bytes	Variable-length encoding.
UUID	16 bytes	Consists of a mix of numbers and letters
Image ( jpeg)	~500 Kb to 5 MB or more per image	Depends on resolution and compression
Image PNG	~200 kb to 10 MB or more per image	Lossless compression, larger files
Video (720p)	~1.5 GB per hour	Depends on bitrate and codec
Video 1080p	~3 gb per hour	Higher resolution increases its size
Audio mp3	~1 mb per minute	Depends on bitrate (128 kbps)
Email	Varies [~20KB for text only]	Size can vary depending on content, attachments, and encoding
Web page (HTML)	~1kb to 1 MB per page	Depends on content and resources
Book	~300kb to 2mb 	Depends on formatting and length
Ten page docu	~100 KB to 500 KB	Varies with images, formatting, and content


Networks
Estimated Round-trip Times** (RTT):

Distance Type	Typical Latency
Within the same continent	20 to 100 ms
Intercontinental	100 to 200 ms
Around the world	300 ms or more

Time values and relations

Time unit	Estimate Value in relation to
Days in a month	30 days/month
Hours in a month	720
Minutes	40000
Seconds	2,500,000
Seconds in a day	100,000

Requests per x	Request per y
1 billion/month	33,333,333 per day
1 billion/month	400 per second
1 million/month	33,333 per day
1 million/month	0.4 per second

Therefore, uploading a file of 100 gb with a connection of 100mpbs takes 2 hours


DB

Write capacity
	As an estimate, a single PostgreSQL instance in AWX can handle around 5,000 to 20,000 writes per second ( PER NODE). The reason for the wide throughput window is that this largely depends on the size of your writes.

Quorum consensus
	• N: total number of nodes
	• W: the number of nodes that need to acknowledge (return 201) when you perform a write operation
	• R: the number of nodes that need to be probed when you perform a Read operation. This is so you can compare their response and use the most recent data
	• IF W + R > N, strong consistency is guaranteed because there's an overlapping node that has the latest data to ensure consistency.
	Configuration	Description
	R = 1 and W = N	Optimized for a fast read
	W = 1 and R = N	Optimized for a fast write
	W + R > N	Strong consistency guaranteed ( usually N = 3, W = R = 2)
	W + R < = N	Strong consistency not guaranteed
		
Consistency Models	Description
Strong consistency	Any read operation returns the most updated value; clients never see out-of-data data.
Weak consistency	Subsequent read operation may not see the most updated value
Eventual consistency	Given enough time, all updates are propagated, and all replicas become consistent(weak consistency variant.)
	Ø Strong consistency is usually achieved by forcing a replica not to accept new reads/writes until every replica has agreed on current write. This approach is not ideal for highly available systems because it could block new operations.


API :D

Rest
	Request anatomy
	
	1. method
		Method	Description
		Get	Retrieve data from the server
		Post	Submit data to the server, creating a resource.
		Put	Update an existing resource or create it if it doesn’t exist.
		Delete	Remove a source from the server
		Patch	Partially update an existing resource
		Head	Similar to get, but retrieves only headers
		Options	Describes the communication options for the target resource
	
	2. Url
		a. Protocol: http or https
		b. Domain: the server's address ( dns.example.com)
		c. Path: the specific resource ( e.g. /user/213)
		d. Query parameters ( optional ): key-value pairs for additional filtering ( e.g. ?sort=asc&limit=10)

	3. Headers
		a. Content-type: specifies the media type of the resource ( e.g. application/json)
		b. Authorization: Credentials for authenticating the request ( e.g. reddit token)
		c. Accept: indicates the media types that are acceptable for the response ( e.g. application/json)
	4. Body
		a. JSON
		b. XML
		c. Form Data: Key-value pairs sent as form submissions
			Example:
				  [METHOD, URL, PROTOCOL]
				  POST https://api.example.com/users HTTP/1.1
				
				  [HEADERS]
				  Content-Type: application/json
				  Authorization: Bearer YOUR_JWT_TOKEN
				  Accept: application/json
				
				  [BODY]
				  {
				    "name": "John Doe",
				    "email": "john.doe@example.com",
				    "age": 30
				  }

HTTP status codes
Status code category	Description	Examples
1xx	Informational	100 ( continue)
		101 ( switching protocols)
2xx	Successful	200 (OK)
		201 (created)
		202(accepted)
3xx	Redirection	301 (moved permanently)
		307 (temporary redirect)
4xx	Client error	400 (bad request)
		403 (Forbidden)
		404 (Not found)
5xx	Server error	500 (internal server error)
		502 (bad gateway)
		503 (service unavailable)

Hashing and consistent hashing
	Hash function outputs ( https://md5calc.com/hash/sha256/LSKDJFHSFA)
	Hash function	Output
	CRC32	747900d0
	SHA1	Ffb9e0aec8fefa6497076632823d7bb0704dff95
	SHA256	9b6e9d23eaf779fc30ec88e4ff7ee734528a4b5844234e0247c5ce7ef1a3fd0f
		
Re-read
	• Sloppy Quorums 
		○ Instead of enforcing the quorom requirement, the system chooses the first W healthy servers for write and first R healthy servers for reads on the hash ring. Offline servers are ignored.
	• Hinted handoff 
		○ If a server is unavailable, another server will process requests temporarily. When the down server is up, changes will be pushed back to achieve data consistency.
		○ Used to handle temporary ( non-permanent) failures
	• Anti-entropy ( used for handling permanent node failures)
		○ Uses merkle trees for inconsistency detection and minimizing the amount of data transferred
			§ A hash tree is a tree in which every non-leaf node is labeled with the hash of the labels or values ( in case of leaves) of its child nodes. Hash tress allow efficient and secure verification of the contents of large data structures.
		○ Understanding merkle tree is hard! But the main idea is that from the parent node of two merkle trees ( one for each replica) you can compare their hashes and determine if they have different data. If the hashes don’t match, then there's a conflict and you will recursively do this for their children nodes until you find the conflicting data.
	• Bloom filter
		○ To figure out which SSTables might contain the key
		○ A bloom filter is a space-efficient probabilistic technique to test if an element is a member of a set.
	• Epoch
		○ Where you measure time from a timestamp ( unix )


Fundamentals

Functional vs non-functional requirements

Functional requirements	Non-functional requirements
A functional requirement defines a system or its components	Whereas for non-functional, it defines the quality attribute of a software system.
It specifies " what should the software system do?"	This places constraints on " how should the software system fulfill the functional requirement?"
Functional requirement is specified by User	Non-functional requirement is specified by technical peoples ( technical leaders, architect and software developers.
It is mandatory	Not mandatory
It is capture in use case	Captured as a quality attribute
Defined at a component level	Applied to a system as a whole
Helps you verify the functionality of the software	Helps you to verify the performance of the software
Functional testing like system, integration, end to end, api testing, and other are done.	Non-functional testing like performance, stress, usability, security testing, are done
Usually easy to define	Usually more difficult to define
Examples	
Authentication of user whenever he/she logs in to the system	Emails should be sent with a latency of no greater than 12 hours from such an activity
System shutdown in case of a cyber attack	The processing of each request should be done within 10 secs
Verification email is sent to user whenever it registers for the first time on some software system	The site should load in 3 seconds when the number of simultaneous user are > 10000

Napkin math - " sharding; the horizontal scaling of DBs"
	Ø Sharding separates large databases into smaller, more easily managed parts called shards. Each shard shares the same schema, though the actual data on each shard is unique to the shard.
	Ø The most important factor to consider when implementing a sharding strategy is the choice of the sharding key. Sharding key = partition key. Consists of one or more columns that determine how data is distributed
	Ø Choose a key that can evenly distribute data

Latency numbers every programmer should know! (https://colin-scott.github.io/personal_website/research/interactive_latency.html) when working with data.





Review
	Are all shards stored in a single server; like a group?
		In the event when a user requests data from the partitioned DB, do all shards have to be in the same server? Or can it be on other servers. If all shards need to be on the same server, that would mean that if we scale to other servers then this setup ( all shards needed to complete the whole data record) would have to be in each and every single one of them.
		
	One should know that: independent shards - in a properly designed sharded databases, that each shard typically resides on a different server. This is essential for scalability and performance. Each shard holds a distinct subset of the data, which allows for horizontal scaling -- adding more servers to distribute the load.
	
	Data retrieval: when a user requests data, the application needs to know which shard holds the relevant data. The routing mechanism ( often based on a key or range) directs the request to the appropriate shard.
		If all shards were on a single server, the server would become a bottleneck, limiting the benefits of sharding.
		
	Scaling out
		- If you scale out by adding more servers, each server can host one or more shards. The system can still function if some shards are distributed across different servers. This means that when you add servers, you don’t have to replicate all shards on each server.
		- Instead, you distribute the shards among the available servers. For example, if you have 4 shards and 4 servers, each server could host one shard. If you add more servers, you could redistribute shards across the new setup.
	
	Whole data records
		If a user needs data that spans multiple shards ( e.g. in a case where data is partitioned by user ID, and a request requires data from two different users), the application layer must handle combining that data from the respective shards. This means that it need to query multiple servers
		
Summary
	- Not all shards need to be on the same server. In a well-designed sharding architecture, shards are typically distributed across multiple servers, allowing for better scalability and performance. Each server can independently manage its shard(s), and the application can route requests accordingly, this setup allows for efficient scaling without the need to replicate all shards on every server.

Replication to shards that don’t store the same keys
| Question: How does partitioning and replication work together? If you have a database and then you partition it into shards ( it became too big), how are shards replicated then? Are there multiple replicas of every shard? |

	Ø Partitioning and replication are key strategies in database design for scalability and fault tolerance.

Partitioning ( sharding )
	• Sharding involves dividing a large dataset in smaller, more manageable pieces called shards. Each shard holds a subset of the data, allowing for horizontal scaling. For example, you might shard a user database by user ID ranges or geographic regions.
Replication
	• Replication refers to creating copies of data to ensure availability and durability. Each shard can have one or more replicas.
How they work together
	• Multiple replicas per shard: typically, each shard has multiple replicas to handle failures and load balancing. For instance, if a shard is partitioned into three replicas ( primary and two secondaries), all read and write operations can be directed to the primary, while reads can be distributed among secondaries.
	• Consistency models: depending on the consistency requirements, replicas can be configured for different behaviors ( e.g. eventual consistency, strong consistency).
	• Data distribution: when a write occurs, its sent to the primary replica of the appropriate shard. The primary then replicates the change to its secondary replicas.
In summary, a system with partitioning and replication:
	1. Each shard has its own set of replicas
	2. The number of replicaas can be adjusted based on fault tolerance needs
	3. The system can handle more reads by distributing them across replicas while maintaining the integrity of the data across shards.
	
Follow up
	| Shards only replicate data to shards that "belong" to the same type . . . They hold the same keys for storage |
	
	Shards replicate only within their own group or type. Each shard is responsible for a specific subset of keys and replication occurs among replicas of that particular shard.
	
	Key points:
		• Each shard holds a distinct portion of the dataset based on the sharding key. e.g. if youre sharding by user ID, one shard might handle users 1 - 1000, while another handles users 1001 - 2000.
		• Local replication: replication is local to each shard, meaning that the replicas of a shard only contain the data for that shard. This ensures that replicas are always in sync with their primary shard.
		• Scalability: this approach allows you to scale your database horizontally while maintaining efficient data access and redundancy within each shard.
	
Design Patterns
	Are reusable solutions to common problems that occur in software design. They provide a template or blueprint for solving specific issues, making it easier to build systems that are flexible, maintainable, and scalable.
		1. Categories: Design patterns are typically categorized into three main types:
			i. Creational patterns: Deal with object creation mechanisms, trying to create objects in a manner suitable to the situation. e.g. singleton, factory method, and abstract factory.
			ii. Structural patterns: Focus on how classes and objects are composed to form larger structures. Examples include adapter, composite and proxy.
			iii. Behavioral patterns: concerned with algorithms and the assignment of responsibilities between objects. e.g. observer, strategy and command.
		2. Not a finished product: patterns are not code that you can just plug into your application. They are guidelines or best practices that help developers think about the design of their systems.
		3. Facilitate communication: they provide a common vocabulary for developers, making it easier to discuss solutions to design problems.
		4. Promote Reusability: by using established patterns, developers can avoid reinventing the wheel and can rely on proven solutions
		5. Encourage good practices: many patterns encourage principles like separation of concerns, encapsulation, and adherence to Solid principles, which help in creating cleaner, more maintainable code.
	
	e.g. singleton pattern
		This pattern ensures that a class has only one instance and provides a global point of access to it. Its commonly used for managing shared resources, like database connections or configuration settings.
	
SUMMARY
	Design patterns are valuable tools in software development that help streamline design processes and foster collaboration among developers by providing well-understood, reusable solutions to common challenges.
	
Main types of design patterns
	1. Creational patterns - since design patterns are common solutions to recurring design problems in software development, one example is the creational patterns. This one deal with object creation mechanisms, aiming to create objects in a manner suitable to the situation.
			i. Singleton: ensures a class has only on instance and provide a global point of access to it.
					a) Use case: when you need to control access to a shared resource, such as a configuration manager or logging service.
			ii. Factory method: defines an interface for creating an object but allows subclasses to alter the type of created objects.
					a) Use case: when a class cannot anticipate the type of objects it needs to create, allowing subclasses to define specific types.
				
			iii. Abstract factory: provides an interface for creating families of related or dependent objects without specifying their concrete classes
					a) Use case: when you need to create families of related or dependent objects,, such as UI components for different platforms ( Windows, macOS, Linux).
				
			iv. Builder: Separates the construction of a complex object from its representation, allowing the same construction process to create different representations
					a) Use case: when you want to construct a complex object step by step, such as building a pizza with various toppings.
				
			v. Prototype: Creates new objects by copying an existing object, known as the prototype.
					a) Use case: when object creation is costly, and you can create new instances by copying existing ones, like cloning complex configurations.
					
	2. Structural Patterns - these patterns focus on how objects and classes are composed to form larger structures, ensuring that if one part changes, the entire system doesn’t need to change.
			i. Adapter: allows incompatible interfaces to work together by wrapping an existing class with a new interface.
					a) Use case: when you need to integrate a new system with an existing incompatible interface, such as adapting a new payment processor to a legacy system.
			ii. Composite: composes objects into tree structures to represent part-whole hierarchies, allowing clients to treat individual objects and compositions uniformly.
					a) Use case: when you need to treat individual objects and composition uniformly, like in a file system where files and directories are treated as the same type.
			iii. Proxy: provides a surrogate or placeholder for another object to control access to it.
					a) Use case: when you want to control access to an object, such as lazy loading of an image to improve performance.
			iv. Decorators: adds new functionality to an existing object dynamically without altering its structure.
					a) Use case: when you need to add responsibilities to objects dynamically, such as adding scrollbars to a window or additional features toa graphical user interface.
			v. Façade: Simplifies a complex subsystem by providing a unified interface to a set of interfaces in that subsystem
					a) Use case: when you want to simplify interactions with a complex system, like providing a simple interface for a complex library or API.
			vi. Bridge: separates an object's abstraction from its implementation, allowing both to evolve independently.
					a) Use case: when you want to decouple an abstraction from its implementation, such as in a graphics library where shapes can have different rendering options.

	3. Behavioral patterns - these patterns are concerned with the interaction and responsibility between objects, helping define how they communicate.
			i. Observer: defines a one to many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
					a) Use case: when you need to maintain consistency between related objects, such as in a stock price display where multiple clients need updates when the price changes.
			ii. Strategy: defines a family of algorithms, encapsulates each one, and makes them interchangeable, allowing the algorithm to vary independently from clients that use it.
					a) Use case: when you want to define a family of algorithms that can be swapped at runtime, such as sorting algorithms in a collection management application.
			iii. Command: encapsulates a request as an object, thereby allowing parameterization of clients with queues, requests, and operations.
					a) Use case: when you want to parameterize actions, like in a text editor where commands ( e.g. copy, paste) can be queued and executed later.
			iv. Iterator: provides a way to access the elements of a collection sequentially without exposing its underlying representations
					a) Use case: when you need to traverse a collection without exposing its underlying structure, such as in a custom collection class.
			v. State: allows an object to alter its behavior when its internal state changes, appearing to change its class.
					a) Use case: when an object needs to change its behavior based on its state, like a media player that behaves differently when playing, pause or stopped.
			vi. Mediator: defines an object that encapsulates how a set of objects interact, promoting loose coupling by preventing direct interactions between the objects.
					a) Use case: when you want to reduce the complexity of communication between multiple objects, such as in a chat application where a central server manages interactions between users.

API DESIGN
	Ø Create
		○ POST /v1/products
			§ Creates a new product
				Request Body: { "name": "Product A", "price": 100, "imageUrl": "http://example.com/image.jpg" }
	Ø Read
		○ GET /v1/products
			§ Retrieves a list of products with pagination
			§ Query Parameters 	?page=2&limit=50
			Response	{
				  "products": [{ "id": 123, "name": "Product A", "price": 100 }, ...],
				  "page": 2,
				  "totalPages": 10
				}
			
			- GET /v1/products/{id}
			Retrieves a specific product by ID.
			Example: GET /v1/products/123
	Ø Update
		• PUT /v1/products/{id}
		Updates a specific product by ID.
		Request Body: { "name": "Updated Product A", "price": 120, "imageUrl": "http://example.com/newimage.jpg" }
		
		• PATCH /v1/products/{id}
		Partially updates a specific product by ID.
		Request Body: { "price": 110 }
		
	Ø Delete
		• DELETE /v1/products/{id}
		Deletes a specific product by ID.
		Example: DELETE /v1/products/123
	Ø Media Attachments
		POST /v1/products/{id}/media
		Uploads media for a specific product.
		Request Body: Form-data containing the file.
		Response:
		
			{ "message": "Media uploaded successfully", "mediaUrl": "http://example.com/media/456" }
			
|P - Sets |
	1. Versioning: Use versioning in your endpoints (e.g., /v1/) to manage changes.
	2. Nouns for Resources: Use nouns (e.g., products, users) for resource names rather than verbs.
	3. Consistent Naming: Keep naming conventions consistent (e.g., plural vs. singular).
	4. Use HTTP Methods Correctly: Use GET for retrieval, POST for creation, PUT for full updates, PATCH for partial updates, and DELETE for removal.
	5. Status Codes: Return appropriate HTTP status codes (e.g., 200, 201, 204, 404, 500).
	
Extra 	https://www.hellointerview.com/practice
