# project TicTacToe

import random

board = [' '] * 10
computer = 'x'
human = 'o'


def display_board(board):
    print(f'{board[1]} | {board[2]} | {board[3]}')
    print(f'{board[4]} | {board[5]} | {board[6]}')
    print(f'{board[7]} | {board[8]} | {board[9]}')
    print('_' * 10)


def check_win():
    win_conditions = [
        (1, 2, 3), (4, 5, 6), (7, 8, 9),
        (1, 4, 7), (2, 5, 8), (3, 6, 9),
        (1, 5, 9), (7, 5, 3)
    ]
    for (a, b, c) in win_conditions:
        if board[a] == board[b] == board[c] and board[a] != ' ':
            return True
    return False


def check_draw():
    return ' ' not in board[1:]


def is_available(pos):
    return board[pos] == ' '


def insert(letter, pos):
    if is_available(pos):
        board[pos] = letter
        display_board(board)
        if check_win():
            if letter == 'x':
                print("Computer wins!")
                exit()
            else:
                print("You win!")
                exit()
        if check_draw():
            print('Draw!')
            exit()
    else:
        if letter == 'o':
            pos = int(input("Not free! Please re-enter a position: "))
            insert(letter, pos)
        else:
            pos = random.randint(1, 9)
            while not is_available(pos):
                pos = random.randint(1, 9)
            insert(letter, pos)


def human_move(letter):
    pos = int(input("Enter the position to insert: "))
    insert(letter, pos)


def computer_move(letter):
    pos = random.randint(1, 9)
    while not is_available(pos):
        pos = random.randint(1, 9)
    insert(letter, pos)


while True:
    display_board(board)
    computer_move(computer)
    if check_win() or check_draw():
        break
    human_move(human)
    if check_win() or check_draw():
        break
