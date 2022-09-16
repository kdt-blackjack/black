## HOW TO CODE BLACKJACK(블랙잭 코드 이렇게 하세요. 모르시면 구글링)

import os
import random

deck = [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]*4

def deal(deck):
    hand = []
    for i in range(2):
	    random.shuffle(deck)
	    card = deck.pop()
	    if card == 11:card = "J"
	    if card == 12:card = "Q"
	    if card == 13:card = "K"
	    if card == 14:card = "A"
	    hand.append(card)
    return hand

def play_again(): #2022-09-16,YSJ 리겜이요. 
    again = input("Do you want to play again? (Y/N) : ").lower()
    if again == "y":
	    dealer_hand = []
	    player_hand = []
	    deck = [2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14]*4
	    game()
    else:
	    print("Bye!")
	    exit()

def total(hand):
    total = 0
    for card in hand:
	    if card == "J" or card == "Q" or card == "K":
	        total+= 10
	    elif card == "A":
	        if total >= 11: total+= 1
	        else: total+= 11
	    else: total += card
    return total

def hit(hand):
	card = deck.pop()
	if card == 11:card = "J"
	if card == 12:card = "Q"
	if card == 13:card = "K"
	if card == 14:card = "A"
	hand.append(card)
	return hand

def clear():
	if os.name == 'nt':
		os.system('CLS')
	if os.name == 'posix':
		os.system('clear')

def print_results(dealer_hand, player_hand):
	clear()
	print ("The dealer has a " + str(dealer_hand) + " for a total of " + str(total(dealer_hand)))
	print ("You have a " + str(player_hand) + " for a total of " + str(total(player_hand)))

def blackjack(dealer_hand, player_hand):
	if total(player_hand) == 21:
		print_results(dealer_hand, player_hand)
		print ("Congratulations! You got a Blackjack!\n")
		play_again()
	elif total(dealer_hand) == 21:
		print_results(dealer_hand, player_hand)		
		print ("Sorry, you lose. The dealer got a blackjack.\n")
		play_again()

def score(dealer_hand, player_hand):
	if total(player_hand) == 21:
		print_results(dealer_hand, player_hand)
		print ("Congratulations! You got a Blackjack!\n")
	elif total(dealer_hand) == 21:
		print_results(dealer_hand, player_hand)		
		print ("Sorry, you lose. The dealer got a blackjack.\n")
	elif total(player_hand) > 21:
		print_results(dealer_hand, player_hand)
		print ("Sorry. You busted. You lose.\n")
	elif total(dealer_hand) > 21:
		print_results(dealer_hand, player_hand)			   
		print ("Dealer busts. You win!\n")
	elif total(player_hand) < total(dealer_hand):
		print_results(dealer_hand, player_hand)
        #print ("Sorry. Your score isn't higher than the dealer. You lose.\n")
	elif total(player_hand) > total(dealer_hand):
		print_results(dealer_hand, player_hand)			   
		print ("Congratulations. Your score is higher than the dealer. You win\n")		

def game():
	choice = 0
	clear()
	print ("WELCOME TO BLACKJACK!\n")
	dealer_hand = deal(deck)
	player_hand = deal(deck)
	while choice != "q":
		print ("The dealer is showing a " + str(dealer_hand[0]))
		print ("You have a " + str(player_hand) + " for a total of " + str(total(player_hand)))
		blackjack(dealer_hand, player_hand)
		choice = input("Do you want to [H]it, [S]tand, or [Q]uit: ").lower()
		clear()
		if choice == "h":
			hit(player_hand)
			while total(dealer_hand) < 17:
				hit(dealer_hand)
			score(dealer_hand, player_hand)
			play_again()
		elif choice == "s":
			while total(dealer_hand) < 17:
				hit(dealer_hand)
			score(dealer_hand, player_hand)
			play_again()
		elif choice == "q":
			print ("Bye!")
			exit()
	
if __name__ == "__main__":
    game()

## Origin of BlackJack

블랙잭은 카지노 뱅킹 게임입니다. 세계에서 가장 널리 사용되는 카지노 뱅킹 게임인 이 게임은 52개의 카드로 구성된 데크를 사용하며 Twenty-One으로 알려진 글로벌 카지노 뱅킹 게임 제품군의 후손입니다. 이 카드 게임 제품군에는 영국 게임인 Pontoon과 유럽 게임인 Vingt-et-Un도 포함됩니다.

<from. Google >

##The rule of Black Jack

1. 블랙잭은 본인과 딜러 간의 1:1 대결

2. 카드 자수의 상관없이 카드의 숫자 합을 21을 만들거나 딜러보다 21에 더 가깝게 만들면 승리

3. 본인의 카드를 확인하며 Hit 또는 Stand를 외치고 카드의 합이 21이 넘어가면 자동으로 게임은 종료된다.

### 용어 정리
1. HIT : 카드를 추가로 받기

2. STAND : 카드를 받지 않기

3. BUST : 카드의 합이 21을 초과

### 알파벳 숫자 계산
1. J, Q, K ==10

2. A ==1


