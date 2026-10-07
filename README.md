# Stack-Operations
A C programming code on Stack Operation

#include <stdio.h>
#include <stdbool.h>

#define MAX 5  // Maximum capacity of the stack

// Structure to represent the stack
struct Stack {
    int items[MAX];
    int top;
};

// Initialize the stack top pointer to -1 (indicates empty stack)
void initStack(struct Stack* s) {
    s->top = -1;
}

// Check if the stack is full
bool isFull(struct Stack* s) {
    return s->top == MAX - 1;
}

// Check if the stack is empty
bool isEmpty(struct Stack* s) {
    return s->top == -1;
}

// Add an element to the top of the stack (Push)
void push(struct Stack* s, int value) {
    if (isFull(s)) {
        printf("Stack Overflow! Cannot push %d.\n", value);
    } else {
        s->top++;
        s->items[s->top] = value;
        printf("Successfully pushed %d onto the stack.\n", value);
    }
}

// Remove and return the top element of the stack (Pop)
int pop(struct Stack* s) {
    if (isEmpty(s)) {
        printf("Stack Underflow! Nothing to pop.\n");
        return -1; // Return an error value
    } else {
        int poppedValue = s->items[s->top];
        s->top--;
        return poppedValue;
    }
}

// Return the top element without removing it (Peek)
int peek(struct Stack* s) {
    if (isEmpty(s)) {
        printf("Stack is empty! No top element.\n");
        return -1;
    } else {
        return s->items[s->top];
    }
}

// Display all current elements in the stack
void display(struct Stack* s) {
    if (isEmpty(s)) {
        printf("Stack is empty.\n");
    } else {
        printf("Stack elements (top to bottom): ");
        for (int i = s->top; i >= 0; i--) {
            printf("%d ", s->items[i]);
        }
        printf("\n");
    }
}

int main() {
    struct Stack s;
    initStack(&s);
    
    int choice, value;
    
    printf("--- Stack Operations Menu ---\n");
    printf("1. Push\n2. Pop\n3. Peek\n4. Display Stack\n5. Exit\n");

    while (1) {
        printf("\nEnter your choice (1-5): ");
        scanf("%d", &choice);
        
        switch (choice) {
            case 1:
                printf("Enter value to push: ");
                scanf("%d", &value);
                push(&s, value);
                break;
                
            case 2:
                value = pop(&s);
                if (value != -1) {
                    printf("Popped value: %d\n", value);
                }
                break;
                
            case 3:
                value = peek(&s);
                if (value != -1) {
                    printf("Top element is: %d\n", value);
                }
                break;
                
            case 4:
                display(&s);
                break;
                
            case 5:
                printf("Exiting program.\n");
                return 0;
                
            default:
                printf("Invalid choice! Please select between 1 and 5.\n");
        }
    }
    return 0;
}
