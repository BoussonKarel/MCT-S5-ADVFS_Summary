# NoSQL
## More than just SQL
### Different storage systems
- **Relationeel**
  - Highly structured
  - *MySQL, PostgreSQL, MSSQL*
- **Document**
  - Unstructured, variable data objects
  - *MongoDB, Elasticsearch, RethinkDB*
- **Time-Series**
  - Data with timestamps (sensor logs, stock prices...)
  - *InfluxDB, Prometheus*
- **Blob**
  - Video, Audio, Big files
  - *~ File Storage, Azure Blob Storage, Amazon S3*

### Relationele database
*MySQL, PostgreSQL, MSSQL*
- Useful for **relations** between data
- SQL
- **Structured** data
- Niet echt **horizontaal** schaalbaar

### Document Store database
*MongoDB, Elasticsearch, RethinkDB*
- **NoSQL** (= Not only SQL)
- **Unstructured (variable)** data
- Volledig object
- *Bv. user profiles*
- Easily distributed to multiple machines

+ Querying data with no **fixed** structure
+ Elasticsearch: Query DSL
  + Easily readable
  + Harder to write (less known)


![picture 1](../images/e706b7781a8d269d4fc601b0e072fc50db95575c2717c5af2da8c39870598542.png)

### Time-Series database
*InfluxDB, OpenTSDB*
- **NoSQL**
- **Timestamp** sorted data
- One line = one measurement
  - Temperature, Sensors...
  - Logs

+ Horizontal scaling


### BLOB Storage
*Azure Blob Storage, Amazon S3*
- **B**inary **L**arge **Ob**ject
- Automatic horizontal **scaling**
- Usually **Cloud** storage
- Work with **API**
- **Blob Containers**
  - *Picture container, Movies container...*

### Relational vs NoSQL
| NoSQL | Relational |
| -- | -- |
| Non-relational data | Highly structured, relational data |
| Unclear data requirements (changes to structured, undefined format) | A (fixed) database model is required |
| Highly scalable | Easy to query |

### Combinations
Some setups require combinations
- Blob storage + relational data
- Time-series + Document store
  - Aggregating an unstructured document with time-series data

### Conclusion
- NoSQL is not always the best solution
- Think about the future
  - Scaling
  - New data structures
- Think about usability
  - SQL/relational databases are well known
  - Different NoSQL databases have a custom querying language (InfluxDB - Flux, Elasticsearch - Query DSL ...)

## MongoDB
### NoSQL
NoSQL databases are **non-tabular** databases and store data differently than **relational** tables. NoSQL databases come in a variety of types based on their data model. Main types are **document, key-value**, wide-column and **graph**. They provide flexible schemas and scale easily with large amounts of data and high user loads.

- Store data in documents similar to JSON. Each document containers pairs of fields and values. Values can be a variety of types like strings, numbers, booleans, arrays or objects.
- Key-value databases are a simpler type of database where each item contains keys and values.
- Wide-column stores store data in tables, rows and dynamic columns.
- Graph databases store data in nodes and edges. Nodes typically store information about people, places and things, while edges store information about the relationships between the nodes.

### NoSQL - Relations
- Not a relational database, with typical **tables** and **primary keys**
- Relations are non-existent
  - You just give all the connected info about the main object
- Relations are "still there", but not in the same way
  - Can be easier to query!

### NoSQL - Transactions
- A relational database is **transactional**, meaning that we can execute multiple transactions and await for them to be added before going on to the next one.
- Transactions exist in **some** NoSQL databases, like MongoDB, but **not in all.**

### NoSQL - Pros and cons (MongoDB)
- ✅ Flexible schemas
- ✅ Horizontal scaling
- ✅ Fast queries due to the data model
  - Easily mapped to objects in Typescript, Python, .NET...
- ✅ Ease of use for developers

+ ❌ Different query languages
+ ❌ Not all support ACID transactions

## Remember
- What is NoSQL?
- How is NoSQL different from relational databases?
- What are the different types of NoSQL databases?
- Name a few examples of NoSQL databases?