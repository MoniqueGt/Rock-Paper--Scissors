# Rock-Paper--Scissors

import random

moves = ['rock', 'paper', 'scissors']

class Player:
    def move(self):
        return 'rock'
    def learn(self, my_move, their_move):
        pass

def beats(one, two):
    return ((one == 'rock' and two == 'scissors') or
            (one == 'scissors' and two == 'paper') or
            (one == 'paper' and two == 'rock'))

class Random_Player(Player):
    def move(self):
        return(random.choice(moves))

class Human_Player(Player):
    def move(self):
        while True:
            Input = input("Make your move\n")
            if Input.lower() not in moves:
                print("Inoperative\n")
            else:
                print(f"You played {Input}")
                return(Input.lower(moves))

class ReflectPlayer(Player):
    def move(self, my_move, their_move):
        if their_move == "paper":
            return "paper"
        elif their_move == "scissors":
            return "scissors"
        else:
            return "rock"



class Cycle(Player):
    def move(self, my_move, their_move):
        if my_move == "rock":
            return "paper"
        elif my_move == "paper":
            return "scissors"
        else:
            return "rock"
class Game:
    def __init__(self, p1, p2):
        self.p1 = p1
        self.p2 = p2
        self.p1_score = 0
        self.p2_score = 0
    def play_round(self):
        move1 = self.p1.move()
        move2 = self.p2.move()
        print(f"Player 1: {move1}  Player 2: {move2}")
        self.p1.learn(move1, move2)
        self.p2.learn(move2, move1)

    def play_game(self):
        print("Let the games begin")
        round_num = int(input("How many rounds? "))
        move1 = self.p1.move()
        move2 = self.p2.move()
        for round in range(round_num):
            print(f"Round {round}:")
            self.play_round()
            print(f"The score is {self.p1_score} to {self.p2_score}")
            if self.p1_score > self.p2_score:
                print("You're the winner!")
            elif self.p1_score < self.p2_score:
                print("You lose")
            else:
                print("Tie")


if __name__ == '__main__':
    game = Game(Human_Player(), Random_Player())
    game.play_game()

