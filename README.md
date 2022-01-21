## CAT - C Adapted Two

An adapted version of C++ (C2) with support for more advanced programming.

### Additions

#### 0 argument function calls 

Functions that do not take arguments can be called either with or without an open/close parentheses.
For example, the function `onePlusTwo` would be written as:

```c++
int onePlusTwo() { return 1 + 2; }
```

Calling the function could be done two ways:
```c++
int three = onePlusTwo;
int three = onePlusTwo();
```

The functionality is the same either way.

#### Function pointers

In c++, getting the address of a function is done by writing the function without an open/close parentheses:

```c++
int myFunction(int a, int b, int c) { return 0; }
int* myFunctionAddress = myFunction;
```

However, in cat, functions written with or without an open/close parentheses are the same.
Because of this, in cat, function addresses are obtained by writing the address operator ( & ) before the function name:

```c++
int* myFunctionAddress = &myFunction;
```

Arguments can be supplied in this case, but they will be ignored and it is advised to not supply arguments.

```c++
int* myFunctionAddress = &myFunction(0,1,2); // The arguments are ignored here.
int* myFunctionAddress = &myFunction(); // This has the same effect, since the arguments are irrelevant.
```

#### Link ( <=> ) operator

Similar to the equal ( **=** ) operator. Used for setting the value of a variable.
Makes a 'linked' variable, which always has the same value as one previously defined variable.
This is identical to giving an existing variable an alternate name.
Defining a linked variable DOES NOT use new memory or create new data. It instead refers to the memory and data of the linked variable.
Changing the value of either the original or the linked variable will update BOTH variables.

NOTE: This has the same effect as creating a reference in C++.

```c++
int value = 5;
int same <=> value;
printf("value: %i, same: %i \n"); // value: 5, same: 5
value = 256; 
printf("value: %i, same: %i \n"); // value: 256, same: 256
same = 0; 
printf("value: %i, same: %i \n"); // value: 0, same: 0
int* addressOfValue = &value;
int* addressOfSame = &same;
printf("value address: %p, same address: %p \n"); // value address: 0x00CAT2, same address: 0x00CAT2
```

#### Dependent ( <= ) operator

This operator is used to create a variable that evaluates a single expression each time its value is accessed. Like a linked variable, a 'dependent' variable has none of its own memory or data. It acts functionally similar to an inlined function, in that it will collapse to an expression that gets evaluated on the spot each time it is referenced.
Below is an example of how this could be utilized to create a variable that keeps track of the bottom-right point of a rectangle that keeps variables for only its top-left corner and size.

```c++
struct pt {
	int x, y;
	pt() {
		x = 0; y = 0;
	}
	pt(int nx, int ny) {
		x = nx; y = ny;
	}
};
struct rect {
	pt pos = pt(0,0);
	int w = 10;
	int h = 10;
	int center <= pt(pos.x + w, pos.y + h);
}
```

#### Namespace inheritance

In c++ a namespace cannot be inherited like a class or struct can. In cat, a namespace can inherit another just like a class:

```c++
namespace basicMath {
	virtual int add(int a, int b) {
		return a + b;
	}
	int multiply(int a, int b) {
		return a * b;
	}
};
namespace advancedMath:  {
	int add(int a, int b) {
		return 0 + a + b + 0;
	}
};
```

In this example the namespace `advancedMath` already has the `multiply` function defined in `basicMath`.
