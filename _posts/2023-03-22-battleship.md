---
layout: post
title: "Battleship"
permalink: /battleship
---

I implemented the UI for a desktop version of the classic board game Battleship using Kotlin and JavaFX, where the user plays against a computer player. This assignment was for my User Interfaces course and focused on graphics, animations, hit-testing, and transformations. 

## Game Overview
Battleship is a competitive two-player game where players take turns attempting to sink their opponent's ships.

The game has three phases.

1. **Setup**: Each player has a board and a set of 5 ships. Players place their ships on their board. They can't see where their opponent's ships are.
2. **Game loop**: On their turn, the player picks a square on their opponent's board to fire at. If a ship is in that square, they can fire again, otherwise their turn ends. A ship sinks when all the squares it's in has been fired at.
3. **Ending**: A player wins once they sink all of their opponent's ships.

## Features
### Setup
The UI consists of two 10 x 10 boards. The left board represents the user's (hereafter referred to as "the player's") board. The right board represents the player's view of the opponent's (the computer's) board.

The player's ships are initially located between the boards.

The player can click on a ship to pick it up or put it down. Once picked up, the player can move it around and right-click to toggle between orientations. When a ship is placed on the board, it will snap to the closest position. If the location isn't valid (e.g. there's a ship in the way or it's not on the board), then the ship will return to its initial position.

<video width="100%" controls autoplay muted loop>
  <source src="assets/battleship/setup.mp4" type="video/mp4" />
</video>

Once all the ships are placed, the player can click the Start Game button. After clicking, the ships can't be moved.

### Game Loop
The player goes first and can click a cell on the opponent's board to attack it. Light gray represents a miss, coral represents a hit, and dark gray represents a sunken ship.

<video width="100%" controls autoplay muted loop>
  <source src="assets/battleship/game-loop.mp4" type="video/mp4" />
</video>

### Ending
Once the game ends, the player's sunken ships remain on their board while the other ships return to their original positions. The text above the boards reflect who won.

<video width="100%" controls autoplay muted loop>
  <source src="assets/battleship/ending.mp4" type="video/mp4" />
</video>

## Architecture

This app uses the Model-View-Controller (MVC) design pattern. When the player interacts with the UI, the following steps occur:
1. The player clicks something in the View, sending the input to the Controller. 
2. The Controller tells the Model to update the game state.
3. The Model notifies the View that there's been an update.
4. The View refetches the game state from the Model and redraws the boards.

My assignment was to implement the View and Controller - the Model and computer player were provided in the assignment starter code.
