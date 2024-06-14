# TictacGame
//Started with simple code
#include <stdio.h>

char board[3][3];
char current_marker;
char current_player;

void initialize_board() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            board[i][j] = '1' + i * 3 + j; // Initializing the board with numbers 1 to 9
        }
    }
}

void print_board() {
    printf(" %c | %c | %c \n", board[0][0], board[0][1], board[0][2]);
    printf("---|---|---\n");
    printf(" %c | %c | %c \n", board[1][0], board[1][1], board[1][2]);
    printf("---|---|---\n");
    printf(" %c | %c | %c \n", board[2][0], board[2][1], board[2][2]);
}

int place_marker(int slot) {
    int row = (slot - 1) / 3;
    int col = (slot - 1) % 3;

    if (board[row][col] != 'X' && board[row][col] != 'O') {
        board[row][col] = current_marker;
        return 1;
    }
    return 0;
}

int check_winner() {
    // Check rows and columns
    for (int i = 0; i < 3; i++) {
        if ((board[i][0] == board[i][1] && board[i][1] == board[i][2]) ||
            (board[0][i] == board[1][i] && board[1][i] == board[2][i])) {
            return 1;
        }
    }
    // Check diagonals
    if ((board[0][0] == board[1][1] && board[1][1] == board[2][2]) ||
        (board[0][2] == board[1][1] && board[1][1] == board[2][0])) {
        return 1;
    }
    return 0;
}

void swap_player_and_marker() {
    if (current_marker == 'X') {
        current_marker = 'O';
        current_player = '2';
    } else {
        current_marker = 'X';
        current_player = '1';
    }
}

int main() {
    initialize_board();
    current_marker = 'X';
    current_player = '1';
    int slot;
    int winner = 0;

    for (int i = 0; i < 9; i++) {
        print_board();
        printf("Player %c, enter your move (1-9): ", current_player);
        scanf("%d", &slot);

        if (slot < 1 || slot > 9 || !place_marker(slot)) {
            printf("Invalid move. Try again.\n");
            i--;
            continue;
        }

        if (check_winner()) {
            winner = 1;
            break;
        }
        swap_player_and_marker();
    }
    print_board();
    if (winner) {
        printf("Player %c wins!\n", current_player);
    } else {
        printf("It's a draw!\n");
    }
    return 0;
}
