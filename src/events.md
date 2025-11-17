# `Events`

## `events.rs`
Handles the Event Checking Logic. Declares the sub mods checks, weather, wagon, party, combat.

## checks.rs

### `FUNCTION check_for_riders(game_state: BYREF MUTABLE GameState)`
* Runs the checks to see if riders are spotted:
    * num = a random number between 1 and 10
    * a = (miles_traveled / 100 - 4)^2
    * b = (a + 72) / (a + 12)
    * c = b - 1
    * Riders spotted if num <= c
* Runs a check to see if they _look_ hostile: random number between 1 and 10 < 8
* Sets a flag, true for looks hostile, false for looks friendly
* Output:
> TACTICS
>
> (1) RUN (2) ATTACK (3) CONTINUE (4) CIRCLE WAGONS

* After the output, determine if the riderss are actually hostile:
    * generate random number between 1 and 10 > 2 then flag = !flag to flip it
* Take user input
* If flag is true (hostile):
    * Call hostile_riders function
* Else:
    * Call friendly riders function

### `FUNCTION check_for_event(game_state: BYREF MUTABLE GameState)`
This function is the main entry point for all the random events. It will generate a random number between 1 and 100 and choose a random event based on the number generated.
* Call the get_random_int function with min=1 and max=100.
* Call the appropriate function based on the random number generated:

|Number Range|Event|
|---|---|
|1-3|bandits|
|4-13|wild_animals|
|14-15|wagon_fire|
|16-21|wagon_breakdown|
|22-31|wagon_swamped|
|32-41|weather_event|
|42-46|hail|
|47-51|fog|
|52-53|broken_arm|
|54-55|wandering_ox|
|56-57|lost_son|
|58-59|snake_bite|
|60-64|ox_injury|
|65-69|unsafe_water|
|70-75|helpful_natives|
|76-100|illness_chance|

* Based on event, either return None, or return the result of the event (Either None or Some(CauseOfDeath))

## combat.rs

### `FUNCTION bandits(game_state: BYREF MUTABLE GameState)`
> BANDITS ATTACK
* Call the shooting subroutine
* Lose ammo = ammo - 20 * time_taken
* If time_taken <= 1 and ammo >= 0:
    > QUICKEST DRAW OUTSIDE OF DODGE CITY!!!
    > YOU GOT 'EM!
* Else:
    * If ammo < 0:
        * Set money = money / 3
        > YOU RAN OUT OF BULLETS---THEY GET LOTS OF CASH
    > YOU GOT SHOT IN THE LEG AND THEY TOOK ONE OF YOUR OXEN
    * Set injured flag
    * Set miscellaneous supplies = miscellaneous supplies - 5
    * Set oxen = oxen - 20
    > BETTER HAVE A DOC LOOK AT YOUR WOUND

### `FUNCTION wild_animals(game_state: BYREF MUTABLE GameState) -> Option<CauseOfDeath>`
> WILD ANIMALS ATTACK!
* Call the shooting subroutine
* If ammo <= 39:
    > YOU WERE TOO LOW ON BULLETS--
    > THE WOLVES OVERPOWERED YOU
    * Set cause_of_death to CauseOfDeath::Injury
    * Return Some(cause_of_death)
* If time_taken <= 2
    > NICE SHOOTIN' PARDNER---THEY DIDN'T GET MUCH
* Else:
    > SLOW ON THE DRAW---THEY GOT AT YOUR FOOD AND CLOTHES
* Set ammo = ammo - 20 * time_taken
* Set clothes = clothes - time_taken * 4
* Set food = food - time_taken * 8
* Return None

## wagon.rs

### `FUNCTION wagon_fire(game_state: BYREF MUTABLE GameState)`
> THERE WAS A FIRE IN YOUR WAGON---FOOD AND SUPPLIES DAMAGE!
* Set food = food - 40
* Set ammo = ammo - 400
* Set misc = misc - 3 - random(1..8)
* Set miles_traveled = miles_traveled - 15

### `FUNCTION wagon_breakdown(game_state: BYREF MUTABLE GameState)`
> WAGON BREAKS DOWN--LOSE TIME AND SUPPLIES FIXING IT
* Set miles_traveled = miles_traveled - 15 - random(1..5)
* Lose 8 misc supplies

### `FUNCTION wagon_swamped(game_state: BYREF MUTABLE GameState)`
> WAGON GETS SWAMPED FORDING RIVER--LOSE FOOD AND CLOTHES
* Set food = food - 30
* Set clothes = clothes - 20
* Set miles_traveled = miles_traveled - 20 - random(1..20)

## weather.rs

### `FUNCTION weather_event(game_state: BYREF MUTABLE GameState)`
* Check if miles_traveled > 950
    * True:
        > HEAVY RAINS---TIME AND SUPPLIES LOST
        * Set food = food - 10
        * Set ammo = ammo - 500
        * Set misc = misc - 15
        * Set miles_traveled = miles_traveled - 5 - random(1..10)
    * False:
        > COLD WEATHER---BRRRRRRR!--YOU
        * Check if clothes < 22 + random(1..4):
            > DON'T
            * Set insufficient clothes flag
        > HAVE ENOUGH CLOTHING TO KEEP YOU WARM
        * If insufficient clothes flag is set:
            * Call illness subroutine


### `FUNCTION hail(game_state: BYREF MUTABLE GameState)`
> HAIL STORM---SUPPLIES DAMAGED
* Set miles_traveled = miles_traveled - 5 - random(1..3)
* Set ammo = ammo - 200
* Set misc = misc - 4 - random(1..3)

### `FUNCTION fog(game_state: BYREF MUTABLE GameState)`
> LOSE YOUR WAY IN HEAVY FOG---TIME IS LOST
* Set miles_traveled = miles_traveled - 10 - random(1..5)

## party.rs

### `FUNCTION broken_arm(game_state: BYREF MUTABLE GameState)`
> BAD LUCK---YOUR DAUGHTER BROKE HER ARM
> YOU HAD TO STOP AND USE SUPPLIES TO MAKE A SLING
* Set miles_traveled = miles_traveled - 5 - random(1..4)
* Set misc = misc - 2 - random(1..3)

### `FUNCTION wandering_ox(game_state: BYREF MUTABLE GameState)`
> OX WANDERS OFF---SPEND TIME LOOKING FOR IT
* Set miles_traveled = miles_traveled - 17

### `FUNCTION lost_son(game_state: BYREF MUTABLE GameState)`
> YOUR SON GETS LOST---SPEND HALF THE DAY LOOKING FOR HIM
* Set miles_traveled = miles_traveled - 10

### `FUNCTION snake_bite(game_state: BYREF MUTABLE GameState)`
> YOU KILLED A POISONOUS SNAKE AFTER IT BIT YOU
* Set ammo = ammo - 10
* Set misc = misc - 5
* If misc < 0:
    > YOU DIE OF SNAKEBITE SINCE YOU HAVE NO MEDICINE
    * Return Some(CauseOfDeath::Other)
* Return None

### `FUNCTION ox_injury(game_state: BYREF MUTABLE GameState)`
> OX INJURES LEG---SLOWS YOU DOWN REST OF TRIP
* Set miles_traveled = miles_traveled - 25
* Set oxen = oxen - 20

### `FUNCTION unsafe_water(game_state: BYREF MUTABLE GameState)`
> UNSAFE WATER--LOSE TIME LOOKING FOR CLEAN SPRING
* Set miles_traveled = miles_traveled - 2 - random(1..10)

### `FUNCTION helpful_natives(game_state: BYREF MUTABLE GameState)`
> HELPFUL NATIVES SHOW YOU WHERE TO FIND MORE FOOD
* Set food = food + 14

### `FUNCTION illness_chance(game_state: BYREF MUTABLE GameState)`
* Match on ration level:
    * Poor:
        * Call illness subroutine
    * Moderate:
        * If random(0..1) > .25:
            * Call illness subroutine
    * Well:
        * If random(0..1) < .5:
            * Call illness subroutine

## mountains.rs

### `FUNCTION mountain_encounter_check(game_state: BYREF MUTABLE GameState) RETURNS Option<CauseOfDeath>`
Checks if the player has gotten to 950 miles, returns if less than 950 miles. If over 950 miles then it runs a check to see if the player encounters the rugged mountains, South Pass, or Blue Mountains.
* If mileage >= 950 miles:
    * Check if random number between 1..10 <= 9 - ((Mileage/100 - 15)^2 + 72) / ((Mileage / 100 - 15)^2 + 12)
        * True: Call rugged mountains event
        * False: if Flag::has_cleared_south_pass
            * True: If Mileage > 1700 and not Flag::has_cleared_blue_mtn
                * True: Call blue mountains event
            * False: Set the Flag::has_cleared_south_pass
                * Check random number between 1 and 10 < 8
                    * True:
                        * Call blizzard event
                    * False:
                        > YOU MADE IT SAFELY THROUGH SOUTH PASS--NO SNOW

### `FUNCTION rugged_mountains(game_state: BYREF MUTABLE GameState) RETURNS Option<CauseOfDeath>`
> RUGGED MOUNTAINS
* Check random number between 1 and 100 < 10
    * True:
        > YOU GOT LOST---LOSE VALUABLE TIME TRYING TO FIND TRAIL!
        * Set miles = miles - 60
    * False:
        * Check random number between 1 and 100 < 11
            * True:
                > WAGON DAMAGED!---LOSE TIME AND SUPPLIES
                * Set misc = misc - 5
                * Set bullets = bullets - 200
                * Set miles - miles -20 - random between 1..30
            * False:
                > THE GOING GETS SLOW
                * Set miles = miles - 45 - random number between 1 and 100 / 2
    * Flag for clearing south pass if not already set to true.

### `FUNCTION blue_mountains(game_state: BYREF MUTABLE GameState) RETURNS Option<CauseOfDeath>`
* Set Flag::has_cleared_blue_mtn
* Check random number between 1 and 10 < .7
   * True:
        * Call blizzard function


### `FUNCTION blizzard(game_state: BYREF MUTABLE GameState) RETURNS Option<CauseOfDeath>`
> BLIZZARD IN MOUNTAIN PASS--TIME AND SUPPLIES LOST
* Set flag for blizzard
* Set food = food - 25
* Set Misc = Misc - 10
* Set Bullets = Bullets - 300
* Miles = Miles - 30 - random between 1..40
* If clothing < 18 + random 1..2
    * Illness Check


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
            * time_taken < 1
                > NICE SHOOTING---YOU DROVE THEM OFF
            * time_taken <= 4
                > KINDA SLOW WITH YOUR COLT .45
            * else ->
                > LOUSY SHOT---YOU GOT KNIFED
                * set injured flag
                > YOU HAVE TO SEE OL' DOC BLANCHARD
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
    > RIDERS WERE HOSTILE--CHECK FOR LOSSES
    * If bullets < 0, then:
        > YOU RAN OUT OF BULLETS AND GOT MASSACRED BY THE RIDERS
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
        > RIDERS WERE FRIENDLY, BUT CHECK FOR POSSIBLE LOSSES

