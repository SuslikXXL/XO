print("---------------------------")
print("")
print("")
print(" Добро пожаловать в игру\n   'Крестики - Нолики'")
print("")
print("")
print("")
print("---------------------------")

board = list(range(1, 10))

def play_board(board):
    for i in range(3):
        print("|", board[0+i*3], "|", board[1+i*3], "|", board[2+i*3], "|")
        print("---------------")

def put_input(symbol):
    valid = False
    while not valid:
        answer = input("Вместо какой цифры поставите символ? " + symbol + "? ")
        try:
            answer = int(answer)
        except:
            print("Неверный ввод!")
            continue
        if answer >= 1 and answer <= 9:
            if (str(board[answer-1]) not in "XO"):
                board[answer-1] = symbol
                valid = True
            else:
                print ("Эта клеточка уже занята")
        else:
            print ("Неверный ввод! Введите число от 1 до 9.")

def check_win(board):
    win_coord = ((0, 1, 2),(3, 4, 5),(6, 7, 8),(0, 3, 6),(1, 4, 7),(2, 5, 8),(0, 4, 8),(2, 4, 6))
    for each in win_coord:
        if board[each[0]] == board[each[1]] == board[each[2]]:
            return board[each[0]]
    return False

def main(board):
    counter = 0
    win = False
    while not win:
        play_board(board)
        if counter % 2 == 0:
            put_input("X")
        else:
            put_input("O")
        counter += 1
        if counter > 4:
            tmp = check_win(board)
            if tmp:
                print (tmp, "Вы выиграли!")
                win = True
                break
        if counter == 9:
            print ("Ничья!")
            break
    play_board(board)
main(board)
