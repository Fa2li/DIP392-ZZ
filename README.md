https://docs.google.com/document/d/1fsD1r7vEmSF3nPOAT5xL7sQdENsL_G5U-zZ-XRtDb38/edit?usp=sharing


class Connect4:
    def __init__(self, starting_player=0):
        self.board = [[' ' for _ in range(7)] for _ in range(6)]
        self.players = ['Yellow', 'Red']
        self.current_player = starting_player

    def print_board(self):
        for row in self.board:
            print('|'.join(row))
            print('-------------')
    
    def is_valid_move(self, column):
        return column >= 0 and column < 7 and self.board[0][column] == ' '

    def drop_disc(self, column):
        for row in range(5, -1, -1):
            if self.board[row][column] == ' ':
                self.board[row][column] = self.players[self.current_player]
                return True
        return False

    def check_win(self):
        # Check rows
        for row in range(6):
            for col in range(4):
                if self.board[row][col] != ' ' and self.board[row][col] == self.board[row][col+1] == self.board[row][col+2] == self.board[row][col+3]:
                    return True

        # Check columns
        for col in range(7):
            for row in range(3):
                if self.board[row][col] != ' ' and self.board[row][col] == self.board[row+1][col] == self.board[row+2][col] == self.board[row+3][col]:
                    return True

        # Check diagonals
        for row in range(3):
            for col in range(4):
                if self.board[row][col] != ' ' and self.board[row][col] == self.board[row+1][col+1] == self.board[row+2][col+2] == self.board[row+3][col+3]:
                    return True

        for row in range(3, 6):
            for col in range(4):
                if self.board[row][col] != ' ' and self.board[row][col] == self.board[row-1][col+1] == self.board[row-2][col+2] == self.board[row-3][col+3]:
                    return True

        return False

    def play(self):
        while True:
            self.print_board()
            column = int(input(f"{self.players[self.current_player]}, choose a column (0-6): "))
            if self.is_valid_move(column):
                if self.drop_disc(column):
                    if self.check_win():
                        self.print_board()
                        print(f"{self.players[self.current_player]} wins!")
                        break
                    elif all(self.board[row][col] != ' ' for row in range(6) for col in range(7)):
                        self.print_board()
                        print("It's a tie!")
                        break
                    else:
                        self.current_player = 1 - self.current_player
                else:
                    print("Column is full. Try again.")
            else:
                print("Invalid column. Try again.")


# Let the players choose their color
color_choice = int(input("Choose your color:\n0. Yellow\n1. Red\n"))
game = Connect4(color_choice)
game.play()
![image](https://github.com/Fa2li/DIP392-ZZ/assets/54802357/26f04df1-7df2-4dfb-af30-27bc8fe4cb29)
