# Win and Lose Conditions

## `win_lose_conditions.rs`
Handles checking if the game is over, then displaying the victory or defeat messages.

### `FUNCTION has_won(game_state: BYREF GameState, cause: BYREF Option<CauseOfDeath>) -> Option<BOOLEAN>`
Checks if the game is over, either by victory or defeat. Returns True for victory, False for defeat, and None if the game is still ongoing.
* Match on the `cause` variable:
    * `Some(cause)` => Return `Some(false)`
    * None:
        * Check if the miles_traveled >= 2040 -> Return `Some(true)`
        * Else return `None`

### `FUNCTION display_game_over(cause: Option<CauseOfDeath>)`
Displays the correct game over message based on the cause of death.
* Match on the `cause` variable:
    * Starvation =>
        > YOU RAN OUT OF FOOD AND STARVED TO DEATH"
    * Disease =>
        > YOU RAN OUT OF MEDICAL SUPPLIES"
        > YOU DIED OF PNEUMONIA"
    * Injury =>
        > YOU RAN OUT OF MEDICAL SUPPLIES"
        > YOU DIED OF INJURIES"
    * Freezing =>
        > YOU HAVE BEEN ON THE TRAIL TOO LONG ------"
        > YOUR FAMILY DIES IN THE FIRST BLIZZARD OF WINTER"
    * NoMoney =>
        > YOU CAN'T AFFORD A DOCTOR"
* "DUE TO YOUR UNFORTUNATE SITUATION, THERE ARE A FEW"
* "FORMALITIES TO GO THROUGH"
* Output the following and accept user input, but don't act on the input:
    > \nWOULD YOU LIKE A MINISTER?"
    > WOULD YOU LIKE A FANCY FUNERAL?"
* "WOULD YOU LIKE US TO INFORM YOUR NEXT OF KIN?"
* Accept input, on No:
    > BUT YOUR AUNT SADIE IN ST. LOUIS IS REALLY WORRIED ABOUT YOU
* On Yes:
    > THAT WILL BE 50 FOR THE TELEGRAPH CHARGE.
> WE THANK YOU FOR THIS INFORMATION AND WE ARE SORRY YOU
> DIDN'T MAKE IT TO THE GREAT TERRITORY OF OREGON
> BETTER LUCK NEXT TIME\n\n
> SINCERELY\n
> THE OREGON CITY CHAMBER OF COMMERCE

### `FUNCTION display_win(game_state: BYREF GameState)`
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