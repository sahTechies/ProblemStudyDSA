# Array-Based Stack Implementation in C

**Institution:** SRM IST TRICHY <br>
**Subject:** Data Structures and Algorithms (DSA) <br>
**Name:** HEMANT KUMAR SAH<br>
**Registration Number:** RA2511026050326<br>

This repository contains an assignment demonstrating a standard contiguous LIFO (Last-In, First-Out) stack implementation in C. For detailed manual traces and step-by-step execution, please refer to the included file named `report.pdf`.

## Program Components
* **Data Structure:** Array-based Stack operating on the LIFO (Last-In, First-Out) principle.
* **Variables:** 
  * `stack`: An integer array of size 5 representing the stack storage.
  * `top`: An integer representing the index of the top element.
  * `item`: An integer in `main()` to store popped values and push arguments.
  * `i`: A loop counter variable inside `display()`.
* **Initial Values:** `SIZE = 5`, `top = -1`.

## Source Code

```c
#include <stdio.h>
#define SIZE 5

int stack[SIZE];
int top = -1;

void push(int item)
{
    if (top == SIZE - 1)
    {
        printf("Stack Overflow\n");
    }
    else
    {
        top++;
        stack[top] = item;
        printf("Pushed: %d\n", item);
    }
}

int pop()
{
    if (top == -1)
    {
        printf("Stack Underflow\n");
        return -1;
    }
    else
    {
        int item = stack[top];
        top--;
        return item;
    }
}

void display()
{
    int i;

    if (top == -1)
    {
        printf("Stack is Empty\n");
    }
    else
    {
        printf("Stack: ");
        for (i = 0; i <= top; i++)
        {
            printf("%d ", stack[i]);
        }
        printf("\n");
    }
}

int main()
{
    int item;

    push(10);
    push(20);
    push(30);

    display();

    item = pop();
    printf("Popped: %d\n", item);

    push(40);
    push(50);
    push(60);
    push(70);

    display();

    item = pop();
    printf("Popped: %d\n", item);

    item = pop();
    printf("Popped: %d\n", item);

    item = pop();
    printf("Popped: %d\n", item);

    item = pop();
    printf("Popped: %d\n", item);

    item = pop();
    printf("Popped: %d\n", item);

    display();

    item = pop();
    printf("Popped: %d\n", item);

    return 0;
}
```

## Execution and Output

**Predicted Console Output:**
```text
Pushed: 10
Pushed: 20
Pushed: 30
Stack: 10 20 30
Popped: 30
Pushed: 40
Pushed: 50
Pushed: 60
Stack Overflow
Stack: 10 20 40 50 60
Popped: 60
Popped: 50
Popped: 40
Popped: 20
Popped: 10
Stack is Empty
Stack Underflow
Popped: -1
```
*Note: The final stack state results in `top = -1`, meaning the stack is logically empty, although residual integers remain in the physical array memory.*

## Error Triggers and Limitations
* **Stack Overflow:** This is caused by the `push(70);` operation when the `top` index is already at 4 (which is `SIZE - 1`), exceeding the maximum stack capacity of 5.
* **Stack Underflow:** This occurs during the final `item = pop();` call at the end of the `main()` function because all elements have already been removed, resulting in `top = -1`.
* **Fixed Size Limitation:** The array size is hardcoded to 5 and cannot dynamically scale up to accommodate more data.
* **Return Value Ambiguity:** When an underflow occurs, the `pop()` function returns `-1`. If a user intentionally pushes `-1` onto the stack and then pops it, the calling function cannot distinguish between a successful pop of `-1` and an underflow error. A suggested correction is to pass the popped item back via a pointer argument and return a boolean/status code from the `pop()` function.

## Additional Test Cases

| Test Case Intent | Actions | Expected Output |
| :--- | :--- | :--- |
| **Immediate Underflow** | Empty `main()`, call `pop()` | `Stack Underflow`, returns `-1` |
| **Rapid Fill** | Loop `push(1)` 6 times | 5 times `Pushed: 1`, 1 time `Stack Overflow` |
| **Ambiguity Check** | `push(-1); item = pop();` | `Pushed: -1` <br> `Popped: -1` (No underflow printed) |
