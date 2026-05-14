> 🇧🇷 *Leia em [Português](README-pt.md).*

# Matching Game in Logisim

André Lucas de Souza Lima  
Kayky Moreira Morais  
Computer Science - Federal University of Cariri  
Developed for the Digital Circuits course  
Instructed by Professor Ramon Santos Nepomuceno

---

## What is it about

This project is a "Matching Game", a memory-based game created using the Logisim application, which is used to develop low-level circuits simulated in a digital environment.

Below is the image of the main screen:

![main image of the game's main screen](./Pictures/picture_15.png)

The main objective was to offer a fun experience in a functional game and to challenge ourselves with the predominant use of memory structures, such as flip-flops, registers, counters, and other tools that were essential for the final implementation.

Several revisions were also necessary throughout the work so that the result would be solid and free of inconsistencies or bugs, such as the ones that will be shown and explained later.

## How to install Logisim

The fastest and safest way to install Logisim is through the SourceForge website, known for providing downloads on a solid platform. <br>
Steps to install: <br>
By accessing this <a href="https://sourceforge.net/projects/circuit/">link</a>, you should be redirected to the Logisim page on SourceForge, which will look similar to the following image:

![logisim page on sourceforge](./Pictures/picture_14.png)

Here, you simply need to press the main button labeled "Download", which will transfer an executable to your browser and request a storage location on your computer.  
After that, Logisim will already be installed and ready to be executed through this file.

## How to play (rules)

The Matching Game (or memory game) is played by two players who must use their ability to memorize the cards in order to win.

Basically, the game is played in turns, where each player chooses two different cards to reveal their hidden numbers. If the numbers are equal, the score of the player who guessed correctly is increased by one, the chosen cards remain revealed, and they cannot be selected again until the end of the game. Otherwise, the score remains the same and the numbers on the cards are hidden again.

In any case, after the match verification, the turn is passed to the other player, and this repeats until all cards have been revealed and one of the players wins or there is a tie.

## How it works

### State machine

The flow of the game was divided into four states so that the processes would happen in an organized and correct manner. These states are transitioned according to the players' actions and have certain functionalities to occur at their specific moments, which are:

State 0 - this is the idle state, where the circuit waits for the player's first card selection.

State 1 - after the selection, the player presses the "CONFIRM" button over the desired display, and then the card's number is shown and stored as the value of the first selection. Afterwards, it waits for the second choice.

State 2 - in the same way as in state 1, the "CONFIRM" button is pressed over a card different from the first one, its value is revealed and stored like the first number. Next, there is a wait to transition to the next state.

State 3 - by pressing the "CONFIRM" button one more time over any display, the circuit compares both chosen numbers, and if they are equal, the current player scores a point and the chosen displays remain turned on until the end of the game. If they are different, no point is awarded to the player and the values are hidden again. At the end of this state, it automatically transitions back to the initial one, forming a loop.

For the circuit to identify what to do at each moment of the game, a state machine was implemented, which is represented below:

![state machine](./Pictures/picture_16.png)

As soon as the confirm button is triggered (with a delay), its pulse joins an AND coming from an OR with a negated "on" ("ligado") tunnel and a "state 2" to increment the value of a counter responsible for representing the current state. This structure ensures that the choice of the second card only occurs if the choice is not the same as the first one through the negated "on" tunnel (which returns 1 if the current led is on), while also ensuring that the state is changed automatically when the current state is state 2, so the player doesn't have to press the "CONFIRM" button unnecessarily.

On the right side of the image, the counter's result is obtained and compared four times so that it can pass the value 1 only to the tunnel referring to its actual state.

### LEDs

The selection LEDs are an effective way for the player to locate themselves and navigate through the displays to make their move choice.

![led demonstration](./Pictures/picture_18.png)

In the image above, the LED represents the circle above the hexadecimal display. It is turned off on the left of the image and turned on on the right.

Here is the control that allows navigation and defines the LEDs turned on and off:

![led control demonstration](./Pictures/picture_19.png)

Intuitively, the buttons represent the navigation directions between the LEDs on the game grid, which can be up, down, left, and right.

The structure used to implement this LED change is:

![circuit to navigate through the leds](./Pictures//picture_20.png)

The logic is that the LED's position is represented as a row and column pair stored in counters, with higher values for the row and column pointing to LEDs further right and down, since the LED (0, 0) is located in the top-left corner of the grid.

If the right or down arrows are pressed, the column or row counters, respectively, receive a clock pulse and are increased by one unit. In contrast, triggering the left or up arrows activates this same clock while also activating the "load" input, which causes it to decrease the counter by one unit.

### Displays

The hexadecimal displays are the visual representation of the value stored in each of the game's "cards". They remain turned off (a dash in the middle) until they are selected to have their values revealed.

This choice is made by selecting the LED above the