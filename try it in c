#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <stdbool.h>

#define MAX_STACK 1024
#define MAX_DICT 256

typedef void (*XT)();  // Function pointer for execution token

// Custom Forth stack structure
typedef struct {
    int data[MAX_STACK];
    int top;
} ForthStack;

ForthStack rs = { .top = -1 };  // Return stack
ForthStack ss = { .top = -1 };  // Parameter stack

bool compile = false;  // Compile mode flag

// Helper stack functions
void push(ForthStack* stack, int value) {
    if (stack->top < MAX_STACK - 1) {
        stack->data[++stack->top] = value;
    }
}

int pop(ForthStack* stack) {
    if (stack->top >= 0) {
        return stack->data[stack->top--];
    }
    return 0;  // Return 0 if the stack is empty
}

int peek(ForthStack* stack) {
    if (stack->top >= 0) {
        return stack->data[stack->top];
    }
    return 0;  // Return 0 if the stack is empty
}

// Code structure for dictionary entries
typedef struct Code {
    const char* name;
    XT xt;
    bool immd;
} Code;

Code* dict[MAX_DICT];
int dict_size = 0;

// Arithmetic operations
void add() { push(&ss, pop(&ss) + pop(&ss)); }
void subtract() { int a = pop(&ss); push(&ss, pop(&ss) - a); }
void multiply() { push(&ss, pop(&ss) * pop(&ss)); }
void divide() { int a = pop(&ss); push(&ss, pop(&ss) / a); }

// Stack operations
void dup() { push(&ss, peek(&ss)); }
void drop() { pop(&ss); }
void swap() {
    int a = pop(&ss);
    int b = pop(&ss);
    push(&ss, a);
    push(&ss, b);
}
void over() { push(&ss, ss.data[ss.top - 1]); }

// I/O operations
void dot() { printf("%d\n", pop(&ss)); }
void bye() { exit(0); }

void words() {
    printf("Words:\n");
    for (int i = 0; i < dict_size; i++) {
        printf("%s ", dict[i]->name);
    }
    printf("\n");
}

// Dictionary management
Code* create_word(const char* name, XT xt, bool immd) {
    Code* w = (Code*)malloc(sizeof(Code));
    w->name = name;
    w->xt = xt;
    w->immd = immd;
    dict[dict_size++] = w;
    return w;
}

Code* find(const char* s) {
    for (int i = dict_size - 1; i >= 0; i--) {
        if (strcmp(s, dict[i]->name) == 0) {
            return dict[i];
        }
    }
    return NULL;
}

void exec(Code* w) {
    if (w->xt) {
        w->xt();
    }
}

// Outer interpreter
void interpret(const char* idiom) {
    Code* w = find(idiom);
    if (w) {
        if (compile && !w->immd) {
            // Add to current word (if needed)
        } else {
            exec(w);
        }
    } else {
        int n = atoi(idiom);
        push(&ss, n);
    }
}

// Initialize dictionary with basic words
void init_dict() {
    create_word("bye", bye, false);
    create_word("dup", dup, false);
    create_word("drop", drop, false);
    create_word("swap", swap, false);
    create_word("over", over, false);
    create_word("+", add, false);
    create_word("-", subtract, false);
    create_word("*", multiply, false);
    create_word("/", divide, false);
    create_word(".", dot, false);
    create_word("words", words, false);
}

// Main function
int main() {
    init_dict();
    printf("ceForth v4.1\n");

    char idiom[256];
    while (scanf("%s", idiom) != EOF) {
        interpret(idiom);
        if (!compile) {
            printf("< %d > ok\n", peek(&ss));
        }
    }

    printf("Done!\n");
    return 0;
}
