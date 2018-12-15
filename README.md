# PublicArrayGetter 

An array-manipulating Typescript/Javascript class with methods that return items copied   
from the array. None of the methods modify the array.

To include in your project:

    // if using Typescript:
    import { PublicArrayGetter } from '@writetome51/public-array-getter';
    // if using ES5 Javascript:
    var PublicArrayGetter = require('@writetome51/public-array-getter').PublicArrayGetter;

To instantiate, pass the actual array it will contain into its constructor:

    let get = new PublicArrayGetter( [item1, item2, item3,...] );

You can also reset the array by accessing the class `.data` property:

    get.data = [1,2,3,4,...];


## Properties

	data : any[] (read-writable) // the actual array


## Methods

    copy(): any[]
        // returns independent copy of this.data .

    byIndex(index): any
        // returns item identified by index.  index can be negative or positive.
    
    byIndexes(indexes): any[]
        // returns items identified by indexes.  indexes can be negative or positive.

    head(numItems): any[]
        // returns numItems from beginning of this.data

    tail(numItems): any[]
        // returns numItems from end of this.data

	between(numItemsToIgnoreAtEachEnd): any[]
        // returns middle of this.data, between numItemsToIgnoreAtEachEnd

    adjacentAt(startingIndex, numItems): any[]
        // Beginning at startingIndex, returns adjacent numItems.  
        // startingIndex can be negative or positive.
        
NOTICE: For all the methods below, any parameter called `value` cannot be an object.  
This does not include arrays. Arrays are OK, as long as they don't contain objects.

    adjacentToValue(info: IAdjacentToValueInfo): any[]
	    /********
        Returns adjacent items including, or near, a particular value.
        Only applies to the first instance of value found in array.
        The parameter 'info' is an object that looks like this:
        {
            value: any except object (the value to search for in this.data),
            offset: integer (tells function where, in relation to value, to begin selecting 
                    adjacent items to return.  If offset is zero, the selection will begin 
                    with value.)
            howMany: integer greater than zero (it's how many adjacent items to return)
        }

        Example:
             let get = new PublicArrayGetter( [1,2,3,4,5,6,7,8,9,10] );
             let numbers = get.adjacentToValue({value:5, offset: -2, howMany:3});
             // numbers is now [3,4,5]
        *********/

	allAfterFirst(value: any): any[]
        // returns all items after first instance of value.

	allBeforeFirst(value: any): any[]
        // returns all items before first instance of value.

	allAfterLast(value: any): any[]
        // returns all items after last instance of value.

	allBeforeLast(value: any): any[]
        // returns all items before last instance of value.

	uniqueItems(): any[]
        // returns no duplicates.

	duplicates(): any[]
        // returns every instance of a duplicate, so you may get multiple instances.

	shuffled(): any[]
        // returns new version of this.data with order of items randomized.
        
The last 2 methods below return an array of IValueIndexPairs.  
A IValueIndexPair is this object: `{value: any, index: integer}`  
It represents an array item's value and index.

	byTest(testFunction: ((currentItem, currentIndex?, array?) => boolean)): IValueIndexPair[]
        // Almost exactly like Array.filter(), except it returns array of IValueIndexPairs.
     
	byType(
	    type: 'object' | 'array' | 'number' | 'string' | 'boolean' | 'function' | 'undefined'
	):  IValueIndexPair[] 
        // returns all items that match the passed type. 
        // The passed type can be any one of the possible type hints above.