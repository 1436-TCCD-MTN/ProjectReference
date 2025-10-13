# Status
// --- Game Status Checks ---
// status.rs -- Declares the sub mods date, display, travel

## `date.rs`

// Uses the turn number to iterate on the game date
### `FUNCTION set_date(game_state: BYREF MUTABLE GameState)`

// Prints the date formatted for the status display
### `FUNCTION print_date(game_state: BYREF GameState)`

## `display.rs`

### `FUNCTION display_status(game_state: BYREF GameState)`

## `travel.rs`

### `FUNCTION calculate_mileage(game_state: BYREF MUTABLE GameState)`