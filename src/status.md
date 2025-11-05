# Status

## status.rs

### `FUNCTION set_date(game_state: BYREF MUTABLE GameState) -> STRING`
Uses the turn number to iterate on the game date
* Dates list:
    * MARCH 29, APRIL 12, APRIL 26, MAY 10, MAY 24, JUNE 7, JUNE 21, JULY 5, JULY 19, AUGUST 2, AUGUST 16, AUGUST 31, SEPTEMBER 13, SEPTEMBER 27, OCTOBER 11, OCTOBER 25, NOVEMBER 8, NOVEMBER 22, DECEMBER 6, DECEMBER 20
* Return dates[turn]

### `FUNCTION print_date(date: BYREF STRING) -> Option<CauseOfDeath>`
Prints the date formatted for the status display
* Checks if on turn 20
     > YOU HAVE BEEN ON THE TRAIL TOO LONG ------
     > 
     > YOUR FAMILY DIES IN THE FIRST BLIZZARD OF WINTER
     * Return Some(Freezing)
* Prints "MONDAY {date} 1847"
* Return None 

### `PUBLIC FUNCTION display_status(game_state: BYREF GameState)`
Displays the current player status
* Calls set_date function, takes return value
* Calls print_date function with previous return
* If Food < 13 output:
    * "YOU'D BETTER DO SOME HUNTING OR BUY FOOD SOON!!!!"
* Check the Injury and Illness flags
    * If either is true:
        * Reduce money by 20
        * If money is > 0:
            * "DOCTOR'S BILL IS $20"
            * Set both flags to false
        * else:
            * Set cause of death flag to NoMoney and return
* Output: "TOTAL MILEAGE IS {miles_traveled}"
* Output: "FOOD\tBULLETS\tCLOTHING\tMISC. SUPP.\tCASH"
* Output: values for the above


### `FUNCTION calculate_mileage(game_state: BYREF MUTABLE GameState)`
Calculates how far the player has traveled in 2 weeks.
* Uses the following equation:
   * Miles = Miles + 200 + (OxenAmount - 200)/3 + random between 1..10


