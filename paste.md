To read JSONB data into IndexedDB, you typically follow these steps:

1. **Open or Create an IndexedDB Database**: Use the `indexedDB.open` method to create or open a database.

2. **Create an Object Store**: If the database is newly created, you need to create an object store to hold your data.

3. **Insert JSONB Data**: Convert your JSONB data into a format that can be stored in IndexedDB (usually a plain JavaScript object) and then use the `add` or `put` method to insert it into the object store.

4. **Retrieve Data**: Use the `get` or `getAll` methods to read the data back from IndexedDB.

Here’s a simple example in JavaScript:

```javascript
// Step 1: Open or create a database
const request = indexedDB.open("MyDatabase", 1);

request.onupgradeneeded = function(event) {
    const db = event.target.result;
    // Step 2: Create an object store
    const objectStore = db.createObjectStore("MyObjectStore", { keyPath: "id" });
};

request.onsuccess = function(event) {
    const db = event.target.result;

    // Example JSONB data (as a JavaScript object)
    const jsonData = {
        id: 1,
        name: "John Doe",
        age: 30,
        address: {
            city: "New York",
            state: "NY"
        }
    };

    // Step 3: Insert JSONB data
    const transaction = db.transaction(["MyObjectStore"], "readwrite");
    const objectStore = transaction.objectStore("MyObjectStore");
    const addRequest = objectStore.add(jsonData);

    addRequest.onsuccess = function() {
        console.log("Data added to the database.");
    };

    // Step 4: Retrieve data
    const getRequest = objectStore.get(1);
    getRequest.onsuccess = function() {
        console.log("Data retrieved from the database:", getRequest.result);
    };
};

request.onerror = function(event) {
    console.error("Database error:", event.target.errorCode);
};
```

### Explanation:
- **Opening the Database**: The `indexedDB.open` method is used to open a database. If the database version is new or has changed, the `onupgradeneeded` event is triggered, allowing you to create an object store.
- **Creating an Object Store**: The object store is created with a key path (in this case, `id`).
- **Inserting Data**: The JSONB data is added to the object store using the `add` method.
- **Retrieving Data**: The data can be retrieved using the `get` method, which fetches the record with the specified key.

This example demonstrates how to work with JSONB-like data in IndexedDB. You can adapt the structure of the `jsonData` object to match your specific JSONB data structure.