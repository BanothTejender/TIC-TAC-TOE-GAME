# TIC-TAC-TOE-GAME
#include <iostream>
using namespace std;

const int BOARD_SIZE = 3;

class TicTacToe {
private:
    char board[BOARD_SIZE][BOARD_SIZE] = {
        {'1', '2', '3'},
        {'4', '5', '6'},
        {'7', '8', '9'}
    };

public:
    void printBoard() {
        cout << "T I C   T A C   T O E" << endl;
        cout << "PLAYER 1: [X]" << endl;
        cout << "PLAYER 2: [O]" << endl;

        for (int i = 0; i < BOARD_SIZE; i++) {
            cout << "     |     |     " << endl;
            cout << "  " << board[i][0] << "  |  " << board[i][1] << "  |  " << board[i][2] << endl;
            cout << "_____|_____|_____" << endl;
        }
        cout << "     |     |     " << endl;
    }

    void playGame() {
        int turnCount = 1;
        int choice;

        while (turnCount <= BOARD_SIZE * BOARD_SIZE) {
            int player = (turnCount % 2 == 1) ? 1 : 2;
            cout << "PLAYER " << player << " TURN:" << endl;
            cin >> choice;

            int row = (choice - 1) / BOARD_SIZE;
            int col = (choice - 1) % BOARD_SIZE;

            if (choice < 1 || choice > BOARD_SIZE * BOARD_SIZE || board[row][col] == 'X' || board[row][col] == 'O') {
                cout << "Invalid move. Try again." << endl;
                continue;
            }

            char symbol = (player == 1) ? 'X' : 'O';
            board[row][col] = symbol;

            if (checkWin(symbol)) {
                cout << "PLAYER " << player << " WON!" << endl;
                break;
            }

            turnCount++;
        }

        if (turnCount > BOARD_SIZE * BOARD_SIZE) {
            cout << "It's a tie!" << endl;
        }
    }

    bool checkWin(char symbol) {
        for (int i = 0; i < BOARD_SIZE; i++) {
            // Check rows
            if (board[i][0] == symbol && board[i][1] == symbol && board[i][2] == symbol)
                return true;

            // Check columns
            if (board[0][i] == symbol && board[1][i] == symbol && board[2][i] == symbol)
                return true;
        }

        // Check diagonals
        if ((board[0][0] == symbol && board[1][1] == symbol && board[2][2] == symbol) ||
            (board[0][2] == symbol && board[1][1] == symbol && board[2][0] == symbol))
            return true;

        return false;
    }
};

int main() {
    TicTacToe game;
    game.printBoard();
    game.playGame();

    return 0;
}
