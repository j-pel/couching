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

###clear()
To delete the entire database from CouchDB instance.
It works only if the logged user has admin capabilities.

###restart()
To restart current CouchDB server.
A Promise is returned with the required information or error.

###session()
To get the current session information from CouchDB.
A Promise is returned with the required information or error.

###head(id)
The lightest and fastest call to seek for a document knowing its
id. It will return the header information as a javascript object
with a property called ETag with the current revision number
if the document exists. Otherwise, the object will have an error
property plus the other header information.
A Promise is returned with the required header or error message.
@param {id} document internal id.

###get(id)
To retrieve the document with given id. It will return the current
document as a javascript object if the document exists. Otherwise,
it will return {Error: not found}.
A Promise is returned with the required document or error message.
@param {id} document internal id.

###uuid(count)
Requests one or more Universally Unique Identifiers (UUIDs) from
the CouchDB instance. The response is a JSON object providing a
list of UUIDs.
A Promise is returned with an array with the UUIDs.
@param {count} Number of UUIDs to return. Default is 1.

###delete(id)
To delete the document with given id. Document current revision is
obtained by HEAD request to the database.
If successful, it will return the revision id for the deletion stub.
Otherwise, it will return 404 (not found).
Deleted documents remain in the database forever, even after
compaction, to allow eventual consistency when replicating.
If you delete using this DELETE method, only the _id, _rev
and a deleted flag are preserved. If you deleted a document by
adding "_deleted":true then all the fields of the document are
preserved. This is to allow, for example, recording the time you
deleted a document, or the reason you deleted it. (Implementation
of the latter is pending)
@param {id} document internal id.

###put(doc)
To store new documents into the database or to revise an existing
document. If the document does not contain an id, a new uuid is
assigned.
CouchDB requires the id to be a string.
If the document exists, a new revision is generated.

A Promise is returned with the response from CouchDB.

@param {doc} document as a javascript object.

###post(doc)
To store new documents into the database. Unlike put call, it will
always create a new document with an id that is assigned during
document creation. If doc._id is passed, it is discarded.
This implementation does not use the POST method. The reason comes
from CouchDB docs: "It is recommended that you avoid POST when
possible, because proxies and other network intermediaries will
occasionally resend POST requests, which can result in duplicate
document creation."
A Promise is returned with the response from CouchDB.
@param {doc} document as a javascript object.

###query(view, options)
To query a map design/view on the database considering the
options' values. The resulted documents will be passed
to the callback function.
A Promise is returned with the query result from CouchDB.
@param {view} name of the design/view as defined on database.
@param {options} query options as a javascript object.
