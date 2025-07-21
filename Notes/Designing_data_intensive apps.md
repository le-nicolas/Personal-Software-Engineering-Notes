Designing Data-intensive apps
Availability - percentage of time a system or service is operational and accessible when needed. It measures how often the system is up compared to the total time it should be available.

Reliability - Measures how consistently and correctly a system performs its intended functions over time without failure.
	Measurement: Often assessed using metrics such as Mean Time between Failures or Mean time to failure, which quantifies how long the system performs correctly before encountering a failure.
	
Redundancy - The inclusion of extra components or systems to ensure continued operation in the event of a failure.
	- Hardware: Spare hardware components ( server, power supplies, network links) that can take over if primary components fail.
	- Data redundancy: replicating data across multiple storage devices or locations ot protect against data loss.
	- Geographic redundancy: across different locations or data centers to protect against site-specific failures.

Maintainability - system can work productively over time
	Operability: make it easy for operations teams to keep the system running smoothly
	Simplicity: make it easy for new engineers to understand the system
	Evolvability: make it easy for engineers to make changes to the system in the future.
	
Fault - deviation of one component from its specification
Failure - when the system as a whole stops providing the required service to the user.

Rolling upgrade - method of upgrading a system without shutting it down or interrupting its operation

Throughput - the amount of work processed by a system or component in a given amount of time
	E.g. systems performance: requests per second
	Networks: Megabits per second
	Databases: Queries per second
	
Latency - the time delay between the initiation of a request and the beginning of a response

Service time - the time it takes to process a request, including tasks like authorization and load balancing.

Response time - Total time from the initiation of a request until the entire response is received and processed. Encompasses both latency and service time.
	Metric: 
		Average response time: often reported as the arithmetic mean, but may not reflect the typical user experience.
		
		Percentile: provide a better understanding of response time, with the median being the halfway point. Percentile algorithms including the 
			Forward Decay, T-Digest, HDRHistogram
			
Scaling 
	Vertical scaling: Scaling up by improving the hardware of the hosting machine.
	Horizontal Scaling: Scaling out by adding more machines to handle increased load. Known as a shared-nothing architecture
	
SLA ( service level agreement) - contracts that define the expected performance and availability of a service.

Telemetry - monitoring performance metrics and error rates. Essential for understanding system status after deployment

Load parameters
	Request per second, reads to writes ratio
	
Elastic systems - systems that can scale automatically.


Data Models and Query languages
	Relational vs document model
	
	Ø SQL Databases:
		○ Pros:
			§ Better support for joins, and many-to-one and many-to-many relationships
			§ Reliable for complex transactions and strong consistency
		○ Cons
			§ Splitting a document like structure into multiple tables can lead to cumbersome schemas and complex application code
	Ø No SQL databases:
		○ Pros
			§ Schema flexibility
			§ Better performance due to locality
			§ For some applications, closer to the data structures used by the application
		○ Cons:
			§ Document model can become less appealing for applications with many-to-many relationships

Data model
	• SQL data bases:
		○ Relational model with tables, rows, and columns.
		○ Accessed via sql queries
		○ Schema is predefined and changes can be complex
	• No sql databases:
		○ Varied models including document stores, key-value stores, column-fmaily stores, and graph databases.
		○ Flexible schema, allowing for adjustments and hierarchical or nested data structures.


Schema Flexibility
	• SQL databases:
		○ Fixed Schema
		○ Schema changes require migrations, which can be time-consuming
	• NoSQL databases:
		○ Dynamic schema
		○ Easier to store different fields or structures in records w/o predefined schema changes.

Consistency and Transactions
	• SQL databases
		○ Adhere to Atomicity, consistency, isolation, durability properties
		○ Ensure reliable transactions and consistency even in system failures.
	• NosQL databases:
		○ May prioritize availability and partition tolerance (CAP theorem) over strict consistency
		○ Often offer eventual consistency instead of strong consistency
		○ Multi-statement transactions might not be as robust.
Scalability
	• SQL databases: Typically scale vertically (adding resources to a single server).
	• NoSQL Databases: Designed to scale out horizontally (distributing data across multiple servers). Can handle large volumes of data and high-velocity workloads more effectively.

Query Language
	• SQL databases:
		○ Use structured query language
		○ SQL is powerful for complex queries involving multiple tables.
	• NoSQL databases:
		○ Query mechanisms vary by database type.
		○ Document stores might use JSON-based queries; key-value stores use simple key-based lookups

Use cases
	• SQL databases:
		○ Best for applications needing complex transactions, strong consistency, and well-defined schemas
	• NOSQL database:
		○ Ideal for scenarios where scalability, flexibility, and high performance are critical
		○ Some good applications are Real-time web applications, big data applications, content management systems

Document storage
	• A document is usually stored as a single continuous string, encoded as JSON, XML, or a binary variant (e.g., MongoDB’s BSON). If your application often needs to access the entire document (e.g., to render it on a web page), there is a performance advantage due to this storage locality.
	• If data is split across multiple tables. . . . multiple index lookups are required to retrieve it all. This can result in more disk seeks and longer retrieval times. The locality advantage is significant if large parts of the document are needed simultaneously.


Imperative and Declarative Language
	Ø Imperative: specifies the exact operations in a particular order ( JS, Python)
	Ø Declarative: Specifies what the result should be, without detailing how to achieve it (CSS, react)


Map reduce
	Ø programming model for handling large amounts of data across many machines, popularized by Google.

------------------------------------------------------------
	    # Map
	    # Applies a given function to all items in an iterable (like a list) and returns an iterator that produces the results
	    
	    # Define a function to be applied to each element
	    def square(x):
	        return x * x
	    numbers = [1, 2, 3, 4, 5]
	    # Apply the function to each item in the list using map
	    squared_numbers = map(square, numbers)
	    # Convert the map object to a list and print it
	    print(list(squared_numbers))  # Output: [1, 4, 9, 16, 25]
	
	    # Reduce
	    # Applies a binary function (a function that takes two arguments) cumulatively to the items of an iterable, from left to right, so as to reduce the iterable to a single value.
	    from functools import reduce
	    # Define a function to be used for reduction
	    def add(x, y):
	        return x + y
	    numbers = [1, 2, 3, 4, 5]
	    # Apply the function cumulatively using reduce
	    sum_of_numbers = reduce(add, numbers)
	
	    print(sum_of_numbers)  # Output: 15
	  ```
----------------------------------------------------------------------------
	
Graph-like Data models
In scenarios where many-to-many relationships are prevalent, a graph-like data model can be particularly effective. This model consists of the following key components:

Vertices (also known as nodes or entities):

Represent individual objects or entities in the graph.
Each vertex can contain attributes or properties that describe the entity it represents.
Examples: People, locations, products, or any distinct objects.
Edges (also known as relationships or arcs):

Represent the connections or relationships between vertices.
Edges can be directed or undirected:
Directed edges have a direction, indicating a one-way relationship (e.g., A → B).
Undirected edges do not have a direction, indicating a mutual relationship (e.g., A ↔ B).
Each edge can also have attributes or properties that describe the relationship.



Key Characteristics
Flexible Schema:

Graph models do not require a rigid schema, allowing the addition of new types of relationships or entities without altering existing data.
Efficient Traversal:

Graph databases are optimized for traversing and querying relationships between vertices, making them suitable for applications requiring complex queries over interconnected data.
Use Cases:

Social networks (e.g., users, friends, and interactions)
Recommendation systems (e.g., users and products)
Fraud detection (e.g., transactions and accounts)
Network and IT infrastructure (e.g., servers, connections, and configurations)
Examples

Social Network:

Vertices: Users

Edges: Friendships, messages, posts

Recommendation System:

Vertices: Users, Products

Edges: Purchases, ratings, reviews

Triple Stores and SPARQL
Triple Stores:

Triple Stores are a type of graph database designed to store and manage RDF (Resource Description Framework) data, represented as triples. Each triple consists of:

Subject: The entity being described.
Predicate: The property or relationship.
Object: The value or another entity related to the subject.
Triple stores are particularly suited for managing semantic data and ontologies.

Examples of Triple Stores:

Apache Jena
RDF4J
Virtuoso
SPARQL:

SPARQL (SPARQL Protocol and RDF Query Language) is a query language specifically designed for querying RDF data. It allows users to perform complex queries to retrieve and manipulate data stored in triple stores.

Basic SPARQL Query Structure:

SELECT: Specifies the variables to return.
WHERE: Contains the pattern to match in the data.
FILTER: (Optional) Refines the results based on conditions.
Example Query:

  PREFIX ex: <http://example.org/>

  SELECT ?person ?email
  WHERE {
    ?person ex:hasEmail ?email .
    FILTER (CONTAINS(?email, "@example.com"))
  }


Additional Concepts
Normalization:

In databases, normalization means to store the data in such a way that it is unique and not duplicated. For example, in LinkedIn, your profile has a city or location, but the database has separate tables for users and cities. If you update the city name in the cities table, all users with that city will have their data updated.
Schema-on-Read:

XML databases don't have concrete schemas like relational databases. This doesn't mean they lack structure; the structure is implicit, as the application ensures data validity. Hence, "schema-on-read" is a more accurate term than "schema-less."
Heterogeneous Data:

Data that does not follow the same structure across all records. Example: Chocolate chip cookies vary in shape and size.
Homogeneous Data:

Data that follows the same structure or pattern across all records. It does not mean all records have identical information, but they adhere to a consistent format.
Declarative Language:

Specifies what outcome you want without detailing the steps to achieve it.
Imperative Language:

Specifies the exact steps needed to achieve the desired outcome.



Chapter 3: Storage and Retrieval
	Ø LOG - an append-only sequence of records
		○ Many databases internally use a log, which is an append-only data file
		○ Applications
			§ Logs record events and activities within an application
			§ Capture user interactions, errors, system events
		○ DB LOG
			§ Some databases use an internal append-only log to track records
		○ Understanding logs:
			§ Logs are essential for tracking changes and maintaining a history of operations in databases.
			§ The append-only nature of logs ensures that all changes are recorded sequentially, which aids in data recovery and consistency.

Database indexing structures
	- Index: an additional structure derived from the primary data. It allows faster record searches in the database but can slow down writes

Hash indexes
	Imagine you're writing notes in a notebook, but you never erase anything—you only keep adding new notes to the end of the book.
	
	Now, to keep track of where each note is, you have a sticky note on the side that says:
	
	"Shopping List: page 10"
	
	"Grandma's recipe: page 15"
	
	"Meeting notes: page 25"
	
	That sticky note is like your index.
	
	In computer terms:
	
	The notebook is a file on disk, and you’re only appending—adding to the end.
	
	The sticky note is an in-memory hash map (a kind of fast digital lookup list).
	
	Each entry in the hash map maps a key (like "Shopping List") to a location in the file (like "page 10" — except computers use byte offsets).
	
	So when you want to read the "Grandma's recipe", the system quickly checks the sticky note, finds it's on "page 15", flips there, and reads it.


SSTables and LSM-Trees
	• Sorted String tables:
		Think of SSTables like a well-organized recipe book:
		Everything is in order:
		Unlike a messy notebook (log file) where you scribble randomly, this book has recipes sorted alphabetically—so "Apple Pie" comes before "Zucchini Bread".
		
		No duplicates in each section:
		Each recipe appears only once per section of the book. If you updated a recipe, you'd combine ("compact") your notes and keep only the latest version, cleaning out the old.
		
		You don’t need the full table of contents in memory:
		You only remember a few key points—like "A starts on page 1", "M starts on page 50", and "Z starts on page 100". If you’re looking for “Pumpkin Pie”, you jump to page 50 and start scanning from there.
		
		Blocks and compression:
		To save space, you group recipes into pages and zip them up before putting them into the book. This saves storage and speeds up reading multiple entries in one go.
		
		Merging is like Merge Sort:
		When you have multiple recipe books (files), you can combine them easily because everything is already in order—just like how merge sort efficiently combines sorted lists.
		
	• Log-structured merge-tree (LSM-Tree):
		Think of an LSM-Tree like a cake with multiple layers of note-taking:
		You always write new notes on a small notepad first (this is like the in-memory table, or MemTable).
		
		It’s fast and easy to write on.
		
		When it fills up, you close it and file it away on your shelf as a mini recipe book (called an SSTable).
		
		Over time, your shelf gets cluttered with these mini-books, and it gets harder to find a specific recipe.
		
		So every so often, you merge and tidy up the mini-books.
		
		You create a new big book, combining and compacting everything in sorted order.
		
		This is called compaction—removing old versions, keeping things sorted, and compressing space.
		
		Searching for a recipe?
		
		First, check the in-memory notepad.
		
		If it’s not there, look in the latest mini-books on the shelf, top to bottom.
		
		Because each layer is sorted, you can search efficiently using just sparse indexes.
		
		The more popular the recipe, the more recently it was probably written, so reads are still fast!
		
	Ø Compaction Strategies:
		Size-Tiered Compaction: Newer, smaller SSTables are merged into older, larger SSTables.
			Used by: Cassandra, HBase
		Leveled Compaction: Splits the key range into smaller SSTables and moves older data into separate levels, allowing more incremental compaction and less disk space usage.
			Used by: LevelDB, RocksDB, Cassandra
	
	Ø Advantages:
		Sorted data supports efficient range queries, and sequential disk writes enable high write throughput.



Other Indexing Structures
	Key-Value Indexes: As discussed, similar to a primary key index in the relational model.
	Secondary Indexes: Can be created using the CREATE INDEX command in relational databases. Both B-trees and log-structured indexes can serve as secondary indexes.
	
Storing Values within the Index
	Heap File:

		The index's key is used for queries, while the value can be:
			The actual row data.
			A reference to the row stored elsewhere in a heap file, which maintains data in no particular order.

Clustered Index:

	Stores the indexed row directly within the index, optimizing read performance but potentially increasing storage and write overhead.

Covering Index:

	Stores some columns of a table within the index, allowing queries to be answered by the index alone. This reduces read times but increases storage and write overhead.

Multi-Column Indexes
	Concatenated Index:

		Combines several fields into one key by appending columns, e.g., (lastname, firstname). Useful for queries involving multiple fields in a specific order.

	Multi-Dimensional Indexes:

		Generalize querying multiple columns, important for geospatial data and other multi-dimensional queries.
			Examples:
				Ecommerce: Search products by color (RGB dimensions).
				Weather Database: Search for temperature observations within a range on specific dates.


