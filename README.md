include <stdbool.h> 
#include <stdio.h> 
#include <stdlib.h> 
#include <time.h> 
#define COMPUTER 1 
#define HUMAN 2 
#define SIDE 3 
#define COMPUTERMOVE 'O' 
#define HUMANMOVE 'X' 
  
// ---------------- Intelligent Moves start 
  
struct Move { 
    int row, col; 
}; 
  
char player = 'x', opponent = 'o'; 
  
// This function returns true if there are moves 
// remaining on the board. It returns false if 
// there are no moves left to play. 
bool isMovesLeft(char board[3][3]) 
{ 
    for (int i = 0; i < 3; i++) 
        for (int j = 0; j < 3; j++) 
            if (board[i][j] == '_') 
                return true; 
    return false; 
} 
  
// This is the evaluation function 
int evaluate(char b[3][3]) 
{ 
    // Checking for Rows for X or O victory. 
    for (int row = 0; row < 3; row++) { 
        if (b[row][0] == b[row][1] 
            && b[row][1] == b[row][2]) { 
            if (b[row][0] == player) 
                return +10; 
            else if (b[row][0] == opponent) 
                return -10; 
        } 
    } 
    // Checking for Columns for X or O victory. 
    for (int col = 0; col < 3; col++) { 
        if (b[0][col] == b[1][col] 
            && b[1][col] == b[2][col]) { 
            if (b[0][col] == player) 
                return +10; 
    else if (b[0][col] == opponent) 
                return -10; 
        } 
    } 
    // Checking for Diagonals for X or O victory. 
    if (b[0][0] == b[1][1] && b[1][1] == b[2][2]) { 
        if (b[0][0] == player) 
            return +10; 
        else if (b[0][0] == opponent) 
            return -10; 
    } 
    if (b[0][2] == b[1][1] && b[1][1] == b[2][0]) { 
        if (b[0][2] == player) 
            return +10; 
        else if (b[0][2] == opponent) 
            return -10; 
    } 
    // Else if none of them have won then return 0 
    return 0; 
} 
