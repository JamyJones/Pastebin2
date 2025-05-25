In IndexedDB, the `db.transaction().objectStore()` method is used to access a specific object store within a transaction. When you call `objectStore()` on a transaction, it returns an `IDBObjectStore` instance, which allows you to perform operations on the records in that object store.

To retrieve all records from an object store, you can use the `getAll()` method of the `IDBObjectStore` instance. Here’s a basic example of how to do this:

```javascript
// Open a transaction and access the object store
const transaction = db.transaction('yourObjectStoreName', 'readonly');
const objectStore = transaction.objectStore('yourObjectStoreName');

// Use getAll() to retrieve all records
const request = objectStore.getAll();

request.onsuccess = function(event) {
    const allRecords = event.target.result;
    console.log(allRecords); // This will log all records in the object store
};

request.onerror = function(event) {
    console.error('Error retrieving records:', event.target.error);
};
```

In this example:
- Replace `'yourObjectStoreName'` with the name of your object store.
- The `getAll()` method retrieves all records and returns them in an array when the request is successful. You can handle the results in the `onsuccess` event handler.