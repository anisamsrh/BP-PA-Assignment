# For IUP Students

## Mini Project
There is no project for this module

## Problem Set
### Set 1
```c
#include <stdio.h>

int x = 10; 

void process() {
    int x = 5; 
    x = x + 2;
}

int main() {
    printf("%d", x);
    process();
    printf("%d", x);
    return 0;
}
```
1. What value will be printed on the screen when the program is run? 
2. Why is the function process(); does not change the value printed on the second printf ? 

### Set 2
```c
#include <stdio.h>

int times_two(int a) {
    a = a * 2;
    return a;
}

int main() {
    int number = 4;
    times_two(number);
    printf("Result: %d", number);
    return 0;
}
```
If you run the program the output is Result: 4, not 8. 
1. Explain technically why the variable number inside  main()does not change! 
2. How to fix the code inside main()so that the output becomes 8?

### Set 3
```c
#include <stdio.h>

int main() {
print_message();
    return 0;
}

void print_message() {
    printf("Hello from function!");
}
```
The  program above will produce the message error or warning when compiled (build). 
1. Why does this happen? 
2. Fix the problem!

### Set 4
```c
#include <stdio.h>

int add(int n) {
    if (n == 0) { 
        return 0;
    } else {
        return n + add(n -1);
    }
}

int main() {
    printf("%d", add(-3));
    return 0;
}
```
If we call the function add(-3) with negative number arguments as in the function main() above, what will happen to the program? Connect your answer to the concept Base Case on recursion function!

### Set 5
```c
#include <stdio.h>

void print_number(int n) {
    if (n > 0) { // Implicit base case: stop if n <= 0
print_number(n-1); // Recursive call
        printf("%d ", n);
    }
}

int main() {
print_number(3);
    return 0;
}
```
1. If the program is run, does the output printed on the screen is 3 2 1 or 1 2 3?
2. Explain technically why that sequence of numbers is printed!
3. If we want to change output to be the opposite order, which part of the code should be moved?
