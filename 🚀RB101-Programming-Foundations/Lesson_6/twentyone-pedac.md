# Twenty One Game

Twenty one is a game similar to Blackjack but significantly simpler

## Problem

**Input** - Player choice ( hit or stay )

**Output** - Display result of game

### Rules

- Goal - get as close to 21 as possible without going over
- Setup
  - Start with a normal 52-card deck
    - four suits - clubs, diamonds, hearts, spades
    - 13 ranks - 2, 3, 4, 5, 6, 7, 8, 9, 10, Jack, Queen, King, Ace
  - The game consists of a player and dealer
  - Both participants are initially dealt two cards to start
  - The player can see both their cards but only one of the dealer's cards
- Card Values
  - 2-10 are worth face value
  - Jack, Queen, King are worth 10
  - Ace is worth either 1 or 11
  - An Ace's value is determined each time a new card is drawn from the deck
- Player Turn
  - The player goes first - decides to hit or stay
  - Hit means the player is dealt another card
  - The player can hit as many times as they want
  - The player turn is over when the player either stays or busts (goes over 21)
  - If the player busts, the game is over and the dealer wins
- Dealer Turn
  - Once the player stays, its the dealers turn
  - The dealer must hit until the total is at least 17
  - If the dealer busts, the player wins
- When the player and dealer stay, the cards will be totaled to determine the winner. Highest total wins

### Data Structure

- Card is a hash containing rank and suit

  `{ rank: "2", suit: "club"}`

- Deck and hand is an array of cards

  - `Player_deck = [ {rank: "2", suit: "club"}, {rank: "Ace", suit: "spades"}]`

### Algorithm

1. initialize the deck
2. Deal cards to the player and dealer
3. Player choses to hit or stay
   1. repeat until the player busts or stays
4. If the player busts, the dealer wins
5. Dealer hits or stays - has to hit till total is 17
   1. Repeat until dealer card total is greater than or equal to 17
6. If dealer busts, the player wins
7. Count card total and declare winner