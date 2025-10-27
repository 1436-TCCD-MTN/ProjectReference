# Data Structures used in the game

## inventory.rs

## states.rs

### CauseOfDeath

```
ENUM CauseOfDeath {
    Starvation,
    Disease,
    Injury,
    Freezing,
    NoMoney,
    Other,
}
```

### Flags

```
STRUCT Flags {
    has_sufficient_clothing: bool,
    is_injured: bool,
    is_sick: bool,
    blizzard_happened: bool,
    has_cleared_south_pass: bool,
    has_cleared_blue_mtns: bool,
}
```

### GameState

#### Alpha Version

```
STRUCT GameState {
    total_miles: INTEGER,
    miles_traveled: INTEGER,
    turn: INTEGER,
    date: STRING,
    rations: RationAmount,
    is_sick: BOOLEAN,
    is_injured: BOOLEAN,
    cause_of_death: CauseOfDeath,
    inventory: Inventory,
    difficulty: INTEGER
}
```

#### Possible Refactors

```
STRUCT GameState {
    total_miles: INTEGER,
    miles_traveled: INTEGER,
    turn: INTEGER,
    date: STRING,
    rations: RationAmount,
    flags: Flags,
    cause_of_death: CauseOfDeath,
    inventory: Inventory,
    difficulty: INTEGER
}
```