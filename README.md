# Vocalize

## What it does:
The proposed model provides a textual output upon detecting Indian Sign Language (ISL). This will introduce a medium that'll facilitate an easier form of communication with the deaf people. Thus, the proposed model can be used as a means to help and support the people affected.

## How we built it:
The model was built using languages like python and dart, using the open source framework Flutter for developing an application for the same. The model has been trained using a personally built and procured dataset with sharpened accuracy.

## Challenges we ran into:
The dataset was hard to build and required a lot of patience and perseverance. Integration of the trained  model to perform detection of the signs in flutter was also a demanding task.

## Accomplishments that we're proud of:
The model achieved a decent amount of accuracy and was successfully able to distinguish between several signs. We were also able to form full-fledged sentences using the proposed model, which turned out to be exceptional.

## What we learned:
The hackathon served as a means of testing ourselves and understanding how to perform the set of tasks under a given time constraint. It also allowed us to dive deep into the problems faced by the less-fortunate and be aware of the challenges faced by these people. Thus, by ideating on the solutions to the situations faced by these people, it also helped us to develop our logical skills and perform real life implementation. By working with the goal in mind for the development of society, we developed empathy and a sense of responsibility to do better.

## What's next for Vocalize:
The journey of Vocalize does not end here. Far from it, in fact, as this is just the beginning. The proposed application has the potential of allowing an extremely easy form of communication for people affected with hearing loss of all depths. Upon increasing the number of signs for detection and also enhancing the compatibility and accuracy of the model with the flutter application, the presented prototype has the ability of finally providing a voice to everyone. 


#
#include <iostream>
#include <vector>

using namespace std;

// Function declarations
void board_state(const vector<int>& board);
void player(vector<int>& board);
int minmax(vector<int>& board, int player);
void computer_turn(vector<int>& board);
int win(const vector<int>& board);
bool is_draw(const vector<int>& board);

// Function to draw the board's current state every time the user's turn arrives
void board_state(const vector<int>& board) {
    cout << "Current State Of Board : \n\n";
    for (int i = 0; i < 9; ++i) {
        if (i > 0 && i % 3 == 0)
            cout << "\n";
        
        if (board[i] == 0)
            cout << "- ";
        else if (board[i] == 1)
            cout << "O ";
        else if (board[i] == -1)
            cout << "X ";
    }
    cout << "\n\n";
}

// Function to take the user's move as input and make the required changes on the board
void player(vector<int>& board) {
    cout << "Enter X's position from [1...9]: ";
    int pos;
    cin >> pos;
    if (board[pos - 1] != 0) {
        cout << "Wrong Move!!!";
        exit(0);
    }
    board[pos - 1] = -1;
}

// MinMax function
int minmax(vector<int>& board, int player) {
    // Check for terminal states (win or draw)
    int x = win(board);
    if (x != 0)
        return x * player;

    int pos = -1;
    int value = -2;
    // Iterate over the board to find the best move
    for (int i = 0; i < 9; ++i) {
        if (board[i] == 0) {
            board[i] = player; // Simulate placing a piece
            int score = -minmax(board, player * -1); // Recursively call minmax for the opponent
            if (score > value) {
                value = score;
                pos = i;
            }
            board[i] = 0; // Undo the move for backtracking
        }
    }

    if (pos == -1)
        return 0;
    return value;
}

// Function to make the computer's move using the MinMax algorithm
void computer_turn(vector<int>& board) {
    int pos = -1;
    int value = -2;
    // Iterate over the board to find the best move for the computer
    for (int i = 0; i < 9; ++i) {
        if (board[i] == 0) {
            board[i] = 1; // Simulate placing the computer's piece
            int score = -minmax(board, -1); // Call MinMax for the opponent (human player)
            board[i] = 0; // Undo the move
            if (score > value) {
                value = score;
                pos = i;
            }
        }
    }

    board[pos] = 1; // Place the computer's piece on the board
}

// Function to analyze the game for a win
int win(const vector<int>& board) {
    // Array representing winning combinations
    int cb[8][3] = {
        {0, 1, 2},
        {3, 4, 5},
        {6, 7, 8},
        {0, 3, 6},
        {1, 4, 7},
        {2, 5, 8},
        {0, 4, 8},
        {2, 4, 6}
    };

    // Check each winning combination
    for (int i = 0; i < 8; ++i) {
        if (board[cb[i][0]] != 0 &&
            board[cb[i][0]] == board[cb[i][1]] &&
            board[cb[i][0]] == board[cb[i][2]])
            return board[cb[i][2]]; // Return the player who wins
    }
    return 0; // Return 0 if no winner
}

// Function to check for a draw
bool is_draw(const vector<int>& board) {
    // If there are no more empty positions, the game is a draw
    for (int i = 0; i < 9; ++i) {
        if (board[i] == 0)
            return false; // Game is not a draw
    }
    return true; // Game is a draw
}

// Main function
int main() {
    cout << "=======TIC TAC TOE GAME - AI======\n";
    
    // Initialize the board
    vector<int> board(9, 0);
    cout << "You (X) go first.\n";
    player(board); // Human player's turn

    // Game loop
    for (int i = 1; i <= 9; ++i) {
        if (win(board) != 0) {
            // Check if there is a winner
            board_state(board); // Display the final board state
            cout << (win(board) == -1 ? "X Wins!    O Loose !" : "X Loose!   O Wins !") << "\n";
            break;
        }
        if (is_draw(board)) {
            // Check if the game is a draw
            cout << "Draw!\n";
            break;
        }
        if (i % 2 == 1)
            computer_turn(board); // Computer's turn
        else {
            board_state(board); // Display the board
            player(board); // Human player's turn
        }
    }

    return 0; // End of the program
}