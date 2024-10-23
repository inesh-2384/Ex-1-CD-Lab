# Ex-1 IMPLEMENTATION-OF-SYMBOL-TABLE
# AIM :
## To write a C program to implement a symbol table.
# ALGORITHM
1.	Start the program.
2.	Get the input from the user with the terminating symbol ‘$’.
3.	Allocate memory for the variable by dynamic memory allocation function.
4.	If the next character of the symbol is an operator then only the memory is allocated.
5.	While reading, the input symbol is inserted into symbol table along with its memory address.
6.	The steps are repeated till ‘$’ is reached.
7.	To reach a variable, enter the variable to be searched and symbol table has been checked for corresponding variable, the variable along with its address is displayed as result.
8.	Stop the program. 
# PROGRAM
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_SYMBOLS 100
#define MAX_VAR_NAME 50

typedef struct {
    char name[MAX_VAR_NAME];
    int *address;  // Pointer to the variable's memory address
} Symbol;

Symbol symbolTable[MAX_SYMBOLS];
int symbolCount = 0;

void addVariable(const char *name) {
    if (symbolCount >= MAX_SYMBOLS) {
        printf("Symbol table is full.\n");
        return;
    }

    int *var = (int *)malloc(sizeof(int));
    if (!var) {
        printf("Memory allocation failed.\n");
        return;
    }

    strcpy(symbolTable[symbolCount].name, name);
    symbolTable[symbolCount].address = var;
    symbolCount++;

    printf("Variable '%s' added at address %p.\n", name, (void*)var);
}


void searchVariable(const char *name) {
    for (int i = 0; i < symbolCount; i++) {
        if (strcmp(symbolTable[i].name, name) == 0) {
            printf("Variable '%s' found at address %p.\n", name, (void*)symbolTable[i].address);
            return;
        }
    }
    printf("Variable '%s' not found in the symbol table.\n", name);
}

int main() {
    char input[MAX_VAR_NAME];

    printf("Enter variables (terminate with '$'):\n");
    while (1) {
        scanf("%s", input);
        if (strcmp(input, "$") == 0) {
            break;  // Terminate on '$'
        }

       
        if (input[0] >= 'a' && input[0] <= 'z') {  // Simple check for variable names
            addVariable(input);
        } else {
            printf("Invalid input. Only lowercase letters are allowed for variable names.\n");
        }
    }

   
    printf("Enter a variable name to search (terminate with '$'):\n");
    while (1) {
        scanf("%s", input);
        if (strcmp(input, "$") == 0) {
            break;  // Terminate on '$'
        }
        searchVariable(input);
    }

    
    for (int i = 0; i < symbolCount; i++) {
        free(symbolTable[i].address);  // Free each allocated variable
    }

    return 0;
}

# OUTPUT
The program will prompt you to enter variable names. When you enter $, it will stop accepting new variables and will then prompt you to search for any variable in the symbol table. It will show the address of the variable if found.
# RESULT
The program to implement a symbol table is executed and the output is verified.
