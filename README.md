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


#include<iostream>
using namespace std;

#define PLAYER1 'X'
#define PLAYER2 'O'
#define EMPTY ' '

char board[3][3];

//initializing the board
void initializing(){
    for(int i=0; i<3; i++){
        for(int j = 0; j<3; j++){
            board[i][j] = EMPTY;
        }
    }
}


//displaying the board
void display(){
    printf("-------------\n");
    for(int i=0; i<3; i++){
        printf("| %c | %c | %c |\n", board[i][0], board[i][1], board[i][2]);
        printf("-------------\n");
    }
}

bool isBoardFull(){
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == EMPTY) {
                return 0;
            }
        }
    }
    return 1;
}

void getPlayer1Move() {
    int row, col;
    do {
        printf("Enter your move (row column): ");
        scanf("%d %d", &row, &col);
    } while (row < 0 || row >= 3 || col < 0 || col >= 3 || board[row][col] != EMPTY);

    board[row][col] = PLAYER1;
}

void getPlayer2Move() {
    int row, col;
    do {
        printf("Enter your move (row column): ");
        scanf("%d %d", &row, &col);
    } while (row < 0 || row >= 3 || col < 0 || col >= 3 || board[row][col] != EMPTY);

    board[row][col] = PLAYER2;
}

bool hasPlayerWon(char player) {
    // Check rows
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == player && board[i][1] == player && board[i][2] == player) {
            return 1;
        }
    }

    // Check columns
    for (int j = 0; j < 3; j++) {
        if (board[0][j] == player && board[1][j] == player && board[2][j] == player) {
            return 1;
        }
    }

    // Check diagonals
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
        return 1;
    }

    return 0;
}

void playGame(){

    initializing();
    display();

    while(!isBoardFull()){

        cout<<"Player 1 (X): "<<endl;
        getPlayer1Move();
        display();

        if(hasPlayerWon(PLAYER1)){
            cout<<"Congratulations Player 1 has won!"<<endl;
            break;
        }


        if (isBoardFull()) {
            printf("It's a tie!\n");
            return;
        }

        cout<<"Player 2 (O): "<<endl;
        getPlayer2Move();
        display();

        
        if(hasPlayerWon(PLAYER2)){
            cout<<"Congratulations Player 2 has won!"<<endl;
            break;
        }
        
    }

}

int main() {
    playGame();

    return 0;
}