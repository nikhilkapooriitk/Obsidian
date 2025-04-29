#### Set
Used to store unique elements. Stores them in ascending order. Order can be specified manually too. Strings are lexicographically (dictionary order) sorted.

`set<DataType, Binary Function> setVariableName;` 
`set<int> s1;`
`set<int> s2 = {1, 2, 3, 4};`
`s2 = s1;`
`set.insert(5);`
`set<int>::iterator it1 = s1.begin();         // returns an iterator to first element`
`*it1*          // access the value stored in iterator`
`auto it2 = next(it1. 2)         // moves the value it2 to 2 element after it1`
`auto it3 = s1.end() ;      // iterator to end of set. Not a value here.`
`auto it4 = s1.find(3) ;         // iterator to the value of 3 or to end if 3 is not present`
`s1.erase(3);          // delete element by value`
`s1.erase(s.begin());         // delete first element by iterator`
`it4 != s1.end() ;          // condition to check if value is found`
int n = s1.size() ; 
int emp = s1.empty(); 
`// Traversing using range based for loop`
`for(auto it = s.begin(); it != s.end(); it++) cout<<* it;`
`// take unique elements of a vector into a set`
`set<int> uniqueSet ( v.begin(), v.end() );`

| **Operation**            | **Time Complexity** |
| ------------------------ | ------------------- |
| Insert an element        | *O(log n)*          |
| Delete an element        | *O(log n)*          |
| Find the largest element | *O(1)*              |
| Find smallest element    | *O(1)*              |
| Find element by value    | *O(log n)*          |
| Traverse the set         | *O(n)*              |
#### Map
Used to store key-value pair

`**map*** <key_type, value_type, comp> m;         // if comparator function is not provided, then default is increasing order`
`map<int, string> m {{1, "Geeks"}, {2,"For"}, {3,"Geeks"}} ;`
`m.insert({1, "Geeks"});        // Inserting a key value pair`
`// accessing data elements of map. Use map.at(i) to not create new element. If used map[i] then if the value is not present it'll create a new pair with default value`
`auto it = m.find(2);`
`if(it != m.end() )     // Condition to check if key is found`
`it->first; it->second;        // access first and second elements`
`// Traversing a map`
`for (auto i = m.begin(); i != m.end(); i++) cout<<i->first<<;`
`for(auto i:m) cout<<i.first;`
`m.erase(2);      // Deleting by key`
`m.erase(m.begin());       // Deleting by iterator`
`m.size()      // size of map`
`m.empty()     // return if map is empty`
`m.clear()     // removes all elements of the map`

|****Operation****|****Time Complexity****|
|---|---|
|Insert an element|****O(log n)****|
|Delete an element by key|****O(log n)****|
|Access element by key|****O(log n)****|
|Find an element by key|****O(log n)****|
|Update element by key|****O(log n)****|
|Traverse the map|****O(n)****|