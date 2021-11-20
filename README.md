# blackjack

Mi dirección de GitHub para este repositorio es la siguiente: [GitHub](https://github.com/lauralardies/blackjack)
https://github.com/lauralardies/blackjack

Hemos resuelto un programa para jugar al BlackJack. A partir de una baraja de 52 cartas, juegas contra una banca y tratas de obtener un máximo de 21 puntos. Aquel jugador que tenga un mayor puntuaje sin pasarse de 21 gana el juego. 

El diagrama de flujo que tenemos en nuestro código es el siguiente: 

<br>
<img height="600" src="https://github.com/lauralardies/blackjack/blob/main/blackjackfigma.jpg" />
<br>

```
import random

def updateDeck ():
    max_cards = len(deck)
    return max_cards

def selectCard():
    max_cards = updateDeck()
    while True:
        card = input("Please, choose a card between 1 and " + str(max_cards) + ": ")
        try:
            card = int(card)
        except:
            pass
        else: 
            if 1 <= card <= 52:
                break
    return card-1

def yourGame():
    points = 0
    while True:
        card = selectCard()
        card1 = deck[card]
        points = points + card_values[card1]
        deck.remove(card1)
        print ("The card you have chosen is " + card1 + ".")
        print("You have got " + str(points) + " points so far.")
        if points > 21:
            print("You have more than 21 points! You have lost this game.")
            score.append(points)
            break
        end = input("Do you want another card? [Y]/N: ")
        if str.upper(end) == "N":
            break
    score.append(points)

def dealerGame():
    pointsD = 0
    while True:
        card = random.randint(1,len(deck))
        card1 = deck[card]
        pointsD = pointsD + card_values[card1]
        deck.remove(card1)
        print ("The card the Dealer has chosen is " + card1 + ".")
        print("The Dealer has " + str(pointsD) + " points so far.")
        if pointsD > 21:
            print("The Dealer has over 21 points! You have won this game.")
            score.append(pointsD)
            break
        if pointsD >= 16:
            break
    score.append(pointsD)

def winner ():
    if score[0] > score[1]:
        print("Congratulations! You have won this game.")
    elif score[0] < score[1]:
        print("You have lost this game!")
    elif score[0] == score[1]:
        print("You have lost this game!")
    print("These are the final results: You " + str(score[0]) + " points, the Dealer " + str(score[1]) + " points.")

card_values = { 
    chr(0x1f0a1): 11, 
    chr(0x1f0a2): 2, 
    chr(0x1f0a3): 3, 
    chr(0x1f0a4): 4, 
    chr(0x1f0a5): 5, 
    chr(0x1f0a6): 6, 
    chr(0x1f0a7): 7, 
    chr(0x1f0a8): 8, 
    chr(0x1f0a9): 9, 
    chr(0x1f0aa): 10,
    chr(0x1f0ab): 10, 
    chr(0x1f0ad): 10, 
    chr(0x1f0ae): 10, 
} 

while True:
    score = []
    deck = [chr(0x1f0a1), chr(0x1f0a2), chr(0x1f0a3), chr(0x1f0a4), chr(0x1f0a5), chr(0x1f0a6), chr(0x1f0a7), chr(0x1f0a8), chr(0x1f0a9), chr(0x1f0aa), chr(0x1f0ab), chr(0x1f0ad), chr(0x1f0ae)]*4
    random.shuffle(deck)
    while True: 
        yourGame()
        if score[0] > 21:
            break
        print("Now it is the Dealers' turn!")
        dealerGame()
        if score[1] > 21:
            break
        winner()
        break
    choice = input("Would you like to play again? [Y]/N: ")
    if str.upper(choice) == "N":
        break
