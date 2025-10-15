# Turn
## `turn.rs`
Handles the turn logic.

### `FUNCTION handle_fort_visit(game_state: BYREF MUTABLE GameState)`

### `FUNCTION handle_hunting(game_state: BYREF MUTABLE GameState)`

* Checks if the player has more than 39 bullets
* The player loses 45 miles of progress to stop and hunt
* Calls the shooting subroutine
* If the time taken was <= 1:
    * Gain between 52 and 58 food
    * Lose between 10 and 14 bullets
    * Display message:
        > RIGHT BETWEEN THE EYES---YOU GOT A BIG ONE!!!!
        >
        > FULL BELLIES TONIGHT!
    * Return
* If 13 * time taken <= a random number between 1 and 100:
    * Gain food: 48 - 2 * time taken
    * Lose bullets: 10 + 3 * time taken
    * Display message:
        > NICE SHOT---RIGHT ON TARGET--GOOD EATIN' TONIGHT!!
* Else:
    * Don't lose or gain anything
    * Display message:
        > YOU MISSED---AND YOUR DINNER GOT AWAY.....

### `FUNCTION handle_turn(game_state: GameState)`
Handles the turn logic, should only show the fort option every odd turn, shows the continue and hunting option on every other turn.
* Checks the turn number, calls the get_int_input function with prompt for fort if it is an odd turn, calls the get_int_input with only continue and hunt if it is an even turn.