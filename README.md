# couching.js

## Abstract
Apache CouchDB is a great database for web applications but its documentation is sparse, what makes it hard to follow. The project is a lot quieter right now but it is still being used and its several successors are thriving.
There are some points that make CouchDB compelling for the web and relevant for the future:
* The use of Erlang/OTP for resilience and fault tolerance.
* Simple REST API using web abstractions: very esay to use.
* Master/master replication.
There are some drawbacks and poor design choices but in general is very well conceived and is a fit for many web needs.

In one way or another, CouchDB is going to be relevant in one form or another for years to come.

## Scope
Couching is a project to ease the use of CouchDB from a web browser. A library to access and modify data stored in a database, modify indexes and views to the data and enable permissions and restrict access to the data.

Main access to the REST API is through promises. Each database connection could be queried, modified, created or deleted asynchronously. Multiple databases from different nodes could be connected at once.

There is an html tool to add or modify views, shows and lists. Results are dynamically presented.
