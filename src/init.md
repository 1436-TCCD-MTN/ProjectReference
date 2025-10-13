// --- Game Setup Functions ---
// init.rs

// Initializes the GameState object and sets all the initial values
// {total_miles=2040, miles_traveled=0, turn=0, date="MARCH 29",
// rations=Moderate, is_sick=false, is_injured=false, inventory=
// {oxen=0, food=0, bullets=0, clothing=0, money=700, misc=0}
// difficulty=5}
// Checks if user wants to view the tutorial, calls tutorial if they do
// Calls initial purchases function, calls set difficulty function
// Returns the prepared GameState
FUNCTION initialize_game() RETURNS GameState

// Display the game tutorial
FUNCTION display_tutorial()

// Handles the initial game purchases. Should check at the end that the
// total purchases are less than/equal to the amount of money the player has.
// Also needs to ensure the player spends between 200 and 300 (inclusive) on
// oxen. Loops until user has made correct purchases
FUNCTION handle_initial_purchases(game_state: BYREF MUTABLE GameState)

// Sets the game difficulty
// Should call the get_int_input function with a minimum of 1
// and a maximum of 5 for the difficulty options. The difficulty
// number chosen is how many seconds the player has to enter
// the keyword when doing the shooting subroutine.
FUNCTION set_difficulty(game_state: BYREF MUTABLE GameState)