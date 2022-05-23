# before-finde
More alis
// Properties available
Moralis.Cloud.beforeFind("MyObject", (req) => {
  let query = req.query; // the Moralis.Query
  let user = req.user; // the user
  let triggerName = req.triggerName; // beforeFind
  let isMaster = req.master; // if the query is run with masterKey
  let isCount = req.count; // if the query is a count operation
  let logger = req.log; // the logger
  let installationId = req.installationId; // The installationId
});

// Selecting keys
Moralis.Cloud.beforeFind("MyObject", (req) => {
  let query = req.query; // the Moralis.Query
  // Force the selection on some keys
  query.select(["key1", "key2"]);
});

// Asynchronous support
Moralis.Cloud.beforeFind("MyObject", (req) => {
  let query = req.query;
  return aPromise().then((results) => {
    // do something with the results
    query.containedIn("key", results);
  });
});

// Returning a different query
Moralis.Cloud.beforeFind("MyObject", (req) => {
  let query = req.query;
  let otherQuery = new Moralis.Query("MyObject");
  otherQuery.equalTo("key", "value");
  return Moralis.Query.or(query, otherQuery);
});

// Rejecting a query
Moralis.Cloud.beforeFind("MyObject", (req) => {
  // throw an error
  throw new Moralis.Error(101, "error");

  // rejecting promise
  return Promise.reject("error");
});

// Setting the read preference for a query
Moralis.Cloud.beforeFind("MyObject2", (req) => {
  req.readPreference = "SECONDARY_PREFERRED";
  req.subqueryReadPreference = "SECONDARY";
  req.includeReadPreference = "PRIMARY";
});
