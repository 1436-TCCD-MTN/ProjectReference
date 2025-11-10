# Game Loop

## game_loop.rs

### `FUNCTION game_loop()`
Contains the primary loop for the game.
* Calls the initialize_game function
* Calls get_yes_no_input with prompt
    > DO YOU NEED INSTRUCTIONS (YES/NO)
* If Yes
    * Calls display_tutorial function
* Call set_difficulty function
* Call handle_initial_purchases function
* Start loop
    * Check if miles_traveled >= 2040
        * True: Exit loop
            * Call display_win()
            * return
    * Call display_date function
    * Call display_status function
    * Call handle_turn function
    * Call handle_eating function, check return for game over
    * Call check_for_riders function, check return for game over
    * Call check_for_event function, check return for game over
    * Call check_for_mountains function, check return for game over