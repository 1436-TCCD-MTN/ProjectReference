// --- Helper Functions ---
// utils.rs

// Get a valid integer input from the user within a given range
// Should keep looping until a valid input is provided.
FUNCTION get_int_input(min: INTEGER, max: INTEGER, prompt: BYREF STRING) RETURNS INTEGER

// Get a yes/no (Y/N) response from the user
// Loop until provides a correct response
FUNCTION get_yes_no(prompt: BYREF STRING) RETURNS BOOL

// Generate a random integer within the provided range
FUNCTION get_random_int(min: INTEGER, max: INTEGER) RETURNS INTEGER

// Pause the program for a specified amount of time
FUNCTION wait(ms: INTEGER)