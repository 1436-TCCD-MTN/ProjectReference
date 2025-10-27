# Game Setup
Game Setup Functions

## init.rs

### `FUNCTION initialize_game() RETURNS GameState`
Initializes the GameState object and sets all the initial values
* GameState =
    * total_miles=2040
    * miles_traveled=0
    * turn=0
    * date="MARCH 29",
    * rations=Moderate
    * is_sick=false
    * is_injured=false
    * inventory=
        * oxen=0
        * food=0
        * bullets=0
        * clothing=0
        * money=700
        * misc=0
    * difficulty=5
* Checks if user wants to view the tutorial, calls display_tutorial if they do
* Calls handle_initial_purchases function
* calls set_difficulty function
* Returns the prepared GameState

### `FUNCTION display_tutorial()`
Displays the game tutorial text

### `FUNCTION handle_initial_purchases(game_state: BYREF MUTABLE GameState)`
Handles setting up the initial purchases
* Asks how much the user wants to spend on each inventory item
* Tracks how much is spent on each item.
    * Player can only spend between 200 and 300 on Oxen
    * Checks at the end that the player didn't spend too much and loops if they did
    * If player tries to spend less than 0:
    > IMPOSSIBLE
    > HOW MUCH DO YOU WANT TO SPEND ON YOUR OXEN TEAM
    * Less than 200:
    > NOT ENOUGH
    * More than 300:
    > TOO MUCH
* Outputs:
    > HOW MUCH DO YOU WANT TO SPEND ON FOOD
    > HOW MUCH DO YOU WANT TO SPEND ON AMMUNITION
    > HOW MUCH DO YOU WANT TO SPEND ON CLOTHING
    > HOW MUCH DO YOU WANT TO SPEND ON MISCELLANEOUS SUPPLIES
    >YOU OVERSPENT--YOU ONLY HAD $700 TO SPEND. BUY AGAIN
    >AFTER ALL YOUR PURCHASES, YOU NOW HAVE {money} DOLLARS LEFT

### `FUNCTION set_difficulty(game_state: BYREF MUTABLE GameState)`
Sets the game difficulty
* Display difficulty selection text:
    * "HOW GOOD A SHOT ARE YOU WITH YOUR RIFLE?"
      "  (1) ACE MARKSMAN,  (2) GOOD SHOT,  (3) FAIR TO MIDDLIIN'"
      "         (4) NEED MORE PRACTICE,  (5) SHAKY KNEES"
* Calls the get_int_input with variables:
    * min = 1
    * max = 5
    * prompt = "ENTER ONE OF THE ABOVE -- THE BETTER YOU CLAIM YOU ARE, THE\nFASTER YOU'LL HAVE TO BE WITH YOUR GUN TO BE SUCCESSFUL."
* Set the GameState difficulty based on return value of the get_int_input function.