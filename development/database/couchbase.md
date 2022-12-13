# Couchbase

- [Couchbase](#couchbase)
  - [Introduction and Concepts](#introduction-and-concepts)
  - [Links](#links)
  - [Notes from Linked in Learning course](#notes-from-linked-in-learning-course)
    - [Concepts](#concepts)
    - [Development](#development)

## Introduction and Concepts

Couchbase is a distributed document database (JSON).

## Links

- Intro Documentation - <https://developer.couchbase.com/>
  - <https://docs.couchbase.com/home/index.html>
- What is couchbase YT vid - <https://www.youtube.com/watch?v=uBIJBmc9FWA>
- Linked in learning - <https://www.linkedin.com/learning/introduction-to-couchbase>
- Youtube full course - <https://www.youtube.com/watch?v=pV65gLFf0tI>
- Couchbase Playground - <https://couchbase.live/>

## Notes from Linked in Learning course

- <https://www.linkedin.com/learning/introduction-to-couchbase>

### Concepts

- Cluster - group of interconnected servers/nodes that work together to support applications
  - Recommended Min of 3 nodes for High Avail - 3 data nodes
  - 6 possible types of nodes (todo get all 6 types) - most common - data, query, index
- Data partitioning concepts
  - Bucket - equiv. of Database - spread over data nodes
  - Scope - equiv of schema
  - Collection - equiv of table
  - Documents - equiv of Rows
  - Document formats - for upload csv or json
- Scopes and Collections - help regroup the data - partition it for fast retrieval, isolation for multi-tenancy for example.

### Development

- Can get most recent SDKs from couchbase site
  - e.g. java - <https://docs.couchbase.com/java-sdk/current/hello-world/start-using-sdk.html>

- Keywords and operations
  - Insert and Delete as normal - errors if already existing or not found.
  - UPSERT - couchbase specific notion - create if not existing or replace with data if existing.
  - NoSQL -> SQL++
    - Keywords similar to SQL 
      - SELECT, FROM, WHERE, GROUP BY, HAVING, ORDER BY, LIMIT, OFFSET, JOIN, ORDER BY
      - DISTINCT exists also
      - use ` ` to enclose collection/field names with special characters e.g. SELECT * FROM `My-Collection`
      - Case sensitive -> attribute names and bucket names but not the querying keywords.

- Indexing
  - Should be using indexes always in Couchbase to improve performance.

- Joining
  - Can join on Keys without needing an index since Couchbase is a KEY-VALUE Store