# couching.js

## Abstract
Apache CouchDB is a great database for web applications but its documentation is sparse, what makes it hard to follow. The project is a lot quieter right now but it is still being used and its several successors are thriving.
There are some points that make CouchDB compelling for the web and relevant for the future:
* The use of Erlang/OTP for resilience and fault tolerance.
* Simple REST API using web abstractions: very easy to use.
* Master/master replication.
There are some drawbacks and poor design choices but in general is very well conceived and is a fit for many web needs.

In one way or another, CouchDB is going to be relevant in one form or another for years to come.

## Scope
Couching is a project to ease the use of CouchDB from a web browser. A library to access and modify data stored in a database, modify indexes and views to the data and enable permissions and restrict access to the data.

Main access to the REST API is through promises. Each database connection could be created, queried, modified or deleted asynchronously. Multiple databases from different nodes could be connected at once.

There is an html tool to add or modify views, shows and lists. Results are dynamically presented.

## Usage
###Couching(server)

Starts or changes the database handler to a specific server.
It verifies that the server is a proper CouchDB instance and
opens or create the database of given name.

###login(user)

To verify user credentials to the system and start a session for
the given user. If the credentials are incorrect, the session
is closed and the database is in visitors' access state.
A Promise is returned with the given authorization or an error.
{user} object containing user.name and user.password.

###create()

To create a new database on the CouchDB instance.
It works only if the logged user has admin capabilities.
