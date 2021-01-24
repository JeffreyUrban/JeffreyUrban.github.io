---
title: C++
has_children: true
---

# Runtime type information
Make the details of compiler / system specific size and precision of types available: 

	#include <climits>, #include <cfloat>

# Constant literals
Specify type via postfix including `U`, `L`, `LL`, `F`, `L`, such as `12L` _(long int)_

# Constants

_Recommended instead of `#define` constants (which are just a blind find / replace by pre-processor and lack type checking)._

Use `const <type> <name> {value};`
  
   
# Vectors `std::vector`

_Recommended vs arrays_

```
// initialize all values to zero
Vector <int> my_vector (length); 

// specify list
Vector <int> my_vector {<value>, <value>, <value>}; 

// initialize all values
Vector <int> my_vector (length, <value>); 

// Slice one vector from another
vector<int> my_slice(myVector.begin() + startIndex, myVector.begin() + endIndex);
```

# Type casting

	static_cast<target-type>(<source>)

# Modify io stream

	cout << std::boolalpha; // change mode to write true / false
	cout << std::noboolalpha; // change mode to write 1, 0.

# For loop

	for (size_t i {0}; i < <value>; i++)
	for (char c: s1)

# For-range loop

	for (<type> <variable-name-in-loop>: <collection>) {}
	for (auto <variable-name-in-loop>: <collection>) {}

# String objects

	`#include <string>`
	
Support comparisons, equality

Common methods: `length`, `substr`, `find`, `erase`, `clear`

`my_string += " more string content";`

Input a string:

	cin >> my_string
	get_line(cin, my_string)
	get_line(cin, my_string, '<single-char-delimiter>')

# Bounds checking

For bounds checking, use `.at()` for vector and string objects instead of index.

# Null pointer

Use `nullptr`, not `NULL`, which is deprecated. `nullptr` is a real pointer, whereas `NULL` is just a value.

# Hash Map

	unordered_map<string,int>myMap;
	myMap.insert(make_pair("Purple",16));
	myMap["BLACK"]=4;

# Unordered Set

	unordered_set<string> lightBulbs;
	lightBulbs.insert("incandescent");

# Graph representations

As Edge List: 

	vector<vector<int>> graph = {{0, 1}, {1, 2}, {1, 3}, {2, 3}};

_Keep in mind, this won't include nodes with no edges. Consider separate node list._

As Adjacency List (index is node number): 

	vector<vector<int>> graph = {
		{1},
		{0, 2, 3},
		{1, 3},
		{1, 2}
	};

As Unordered Map (key is node number or name):

	unordered_map<int, vector<int>> graph {
		{0, {1}},
		{1, {0, 2, 3}},
		{2, {1, 3}},
		{3, {1, 2}}
	};
	
As Adjacency Matrix (non-zero when link exists):

	vector<vector<int>> graph {
		{0, 1, 0, 0},
		{1, 0, 1, 1},
		{0, 1, 0, 1},
		{0, 1, 1, 0},
	};

# Monitor class

'syntactic sugar' to wrap operations in mutexes for thread safety.

# Random

Random distributions, etc.

	#include <random>

Random value 0-99: `rand()%100`. Returns `0` to `RAND_MAX`

Seed random number generator:

	#include <ctime>
	srand(time(nullptr));

# Time

	#include <time>

Present time in seconds from epoch: `time(0)`

# Decimal output

Set floating point value to trailing precision in decimal (here, `0.00`): `setprecision(2)`

Can be used inline in text string formation, such as `cout << setprecision(2) << <number>;`

# Parameters

`<type>& <name>`: Use `&` to pass in by reference. Can access directly using `<name>`, without de-reference.

Arrays are passed in by reference anyways.
