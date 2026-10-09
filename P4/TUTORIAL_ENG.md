# 🚀 Practicum Tutorial Module: Struct & Pointer

**Case Study:** Minimarket & Membership CLI App

**Learning Objectives:** Understanding how to manipulate data directly in memory (*Pass by Reference*) using C.

Welcome to the assistance session! We will learn the last two crucial concepts in C (Pointer & Struct) step-by-step, then combine them into a real final project.

## 1. 🎯 Basic Pointer Concepts

### Core Concept (Must Understand!)

A pointer is a special variable that does not store a direct value (like the number 10), but rather stores the **memory address** where that value is located.

Two magic operators you **must** know when playing with pointers:

* 📌 **Reference (`&`) - *Address-of Operator*:**
  Used to **get the address** of a variable.
  *(Analogy: "Where is Budi's house located?")*

* 🔑 **Dereference (`*`) - *Value-at Operator*:**
  Used to **access or change the content/value** at the address pointed to by the pointer.
  *(Analogy: "Open the door of the house at that address, then change what's inside!")*

### 💻 Hands-on 1: Creating and Using Pointers

```
#include <stdio.h>

int main() {
    int number = 10;
    // ptrNumber stores the address of 'number'. Use the & (Reference) symbol.
    int *ptrNumber = &number; 

    printf("Initial number value: %d\n", number);
    printf("Memory address of number: %p\n", &number);
    
    // Using the * (Dereference) symbol to view its value
    printf("Value pointed to by ptrNumber: %d\n", *ptrNumber);

    // Changing the value directly in its original memory via pointer
    *ptrNumber = 25;
    printf("\nNumber value after being changed via pointer: %d\n", number);

    // --- Pointers and Arrays ---
    int arr[3] = {100, 200, 300};
    // The array name itself represents the address of the first element, so no & is needed
    int *ptrArr = arr; 
    printf("\nFirst element of array: %d\n", *ptrArr);
    printf("Second element of array: %d\n", *(ptrArr + 1));

    // 🎯 TODO MINI-CHALLENGE 1:
    // Try to change the value of the THIRD array element (the number 300) to 999 using the ptrArr pointer!
    // Write your code below and print the result:
    

    return 0;
}

```

### 💻 Hands-on 2: The Difference Between *Pass by Reference* and *Pass by Value*

This is the main reason why we use pointers when creating functions!

```
#include <stdio.h>

// Pass by Value (Only sends a photocopy / copy of the data)
void addValue(int x) {
    x = x + 10;
}

// Pass by Reference (Sends the access key to the original address)
void addReference(int *x) {
    *x = *x + 10;
}

int main() {
    int score1 = 5;
    int score2 = 5;

    addValue(score1);
    printf("After Pass by Value: %d (NOT CHANGED)\n", score1);

    // Must use & to send its address
    addReference(&score2); 
    printf("After Pass by Reference: %d (CHANGED!)\n", score2);

    // 🎯 TODO MINI-CHALLENGE 2:
    // 1. Create a new function called 'subtractReference(int *x)' above int main().
    // 2. Make the function subtract the value by 2.
    // 3. Call the function to reduce score2, then print the result!
    

    return 0;
}

```

## 2. 📦 Basic Struct Concepts

### Core Concept (Variable Wrapper)

Structs are used to group several variables (can be of different data types) into a single name or entity. Imagine it like creating a registration form that has name, age, and address fields.

> 💡 **IMPORTANT: DOT (.) VS ARROW (->)**
>
> * If you are accessing a struct variable normally, use a **dot (`.`)**. Example: `student1.age`
>
> * If you are accessing a struct using a **POINTER**, you **MUST** use an **arrow (`->`)**. Example: `ptrStudent->age`. (This will be very useful in our final project!).

*(Note: In this module, we use `typedef struct` to keep the code concise, so we don't have to keep writing the word `struct` as a prefix).*

### 💻 Hands-on 1: Creating and Using Structs

```
#include <stdio.h>
#include <string.h>

typedef struct {
    char name[50];
    int age;
    // 🎯 TODO MINI-CHALLENGE 3 (Part 1):
    // Add a new attribute here called 'gpa' with a float data type!
} Student;

int main() {
    Student std1;
    
    // Remember! You cannot assign a value to a char array using the = (equals) sign.
    // We MUST use strcpy (String Copy)
    strcpy(std1.name, "Budi Santoso"); 
    std1.age = 20;
    
    // 🎯 TODO MINI-CHALLENGE 3 (Part 2):
    // Assign a GPA value (e.g., 3.85) to std1, then print it along with the name and age!

    printf("Name: %s, Age: %d\n", std1.name, std1.age);
    return 0;
}

```

### 💻 Hands-on 2: Creating a Nested Struct

```
#include <stdio.h>
#include <string.h>

typedef struct {
    char streetName[50];
    int zipCode;
} Address;

typedef struct {
    char name[50];
    Address home; // Inserting the Address struct into the Employee struct
} Employee;

int main() {
    Employee emp1;
    strcpy(emp1.name, "Anisa");
    strcpy(emp1.home.streetName, "Jl. Raya ITS");
    emp1.home.zipCode = 60111;

    printf("%s lives at %s (%d)\n", emp1.name, emp1.home.streetName, emp1.home.zipCode);
    
    // 🎯 TODO MINI-CHALLENGE 4:
    // Try changing Anisa's home zipCode to 60115, then reprint the sentence above!

    return 0;
}

```

### 💻 Hands-on 3: Creating a Simple Database with Arrays

```
#include <stdio.h>

typedef struct {
    int id;
    int score;
} ExamData;

int main() {
    // Instant initialization for an array of structs
    ExamData classData[3] = {
        {101, 85},
        {102, 90},
        {103, 78}
    };

    for(int i = 0; i < 3; i++) {
        printf("ID: %d - Score: %d\n", classData[i].id, classData[i].score);
    }

    // 🎯 TODO MINI-CHALLENGE 5:
    // Create a 'totalScore' variable, then loop through the 'classData' array to sum all the scores.
    // After the loop finishes, print the average score!

    return 0;
}

```

## 3. 🏪 Tutorial: Building a Minimarket CLI App

Now it's time to put all the puzzle pieces together! We will start building the main project using the Struct and Pointer concepts we just learned.

### Step 1: Creating the Required Structs

We need `Product` (Item) and `Member`.

```
#include <stdio.h>
#include <string.h>

typedef struct {
    char name[50];
    int price;
    int stock;
} Product;

typedef struct {
    char name[50];
    int points;
} Member;

int main() {
    printf("[STEP 1 OK] Product and Member structs successfully prepared.\n");
    return 0;
}

```

### Step 2: Creating a Basic Database

We will initialize 5 Products and 2 Members using an *Array of Structs* inside the `main()` function.

```
#include <stdio.h>
#include <string.h>

// Declarations hidden so we can focus on data (Assume the structs above exist)
typedef struct { char name[50]; int price; int stock; } Product;
typedef struct { char name[50]; int points; } Member;

int main() {
    Product dbProduct[5] = {
        {"Soap", 5000, 10},
        {"Shampoo", 15000, 5},
        {"Bread", 12000, 8},
        {"Milk", 25000, 15},
        {"Coffee", 22000, 20}
    };

    Member dbMember[2] = {
        {"Anisa", 500},
        {"Budi", 100}
    };

    printf("[STEP 2 OK] Initial database successfully loaded!\n");
    return 0;
}

```

### Step 3: Creating the Transaction Function (Pointers in Action!)

Here is where **Pointers get to work!** Notice the use of the arrow operator (`->`).

This function will deduct the original stock quantity in memory, and add member points if the purchase total is >= 20,000.

```
#include <stdio.h>

typedef struct { char name[50]; int price; int stock; } Product;
typedef struct { char name[50]; int points; } Member;

// --- Basic Display Functions ---
void checkProduct(Product db[], int size) {
    printf("\n--- Product Catalog ---\n");
    for(int i = 0; i < size; i++) {
        printf("%d. %s - Rp%d (Stock: %d)\n", i+1, db[i].name, db[i].price, db[i].stock);
    }
}
void checkMember(Member db[], int size) {
    printf("\n--- Member Data ---\n");
    for(int i = 0; i < size; i++) {
        printf("%d. %s - Points: %d\n", i+1, db[i].name, db[i].points);
    }
}

// --- MAIN FUNCTION (Using Pointers) ---
// Receives a Product pointer (*p) and a Member pointer (*m)
void buyProduct(Product *p, Member *m, int qty) {
    if (p->stock >= qty) {
        p->stock -= qty; // Manipulate original memory via arrow -> operator
        
        int total = p->price * qty;
        printf("\n[TRANSACTION SUCCESSFUL] Bought %d %s. Total: Rp%d\n", qty, p->name, total);

        // Check points requirement & ensure member pointer is not empty (NULL)
        if (total >= 20000 && m != NULL) {
            m->points += 100;
            printf("[INFO] Congratulations! Member %s earned +100 Points!\n", m->name);
        }
    } else {
        printf("\n[TRANSACTION FAILED] Insufficient stock for %s!\n", p->name);
    }
}

int main() {
    printf("[STEP 3 OK] Transaction function compiled successfully!\n");
    return 0;
}

```

### Step 4: Combining Everything into a CLI App

Run the code block below to see our minimarket simulation in action!

```
#include <stdio.h>
#include <string.h>

typedef struct { char name[50]; int price; int stock; } Product;
typedef struct { char name[50]; int points; } Member;

void checkProduct(Product db[], int size) {
    printf("\n--- Product Catalog ---\n");
    for(int i=0; i<size; i++) {
        printf("%d. %s - Rp%d (Stock: %d)\n", i+1, db[i].name, db[i].price, db[i].stock);
    }
}
void checkMember(Member db[], int size) {
    printf("\n--- Member Data ---\n");
    for(int i=0; i<size; i++) {
        printf("%d. %s - Points: %d\n", i+1, db[i].name, db[i].points);
    }
}
void buyProduct(Product *p, Member *m, int qty) {
    if (p->stock >= qty) {
        p->stock -= qty;
        int total = p->price * qty;
        printf("\n[TRANSACTION] %d %s Sold. Total: Rp%d\n", qty, p->name, total);
        if (total >= 20000 && m != NULL) {
            m->points += 100;
            printf("  -> Member %s earned +100 Points!\n", m->name);
        }
    } else {
        printf("\n[FAILED] Stock for %s (Remaining: %d) is not enough to buy %d!\n", p->name, p->stock, qty);
    }
}

int main() {
    // 1. Setup Database
    Product dbProduct[5] = { {"Soap", 5000, 10}, {"Shampoo", 15000, 5}, {"Bread", 12000, 8}, {"Milk", 25000, 15}, {"Coffee", 22000, 20} };
    Member dbMember[2] = { {"Anisa", 500}, {"Budi", 100} };

    printf("=== WELCOME TO THE MINIMARKET ===\n");
    checkProduct(dbProduct, 5);
    checkMember(dbMember, 2);

    // 2. Transaction Simulation
    // REMEMBER! Use the & (Reference) symbol to pass the struct address from the array!
    buyProduct(&dbProduct[3], &dbMember[1], 2); // Budi buys 2 Milk (50k) -> Gets points
    buyProduct(&dbProduct[0], &dbMember[0], 1); // Anisa buys 1 Soap (5k) -> No points
    buyProduct(&dbProduct[2], NULL, 3);         // Non-member buyer buys 3 Bread (36k)

    // 🎯 TODO MINI-CHALLENGE 6:
    // Try simulating Budi buying 10 "Shampoo" below (It will definitely fail because stock is only 5).


    // 3. Prove that the data has been modified
    printf("\n=== DATA UPDATE AFTER TRANSACTIONS ===");
    checkProduct(dbProduct, 5);
    checkMember(dbMember, 2);

    return 0;
}

```

## 🛠️ 4. PRACTICUM TASK: Mandatory Challenges

**CHOOSE 2 OUT OF THE 3 CHALLENGES BELOW:**
Add/modify code from *Step 4* to implement the features below using Pointer concepts.

### 1. Update Product Price (Modifying Numbers)

Create a function `void updatePrice(Product *p, int newPrice)` that can be called by an Admin to permanently revise a product's price.

> 💡 **PRICE UPDATE TIPS:**
>
> You simply need to do value reassignment inside the function (example: `p->price = newPrice`). Try calling the function in `main` and see the changes using the `checkProduct` function.

### 2. Update Product Name (Typo Correction)

Create a function `void updateName(Product *p, char newName[])`.

> 💡 **STRING UPDATE TIPS:**
>
> Remember, in C, you **CANNOT** overwrite a *char array* directly using an equals sign (example: `p->name = newName` is **WRONG**). You must use the `<string.h>` library and the `strcpy(p->name, newName)` function.

### 3. Redeem Points = Discount (Logic)

Modify the logic inside the `buyProduct` function. If a member has points greater than or equal to `1000`, automatically give a 10% discount off their total purchase, and deduct 1000 from their member points!

> 💡 **REDEEM POINTS TIPS:**
>
> Add an *if-statement* inside the code block that handles the total price. Make sure you check whether `m` is not `NULL` first, and then check `m->points >= 1000`. If yes, deduct the points with `m->points -= 1000` and recalculate the `total` variable.

## 🏆 5. BONUS: Extra Challenge

For those who want maximum scores (*A/A+*), complete the extra challenge that will make your application feel like a real program!

### Interactive Menu (CLI Looping)

Change the program from *Step 4*, which originally ran statically just once and finished, into a **continuous interactive application** until the user chooses the "Exit" option.

> 💡 **BONUS CHALLENGE EXECUTION TIPS:**
>
> 1. **Use an Infinite Loop:** Wrap the entire logic flow inside the `main()` function (after initial database setup) into a `while(1)` or `do-while` loop.
>
> 2. **Create a Menu Display:** Print the menu navigation using `printf` every time the loop starts.
>
>    Example: `[1] View Products | [2] Buy Product | [3] Check Members | [4] Exit`
>
> 3. **Accept User Input:** Use `scanf` to capture the user's menu choice, then utilize a `switch-case` block to execute instructions based on the selected number.
>
> 4. **Exit the App:** If the user selects menu 4, execute the `break;` command to exit the loop, which will automatically stop the program from running.