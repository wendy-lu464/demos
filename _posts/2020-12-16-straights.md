---
layout: post
title: "Straights"
permalink: /straights
---

I implemented a four-player command line card game using C++ as the final project for my Object-Oriented Programming course.

## Game Overview
A standard card deck without jokers is dealt out to four players. The general idea is to form four piles of cards in numerical order, one pile per suit. 

> Cards are represented by `[rank][first letter of suit]`. For example, `7S` represents the 7 of spades while `AC` represents the ace of clubs. 

The player with `7S` goes first and plays it onto the spades pile. From there, players take turns adding to the piles. 

On a player's turn, they can either play a card onto an existing pile or start a new pile by playing a 7. A card can be added to an existing pile if it's
1. one less than the card at the bottom of the pile, or
2. one greater than the card at the top of the pile.

If the player can't play a card, they must discard a card, which is added to their point total.

> Aces count for 1 point, jacks for 11 points, queens for 12 points, and kings for 13 points.

Once all cards have been played or discarded, the round is over. If no one has over 80 points, a new round begins. 

The game ends when a player exceeds 80 points. The winner is the player with the least number of points.

## Features
### Setup
When starting the game, the user can provide an integer command line argument as the seed. If one isn't provided, the program uses a seed based on the time.

The program then prompts the user to specify which players are human and which are computers.

<img src="assets/straights/setup-h-or-c.png" alt="Screenshot of the interface specifying human and computer players." width="75%">

### Game Loop
During each human player's turn, the program prints out the cards in each pile, the cards in the player's hand, and what the legal plays are.

<img src="assets/straights/game-loop-h.png" alt="Screenshot of the interface when it's a human player's turn." width="75%">

The player can type in the following commands:

`play [card]`: Plays the card onto the appropriate pile. If it's not a legal play or a valid card, the program will print an error.

<img src="assets/straights/game-loop-play.png" alt="Screenshot of the interface when a human player plays a card." width="75%">

`discard [card]`: Discards the card. 

<img src="assets/straights/game-loop-valid-discard.png" alt="Screenshot of the interface when a human player discards a card." width="75%">

If the player tries to discard when a legal play is available, the program will print an error.

<img src="assets/straights/game-loop-invalid-discard.png" alt="Screenshot of the interface when a human player discards a card while a legal play is available." width="75%">

`quit`: Ends the program.

`ragequit`: Replaces the current player with a computer player.

<img src="assets/straights/game-loop-ragequit.png" alt="Screenshot of the interface when a human player ragequits." width="75%">

When it's a computer player's turn, the program simply prints what card it plays or discards.

<img src="assets/straights/game-loop-c.png" alt="Screenshot of the interface when computer players take their turns." width="75%">

### End
At the end of each round, the program prints each player's discarded cards and their previous and current score.

<img src="assets/straights/end-round.png" alt="Screenshot of the interface when a round ends." width="75%">

When the game ends, the program prints which player won. If there's a tie, then it'll print a statement for each winner.

<img src="assets/straights/end-game.png" alt="Screenshot of the interface when the game ends." width="75%">

### Other Features
During a human player's turn, the following commands are available for debugging purposes: 

`deck`: Prints the cards in the deck prior to dealing.

<img src="assets/straights/game-loop-deck.png" alt="Screenshot of the interface after running the 'deck' command." width="75%">

`endscore [score]`: Sets the point total needed to end the game.

<img src="assets/straights/game-loop-endscore1.png" alt="Screenshot of the interface after running the 'endscore 25' command." width="75%">

In the above example, the game will now end when a player exceeds 25 points, instead of the default 80 points.

<img src="assets/straights/game-loop-endscore2.png" alt="Screenshot of the interface showing how the game ends after a player exceeds 25 points." width="75%">

#### Support for Other Player Counts
The game by default has four players, but by starting the game with the `-bonus` command line argument, the user can choose the number of players.

<img src="assets/straights/set-start-player-count.png" alt="Screenshot of the interface when specifying the number of players." width="75%">

Since the deck doesn't necessarily divide evenly between the players, the first player dealt to changes from round to round to avoid dealing the largest hands to the same players. If a player runs out of cards because they had a smaller hand, they simply don't do anything for the rest of the round.

## Architecture

Since a large portion of the project was to design the classes and class interactions, this section is kept vague for academic integrity reasons. More details can be provided in an interview setting, if desired. 

I followed the principles of object-oriented programming during design and implementation.

- **Abstraction**: Each class represents a different component of the game, and their interactions mimic how Straights would be played in real life. When designing the classes, I aimed for high cohesion and low coupling for testing and readability purposes.
- **Encapsulation**: Class methods are only public if it's called by another class. All fields and other methods are private.
- **Inheritance** and **polymorphism**: To reuse code, I used parent and child classes and virtual methods when implementing the cards and various types of card piles.

I also designed my code with adaptability in mind.
- I adapted the Strategy design pattern for use when implementing the players so human players can efficiently switch to computer players when running the `ragequit` command. It also allows for the addition of various computer player difficulties.
- Game parameters are stored in class fields (e.g. the score needed to end the game) in case they need to be modified for new features. 

### Memory Management

Memory management is a notable topic in C++ and one of the bonus challenges was to avoid explicit memory management. To do that, I used STL containers and unique pointers to allocate and free memory.

In addition, I used RAII (Resource Acquisition Is Initialization) to prevent memory leaks by tying all object lifetimes to a single instance of the main game object. When the main game object is constructed, it constructs all the other objects necessary to run the game. Once the game ends, the main game object is destroyed, which in the process destroys all of the other objects as well.
