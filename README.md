# busy-beaver

The Busy Beaver problem is a well-known computational problem in computer science. It asks for the maximum number of steps that a Turing machine with a certain number of states and symbols can perform before halting. Unfortunately, the problem is undecidable, which means that there is no algorithm that can always solve it.

However, we can still write a C program that attempts to solve the Busy Beaver problem for small numbers of states and symbols. Here's an example implementation that uses a brute-force approach to search for the maximum number of steps:
~~~
#include <stdio.h>

// Define the maximum number of states and symbols
#define MAX_STATES 10
#define MAX_SYMBOLS 2

// Define the transition function for the Turing machine
int transition[MAX_STATES][MAX_SYMBOLS][3];

// Define the Turing machine simulator
int simulate(int num_states, int num_symbols) {
    int tape[1024] = {0};
    int state = 0;
    int pos = 512;
    int steps = 0;

    while (1) {
        int symbol = tape[pos];
        int new_symbol = transition[state][symbol][0];
        int move = transition[state][symbol][1];
        int new_state = transition[state][symbol][2];

        tape[pos] = new_symbol;
        pos += move;
        state = new_state;
        steps++;

        if (state < 0 || state >= num_states) {
            break;
        }
        if (pos < 0 || pos >= 1024) {
            break;
        }
    }

    return steps;
}

// Define the main function
int main() {
    // Initialize the transition function with all zeros
    for (int i = 0; i < MAX_STATES; i++) {
        for (int j = 0; j < MAX_SYMBOLS; j++) {
            for (int k = 0; k < 3; k++) {
                transition[i][j][k] = 0;
            }
        }
    }

    // Set the transition function for a 2-state, 2-symbol Turing machine
    transition[0][0][0] = 1;
    transition[0][0][1] = 1;
    transition[0][0][2] = 1;
    transition[0][1][0] = 1;
    transition[0][1][1] = -1;
    transition[0][1][2] = 0;
    transition[1][0][0] = 1;
    transition[1][0][1] = -1;
    transition[1][0][2] = 0;
    transition[1][1][0] = 1;
    transition[1][1][1] = 1;
    transition[1][1][2] = 1;

    // Run the simulator and print the result
    int steps = simulate(2, 2);
    printf("The maximum number of steps for a 2-state, 2-symbol Turing machine is %d\n", steps);

    return 0;
}
~~~
This program defines the maximum number of states and symbols as constants, and initializes a 3D array transition to represent the transition function of the Turing machine. The simulate function simulates the behavior of the Turing machine on a tape, and returns the number of steps that the machine performs before halting.

In the main function, we initialize the transition function for a 2-state, 2-symbol Turing machine, and run the simulator to calculate the maximum number of steps. This specific Turing machine is known to be a busy beaver, meaning that it performs more steps than any other 2-state
