# `Events`

## `events.rs`
Handles the Event Checking Logic. Declares the sub mods checks, weather, wagon, party, combat.

## checks.rs

### `FUNCTION check_for_riders(game_state: BYREF MUTABLE GameState)`
* Runs the checks to see if riders are spotted:
    * num = a random number between 1 and 10
    * a = (miles_traveled / 100 - 4)^2
    * b = (a + 72) / (a * 12)
    * c = b - 1
    * Riders spotted if num <= c
* Runs a check to see if they _look_ hostile: random number between 0 and 1 < 0.8
* Sets a flag, true for looks hostile, false for looks friendly
* Output:
> TACTICS
> () RUN (2) ATTACK (3) CONTINUE (4) CIRCLE WAGONS

* After the output, determine if the riderss are actually hostile:
    * generate random number between 0 and 1, > 0.2 then flag = !flag to flip it
* Take user input and resolve based on their choice.

### `FUNCTION check_for_mountains(game_state: BYREF MUTABLE GameState) `
* Runs the checks to see if the player has reached the mountain ranges. There are two that they can encounter, the South Pass and the Blue Mountains. This event can only happen once the player has passed 950 miles.
* Once the player has reached 950 miles, the chance for the event to occur is calculated as follows:
    * num = a random number between 1 and 10
    * a = (miles_traveled / 100 - 15)^2
    * b = (a + 72) / (a + 12)
    * c = 9 - b
    * If num <= c, then the player has reached the mountain ranges.

## combat.rs

### `FUNCTION bandits_attack(game_state: BYREF MUTABLE GameState) RETURNS Option<CauseOfDeath>`

### `FUNCTION wild_animal_attack(game_state: BYREF MUTABLE GameState) RETURNS Option<CauseOfDeath>`

## mountains.rs

### `

## party.rs

## riders.rs

Handles the outcomes of the player's choice and the riders' hostility.

### `FUNCTION hostile_riders(game_state: BYREF MUTABLE GameState, choice: INT) RETURNS Option<CauseOfDeath>`
* Match with the user choice:
    * 1
        * Gain 20 miles on miles_traveled
        * Lose 15 misc supplies
        * Lose 150 bullets
        * Lose 40 oxen value
    * 2
        * Call the shooting subroutine
        * Lose bullets = bullets - time_taken * 40 - 80
        * Print the message depending on the shooting result:
            * time_taken < 1 -> "NICE SHOOTING---YOU DROVE THEM OFF"
            * time_taken <= 4 -> "KINDA SLOW WITH YOUR COLT .45"
            * else -> "LOUSY SHOT---YOU GOT KNIFED"
                * set injured flag
                * output "YOU HAVE TO SEE OL' DOC BLANCHARD"
    * 3
        * Check if they attack -> random number between 0 and 1 <= 0.8
            * Lose 150 bullets
            * Lose 15 misc supplies
        * Else:
            > THEY DID NOT ATTACK
            * Return
    * 4
        * Call the shooting subroutine
        * Lose bullets = bullets - time_taken * 30 - 80
        * Lose 25 miles
* Final Result:
    * "RIDERS WERE HOSTILE--CHECK FOR LOSSES"
    * If bullets < 0, then:
    * "YOU RAN OUT OF BULLETS AND GOT MASSACRED BY THE RIDERS"
    * Set is_game_over to true

### `FUNCTION friendly_riders(game_state: BYREF MUTABLE GameState, choice: INT)`
* Match with the user choice:
    * 1
        * Gain 15 miles
        * Lose 10 oxen value
    * 2
        * Lose 5 miles
        * Lose 100 bullets
    * 3
        * Nothing
    * 4
        * Lose 20 miles
    * Final Result:
        * "RIDERS WERE FRIENDLY, BUT CHECK FOR POSSIBLE LOSSES"


## wagon.rs

## weather.rs