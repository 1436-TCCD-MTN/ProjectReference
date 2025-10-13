// --- Main Game Loop ---
// game_loop.rs

// Contains the primary loop for the game. Starts with calling the
// Game init function to initialize the game, then starts a loop. On each
// loop, calls the turn progression, calls the date handling functions
// calls the random event checks, and checks for win or loss conditions
FUNCTION game_loop(game_state: BYREF MUTABLE GameState)