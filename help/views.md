#Views
CouchDB available docs are dense, vast but incomplete. This is an attempt to document each feature from end to end.
##Erlang native query server
Bear in mind that the native query server is not sandboxed and have access to the whole Erlang VM. That is, it will have access to the whole server's Operating System.
### Handling JSON structures from Erlang
[http://jamietalbot.com/2010/03/18/handling-json-objects-in-couchdb-native-erlang-views/]

### BuiltIn reduce functions
CouchDB has three built-in reduce functions. These are implemented in Erlang and run right inside CouchDB, so they are much faster than the equivalent JavaScript functions.
[http://wiki.apache.org/couchdb/Built-In_Reduce_Functions]
```javascript
{
  "_id":"_design/company",
  "_rev":"12345",
  "language": "javascript",
  "views":
  {
    "all_customers": {
      "map": "function(doc) { if (doc.type == 'customer')  emit(doc.id, 1) }",
      "reduce" : "_count"
    },
    "total_purchases_by_customer": {
      "map": "function(doc) { if (doc.type == 'purchase')  emit(doc.customer_id, doc.amount) }",
      "reduce": "_sum"
    }
  }
}
```
