# Sudoku-game
I created a Sudoku game, but it's not your usual Sudoku game.

#include <iostream>
#include <vector>
#include <cstdlib>
#include <time.h>

using namespace std;

//Introduction to the game

void Introduction()
{

    cout << "Welcome to Sudoku game." << endl;
    cout << "Games purpose is to put numbers in the right spot." << endl;
    cout << endl;
    cout << "Here's the rules: " << endl;
    cout << "* Input numbers in to the right spot on the board." << endl;
    cout << "* For every wrong move (wrong number selection, etc...). " << endl;
    cout << "* The game will end if you do 3 mistakes. " << endl;
    cout << "* You will win the game if the game board is full with the right numbers and at the right spot" << endl;
    cout << "* GOOD LUCK! " << endl;
}
//Player chooses game board

void ChoosingBoard()
{

    cout << "Game is starting by choosing game board size." << endl;
    cout << "I want to remind you that original SUDOKU game board is 9x9." << endl;
    cout << "But in this game I will let you choose any board size." << endl;
    cout << "By choosing the larger board size, the game will be harder." << endl;
    cout << "The minimal board size still is left 9x9. Like the original Sudoku game." << endl;

}

//board Initialisation

void BoardInitialisation(vector <vector <char>> DrawingBoard )
{

    for (size_t i = 0; i < DrawingBoard.size(); i++)
    {
        for (size_t j = 0; j < DrawingBoard[i].size(); j++)
        {
            DrawingBoard[i][j] =' ';
        }
    }
}

//Checking if there's no same numbers in the rows or collums

void RandomNumberChecker(int BoardSize, vector <vector <int>> &board)
{

    for (int i = 0; i < BoardSize; i++)
    {
        for (int j = 0; j < BoardSize; j++)
        {
            for (int k = 0; k < BoardSize; k++)
            {
                if (j != k && board[i][j] == board[i][k])
                {
                    board[i][j] = 0;
                    //board[i][k] = 0;
                    
                }
            }
            for (int k = 0; k < BoardSize; ++k) {
                if (i != k && board[i][j] == board[k][j]) {
                    board[i][j] = 0;
                   // lentele[k][j] = 0;
                    
                }
            }
        }
    }
}

//An example board

void ExampleBoard(const vector <vector <char>>& DrawingBoard, int BoardSize,
    vector <vector <int>> &board )
{ 

    srand(time(0));
    int yAxisRandom;
    int xAxisRandom;
    //Generating random number and putting them in the random possitinions
    //in the board
    for (int i = 0; i < BoardSize; i++)
    {
        for (int j = 0; j < BoardSize; j++)
        {
            yAxisRandom = rand() % BoardSize;
            xAxisRandom = rand() % BoardSize;
            board[xAxisRandom][yAxisRandom] = (rand() % BoardSize) + 1;

        }
        //Checking if the random numbers doesn't duplicate
        RandomNumberChecker(BoardSize, board);
    }
    cout << endl;

    //x axis numbering

    cout << "    X->     ";
    for (int l = 1; l <= BoardSize; l++)
    {
            cout <<  l << "     ";
    }

        cout << endl;

    int yAxis = 1;

    //Loopis for y axis numbering and for board drawing 
    cout << "Y |" << endl;
    cout << "  v" << endl;
        for (size_t i = 0; i < DrawingBoard.size(); i++)
        {
            if (yAxis >= 10)
            {
                cout << yAxis << "      ";
            }
            else
            {
                cout << yAxis << "       ";
            }
            
            yAxis++;

            //Loop is for drawing the board
            for (size_t j = 0; j < DrawingBoard[i].size(); j++)
            {
               
                cout << "|" << DrawingBoard[i][j] <<" "<<
                    board[i][j] << "  ";
                

                if (board[i][j] < 10)
                {
                    cout << " ";
                }
            }

            cout << "|" << endl;
            cout << "        ";

            if (i < DrawingBoard.size() - 1)
            {
                for (size_t j = 0; j < DrawingBoard[i].size(); j++)
                {
                    cout << "+-----";
                }
                cout << "+" << endl;
            }
           
        }

    cout << endl;

   }

void BoardForPlaying(const vector <vector <char>>& Drawingboard, int BoardSize,
    vector <vector <int>>& board)
{

    cout << endl;

    //X axisnumbering

    cout << "           ";
    for (int l = 1; l <= BoardSize; l++)
    {
        cout << l << "     ";
    }

    cout << endl;
    cout << endl;

    int yAxis = 1;

    //Loop is for y axis numbering and drawing a playing board
    for (size_t i = 0; i < Drawingboard.size(); i++)
    {
        if (yAxis >= 10)
        {
            cout << yAxis << "      ";
        }
        else
        {
            cout << yAxis << "       ";
        }

        yAxis++;

        //Loop is for craeting a playing board and putting numbers in it
        for (size_t j = 0; j < Drawingboard[i].size(); j++)
        {

            cout << "|" << Drawingboard[i][j] << " " <<
                board[i][j] << "  ";


            if (board[i][j] < 10)
            {
                cout << " ";
            }
        }

        cout << "|" << endl;
        cout << "        ";

        if (i < Drawingboard.size() - 1)
        {
            for (size_t j = 0; j < Drawingboard[i].size(); j++)
            {
                cout << "+-----";
            }
            cout << "+" << endl;
        }

    }

    cout << endl;


}

//Checking the number entered in the board

bool NumberChecker(int yAxis, int xAxis, int number, int BoardSize,
    vector <vector <int>>& board)
{

    for (int i = 0; i < BoardSize; i++)
    {
        if (i == yAxis)
        {
            continue;
        }
        if (number == board[i][xAxis])
        {
            return true; 
        }
    }
    for (int i = 0; i < BoardSize; i++)
    {
        if (i == xAxis)
        {
            continue;
        }
        if (number == board[yAxis][i])
        {
            return true; 
        }
    }

    return false;
}

//Win or lose checker

bool winOrLose(vector <vector <int>> board, int BoardSize)
{

    for (int i = 0; i < BoardSize; i++)
    {
        for (int j = 0; j < BoardSize; j++)
        {
            for (int k = 0; k < BoardSize; k++)
            {
        
             if (board[i][j] == 0)
                {
                    return true;
                }
            }


        }
    }
    return false;

}

//Checking if the board is full with numbers

bool BoardChecking(const vector<vector<int>>& board) 
{

    for (const auto& row : board) {
        for (int value : row) {
            if (value == 0) {
                return true; //There is still at least one 0
            }
        }
    }
    return false; //THe board is full
}


int main()
{

    Introduction();
    ChoosingBoard();
    int BoardSize;
    cout << "Enter board size: ";
    cin >> BoardSize;

    //Checking is the board size correct
    while (BoardSize < 9)
    {
        cout << "The board size is entered incorrect, please re-entry: ";
            cin >> BoardSize;
    }

    cout << endl;

    vector <vector <char>> DrawingBoard(BoardSize, vector <char>(BoardSize));
    vector <vector <int>> board(BoardSize, vector <int>(BoardSize));

    BoardInitialisation(DrawingBoard);
    ExampleBoard(DrawingBoard, BoardSize, board);
    

    cout << "0 in the board must be changed between 1 - " << BoardSize << endl;
    
    int mistake = 0;
    //Main game loop
    do
    {
        BoardChecking(board);
        int xAxis, yAxis;
        int number = 0;
        for (int i = 0; i < BoardSize; i++)
        {
            for (int j = 0; j < BoardSize; j++)
            {
                

                cout << "Choose coordinates from 1 (x) to " << BoardSize <<
                " (y)" << endl;
                cin >> xAxis;
                cin >> yAxis;
                xAxis--;
                yAxis--;

                while (board[yAxis][xAxis] != 0)
                {
                    cout << "In this coordinates, there's already a number.";
                    cout << "Choose other coordinates:" << endl;
                    cin >> xAxis >> yAxis;
                    xAxis--;
                    yAxis--;
                }

                cout << "Enter a number that you want to put: ";
                cin >>  number;

                while (number > BoardSize)
                {
                    cout << "The number is to big for this game board.";
                    cout << " Please entry different number: ";
                    cin >> number;
                }

                while (NumberChecker(yAxis, xAxis, number, BoardSize,board))
                {
                    mistake++;
                    //By making 3 mistakes, game will end
                    if (mistake == 3)
                    {
                        cout << "GAME OVER "<< endl;
                        cout << "You have done " << mistake << " mistakes." << endl;
                        cout << endl;
                        BoardForPlaying(DrawingBoard, BoardSize, board);
                        cout << endl;
                        cout << "Thank you for playing" << endl;
                        exit(0);
                    }
                    else if (mistake < 3)
                    {
                        cout << mistake << " mistkae" << endl;
                        cout << "Entered number is not suitable.";
                        cout << "Re-entry number: ";
                        cin >> number;
                    }
                }
                board[yAxis][xAxis] = number;
                for (int i = 0; i < BoardSize; i++)
                {   
                    winOrLose(board, BoardSize);
                }
                system("CLS");
                if (winOrLose(board, BoardSize))
                {
                    BoardForPlaying(DrawingBoard, BoardSize, board);
                }
                
                else if (winOrLose(board, BoardSize) == false)
                {
                    cout << "YOU WON! CONGRATS!" << endl;
                    BoardForPlaying(DrawingBoard, BoardSize, board);
                    break;
                }
                cout << endl;

            }

        }

    } while (mistake < 3 && winOrLose(board, BoardSize) );

    cout << "Thank you for playing" << endl;

    return 0;
 }
