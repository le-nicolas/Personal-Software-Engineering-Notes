Relational DBs

<img width="750" height="500" alt="image" src="https://github.com/user-attachments/assets/4b964c07-7f75-4b08-ab60-5583474f620f" />


	Ø Joins
	Ø Indexes
	Ø Transaction

NoSQL DBs
	
	- Key-Value
	    - Fast Access.
	    - Simple Model.
	
	- Document
	    - Schemaless.
	    - Versatile.
	
	- Graph
	    - Relationships.
	    - Effective Retrieval.
	
	- Column
	    - High performance for writes.
	    - Easy to remember: Instead of writing rows it literally writes columns.
	

Blob Storage

<img width="750" height="500" alt="image" src="https://github.com/user-attachments/assets/40269770-8089-4929-925f-f628949e7e6f" />


Services like amazon s3, google cloud storage where you upload a file and you get back a link to access it.
	Ø Has file access restrictions
	Ø Good scalability ( used by netflix)
	Ø Often combined with CDNs to get fast downloads worldwide

Search optimized DB's
<img width="750" height="500" alt="image" src="https://github.com/user-attachments/assets/c12b71df-b93c-4e40-88c8-27d56e3b8b3d" />


	Ø Document search like Elastic Search/ AWS OpenSearch
		○ Key concepts:
			§ Tokenization: breaking a piece of text into individual words.
			§ Stemming: reducing words to their root form. Allows you to match different forms of the same word
			§ Fuzzy search: the ability to find results that are similar to a given search term
				□ Tolerates slight misspellings.
				□ Edit distance calculations
					® Measures how many letters need to be changed, added, or removed to transform one word into another.
			§ Inverted index: instead of having a key matching like in a country matching several records, you have a work with a list of all the documents it appears in ( think of the elastic search contexxt)
					    {
					        "word1": [doc1, doc2, doc3],
					        "word2": [doc2, doc3, doc4],
					        "word3": [doc1, doc3, doc4]
					    }
					
API Gateway
<img width="750" height="500" alt="image" src="https://github.com/user-attachments/assets/0c73e9f8-1e08-418c-980c-d8fd2a21fd12" />


	Ø Microservice responsible for:
		○ Routing incoming requests and returning responses.
		○ Authentication
		○ Rate limiting
		○ Logging
			Examples: AWS API gateway, Kong, Apigee
			
Load BALANCER
<img width="750" height="500" alt="image" src="https://github.com/user-attachments/assets/76f29d1d-3e1d-4436-8da3-b3b8b944c524" />


	Ø Distributes work across your system.
	Ø It can be redundant to draw a load balancer in front of every service.
		○ Instead, either omit a load balancer from your design altogether or add one only to the front of the design as an abstraction.
		○ Examples: AWS Elastic load balancer, Nginx, HAProxy

Queue
<img width="750" height="500" alt="image" src="https://github.com/user-attachments/assets/22fe7f6c-cbcc-4cdc-a01c-6f6eeb62824c" />


	Ø Send request to queues and you then forget about them. Then the workers, who are working at their own pace, take the requests from the queue and return the response.
		○ But becareful of introducing queues into synchronous workloads.
	Ø Use cases:
		○ Buffer for Bursty Traffic: in Uber if the traffic (requests) gets too high, your petition for a ride gets pushed into a queue where you'll timely wait for your turn for a driver.
		○ Distribute work across a system: in a cloud-based photo processing service, queues can be used to distribute expensive image processing tasks.
	Ø Remember producer/consumer (Topics) Architecture.
	Ø Healthy note:
		○ Message ordering: most queues are FIFO, but others like Kafka offer more complex ordering like priority based.
		○ Retry mechanisms: Queues attempt to redeliver a message to a certain number of times before considering it a failure.
			§ The time between attempts and the number of retries is configurable
		○ Dead Letter Queues: you use them to store messages that failed to be processed to later check why
			§ Useful for debugging and auditing.
		○ Scaling with Partitions: Queues can be partitioned across multiple servers so that they can scale to handle more messages. Each partition can be processed by a different set of workers. Just like databases, you will need to specify a partition key to ensure that related messages are stored in the same partition.
		○ Backpressure: is a way of slowing down the production of messages when the queue is overwhelmed. This helps prevent queue from becoming a bottleneck in your system
			§ e.g., if a queue is full, you might want to reject new messages or slow down the rate at which new messages are accepted, potentially returning an error to the user or producer.
		Examples:
			Kafka
			SQS ( Managed by AWS )
			
Streams
	• Useful for scenarios where you're processing vast amounts of data in real-time or supporting complex processing scenarios, such as event sourcing.
		○ Event sourcing is a technique where changes in application state are stored as a sequence of events. These events can be replayed to reconstruct the application state at any point in time.
	• Unlike message queues, streams can retain data for a configurable period of time, allowing consumers to read and re-read messages from the same position or from a specified time in the past.
	• This is good choice for
		○ Processing a large amounts of data in real-time: designing a system for a social media platform where you need to display real-time analytics of user engagements ( likes, comments, shares) on posts. You can use a stream to ingest high volumes of engagement events generated by users across the globe. A stream processing system like Apache Flink or Spark Streaming can process these events in real-time to update the analytics dashboard.
		○ When you need to support complex processing scenarios like event sourcing: e.g. a banking system where every transaction ( deposits, withdrawals, transfers) needs to be recorded and could affect multiple accounts, using event sourceing with a stream like Kafka, each transaction is an event that can be stored, processed, and replayed. Thus, this setup not only allows for real-time processing of transactions but also enables the bank to audit transactions, rollback changes, or reconstruct the state of any account at any point in time by replaying the events
	• Useful for scenarios where you're processing vast amounts of data in real-time or supporting complex processing scenarios, such as event sourcing.
		○ Event sourcing is a technique where changes in application state are stored as a sequence of events. These events can be replayed to reconstruct the application's state at any point in time.
		○ Unlike message queues, streams can retain data for a configurable period of time, allowing consumers to read and re-read messages from the same position or from a specified time in the past.
	• Good Choice for:
		○ When you need to process large amounts of data in real-time:

	• Things you should know about streams
		○ Scaling with partitioning: in order to scale streams, they can be partitioned across multiple servers. Each partition can be processed by a different consumer, allowing for horizontal scaling
			§ You'll need to provide a partition key
		○ Multiple consumer groups: streams can support multiple consumer groups, allowing different consumers to read form the same stream independently. This is useful to scenarios where you need to process the same data in different ways. e.g. real-time analytics system
		○ Replication: in order to support fault tolerance streams can replicate data across multiple servers
		○ Windowing: a way of grouping events together based on time or count. This is useful for scenarios where you need to process events in batches, such as calculating hourly or daily aggregates of data
			§ A real-time dashboard that shows mean delivery time per region over the last 24 hours.
			
			Examples: Apache Flink, Spark Streaming, Kafka, Kinesis ( Managed by AWS)
			
Distributed Lock
	Traditional ACID DBs use transaction locks to keep data consistent, which is great for ensuring that while one user is updating a record, no one else can update it, but they're not designed for long-term locking.
		• Distributed locks are perfect for situations where you need to lock something across different systems or processes for a reasonable period of time.
			§ It is often implemented using a distributed key-value store ( like Redis or Zookeper)
			§ You can use key-value store to store a lock and then use the atomicity of the key-value store to ensure that only on process can acquire the lock at a time.
		• Another handy feature of distributed locks is that they can be set to expire after a certain amount of time . . . . But what if the process crashes?
		• System examples
			§ E-commerce Checkout system: lock high demand items for a period of time during checkout
			§ Ride-sharing matchmaking: when a rider request a ride, the system can lock a nearby driver, preventing them from being matched with multiple riders simultaneously. This lock can be held until the driver confirms or declines the ride or until a certain amount of time has passed.
			§ Distributed Cron Jobs: for systems that run scheduled tasks ( cron jobs) across multiple servers, a distributed lock ensures that a task is executed by only one server at a time.
			§ Online auction bidding system: distributed lock can be used during the final moments of bidding to ensure that when a bid is placed in the last seconds, the system locks the item to prevent other users biding at the item at the same time.
		
Things you should know
	• Locking Mechanisms: One common implementation uses Redis = Redlock. Redlock uses multiple Redis instances to ensure that a lock is acquired and released in a safe and consistent manner.
	• Lock expiry: distributed locks can be set to expire after a certain amount of time. This is important for ensuring that locks don’t get stuck in a locked state if a process crashes or is killed.
	• Locking granularity: you can lock a single resource or a group of resources
		• e.g. lock a single ticket in a ticketing system or lock a group of tickets
	• Deadlocks: occur when two or more processes are waiting for each other to release a lock. Think about a situation where two processes are trying to acquire two locks at the same time:
			§ One process acquires lock A and then tries to acquire lock B, while other process acquires lock B and then tries to acquire lock A.
	
Distributed Caches
A cache is just a server or a cluster of servers, that stores data in memory. Which is great for storing data that's expensive to compute or retrieve from a database
	Ø Lower the latency, scale the system
	
	
	• Use cases
		• Save Aggregated Metrics: when a user requests a dashboard, the platform can retrieve the calculated analytics and data from the cache instead of recomputing it, reducing the latency.
		• Reduce number of DB Queries: User session are often stored in a cache to reduce the load on the database.
			§ When a user logs in, the system can store their session data in the cache, allowing the system to quickly retrieve the data when the user makes a request.
			§ Important for systems with lots of users
		• Speed up expensive queries: remember the twitter landing page
			§ Which is a complex query that requires joining multiple tables and filtering by multiple columns. Instead, you can run the query once, store the results in a distributed cache, and then retrieve the results from the cache when a user request the.
				□ Remember the fan-out solution: slowed writes for users but by caching user's landing pages reading is way faster
	• Important stuff!
		• Eviction policies: determine which items to remove from cache when full
			§ Least recently used: evicts the least recently accessed items first.
			§ First in, First out: evicts items in the order they were added
			§ Least frequently used: removes items that are least frequently accessed.
		• Cache invalidation strategy: Strategy to ensure the data in your cache is up to date
			§ e.g. if you are designing Ticketmaster and caching popular events, the youll need to invalidate an event in the cache if the event in your database was updated ( like the venue changed).
		• Cache write strategy: ensure data is written to cache consistently.
			§ Write-through cache: writes data to both the cache and the underlying data store simultaneously. Ensure consistency but can be slower for write operations
			§ Write around cache: writes data directly to the datastore, bypassing the cache. This can minimize cache pollution but might increase data fetch times on subsequent reads
			§ Write-back cache: writes data to the cache and then asynchronously writes the data to the datastore. This can be faster for write operation but can lead to data loss if the cache is not persisted to disk.
	• Healthy Note
		• Modern caches have many different data structures in which you can leverage, but they are not just simply key-value stores.
		• Be explicit about what data you are storing in the cache, including the data structure you're using
	• Redis
		• Strings
		• Hashes
		• Lists
		• Sets
		• Sorted sets
		• Bitmaps
		• Hyperloglogs
	• Memcached
		• Strings
		• Binary objects

CDN - content delivery network is a type of cache that uses distributed servers to deliver content to users based on their geographic location.

CDNs are often used to deliver static content like images, videos, and HTML files, but they can also be used to deliver dynamic content like API responses
	Ø CDNs are often used to deliver static content like images, videos, and HTML files, but they can also be used to deliver dynamic content like API responses

The most common application of a CDN in an interview is to cache static media assets like images and videos.

Healthy note: CDNs are not just for static assets, they can store dynamic content. This is useful for content that is accessed frequently, but changes infrequently.
	• Example. A blog post that is updated once a day can be cached by a CDN.

CDNs can be used to cache API responses: if you have an API that is accessed frequently, you can use a CDN to cache the responses.

Eviction policies: like other caches, CDNs have eviction policies that determine when cached content is removed
	• You can set a time-to-live for cached content, or you can use a cache invalidation mechanism to remove content from the cache when it changes.

Cloudflare
Amazong CloudFront
	Ø Caching, DDoS protection, and web application firewalls.

