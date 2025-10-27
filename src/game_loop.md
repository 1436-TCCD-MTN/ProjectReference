# Game Loop

## game_loop.rs

### `FUNCTION game_loop(game_state: BYREF MUTABLE GameState)`
Contains the primary loop for the game.
* Calls the initialize_game function
* Calls get_yes_no_input with prompt
    > DO YOU NEED INSTRUCTIONS (YES/NO)
* If Yes
    * Calls display_tutorial function
* Call set_difficulty function
* Call handle_initial_purchases function
* Start loop
    * Call display_date function
    * Call display_status function
    * Call handle_turn function
    * Call 