##  Problem Overview

You will implement a `HashTable` class that stores:

-   **string keys**
-   **int values**

You are NOT allowed to use:

-   `std::unordered_map`
-   `std::map`

You must implement the data structure manually.

## Part 1 -- Class Structure

Use the following internal structure:

```cpp
#include <vector>
#include <list>
#include <string>
using namespace std;

class HashTable {
private:
    vector<list<pair<string, int>>> table;
    int currentSize;
    int capacity;
    int collisionCount;

    int hashFunction(const string& key) const;
    void rehash();

public:
    HashTable(int size = 11);

    void insert(const string& key, int value);
    bool remove(const string& key);
    int search(const string& key) const;
    double loadFactor() const;
    int size() const;
    bool isEmpty() const;
    void printTable() const;
};
```

##  Part 2 -- Hash Function

Implement a polynomial rolling hash:

```cpp
int HashTable::hashFunction(const string& key) const {
    const int prime = 31;
    long long hash = 0;

    for (char c : key) {
        hash = hash * prime + c;
    }

    return hash % capacity;
}
```

## Part 3 -- Insert & Collision Handling

-   Use separate chaining (`vector<list<>>`)
-   If inserting into a non-empty bucket, increment `collisionCount`
-   If key already exists, update value instead of duplicating

## Part 4 -- Resizing (Rehashing)

When:

    loadFactor() > 0.75

You must:

1.  Double the table capacity
2.  Reinsert all existing elements
3.  Reset collision counter appropriately

## Part 5 -- Testing Program

In `main()`:

1.  Insert at least 100 words
2.  Print:
    -   Table capacity
    -   Number of elements
    -   Load factor
    -   Total collisions
3.  Search for:
    -   Existing key
    -   Non-existing key
4.  Remove some keys and verify correctness

## Part 6 -- Experimental Analysis

Test three input types:

1.  Random strings  
2.  Sequential keys (e.g., student1, student2, ...)  
3.  Same prefix keys (e.g., data_0001, data_0002, ...)

Record:

-   Total collisions
-   Maximum bucket size
-   Average bucket length

Write a short explanation (1--2 paragraphs) describing what you observe.

------------------------------------------------------------------------

## Full Code :

```
#include <iostream>
#include <vector>
#include <list>
#include <string>
using namespace std;

//part 1 provided code for hashtable
class HashTable {
private:
    vector<list<pair<string, int>>> table;
    int currentSize;
    int capacity;
    int collisionCount;

    int hashFunction(const string& key) const;
    void rehash();

public:
    HashTable(int size = 11);

    void insert(const string& key, int value);
    bool remove(const string& key);
    int search(const string& key) const;
    double loadFactor() const;
    int size() const;
    bool isEmpty() const;
    void printTable() const;
};

//sets up hashtable and sets values to 0 so we can start recording
HashTable::HashTable(int size) {
    capacity = size;
    currentSize = 0;
    collisionCount = 0;
    table.resize(capacity);
}

//part 2 provided code for hashfunction which converts the strings I provide into numbers
int HashTable::hashFunction(const string& key) const {
    const int prime = 31;
    long long hash = 0;

    for (char c : key) {
        hash = hash * prime + c;
    }

    return hash % capacity;
}

//insert algorithm that adds a new key-value pair or updates if it already exists
void HashTable::insert(const string& key, int value){
    int position = hashFunction(key);

    //checking if table is not empty, then it is a collision
    if (!table[position].empty()){
        collisionCount++;
    }
    //check if key already exists then update
    for (auto it = table[position].begin(); it != table[position].end(); ++it){
        if (it->first == key){
            it->second = value;
            return;
        }
    }
    //when key does not yet exist, then add value
    table[position].push_back({key, value});
    currentSize++; // increase counter for amount of elements

    //check loadfactor incase we need to increase table size
    if (loadFactor() > 0.75) {
        rehash();
    }
    
}

//remove algorithm that deletes key value pairs from table
bool HashTable::remove(const string& key){
    int position = hashFunction(key);

    //searches for specific key and deletes it as well as lowers counter
    for (auto it = table[position].begin(); it != table[position].end(); ++it){
        if (it->first == key){
            table[position].erase(it);
            currentSize--;
            return true;
        }
    }
    return false; //in case key that we want deleted does not exist yet
}

//search algorithm to look up key based on string that is requested
int HashTable::search(const string& key) const {
    int position = hashFunction(key);

    //looks through table based on provided string
    for (auto it = table[position].begin(); it != table[position].end(); ++it){
        if (it->first == key){
            return it->second;
        }
    }
    return -1; // just in case key does not exist
}

//calculates how full table is which is load Factor
double HashTable::loadFactor() const {
    return (double)currentSize / capacity;
}

//current number of elements
int HashTable::size() const {
    return currentSize;
}

//prints out each bucket and the key value pairs inside of each one
void HashTable::printTable() const {
    for (int i = 0; i < capacity; i++) {
        cout << "Bucket [" << i << "]: ";
        for (auto it = table[i].begin(); it != table[i].end(); ++it) {
            cout << "(" << it->first << ", " << it->second << ") ";
        }
        cout << "\n";
    }
}

//rehash algorithm which is only called when load factor/table is too full
void HashTable::rehash(){
    int oldCapacity = capacity;
    capacity = capacity * 2 + 1; // just doubles capacity

    //resets the table completely and all counters like collisions and size
    vector<list<pair<string, int>>> oldTable = table;
    table.clear();
    table.resize(capacity);
    currentSize = 0;
    collisionCount = 0;

    //reinsterts each element from the old table into the new bigger one
    for (int i = 0; i < oldCapacity; i++){
        for (auto it = oldTable[i].begin(); it != oldTable[i].end(); ++it){
            insert(it->first, it->second);
        }
    }
}

int main(){
    HashTable ht; // creates our hash table

    //my 100 word list which are animals
    string words[] = {
        "cat","dog","fish","bird","frog","lion","tiger","bear","wolf","fox",
        "deer","duck","goat","sheep","horse","cow","pig","hen","rat","bat",
        "snake","shark","whale","eagle","hawk","crow","dove","swan","crane","stork",
        "zebra","koala","panda","sloth","otter","skunk","moose","bison","camel","llama",
        "gecko","iguana","cobra","viper","python","boa","newt","toad","salamander","axolotl",
        "crab","clam","squid","prawn","shrimp","lobster","oyster","mussel","starfish","urchin",
        "ant","bee","wasp","moth","flea","tick","mite","louse","cricket","firefly",
        "parrot","toucan","penguin","ostrich","emu","kiwi","finch","robin","sparrow","wren",
        "mole","vole","shrew","stoat","ferret","badger","weasel","mongoose","meerkat","lemur",
        "clownfish","swordfish","catfish","pufferfish","jellyfish","seahorse","narwhal","walrus","manatee","platypus"
    };

    //goes through each word and inserts it into the hash table. i starts from 0 and counts until finished
    int numWords = sizeof(words) / sizeof(words[0]);
    for (int i = 0; i < numWords; i++){
        ht.insert(words[i], i + 1);
    }
    // prints amount of elements and load factor once all elements are in the hashtable
    cout << "Elements: " << ht.size() << "\n";
    cout << "Load factor: " << ht.loadFactor() << "\n";

    // searching for a cat which is a word that exists inside the table. Returns 1
    cout << "Search cat: " << ht.search("cat") << "\n";

    //diyor was never inside the table so it will return -1
    cout << "Search diyor: " << ht.search("diyor") << "\n";

    // calls the remove function and verifies that it has been removed
    bool removed = ht.remove("dog");
    if (removed) {
        cout << "Removing dog: success\n";
    } else {
        cout << "Removing dog: not found\n";
    }

    int dogSearch = ht.search("dog");
    if (dogSearch == -1) {
        cout << "Search dog after remove: not found\n";
    } else {
        cout << "Search dog after remove: found\n";
    }

    return 0;
} 


```
