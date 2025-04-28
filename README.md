
//1)Implementation of insertion and deletion in a specific position in an array using function
 
#include <stdio.h>
#define MAX_SIZE 100
 
void insertElement(int arr[], int *size, int item, int pos) {
    if (*size == MAX_SIZE) {
        printf("Array is full! Cannot insert more elements.\n");
        return;
    }
    if (pos < 1 || pos > *size + 1) {
        printf("Invalid position!\n");
        return;
    }
    // Shift elements to the right to make space for the new element
    for (int i = *size; i >= pos; i--) {
        arr[i] = arr[i - 1];
    }
    arr[pos - 1] = item; // Insert the new element
    (*size)++;
    printf("Element inserted successfully.\n");
}
 
void deleteElement(int arr[], int *size, int key) {
    if (*size == 0) {
        printf("Array is empty! No elements to delete.\n");
        return;
    }
    int found = 0;
    for (int i = 0; i < *size; i++) {
        if (arr[i] == key) {
            found = 1;
            // Shift elements to the left to remove the element
            for (int j = i; j < *size - 1; j++) {
                arr[j] = arr[j + 1];
            }
            (*size)--; // Decrease the size of the array
            printf("Element deleted successfully.\n");
            break; // Exit the loop after deleting the first occurrence
        }
    }
    if (!found) {
        printf("Element not found!\n");
    }
}
 
void displayArray(int arr[], int size) {
    if (size == 0) {
        printf("Array is empty!\n");
    } else {
        printf("Current array: ");
        for (int i = 0; i < size; i++) {
            printf("%d ", arr[i]);
        }
        printf("\n");
    }
}
 
int main() {
    int arr[MAX_SIZE];
    int size = 0, choice, item, pos, key;
 
    printf("Enter the number of initial elements (up to %d): ", MAX_SIZE);
    scanf("%d", &size);
    if (size > MAX_SIZE || size < 0) {
        printf("Invalid size!\n");
        return 1;
    }
 
    printf("Enter %d elements: ", size);
    for (int i = 0; i < size; i++) {
        scanf("%d", &arr[i]);
    }
 
    do {
        printf("\nMenu:\n");
        printf("1. Insert an element\n");
        printf("2. Delete an element\n");
        printf("3. Display the array\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
 
        switch (choice) {
            case 1:
                printf("Enter the element to be inserted: ");
                scanf("%d", &item);
                printf("Enter the position: ");
                scanf("%d", &pos);
                insertElement(arr, &size, item, pos);
                break;
            case 2:
                printf("Enter the element to delete: ");
                scanf("%d", &key);
                deleteElement(arr, &size, key);
                break;
            case 3:
                displayArray(arr, size);
                break;
            case 4:
                printf("Exiting program.\n");
                break;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    } while (choice != 4);
 
    return 0;
}
_______________________________________________________________________________________________________________________________________
//2)Implementation of a recursive program factorial 
#include <stdio.h>
 
// Function to calculate factorial using recursion
unsigned long long factorial(unsigned int n) {
    // Base Case: Factorial of 0 is 1
    if (n == 0 || n == 1) {
        return 1;
    }
    // Recursive case: n * factorial(n - 1)
    return n * factorial(n - 1);
}
 
int main() {
    unsigned int num;
 
    // Prompt user for input
    printf("Enter a non-negative integer: ");
    scanf("%u", &num);
 
    // Calculate and display the factorial
    printf("Factorial of %u is %llu\n", num, factorial(num));
    return 0;
}
_______________________________________________________________________________________________________________________________________
//3)Array implementation of stack
#include <stdio.h>
#define SIZE 10
 
// Function prototypes
void push(int value);
void pop();
void display();
void peek();
 
// Global variables
int stack[SIZE], top = -1;
 
int main() {
    int value, choice;
 
    do {
        printf("\n\n***** MENU *****\n");
        printf("1. Push\n2. Pop\n3. Display\n4. Peek\n5. Exit\n");
        printf("\nEnter your choice: ");
        scanf("%d", &choice);
 
        switch (choice) {
            case 1:
                printf("Enter the value to be inserted: ");
                scanf("%d", &value);
                push(value);
                break;
            case 2:
                pop();
                break;
            case 3:
                display();
                break;
            case 4:
                peek();
                break;
            case 5:
                printf("Exiting program.\n");
                break;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    } while (choice != 5);
 
    return 0;
}
 
void push(int value) {
    if (top == SIZE - 1) {
        printf("\nStack is Full!!! Insertion is not possible!!!\n");
    } else {
        top++;
        stack[top] = value;
        printf("\nInsertion success!!!\n");
    }
}
 
void pop() {
    if (top == -1) {
        printf("\nStack is Empty!!! Deletion is not possible!!!\n");
    } else {
        printf("\nDeleted: %d\n", stack[top]);
        top--;
    }
}
 
void peek() {
    if (top == -1) {
        printf("\nStack is Empty!!!\n");
    } else {
        printf("Stack top is %d\n", stack[top]);
    }
}
 
void display() {
    if (top == -1) {
        printf("\nStack is Empty!!!\n");
    } else {
        printf("\nStack elements are:\n");
        for (int i = top; i >= 0; i--) {
            printf("%d\n", stack[i]);
        }
    }
}
_______________________________________________________________________________________________________________________________________
//4)Array implementation of linear queue
#include <stdio.h>
#include <stdlib.h>
#define MAX 50
 
int queue[MAX];
int front = -1, rear = -1;
 
// Function to insert an element into the queue
void insert() {
    int add_item;
    if (rear == MAX - 1) {
        printf("Queue Overflow \n");
    } else {
        if (front == -1) { // Initialize front if it's the first element
            front = 0;
        }
        printf("Insert the element in queue: ");
        scanf("%d", &add_item);
        rear = rear + 1;
        queue[rear] = add_item;
        printf("Inserted: %d\n", add_item); // Confirmation message
    }
}
 
// Function to delete an element from the queue
void delete() {
    if (front == -1 || front > rear) { // Check for underflow
        printf("Queue Underflow \n");
        return;
    } else {
        printf("Element deleted from queue is: %d\n", queue[front]);
        front = front + 1; // Move front to the next element
        // Reset front and rear if the queue becomes empty
        if (front > rear) {
            front = rear = -1; // Reset the queue
        }
    }
}
 
// Function to display the elements of the queue
void display() {
    if (front == -1) {
        printf("Queue is empty \n");
    } else {
        printf("Queue is: \n");
        for (int i = front; i <= rear; i++) {
            printf("%d ", queue[i]);
        }
        printf("\n");
    }
}
 
int main() {
    int choice;
    while (1) {
        printf("1. Insert element to queue \n");
        printf("2. Delete element from queue \n");
        printf("3. Display all elements of queue \n");
        printf("4. Quit \n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        switch (choice) {
            case 1:
                insert();
                break;
            case 2:
                delete();
                break;
            case 3:
                display();
                break;
            case 4:
                printf("Exiting program.\n");
                exit(0); // Clean exit
            default:
                printf("Invalid choice! Please try again.\n");
                break;
        }
    }
    return 0;
}
_______________________________________________________________________________________________________________________________________
//5)Array implementation of circular queue
#include <stdio.h>
#define SIZE 5
 
void insertq(int queue[], int item);
void deleteq(int queue[]);
void display(int queue[]);
 
int front = -1;
int rear = -1;
 
int main() {
    int n, ch;
    int queue[SIZE];
 
    do {
        printf("\n\n Circular Queue:\n1. Insert \n2. Delete\n3. Display\n0. Exit");
        printf("\nEnter Choice 0-3? : ");
        scanf("%d", &ch);
        switch (ch) {
            case 1:
                printf("\nEnter number: ");
                scanf("%d", &n);
                insertq(queue, n);
                break;
            case 2:
                deleteq(queue);
                break;
            case 3:
                display(queue);
                break;
            case 0:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    } while (ch != 0);
 
    return 0;
}
 
void insertq(int queue[], int item) {
    // Check if the queue is full
    if ((front == 0 && rear == SIZE - 1) || (front == rear + 1)) {
        printf("Queue is full\n");
        return;
    } else if (front == -1) { // First element to be inserted
        front = 0;
        rear = 0;
    } else if (rear == SIZE - 1 && front > 0) {
        rear = 0; // Wrap around
    } else {
        rear++;
    }
    queue[rear] = item;
    printf("Inserted: %d\n", item); // Confirmation message
}
 
void display(int queue[]) {
    int i;
    printf("\nQueue elements: ");
    if (front == -1) {
        printf("Queue is empty\n");
        return;
    }
    if (front <= rear) {
        for (i = front; i <= rear; i++) {
            printf("%d ", queue[i]);
        }
    } else {
        for (i = front; i < SIZE; i++) {
            printf("%d ", queue[i]);
        }
        for (i = 0; i <= rear; i++) {
            printf("%d ", queue[i]);
        }
    }
    printf("\n");
}
 
void deleteq(int queue[]) {
    if (front == -1) {
        printf("Queue is empty\n");
        return;
    }
    printf("\n%d deleted", queue[front]);
    if (front == rear) { // Queue has only one element
        front = -1;
        rear = -1;
    } else if (front == SIZE - 1) {
        front = 0; // Wrap around
    } else {
        front++;
    }
}
_______________________________________________________________________________________________________________________________________
//6)Implement a Singly Linked List (Create, Display, insert at beginning)
 
#include <stdio.h>
#include <stdlib.h>
 
// Define the structure for a node in the linked list
struct node {
    int data;
    struct node *next;
};
 
// Function prototypes
struct node *create_list(struct node *);
struct node *display(struct node *);
struct node *insert_beg(struct node *);
 
int main() {
    struct node *start = NULL; // Initialize the start of the list
    int option;
 
    do {
        printf("\n*** MAIN MENU ***\n");
        printf("1. Create a list\n");
        printf("2. Display the list\n");
        printf("3. Add a node at the beginning\n");
        printf("4. EXIT\n");
        printf("Enter your option: ");
        scanf("%d", &option);
 
        switch (option) {
            case 1: 
                start = create_list(start);
                printf("LINKED LIST CREATED\n");
                break;
            case 2: 
                start = display(start); 
                break;
            case 3: 
                start = insert_beg(start); 
                break;
            case 4:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid option! Please try again.\n");
        }
    } while (option != 4);
 
    return 0;
}
 
struct node *create_list(struct node *start) {
    struct node *new_node, *ptr;
    int num;
    printf("Enter -1 to end\n");
    printf("Enter the data: ");
    scanf("%d", &num);
 
    while (num != -1) {
        new_node = (struct node *)malloc(sizeof(struct node));
        if (new_node == NULL) {
            printf("Memory allocation failed\n");
            return start;
        }
        new_node->data = num;
        new_node->next = NULL;
 
        if (start == NULL) {
            start = new_node; // First node
        } else {
            ptr = start;
            while (ptr->next != NULL) {
                ptr = ptr->next; // Traverse to the end
            }
            ptr->next = new_node; // Link the new node
        }
        printf("Enter the data: ");
        scanf("%d", &num);
    }
    return start;
}
 
struct node *display(struct node *start) {
    struct node *ptr = start;
    if (ptr == NULL) {
        printf("The list is empty.\n");
        return start;
    }
    printf("List: ");
    while (ptr != NULL) {
        printf("%d -> ", ptr->data);
        ptr = ptr->next;
    }
    printf("NULL\n");
    return start;
}
 
struct node *insert_beg(struct node *start) {
    struct node *new_node;
    int num;
    printf("Enter the data: ");
    scanf("%d", &num);
    new_node = (struct node *)malloc(sizeof(struct node));
    if (new_node == NULL) {
        printf("Memory allocation failed\n");
        return start;
    }
    new_node->data = num;
    new_node->next = start; // New node points to the old start
    return new_node; // New node is the new start
}
_______________________________________________________________________________________________________________________________________
//7)Implement a Singly Linked List (Create, Display, insert at end)
#include <stdio.h>
#include <stdlib.h>
 
// Define the structure for a node in the linked list
struct node {
    int data;
    struct node *next;
};
 
// Function prototypes
struct node *create_list(struct node *);
struct node *display(struct node *);
struct node *insert_end(struct node *);
 
int main() {
    struct node *start = NULL; // Initialize the start of the list
    int option;
 
    do {
        printf("\n*** MAIN MENU ***\n");
        printf("1. Create a list\n");
        printf("2. Display the list\n");
        printf("3. Add a node at the end\n");
        printf("4. EXIT\n");
        printf("Enter your option: ");
        scanf("%d", &option);
 
        switch (option) {
            case 1: 
                start = create_list(start);
                printf("LINKED LIST CREATED\n");
                break;
            case 2: 
                start = display(start); 
                break;
            case 3: 
                start = insert_end(start); 
                break;
            case 4:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid option! Please try again.\n");
        }
    } while (option != 4);
 
    return 0;
}
 
struct node *create_list(struct node *start) {
    struct node *new_node, *ptr;
    int num;
    printf("Enter -1 to end\n");
    printf("Enter the data: ");
    scanf("%d", &num);
 
    while (num != -1) {
        new_node = (struct node *)malloc(sizeof(struct node));
        if (new_node == NULL) {
            printf("Memory allocation failed\n");
            return start;
        }
        new_node->data = num;
        new_node->next = NULL;
 
        if (start == NULL) {
            start = new_node; // First node
        } else {
            ptr = start;
            while (ptr->next != NULL) {
                ptr = ptr->next; // Traverse to the end
            }
            ptr->next = new_node; // Link the new node
        }
        printf("Enter the data: ");
        scanf("%d", &num);
    }
    return start;
}
 
struct node *display(struct node *start) {
    struct node *ptr = start;
    if (ptr == NULL) {
        printf("The list is empty.\n");
        return start;
    }
    printf("List: ");
    while (ptr != NULL) {
        printf("%d -> ", ptr->data);
        ptr = ptr->next;
    }
    printf("NULL\n");
    return start;
}
 
struct node *insert_end(struct node *start) {
    struct node *ptr, *new_node;
    int num;
    printf("Enter the data: ");
    scanf("%d", &num);
    new_node = (struct node *)malloc(sizeof(struct node));
    if (new_node == NULL) {
        printf("Memory allocation failed\n");
        return start;
    }
    new_node->data = num;
    new_node->next = NULL;
 
    if (start == NULL) {
        start = new_node; // If the list is empty, new node becomes the start
    } else {
        ptr = start;
        while (ptr->next != NULL) {
            ptr = ptr->next; // Traverse to the end
        }
        ptr->next = new_node; // Link the new node at the end
    }
    return start;
}
_______________________________________________________________________________________________________________________________________
//8)Implementation of Stack using Linked list
#include <stdio.h>
#include <stdlib.h>
 
// Structure for a stack node
struct stack {
    int data;
    struct stack *next;
};
 
// Global pointer to the top of the stack
struct stack *top = NULL;
 
// Function prototypes
struct stack *push(struct stack *, int);
void display(struct stack *);
struct stack *pop(struct stack *);
int peek(struct stack *);
 
int main() {
    int val, option;
    do {
        printf("\n *** MAIN MENU ***");
        printf("\n 1. PUSH");
        printf("\n 2. POP");
        printf("\n 3. PEEK");
        printf("\n 4. DISPLAY");
        printf("\n 5. EXIT");
        printf("\n Enter your option: ");
        scanf("%d", &option);
 
        switch (option) {
            case 1:
                printf("\n Enter the number to be pushed on stack: ");
                scanf("%d", &val);
                top = push(top, val);
                break;
            case 2:
                top = pop(top);
                break;
            case 3:
                val = peek(top);
                if (val != -1)
                    printf("\n The value at the top of stack is %d", val);
                else
                    printf("\n STACK EMPTY");
                break;
            case 4:
                display(top);
                break;
            case 5:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid option! Please try again.\n");
        }
    } while (option != 5);
 
    // Free the stack before exiting
    while (top != NULL) {
        top = pop(top);
    }
 
    return 0;
}
 
struct stack *push(struct stack *top, int val) {
    struct stack *ptr = (struct stack *)malloc(sizeof(struct stack));
    if (ptr == NULL) {
        printf("Memory allocation failed!\n");
        return top; // Return the original top if allocation fails
    }
    ptr->data = val;
    ptr->next = top; // Link the new node to the previous top
    return ptr; // New node becomes the new top
}
 
void display(struct stack *top) {
    struct stack *ptr = top;
    if (top == NULL) {
        printf("\n STACK EMPTY");
    } else {
        printf("\n Stack elements:");
        while (ptr != NULL) {
            printf("\n %d", ptr->data);
            ptr = ptr->next;
        }
    }
}
 
struct stack *pop(struct stack *top) {
    if (top == NULL) {
        printf("\n STACK UNDERFLOW");
        return top; // Return the original top if the stack is empty
    }
    struct stack *ptr = top;
    top = top->next; // Move top to the next node
    printf("\n The value being deleted is %d", ptr->data);
    free(ptr); // Free the old top node
    return top; // Return the new top
}
 
int peek(struct stack *top) {
    if (top == NULL)
        return -1; // Return -1 if the stack is empty
    else
        return top->data; // Return the data of the top node
}
_______________________________________________________________________________________________________________________________________
//9)Program to Evaluate Postfix Expression using Stack ADT.
#include <stdio.h>
#include <ctype.h>
#include <stdlib.h> // Include stdlib for exit function
#define MAX 100
 
float st[MAX];
int top = -1;
 
// Function prototypes
void push(float st[], float val);
float pop(float st[]);
float evaluatePostfixExp(char exp[]);
 
int main() {
    float val;
    char exp[100];
 
    printf("\nEnter any postfix expression: ");
    scanf("%s", exp);
 
    val = evaluatePostfixExp(exp);
    printf("\nValue of the postfix expression = %.2f\n", val);
 
    return 0;
}
 
float evaluatePostfixExp(char exp[]) {
    int i = 0;
    float op1, op2, value;
 
    while (exp[i] != '\0') {
        if (isdigit(exp[i])) {
            // Convert character to float and push onto stack
            push(st, (float)(exp[i] - '0'));
        } else {
            op2 = pop(st);
            op1 = pop(st);
            switch (exp[i]) {
                case '+':
                    value = op1 + op2;
                    break;
                case '-':
                    value = op1 - op2;
                    break;
                case '/':
                    if (op2 == 0) {
                        printf("Error: Division by zero\n");
                        exit(1);
                    }
                    value = op1 / op2;
                    break;
                case '*':
                    value = op1 * op2;
                    break;
                case '%':
                    value = (int)op1 % (int)op2;
                    break;
                default:
                    printf("Invalid operator: %c\n", exp[i]);
                    exit(1); // Exit if an invalid operator is encountered
            }
            push(st, value);
        }
        i++;
    }
    return pop(st);
}
 
void push(float st[], float val) {
    if (top == MAX - 1) {
        printf("\nSTACK OVERFLOW\n");
    } else {
        top++;
        st[top] = val;
    }
}
 
float pop(float st[]) {
    float val = -1;
    if (top == -1) {
        printf("\nSTACK UNDERFLOW\n");
    } else {
        val = st[top];
        top--;
    }
    return val;
}
