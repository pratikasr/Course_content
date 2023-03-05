Here's an example function that stores data in a key-value store and then displays it using the Cosmos SDK in Go:


    package main

    import (
    "fmt"

    sdk "github.com/cosmos/cosmos-sdk/types"
    "github.com/cosmos/cosmos-sdk/store/dbadapter"
    "github.com/cosmos/cosmos-sdk/store/tracekv"
    "github.com/cosmos/cosmos-sdk/store/types"
    )
    
    func storeData(ctx sdk.Context, storeKey sdk.StoreKey) {
    // set a key-value pair in the store
    key := []byte("hello")
    value := []byte("world")
    ctx.KVStore(storeKey).Set(key, value)
    }
    func displayData(ctx sdk.Context, storeKey sdk.StoreKey) {
    // get the value associated with the key from the store
    key := []byte("hello")
    retrievedValue := ctx.KVStore(storeKey).Get(key)

    // print the retrieved value
    fmt.Printf("retrieved value: %s\n", retrievedValue)
    }

The storeData() function takes a sdk.Context object and a sdk.StoreKey object as input. It uses the context object to create a new KV store using the KVStore() method and the provided store key. It then uses the Set() method of the KV store interface to set a key-value pair in the store. In this case, the key is the byte slice []byte("hello"), and the value is the byte slice []byte("world"). This stores the string "world" in the store with the key "hello".

The displayData() function also takes a sdk.Context object and a sdk.StoreKey object as input. It uses the context object to create a new KV store using the KVStore() method and the provided store key. It then uses the Get() method of the KV store interface to retrieve the value associated with the key "hello" from the store. In this case, the value retrieved is the byte slice []byte("world"). Finally, the function prints the retrieved value to the console using the fmt.Printf() function.