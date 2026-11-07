import random
#function1
def check_win(Boards):
    for i in range(3):
        if Boards[i][0] == Boards[i][1] == Boards[i][2] != "-":
            return Boards[i][0]

        if Boards[0][i] == Boards[1][i] == Boards[2][i] != "-":
            return Boards[0][i]

    # diagonals
    if Boards[0][0] == Boards[1][1] == Boards[2][2] != "-":
        return Boards[0][0]

    if Boards[0][2] == Boards[1][1] == Boards[2][0] != "-":
        return Boards[0][2]

    if len(get_available_moves(Boards)) == 0:
       return "tie"

    return None

#function2
def get_available_moves(Boards):
    available = []
    for i in range(3):
        for j in range(3):
            if Boards[i][j] == "-":
                position = (i * 3) + j + 1
                available.append(position)
    return available


#function3
def play_game():

 Boards = [
    ["-", "-", "-"],
    ["-", "-", "-"],
    ["-", "-", "-"]
 ]

 current_player = "X"
 game_over = False

 print("Welcome to Tic-Tac-Toe!")
 print("You have to choose your moves using num 1-9 (like a keypad)")

 print("\n")
 for i,row in enumerate(Boards):
     print(" | ".join(row))
     if i<2:
         print("----------")

 print("\n")
 while not game_over:
     if current_player == "X":
        move=int(input("Player(X) - Enter your move(1-9): "))
        if move not in range(1,10):
             print("Invalid Move")
             continue
        position = move-1
        row = position // 3
        column = position % 3
        if Boards[row][column] != "-":
            print("Invalid Move, That spot is already taken. try another move ")
            continue
#assigning values
        Boards[row][column] = "X"
        current_player = "O"
     #else statement
     else:
         print("Time for Computer's move...")
         available=get_available_moves(Boards)
         computer_move=random.choice(available)
         position = computer_move-1
         row = position // 3
         column = position % 3
         Boards[row][column] = "O"
         print("Computer marked ")
         current_player = "X"
     for i, row in enumerate(Boards):
         print(" | ".join(row))
         if i < 2:
             print("----------")
     result = check_win(Boards)
     if result:
         game_over = True
         if result == "tie":
             print("Tie! Game Over")
         else:
             print("Player " + result +" wins!")
             print("Game Over")







if __name__ == "__main__":
    play_game()




