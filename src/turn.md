# Turn
## `turn.rs`
Handles the turn logic. Declares the sub mods handle_turn, handle_hunting, and handle_fort_visit

## `handle_fort_visits.rs`

### `FUNCTION handle_fort_visit(game_state: BYREF MUTABLE GameState)`

## `handle_hunting.rs`
Handles the functions related to the hunting minigame.

### `FUNCTION handle_hunting(game_state: BYREF MUTABLE GameState)`

* Checks if the player has more than 39 bullets
* The player loses 45 miles of progress to stop and hunt
* Calls the shooting subroutine
* If the time taken was <= difficulty:
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

## `handle_turn.rs`
