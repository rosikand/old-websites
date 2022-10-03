# Lecture 3: Collections

## Parameter Passing in C++

- When you pass an argument into a function, you are making a copy of the local version of that function--that copy is then the thing that is sent to the function. Thus, any edits that aren't returned regarding that parameter, nothing will happen. This is called "pass **by value**" and the copy of that variable being passed in is referred to as a "xeroxes". Not mutable. However, we can make it mutable. 
- To pass the parameter "**by reference**", which means the parameter changes will persist (mutable), you have the option to do so in C++. The only difference in syntax is by specifying an "&" right after the type in the formal parameter. Like so: `void byReference(int& number)`. 
- To understand this a little better, the latter method **doesn't send a copy** to the function of the variable. It literally sends the variable (as in the memory of the computer). Thus, whatever name you may specify in the formal parameter is what that variable will become. 

##### Strings in C++

- In Python and Java, string variables don't actually hold the contents of the string in memory--they are simply pointers (addresses). However, in C++, the content of a string assigned to variable is exactly that stored in memory. 
- Look at the lecture for mote detail about how this works under the hood, but the functionality of it is still the same as with ints and doubles etc. in C++--just different from Java and Python. What does this mean? Strings are also immutable. However, like with ints etc., you can use the ampersand syntax as shown above to assign an alias to the string contents which effectively makes it mutable. 

##### A Question of Speed

So how do you decide? Pass in something "by value" or "by reference"? 

- Passing by value is obviously slower since you have to make a copy. 
- This is important for longer data (specifically strings etc.) and would slow down the program. 
- Thus, the general principle of when to do what is: "When passing a string into a function, use pass-by-reference unless you actually want a copy of the string". 

##### Pass-by-`const`-Reference

- There exists a third option instead of the two options above. Above, you didn't want to sacrifice speed, but sometimes you don't want to risk changing the content of your variable. Thus, we can use this method: 

- In essence, you hand the original content of the variable to the function as if you were passing by refence--avoiding the need to copy. Except, here, the `const` part means that the function is not eligible to change the contents of the passed in argument. 

  **Syntax**: 

  ```c++
  void someFunction(const string& masterpiece)c{
    /* can read, but not change, the masterpiece.*/
  }
  ```

  Note that if you pass in by `const` and you try to make edits to the thing passed in, then you will get an error.  

##### Parameter Passing Flowchart

When deciding which of the three methods to use, use this flowchart: ![image-20210128050516941](/Users/rosikand/Library/Application Support/typora-user-images/image-20210128050516941.png)

## Container Types

- A container type is a type of the "collection class" that is a data type in C++ that is used to store and organize data in some form. 
- "Some type of thing that stores other things". 
- In Python, these would be like lists, dictionaries, etc. (we just group these under common umbrella called container types in C++). 
- Also referred to as the "collection class", "abstract data type", "container class". 

It is important to analyze the pros and cons of each and see which one to use (regarding efficiency and functionality purposes). 

## The Vector type

- A Vector is a collection class representing a list of things.

- **Like an array/list**. 

- Unlike in Python, C++ vector components **must consist of the same typ**e. 

  **Syntax**:

   `Vector<type> name;` 

  Example: 

  ```c++
  Vector<int> v = {1, 3, 7}; 
  ```

  Notice the use of curly brackets. 

- **Append**: `V += 270;` is equivalent to `V.append(270)` from Python. 

- **Indexing:** works like Python: `V[0]`. 

- **Slicing**: we use "sublists" in C++. Returns a vector. `V.subList(0,2);` where it starts at index 0 and goes 2 more indeces. 

- **Remove:** `V.remove(index);`

- **Looping** through vectors: 

  - ```c++
    // regular, counter-based for loop
    for (int i = 0; i < v.size(); i++) {
    		cout << v[i] << endl;
    }
    ```

  - ```c++
    // 'for-each', range-based for loop
    for (int elem: v) { // replace int with designated data type
      cout << elem << endl;
    }
    ```

##### Objects in C++

- Unlike Java and Python, the variable is storing the actual object contents and is not simply a reference lile in Python and Java. Thus, objects work similarly to strings (see paragraph above). 
- Thus, container types, which are objects of the collections class, work similary to strings. 
- Can also pass objects (and therefore container types by reference with the ampersand). 

## Recursion on Vectors

- Recall that with Strings, when doing recursion, we recommended splitting the string into each individual character and starting with the first. The same process applies here. ![image-20210128055031574](/Users/rosikand/Library/Application Support/typora-user-images/image-20210128055031574.png)



#### Extra Notes on Memory Management

- In Python, the address of the list/string variable is passed in to the function. Thus, any changes will correspond to the same address (hence, mutable). However, in C++, a copy of the actual vector is sent in... not an address. Thus, that copy will be changed instead--unless you pass it in by reference. 

#### Active Recall Questions

https://www.notion.so/Lecture-3-Collections-Active-Recall-43e81b6f108a44408a74bfb6382d82f0

