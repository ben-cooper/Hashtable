# Hashtable with Chaining Library

## Specifications
* constant time lookup and insertion on average case
* chaining using a linked list if more than one element is added to the same hash value
* fixed size for underlying array

## Commands
* init_table creates the hashtable with the size determining the number of buckets
* insert the element with a specified hash into the table
* get_bucket returns the linked list associated to the hash
* destroy_list frees the linked list specified (usually for internal use)
* destroy_table free the hash table specified and each bucket
* print_list prints each element in the list to standard out
* print_table prints each element in the table to standard out

## Examples

```
#include "hashtable.h"
#include <string.h>

size_t hasher(char *word) {
	return strlen(word);
}

int main() {
	//destroy table also free the elements in each the table as well
	char *one = (char *) malloc(6 * sizeof(char));
	char *two = (char *) malloc(7 * sizeof(char));

	strcpy(one, "hello");
	strcpy(two, "world!");

	hashtable *table = init_table(10);

	insert(table, hasher(one), one);
	insert(table, hasher(two), two);
	
	print_list(get_bucket(table, 5));

	destroy_table(table);

	return 0;
}
```

## Algorithm
* The hashtable is actually an array of pointers to linked lists
* Each element added to an array index is prepended to the linked list at the index
* Destroying the table will also free each element in the table
* The size of the table and its corresponding variable in the struct remains fixed
