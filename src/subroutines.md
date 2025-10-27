# Subroutines
Handles subroutines

## `subroutines.rs`

### `FUNCTION illness(game_state: BYREF GameState) RETURNS Option<CauseOfDeath>`

This subroutine determines how sever of an illness the player receives. The outcome is determined by how much food you ate on the previous turn. Eating well provides the best chance of staying healthy.
* Set E based on how well you have eaten
    * Poor => 1
    * Moderate => 2
    * Well => 3
* Generate random number between 1 and 100
* If num < 10 + 35 (E - 1)
    * You gain a mild illness
    * Lose 5 miles
    * Lose 2 misc supplies
    > MILD ILLNESS---MEDICINE USED
* Generate a new random number between 1 and 100
* If num < 100 - (40/(4^(E-1)))
    * Lose 5 miles
    * Lose 2 misc supplies
    > BAD ILLNESS---MEDICINE USED
* If both of the above checks are false, then the following happens:
    > SERIOUS ILLNESS---YOU MUST STOP FOR MEDICAL ATTENTION
    * Lose 10 miles
    * Set is_sick flag to true
* If misc < 0, then Return Some(CauseOfDeath::Disease)

### `FUNCTION shooting(game_state: BYREF GameState) RETURNS INTEGER`
* Displays a random word for the player to type in
* List:
    * BANG
    * BLAM
    * POW
    * WHAM
* Takes current time
* Accept user input
* Take current time
* Time Taken
    * If incorrect word, Time Taken = 9
    * Else: Time Taken = (Stop - Start) - (Difficulty - 1)
* Return Time Taken

### `FUNCTION shopping(item: STRING, game_state: BYREF GameState)`
This subroutine handles shopping for supplies at a fort.
* Creates a formatted string for the user prompt
  > ENTER WHAT YOU WISH TO SPEND ON THE FOLLOWING
  > {item}
* Calls the get_int_input function, passing in min 0 and max as 1000
* On the return, if the amount input is greater than the player's money, output:
    > YOU DON'T HAVE THAT MUCH--KEEP YOUR SPENDING DOWN
    > YOU MISS YOUR CHANCE TO SPEND ON THAT ITEM
* Else, deduct the amount spent from the player's total money and add the appropriate amount of supplies:
    * Ammo: amount_spent * 2/3 * 50
    * Everything else: amount_spent * 2/3