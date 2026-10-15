**MongoDB** is a NoSQL, document-oriented database that stores data in flexible, JSON-like documents rather than traditional relational tables.

- **Invented by:** Dwight Merriman, Eliot Horowitz, and Kevin Ryan founded 10gen, the company that created MongoDB.
- **First released:** 2009.
- **Why it was created:** To support applications that needed flexible data models, horizontal scaling, and the ability to handle large amounts of changing data.

| **Relational database** | **MongoDB** |
| --- | --- |
| Table | Collection |
| Row | Document |
| Column | Field |

#### **To understand MongoDB properly, it helps to learn four areas:**

1. Basic terminology — documents, collections, databases, and BSON.
2. Database concepts — indexing, sharding, partitioning, ACID, and BASE.
3. System features — distributed systems, replication, scalability, and availability.
4. Practical applications — why and when MongoDB is a good choice.

#### **4 ways to implement MongoDB : Shell, GUI, Cloud, Programming language - Driver**

## **1. Understand the basic terminology**

**Database (**Contains collections**)**

                       ↓

**Collection (**Contains documents**)**

                      ↓

**Document (**Contains fields and values**)**

Example document : 

```
{_id:ObjectId("..."),name:"Asha",age:22,skills: ["Java","MongoDB"],address: {city:"Pune" }}
```

- **Database:** Organizes related collections, such as **`college`**.
- **Collection:** Groups related documents, such as **`students`**. It is similar to a table.
- **Document:** A record made up of key-value pairs. MongoDB stores documents in BSON, a binary representation of JSON with additional data types.
- **Object:** In MongoDB discussions, this can mean an embedded document, such as **`address`** above. In programming, an object is a language-specific data structure that can be converted to or from a MongoDB document.
- **Field:** A key such as **`name`**, **`age`**, or **`address`**.
- **`_id`:** The unique primary identifier for each document in a collection. MongoDB generates an **`ObjectId`** by default if you do not supply an **`_id`**. You can also supply your own unique value.
- **BSON:** Binary JSON; supports types such as dates, binary data, and **`ObjectId`**.

### **Advantages of MongoDB**

- **1. Flexible schema:** You can store documents with different fields in the same collection without requiring a fixed table structure.
- **2. High scalability:** MongoDB supports horizontal scaling using sharding, which distributes data across multiple servers.
- **3. High performance:** It can provide fast read and write operations when data is modeled appropriately and queries are indexed.
- **4. Easy to use:** Its document-based structure is convenient for developers working with JSON and JavaScript.
- **5. Handles large amounts of data:** It can manage large datasets and high-volume applications.
- **6. Supports replication:** Replica sets maintain copies of data across multiple servers, improving availability and providing redundancy.
- **7. Rich query capabilities:** MongoDB supports filtering, sorting, indexing, aggregation, and complex document queries.
- **8. Good for rapid development:** Its flexible schema makes it easier to adapt data structures as application requirements change.

### **Disadvantages of MongoDB**

- **1. Higher storage usage:** Documents may use more storage than normalized relational data because fields can be repeated across documents.
- **2. Limited joins compared with SQL databases:** MongoDB supports joins through **`$lookup`**, but relational databases are often more convenient for complex relationships.
- **3. Data duplication:** Denormalization can improve performance but may create duplicate data that must be updated consistently.
- **4. Memory requirements:** Frequently accessed data and indexes can benefit from substantial RAM; performance may suffer when resources are insufficient.
- **5. Transaction complexity:** MongoDB supports multi-document ACID transactions, but they can add overhead and complexity when used extensively.
- **6. Not ideal for every application:** Applications with highly interconnected data and complex relational queries may be easier to implement using a relational database.
- **7. Schema consistency challenges:** A flexible schema can lead to inconsistent document structures unless validation rules and application conventions are enforced.
- **8. Learning curve:** Developers must understand document modeling, indexing, aggregation pipelines, and sharding to use MongoDB effectively.

### **When should you use MongoDB?**

**Choose MongoDB when:**

- You are building applications with changing or flexible data structures.
- You are developing content management systems, product catalogs, or real-time applications.
- You need to distribute large datasets across multiple servers.
- Your application naturally stores data as documents.

**Consider a relational database when:**

- Your application relies heavily on complex joins.
- You need strong relational constraints and structured data.
- You frequently run complex queries across many related tables.

**Conclusion:** MongoDB is a powerful choice for flexible, document-oriented applications that need scalability. However, it is not always better than a relational database; the right choice depends on your application's data structure, queries, consistency requirements, and workload.

## **2. Database Concepts**

### **A. Indexing**

**Indexing helps MongoDB find data faster without scanning every document in a collection.**

Imagine a collection with one million users. If you frequently search by email, an index on the **`email`** field can make the query much more efficient.

```
db.users.createIndex({ email:1 })db.users.find({ email:"rahul@example.com" })
```

Here, **`1`** means ascending index order; **`-1`** means descending.

**Advantages:** Faster queries and sorting, and sometimes efficient enforcement of uniqueness.

**Disadvantages:** Indexes consume storage and memory, and inserts, updates, and deletes may become slower because indexes must be maintained.

### **B. Partitioning**

**Partitioning means dividing a large dataset into smaller parts.**

For example, suppose an application stores 100 million orders. Instead of treating the data as one large logical group, it can divide it into partitions based on a strategy such as date or customer ID.

Partitioning is a general database concept. It can refer to dividing data within a database or distributing it across machines.

### **C. Sharding**

**Sharding is MongoDB's method of distributing a collection's data across multiple servers.** It is a form of horizontal scaling.

For example, an online shopping platform could distribute order records across multiple shards based on a shard key.

- **Benefit:** Data and workload can be spread across multiple machines.
- **Benefit:** Capacity can grow by adding shards.
- **Trade-off:** Poor shard-key selection can create uneven distribution or bottlenecks.
- **Trade-off:** Queries that do not target a particular shard may need to contact multiple shards.

### **D. Replication**

**Replication means maintaining copies of data on multiple servers.**

MongoDB uses replica sets, usually with a primary and secondary members.

If the primary fails, an eligible secondary can be elected as the new primary.

- **Benefit:** Improves availability and provides redundancy.
- **Benefit:** Secondary members can serve certain read workloads when configured.
- **Trade-off:** Replication uses additional storage and network bandwidth.
- **Important:** Replication is not a substitute for backups, and replication lag can occur.

### **E. ACID proper**

ACID describes transaction guarantees used to preserve correctness.

| **Property** | **Meaning** | **Example** |
| --- | --- | --- |
| **A — Atomicity** | All operations in a transaction succeed, or none do | A bank transfer debits one account and credits another |
| **C — Consistency** | A transaction preserves defined data rules | An account balance must follow the application's constraints |
| **I — Isolation** | Concurrent transactions behave according to the isolation guarantees | Two users update related records at the same time |
| **D — Durability** | Committed changes persist according to the configured guarantees | A confirmed payment remains recorded after a restart |

MongoDB supports ACID transactions for single-document operations and multi-document transactions. Single-document writes are atomic by default; multi-document transactions are available when changes across documents or collections must succeed together.

### **F. BASE properties**

BASE is a design philosophy often associated with distributed NoSQL systems.

- **Basically Available:** The system aims to keep responding despite certain failures.
- **Soft State:** Replicas or views may temporarily differ as updates propagate.
- **Eventual Consistency:** If updates stop and replication succeeds, replicas can eventually converge.

BASE is a useful way to discuss some distributed-system trade-offs, but it is **not a strict rule that all NoSQL databases must follow**. MongoDB also offers consistency controls, write concerns, read concerns, and transactions.

MongoDB is not simply “BASE instead of ACID.” It can provide ACID transactions while also supporting distributed replication and sharding.

## **3. System Feature**

Beyond indexing, sharding, replication, ACID, and BASE, these are the major features you should know.

### **1. Distributed system**

A distributed system consists of multiple computers that communicate over a network and cooperate to provide a service.

MongoDB supports distributed data storage through sharding and replication.

**Why it matters:** If one server cannot handle all the data or workload, you can distribute the work across multiple machines. Replication can help keep the database available when a server fails.

### **2. Horizontal and vertical scalability**

- **Horizontal scaling:** Add more servers to distribute data and workload. MongoDB sharding supports this.
- **Vertical scaling:** Increase the CPU, RAM, or storage of an existing server.

Horizontal scaling can provide more capacity, but it requires appropriate shard keys, workload distribution, and operational management.

### **3. Flexible schema**

MongoDB does not require every document in a collection to have exactly the same fields.

For example:

json

```
{
  "name": "Rahul",
  "age": 22
}
```

json

```
{
  "name": "Priya",
  "age": 24,
  "city": "Pune",
  "skills": ["Java", "Python"]
}
```

Both documents can exist in the same collection. Schema validation can still be used to enforce required fields and data types.

### **4. High availability**

Replica sets help a database remain operational when a primary server fails. An eligible secondary can be elected as the new primary.

This reduces downtime, although failover may briefly interrupt writes.

### **5. Aggregation framework**

Aggregation allows you to process data and produce summaries or analytical results.

For example, calculate total sales for each product:

javascript

```
db.orders.aggregate([  {    $group: {      _id:"$product",      totalSales: { $sum:"$amount" }    }  }])
```

It is useful for dashboards, reports, analytics, and data transformations.

### **6. Rich query language**

MongoDB supports filtering, sorting, projections, array queries, and updates.

javascript

```
db.users.find({ age: { $gte:18 } })
```

This returns users whose age is at least 18.

### **7. Embedded documents and arrays**

Related information can be stored inside a single document.

json

```
{
  "orderId": 501,
  "customer": {
    "name": "Rahul",
    "city": "Pune"
  },
  "items": [
    { "product": "Laptop", "quantity": 1 },
    { "product": "Mouse", "quantity": 2 }
  ]
}
```

This can reduce the need for joins when the embedded data is usually accessed together.

### **8. Change streams**

Change streams let applications subscribe to database changes, such as inserted, updated, and deleted documents.

For example, an application can listen for a new order and notify a backend service to process it.

Change streams are useful for event-driven applications, notifications, and synchronization. They are not themselves a complete messaging system.

### **9. Geospatial queries**

MongoDB supports location-based queries, such as finding nearby stores, restaurants, delivery partners, or drivers.

It is useful for location-aware mobile applications.

### **10. Security and access control**

MongoDB supports authentication, role-based authorization, TLS encryption in transit, and encryption options for data at rest.

Proper configuration is essential; these capabilities do not automatically guarantee that an application is secure.

## **4. Practical Implementation**

### Category 1: Database and CRUD

#### 1.1 Database and collection commands

| Command | Explain | Example |
| --- | --- | --- |
| `show dbs` | Lists databases. | `show dbs` |
| `use college` | Switches to the `college` database. | `use college` |
| `db` | Displays the current database. | `db` |
| `db.getName()` | Returns the current database name. | `db.getName()` |
| `db.createCollection()` | Creates a collection explicitly. | `db.createCollection("students")` |
| `show collections` | Lists collections in the current database. | `show collections` |
| `db.getCollectionNames()` | Returns collection names as an array. | `db.getCollectionNames()` |
| `db.getCollection()` | Retrieves a collection object. | `db.getCollection("students")` |
| `db.students.drop()` | Deletes the collection and its indexes. | `db.students.drop()` |
| `db.dropDatabase()` | Deletes the current database. | `db.dropDatabase()` |
| `db.stats()` | Displays database statistics. | `db.stats()` |
| `db.students.stats()` | Displays collection statistics. | `db.students.stats()` |
| `db.version()` | Returns the server version. | `db.version()` |

#### 1.2 Insert commands

| Command | Explain | Example |
| --- | --- | --- |
| `insertOne()` | Inserts one document. | `db.students.insertOne({name:"Amit",age:21})` |
| `insertMany()` | Inserts multiple documents. | `db.students.insertMany([{name:"Riya",age:20},{name:"Raj",age:22}])` |
| `bulkWrite()` | Executes multiple write operations in one call. | `db.students.bulkWrite([{insertOne:{document:{name:"Neha",age:19}}}])` |

#### 1.3 Read commands

| Command | Explain | Example |
| --- | --- | --- |
| `find()` | Retrieves all matching documents. | `db.students.find({})` |
| `findOne()` | Retrieves one matching document. | `db.students.findOne({name:"Amit"})` |
| `pretty()` | Formats query output for readability in compatible shell usage. | `db.students.find().pretty()` |
| `projection` | Returns selected fields. | `db.students.find({}, {name:1,age:1,_id:0})` |
| `sort()` | Sorts ascending (`1`) or descending (`-1`). | `db.students.find().sort({age:-1})` |
| `limit()` | Limits the number of results. | `db.students.find().limit(5)` |
| `skip()` | Skips a specified number of results. | `db.students.find().skip(10)` |
| `countDocuments()` | Counts documents matching a filter. | `db.students.countDocuments({department:"IT"})` |
| `estimatedDocumentCount()` | Estimates the total document count. | `db.students.estimatedDocumentCount()` |
| `distinct()` | Returns unique values for a field. | `db.students.distinct("department")` |
| `explain()` | Shows how MongoDB executes a query. | `db.students.find({age:21}).explain("executionStats")` |
| `hint()` | Specifies an index for a query. | `db.students.find({age:21}).hint({age:1})` |
| `toArray()` | Converts cursor results into an array. | `db.students.find().toArray()` |
| `forEach()` | Executes a function for every result. | `db.students.find().forEach(s=>print(s.name))` |

#### 1.4 Query comparison operators

| Command | Explain | Example |
| --- | --- | --- |
| `$eq` | Equals a value. | `db.students.find({age:{$eq:21}})` |
| `$ne` | Does not equal a value. | `db.students.find({age:{$ne:21}})` |
| `$gt` | Greater than. | `db.students.find({marks:{$gt:80}})` |
| `$gte` | Greater than or equal to. | `db.students.find({marks:{$gte:80}})` |
| `$lt` | Less than. | `db.students.find({age:{$lt:22}})` |
| `$lte` | Less than or equal to. | `db.students.find({age:{$lte:22}})` |
| `$in` | Matches any value in an array of alternatives. | `db.students.find({department:{$in:["IT","CS"]}})` |
| `$nin` | Matches values not in the specified list, including missing fields. | `db.students.find({department:{$nin:["IT","CS"]}})` |

#### 1.5 Logical operators

| Command | Explain | Example |
| --- | --- | --- |
| `$and` | All conditions must be true. | `db.students.find({$and:[{age:{$gte:18}},{marks:{$gte:60}}]})` |
| `$or` | At least one condition must be true. | `db.students.find({$or:[{department:"IT"},{department:"CS"}]})` |
| `$nor` | None of the conditions may be true. | `db.students.find({$nor:[{age:{$lt:18}},{marks:{$lt:40}}]})` |
| `$not` | Negates a field-level condition. | `db.students.find({age:{$not:{$gt:21}}})` |

#### 1.6 Element, evaluation, and array query operators

| Command | Explain | Example |
| --- | --- | --- |
| `$exists` | Checks whether a field exists. | `db.students.find({phone:{$exists:true}})` |
| `$type` | Matches a BSON data type. | `db.students.find({age:{$type:"number"}})` |
| `$expr` | Uses aggregation expressions in a query filter. | `db.orders.find({$expr:{$gt:["$total","$discount"]}})` |
| `$jsonSchema` | Matches documents against a JSON Schema. | `db.students.find({$jsonSchema:{required:["name"]}})` |
| `$mod` | Matches numbers using a remainder condition. | `db.students.find({age:{$mod:[2,0]}})` |
| `$regex` | Matches strings against a regular expression. | `db.students.find({name:{$regex:"^A"}})` |
| `$options` | Specifies regex options, such as case-insensitive matching. | `db.students.find({name:{$regex:"amit",$options:"i"}})` |
| `$text` | Searches text-indexed fields. | `db.articles.find({$text:{$search:"database"}})` |
| `$all` | Requires an array to contain every specified value. | `db.students.find({skills:{$all:["Java","MongoDB"]}})` |
| `$elemMatch` | Matches an array containing an element satisfying the conditions. | `db.students.find({scores:{$elemMatch:{$gte:70,$lt:90}}})` |
| `$size` | Matches arrays with an exact length. | `db.students.find({skills:{$size:2}})` |

#### 1.7 Update commands and operators

| Command | Explain | Example |
| --- | --- | --- |
| `updateOne()` | Updates the first matching document. | `db.students.updateOne({name:"Amit"},{$set:{age:22}})` |
| `updateMany()` | Updates all matching documents. | `db.students.updateMany({department:"IT"},{$set:{active:true}})` |
| `replaceOne()` | Replaces a matching document. | `db.students.replaceOne({name:"Amit"},{name:"Amit",age:22})` |
| `findOneAndUpdate()` | Updates one document and returns a document according to the selected return option. | `db.students.findOneAndUpdate({name:"Amit"},{$inc:{marks:5}},{returnDocument:"after"})` |
| `findOneAndReplace()` | Replaces a document and returns its before or after version. | `db.students.findOneAndReplace({name:"Amit"},{name:"Amit",age:23},{returnDocument:"after"})` |
| `upsert: true` | Inserts a document when no matching document exists. | `db.students.updateOne({name:"Sara"},{$set:{age:20}},{upsert:true})` |
| `$set` | Sets a field's value. | `db.students.updateOne({name:"Amit"},{$set:{age:22}})` |
| `$unset` | Removes a field. | `db.students.updateOne({name:"Amit"},{$unset:{phone:""}})` |
| `$inc` | Increments or decrements a numeric field. | `db.students.updateOne({name:"Amit"},{$inc:{marks:5}})` |
| `$mul` | Multiplies a numeric field. | `db.students.updateOne({name:"Amit"},{$mul:{marks:2}})` |
| `$min` | Sets a field only when the new value is smaller. | `db.students.updateOne({name:"Amit"},{$min:{lowestScore:40}})` |
| `$max` | Sets a field only when the new value is greater. | `db.students.updateOne({name:"Amit"},{$max:{highestScore:95}})` |
| `$rename` | Renames a field. | `db.students.updateMany({},{$rename:{fullname:"name"}})` |
| `$currentDate` | Sets a field to the current date or timestamp. | `db.students.updateOne({name:"Amit"},{$currentDate:{updatedAt:true}})` |
| `$setOnInsert` | Sets fields only when an upsert inserts a new document. | `db.students.updateOne({name:"Sara"},{$setOnInsert:{createdAt:new Date()}},{upsert:true})` |

#### 1.8 Array update operators

| Command | Explain | Example |
| --- | --- | --- |
| `$push` | Adds an element to an array. | `db.students.updateOne({name:"Amit"},{$push:{skills:"Python"}})` |
| `$each` | Adds multiple elements with `$push` or `$addToSet`. | `db.students.updateOne({name:"Amit"},{$push:{skills:{$each:["SQL","React"]}}})` |
| `$addToSet` | Adds a value only if it is not already present. | `db.students.updateOne({name:"Amit"},{$addToSet:{skills:"Java"}})` |
| `$pop` | Removes the first or last array element. | `db.students.updateOne({name:"Amit"},{$pop:{skills:1}})` |
| `$pull` | Removes array elements matching a condition. | `db.students.updateOne({name:"Amit"},{$pull:{scores:{$lt:40}}})` |
| `$pullAll` | Removes all occurrences of specified values. | `db.students.updateOne({name:"Amit"},{$pullAll:{skills:["C","C++"]}})` |
| `$position` | Specifies where `$push` inserts new values. | `db.students.updateOne({name:"Amit"},{$push:{skills:{$each:["Python"],$position:0}}})` |
| `$sort` | Sorts array values during a `$push`. | `db.students.updateOne({name:"Amit"},{$push:{scores:{$each:[90,70],$sort:1}}})` |
| `$slice` | Limits the array length during a `$push`. | `db.students.updateOne({name:"Amit"},{$push:{scores:{$each:[95],$slice:-5}}})` |
| `$` | Updates the first matching array element. | `db.students.updateOne({name:"Amit",scores:80},{$set:{"scores.$":85}})` |
| `$[]` | Updates every array element. | `db.students.updateOne({name:"Amit"},{$inc:{"scores.$[]":1}})` |
| `$[identifier]` | Updates array elements matching `arrayFilters`. | `db.students.updateOne({name:"Amit"},{$set:{"scores.$[s]":100}},{arrayFilters:[{s:{$lt:40}}]})` |

#### 1.9 Delete commands

| Command | Explain | Example |
| --- | --- | --- |
| `deleteOne()` | Deletes the first matching document. | `db.students.deleteOne({name:"Amit"})` |
| `deleteMany()` | Deletes all matching documents. | `db.students.deleteMany({active:false})` |
| `findOneAndDelete()` | Deletes and returns one matching document. | `db.students.findOneAndDelete({name:"Amit"})` |
| `bulkWrite()` | Executes multiple insert, update, replace, and delete operations. | `db.students.bulkWrite([{deleteOne:{filter:{name:"Amit"}}}])` |

### Category 2: Filters and operators

#### 2.1 Projection, sorting, pagination, and query control

| Command | Explain | Example |
| --- | --- | --- |
| Projection inclusion | Returns only selected fields. | `db.students.find({}, {name:1,marks:1,_id:0})` |
| Projection exclusion | Omits selected fields. | `db.students.find({}, {address:0})` |
| Nested projection | Returns a field inside an embedded document. | `db.students.find({}, {"address.city":1,_id:0})` |
| `$slice` projection | Returns a portion of an array. | `db.students.find({}, {skills:{$slice:2}})` |
| `sort()` | Sorts documents by one or more fields. | `db.students.find().sort({department:1,marks:-1})` |
| `skip()` + `limit()` | Implements basic pagination. | `db.students.find().skip(20).limit(10)` |
| `countDocuments()` | Counts documents matching a filter. | `db.students.countDocuments({marks:{$gte:40}})` |
| `distinct()` | Returns unique field values. | `db.students.distinct("department")` |
| `hint()` | Specifies the index used by a query. | `db.students.find({email:"a@b.com"}).hint({email:1})` |
| `explain("executionStats")` | Reports actual query execution statistics. | `db.students.find({age:21}).explain("executionStats")` |
| `comment()` | Attaches a diagnostic comment to a query. | `db.students.find({age:21}).comment("age lookup")` |
| `batchSize()` | Controls the requested cursor batch size. | `db.students.find().batchSize(100)` |

#### 2.2 Advanced query operators

| Command | Explain | Example |
| --- | --- | --- |
| `$expr` | Compares or calculates using document field values. | `db.orders.find({$expr:{$gt:["$total","$discount"]}})` |
| `$regex` | Performs pattern matching on strings. | `db.students.find({name:{$regex:"^A"}})` |
| `$text` | Searches indexed text. | `db.articles.find({$text:{$search:"MongoDB indexes"}})` |
| `$where` | Filters with JavaScript; generally avoid it due to performance and security concerns. | `db.students.find({$where:"this.age > 20"})` |
| `$jsonSchema` | Checks documents against a schema. | `db.students.find({$jsonSchema:{required:["name"]}})` |
| `$all` | Requires all specified array values. | `db.students.find({skills:{$all:["Java","SQL"]}})` |
| `$elemMatch` | Matches an array element against multiple conditions. | `db.students.find({scores:{$elemMatch:{$gte:70,$lt:90}}})` |
| `$exists` | Checks whether a field is present. | `db.students.find({phone:{$exists:true}})` |
| `$type` | Matches a BSON type. | `db.students.find({age:{$type:"number"}})` |
| `$not` | Negates a field-level condition. | `db.students.find({marks:{$not:{$gte:40}}})` |
| `$nor` | Matches documents where none of the conditions is true. | `db.students.find({$nor:[{department:"IT"},{age:{$lt:18}}]})` |
| `$mod` | Matches numeric values using a remainder. | `db.students.find({age:{$mod:[2,0]}})` |

#### 2.3 Array operators and embedded documents

| Command | Explain | Example |
| --- | --- | --- |
| Dot notation | Queries fields inside embedded documents. | `db.students.find({"address.city":"Pune"})` |
| `$in` | Matches one of the specified values. | `db.students.find({skills:{$in:["Java","Python"]}})` |
| `$nin` | Excludes specified values; also matches missing fields. | `db.students.find({skills:{$nin:["C"]}})` |
| `$size` | Matches arrays of an exact length. | `db.students.find({skills:{$size:3}})` |
| `$elemMatch` | Matches at least one array element satisfying a condition. | `db.students.find({scores:{$elemMatch:{$gte:80}}})` |
| `$` | Updates the first array element matching the query. | `db.students.updateOne({scores:80},{$set:{"scores.$":85}})` |
| `$[]` | Updates every element of an array. | `db.students.updateOne({},{$inc:{"scores.$[]":1}})` |
| `$[s]` | Updates elements selected through `arrayFilters`. | `db.students.updateOne({},{$set:{"scores.$[s]":0}},{arrayFilters:[{s:{$lt:35}}]})` |

### Category 3: Aggregation

#### 3.1 Core pipeline stages

| Command | Explain | Example |
| --- | --- | --- |
| `aggregate()` | Executes an aggregation pipeline. | `db.students.aggregate([{$match:{department:"IT"}}])` |
| `$match` | Filters documents entering the next stage. | `{$match:{marks:{$gte:60}}}` |
| `$project` | Selects, removes, or computes fields. | `{$project:{name:1,marks:1,_id:0}}` |
| `$set` | Adds or updates fields in pipeline documents. | `{$set:{bonus:{$multiply:["$marks",0.1]}}}` |
| `$addFields` | Adds computed fields while retaining existing fields. | `{$addFields:{passed:{$gte:["$marks",40]}}}` |
| `$unset` | Removes fields from pipeline documents. | `{$unset:"password"}` |
| `$group` | Groups documents and calculates summary values. | `{$group:{_id:"$department",count:{$sum:1}}}` |
| `$sort` | Sorts pipeline output. | `{$sort:{count:-1}}` |
| `$limit` | Limits the output documents. | `{$limit:10}` |
| `$skip` | Skips output documents. | `{$skip:10}` |
| `$count` | Counts documents reaching the stage. | `{$count:"totalStudents"}` |
| `$unwind` | Creates one output document per array element. | `{$unwind:"$skills"}` |
| `$lookup` | Joins documents from another collection. | `{$lookup:{from:"courses",localField:"courseId",foreignField:"_id",as:"course"}}` |
| `$unionWith` | Combines results from another collection. | `{$unionWith:{coll:"alumni"}}` |
| `$facet` | Runs multiple sub-pipelines on the same input. | `{$facet:{it:[{$match:{department:"IT"}}],cs:[{$match:{department:"CS"}}]}}` |
| `$bucket` | Groups values into specified ranges. | `{$bucket:{groupBy:"$marks",boundaries:[0,40,60,80,101]}}` |
| `$bucketAuto` | Automatically calculates bucket boundaries. | `{$bucketAuto:{groupBy:"$marks",buckets:4}}` |
| `$sortByCount` | Groups values and sorts by frequency. | `{$sortByCount:"$department"}` |
| `$sample` | Selects a random sample of documents. | `{$sample:{size:5}}` |
| `$replaceRoot` | Replaces the root document. | `{$replaceRoot:{newRoot:"$address"}}` |
| `$replaceWith` | Replaces each document with an expression result. | `{$replaceWith:"$address"}` |
| `$redact` | Restricts document content based on conditions. | `{$redact:{$cond:[{$eq:["$visibility","public"]},"$$KEEP","$$PRUNE"]}}` |
| `$out` | Writes results to a collection, replacing its contents. | `{$out:"departmentSummary"}` |
| `$merge` | Writes results using configurable insert or merge behavior. | `{$merge:{into:"departmentSummary",on:"_id",whenMatched:"merge",whenNotMatched:"insert"}}` |

#### 3.2 Aggregation accumulators

| Command | Explain | Example |
| --- | --- | --- |
| `$sum` | Calculates a sum or counts documents with `$sum:1`. | `{$group:{_id:"$department",total:{$sum:"$marks"}}}` |
| `$avg` | Calculates an average. | `{$group:{_id:"$department",avg:{$avg:"$marks"}}}` |
| `$min` | Finds the minimum value. | `{$group:{_id:"$department",min:{$min:"$marks"}}}` |
| `$max` | Finds the maximum value. | `{$group:{_id:"$department",max:{$max:"$marks"}}}` |
| `$first` | Returns the first value in the group's input order. | `{$group:{_id:"$department",first:{$first:"$name"}}}` |
| `$last` | Returns the last value in the group's input order. | `{$group:{_id:"$department",last:{$last:"$name"}}}` |
| `$push` | Collects values into an array. | `{$group:{_id:"$department",names:{$push:"$name"}}}` |
| `$addToSet` | Collects unique values into an array. | `{$group:{_id:"$department",names:{$addToSet:"$name"}}}` |
| `$mergeObjects` | Combines objects. | `{$group:{_id:"$department",details:{$mergeObjects:"$details"}}}` |
| `$stdDevPop` | Calculates population standard deviation. | `{$group:{_id:"$department",sd:{$stdDevPop:"$marks"}}}` |
| `$stdDevSamp` | Calculates sample standard deviation. | `{$group:{_id:"$department",sd:{$stdDevSamp:"$marks"}}}` |
| `$top` | Returns the top document based on a sort order. | `{$group:{_id:"$department",best:{$top:{sortBy:{marks:-1},output:"$$ROOT"}}}}` |
| `$bottom` | Returns the bottom document based on a sort order. | `{$group:{_id:"$department",worst:{$bottom:{sortBy:{marks:1},output:"$$ROOT"}}}}` |
| `$topN` | Returns the top N values or documents. | `{$group:{_id:"$department",top3:{$topN:{n:3,sortBy:{marks:-1},output:"$name"}}}}` |
| `$bottomN` | Returns the bottom N values or documents. | `{$group:{_id:"$department",bottom3:{$bottomN:{n:3,sortBy:{marks:1},output:"$name"}}}}` |
| `$firstN` | Returns the first N values. | `{$group:{_id:"$department",first2:{$firstN:{n:2,input:"$name"}}}}` |
| `$lastN` | Returns the last N values. | `{$group:{_id:"$department",last2:{$lastN:{n:2,input:"$name"}}}}` |
| `$minN` | Returns the N smallest values. | `{$group:{_id:"$department",lowest3:{$minN:{n:3,input:"$marks"}}}}` |
| `$maxN` | Returns the N largest values. | `{$group:{_id:"$department",highest3:{$maxN:{n:3,input:"$marks"}}}}` |

#### 3.3 Arithmetic and conditional expressions

| Command | Explain | Example |
| --- | --- | --- |
| `$add` | Adds values. | `{$project:{total:{$add:["$marks",5]}}}` |
| `$subtract` | Subtracts values. | `{$project:{difference:{$subtract:["$total","$discount"]}}}` |
| `$multiply` | Multiplies values. | `{$project:{price:{$multiply:["$quantity","$unitPrice"]}}}` |
| `$divide` | Divides values. | `{$project:{average:{$divide:["$total","$count"]}}}` |
| `$mod` | Calculates a remainder. | `{$project:{remainder:{$mod:["$age",2]}}}` |
| `$round` | Rounds a number to the requested precision. | `{$project:{rating:{$round:["$rating",2]}}}` |
| `$ceil` | Rounds upward. | `{$project:{value:{$ceil:"$rating"}}}` |
| `$floor` | Rounds downward. | `{$project:{value:{$floor:"$rating"}}}` |
| `$abs` | Returns the absolute value. | `{$project:{value:{$abs:"$difference"}}}` |
| `$sqrt` | Calculates a square root. | `{$project:{value:{$sqrt:"$marks"}}}` |
| `$pow` | Raises a number to a power. | `{$project:{value:{$pow:["$marks",2]}}}` |
| `$ifNull` | Provides a fallback for null or missing values. | `{$project:{city:{$ifNull:["$city","Unknown"]}}}` |
| `$cond` | Implements if/else logic. | `{$project:{result:{$cond:[{$gte:["$marks",40]},"Pass","Fail"]}}}` |
| `$switch` | Selects an output from multiple conditional branches. | `{$project:{grade:{$switch:{branches:[{case:{$gte:["$marks",80]},then:"A"}],default:"B"}}}}` |
| `$literal` | Treats an expression as a literal value. | `{$project:{label:{$literal:"$marks"}}}` |
| `$isNumber` | Checks whether a value is numeric. | `{$project:{numeric:{$isNumber:"$marks"}}}` |

#### 3.4 String expressions

| Command | Explain | Example |
| --- | --- | --- |
| `$concat` | Joins strings. | `{$project:{fullName:{$concat:["$firstName"," ","$lastName"]}}}` |
| `$toLower` | Converts text to lowercase. | `{$project:{name:{$toLower:"$name"}}}` |
| `$toUpper` | Converts text to uppercase. | `{$project:{name:{$toUpper:"$name"}}}` |
| `$trim` | Removes characters or whitespace from both ends. | `{$project:{name:{$trim:{input:"$name"}}}}` |
| `$ltrim` | Trims the left side of a string. | `{$project:{name:{$ltrim:{input:"$name"}}}}` |
| `$rtrim` | Trims the right side of a string. | `{$project:{name:{$rtrim:{input:"$name"}}}}` |
| `$split` | Splits a string into an array. | `{$project:{parts:{$split:["$fullName"," "]}}}` |
| `$replaceOne` | Replaces the first matching substring. | `{$project:{name:{$replaceOne:{input:"$name",find:"Ltd",replacement:""}}}}` |
| `$replaceAll` | Replaces all matching substrings. | `{$project:{name:{$replaceAll:{input:"$name",find:" ",replacement:"_"}}}}` |
| `$strLenCP` | Returns the string length in Unicode code points. | `{$project:{length:{$strLenCP:"$name"}}}` |
| `$strLenBytes` | Returns the string length in UTF-8 bytes. | `{$project:{length:{$strLenBytes:"$name"}}}` |
| `$substrCP` | Extracts a substring using Unicode code-point positions. | `{$project:{part:{$substrCP:["$name",0,3]}}}` |
| `$regexMatch` | Tests a string against a regular expression. | `{$project:{valid:{$regexMatch:{input:"$name",regex:"^A"}}}}` |

#### 3.5 Array expressions

| Command | Explain | Example |
| --- | --- | --- |
| `$arrayElemAt` | Returns an element by array index. | `{$project:{first:{$arrayElemAt:["$skills",0]}}}` |
| `$size` | Returns array length. | `{$project:{count:{$size:"$skills"}}}` |
| `$filter` | Selects array elements satisfying a condition. | `{$project:{passed:{$filter:{input:"$scores",as:"s",cond:{$gte:["$$s",40]}}}}}` |
| `$map` | Transforms each array element. | `{$project:{doubled:{$map:{input:"$scores",as:"s",in:{$multiply:["$$s",2]}}}}}` |
| `$reduce` | Combines array elements into one accumulated result. | `{$project:{total:{$reduce:{input:"$scores",initialValue:0,in:{$add:["$$value","$$this"]}}}}}` |
| `$concatArrays` | Combines arrays. | `{$project:{all:{$concatArrays:["$skills","$extraSkills"]}}}` |
| `$reverseArray` | Reverses an array. | `{$project:{reversed:{$reverseArray:"$skills"}}}` |
| `$sortArray` | Sorts array elements. | `{$project:{sorted:{$sortArray:{input:"$scores",sortBy:1}}}}` |
| `$setUnion` | Combines arrays and removes duplicates. | `{$project:{all:{$setUnion:["$skills","$extraSkills"]}}}` |
| `$setIntersection` | Returns values common to arrays. | `{$project:{common:{$setIntersection:["$skills","$requiredSkills"]}}}` |
| `$setDifference` | Returns values in the first array but not the second. | `{$project:{missing:{$setDifference:["$requiredSkills","$skills"]}}}` |
| `$objectToArray` | Converts object fields to key-value documents. | `{$project:{fields:{$objectToArray:"$address"}}}` |
| `$arrayToObject` | Converts key-value pairs into an object. | `{$project:{obj:{$arrayToObject:[["a",1],["b",2]]}}}` |

#### 3.6 Date and time expressions

| Command | Explain | Example |
| --- | --- | --- |
| `$year` | Extracts the year. | `{$project:{year:{$year:"$createdAt"}}}` |
| `$month` | Extracts the month. | `{$project:{month:{$month:"$createdAt"}}}` |
| `$dayOfMonth` | Extracts the day of the month. | `{$project:{day:{$dayOfMonth:"$createdAt"}}}` |
| `$dayOfWeek` | Returns the weekday number, with Sunday as 1. | `{$project:{weekday:{$dayOfWeek:"$createdAt"}}}` |
| `$hour` | Extracts the hour. | `{$project:{hour:{$hour:"$createdAt"}}}` |
| `$minute` | Extracts the minute. | `{$project:{minute:{$minute:"$createdAt"}}}` |
| `$second` | Extracts the second. | `{$project:{second:{$second:"$createdAt"}}}` |
| `$dateToString` | Formats a date as a string. | `{$project:{date:{$dateToString:{format:"%Y-%m-%d",date:"$createdAt"}}}}` |
| `$dateFromString` | Converts a string into a date. | `{$project:{date:{$dateFromString:{dateString:"2026-10-15"}}}}` |
| `$dateAdd` | Adds a time interval to a date. | `{$project:{future:{$dateAdd:{startDate:"$createdAt",unit:"day",amount:7}}}}` |
| `$dateSubtract` | Subtracts a time interval from a date. | `{$project:{past:{$dateSubtract:{startDate:"$createdAt",unit:"day",amount:7}}}}` |
| `$dateDiff` | Calculates the difference between two dates. | `{$project:{days:{$dateDiff:{startDate:"$start",endDate:"$end",unit:"day"}}}}` |
| `$dateTrunc` | Truncates a date to a chosen time unit. | `{$project:{month:{$dateTrunc:{date:"$createdAt",unit:"month"}}}}` |
| `$dateToParts` | Extracts date components. | `{$project:{parts:{$dateToParts:{date:"$createdAt",timezone:"Asia/Kolkata"}}}}` |

#### 3.7 Window functions and advanced stages

| Command | Explain | Example |
| --- | --- | --- |
| `$setWindowFields` | Calculates values across a defined window of documents. | `{$setWindowFields:{partitionBy:"$department",sortBy:{marks:-1},output:{rank:{$rank:{}}}}}` |
| `$rank` | Assigns ranks, leaving gaps for ties. | `rank:{$rank:{}}` |
| `$denseRank` | Assigns ranks without gaps for ties. | `rank:{$denseRank:{}}` |
| `$documentNumber` | Assigns a sequential number to each document. | `number:{$documentNumber:{}}` |
| `$shift` | Retrieves a value from a document at a relative position. | `previous:{$shift:{output:"$marks",by:-1,default:null}}` |
| `$expMovingAvg` | Calculates an exponential moving average. | `ema:{$expMovingAvg:{input:"$marks",N:5}}` |
| `$linearFill` | Fills missing values through linear interpolation. | `{$setWindowFields:{sortBy:{date:1},output:{value:{$linearFill:"$value"}}}}` |
| `$locf` | Fills missing values with the last observed value. | `{$setWindowFields:{sortBy:{date:1},output:{value:{$locf:"$value"}}}}` |
| `$geoNear` | Finds nearby geospatial documents and calculates distances. | `{$geoNear:{near:{type:"Point",coordinates:[73.8567,18.5204]},distanceField:"distance",spherical:true}}` |
| `$documents` | Supplies literal documents to a pipeline in supported contexts. | `{$documents:[{x:1},{x:2}]}` |
