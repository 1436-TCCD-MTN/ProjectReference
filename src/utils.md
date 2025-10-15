# Utils
Helper functions for use in the game

## utils.rs

### `FUNCTION get_int_input(min: INTEGER, max: INTEGER, prompt: BYREF STRING) RETURNS INTEGER`
* Prints the provided prompt, then accepts user input
* Validates that the input is within the range, displays error message if not and loops to provide the prompt and accept input again.
* Returns input

### `FUNCTION get_yes_no(prompt: BYREF STRING) RETURNS BOOL`
* Prints the provided prompt, then accepts user input
* Validates that the user entered either `y` or `n`.
* Loops until user has entered valid input.
* Returns true for `y` or false for `n`

### `FUNCTION get_random_int(min: INTEGER, max: INTEGER) RETURNS INTEGER`
* Returns a random number that is between min and max inclusive.

### `FUNCTION wait(ms: INTEGER)`
* Pauses the program for the specified amount of time.