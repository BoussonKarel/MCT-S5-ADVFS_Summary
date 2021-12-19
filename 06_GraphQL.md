# GraphQL
## Why GraphQL
### What is GraphQL?
GraphQL is a **query language** for your API
- ✅ **Specification** and query language
- ❌ **Not** a library, **not** a product, **not** a database

An **answer** to the **disadvantages** of **REST API**'s

---

GraphQL is a **query language** for API's and a **runtime** for fulfilling those queries with your existing data.

GraphQL provides a **complete** and **understandable description** of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

### Before GraphQL
- **Under fetching** the REST API
  - *Get show AND episodes*
- **Over fetching** the REST API
  - *Get some properties of a show and some properties of it's episodes*

![picture 3](../images/79ed19ebeb40bb5e10af8ff514a3491718df95bb390a869bfd6b20595dba55f3.png)

### Examples
**Ask what you need**
(<> overfetching)
```graphql
query {
	getShows {
		show {
			id
			name
		}
	}
}
```
```graphql
query {
	getShowsById(id: 82) {
		show {
			id
			url
			name,
      episodes {
        name
      }
		}
	}
}
```
**Multiple queries in one request**
(<> underfetching)
```graphql
query {
	getShowsById(id:82) {
		show {
			id
			url
			name
			type
			language
			episodes {
				name
				episode
			}
		}
	}
	getShowtypes {
		showtype {
			name
		}
	}
}
```

### Rest vs GraphQL
|Rest|GraphQL|
|--|--|
|Multiple round trips to request the information from **multiple** endpoints|1 request to 1 endpoint|
|**Over-** and **under**fetching|You only **get** what you **ask**
|
|Frontend developer has to **rely** on the backend developer (for endpoints and queries)|The frontend developer is **independent** of the backend developer
|

## GraphiQL
Graph**i**QL is a Graphical User Interface to **interact** with a **GraphQL API** as a developer.

As a developer you can enable/disable it on your webserver.

## Core concepts
To write your own GraphQL API

**Type, Query, Mutations, Resolvers**

### Type
Onze API beschrijft hoe een type eruit ziet die hij kan returnen.

> Represent a kind of object you can fetch from your service, and what fields it has.

```js
type Course {
  id: ID // field
  title: String!
  // ! Field can't be null
  stars: Float
  sem: Int
  option: String
}
```

Schema scalar types:
- Int
- Float
- String
- Boolean
- ID
- Enum

Schema types:
- Object

### Query
```js
type Query {
  // getCourses: name of the query
  // [Course]: return type
  getCourses: [Course]
}
```

### Resolvers
```ts
import coursesjson = './data/courses.json';

const resolvers: IResolvers = {
  Query: {
    getCourses: (parent, arg, context, info) => {
      return coursesjson
    }
  }
}
```

### Nesting objects
```ts
type Course {
  ...
  lecturers: [Lecturer]
}
// + Aparte resolver maken voor 'lecturers'

type Lecturer { ... }
```

### Mutations
Net zoals queries, kan je ook je aanpassing-acties opsommen.
```
type Mutation {
  toggleFavoriteCourse(id: ID): Course
}
```

### Mutation with Input Type
*Adding an object, without knowing the ID (which is autonumber)*

*ID is required, so you can't use the object as an argument for the mutation.*

Solution: **input types**

```
type Lecturer {
  id: ID!
  name: String
  language: String
}

input LecturerInput {
  name: String
  language: String
}

type Mutation {
  addNewLecturer(lecturer: LecturerInput): Lecturer
}
```

## Introspection
Query the structure of your GraphQL API = **introspection**

![picture 4](../images/11d5bab6b4eb5faba450f37d8be7bdf24dda63c8b3262ae32732b31c4ed81947.png)  

## Recap
- Strongly typed
- Code generation and introspection
- Queries, mutations *(and subscriptions)*
- Client-specified shape of response
- Efficient

+ Query: Read data
+ Mutate: Write data
+ *Subscribe: Listen for data*

## Remember
- What is GraphQL?
- What is Graph**i**QL?
- How can I query in GraphQL?