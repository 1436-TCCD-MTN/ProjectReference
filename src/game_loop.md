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
    * Call display_date function
    * Call display_status function
    * Call handle_turn function
    * Call handle_eating function, check return for game over
    * Call check_for_riders function, check return for game over
    * Call check_for_event function, check return for game over
    * Call check_for_mountains function, check return for game over
* Final Turn:
    * Set fraction of 2 weeks traveled
        * (2040 - miles_through_prev) / (miles_traveled - miles_through_prev)
    * food = food + (1 - fraction) * (8 + 5 * ration_amount)
    > YOU FINALLY ARRIVED AT OREGON CITY
    > AFTER 2040 LONG MILES---HOORAY!!!!!
    > A REAL PIONEER!
    * fraction = fraction * 14
    * turn = turn * 14 - fraction
    * fraction = (fraction + 1) % 7 (to get the day of the week)
    * day = ["MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY", "SATURDAY", "SUNDAY"]
    * To find the date:
        * turn ranges:
            * 0-124: JULY {turn-93} 1847
            * 125-155: AUGUST {turn-124} 1847
            * 156-185: SEPTEMBER {turn-155} 1847
            * 186-216: OCTOBER {turn-185} 1847
            * 217-246: NOVEMBER {turn-216} 1847
            * Else: DECEMBER {turn-246} 1847
        * Print the date
    * Print status
    >            PRESIDENT JAMES K. POLK SENDS YOU HIS
    >                  HEARTIEST CONGRATULATIONS
    >
    >            AND WISHES YOU A PROSPEROUS LIFE AHEAD
    >
    >                       AT YOUR NEW HOME