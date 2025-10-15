# Data Structures

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

### GameState

```
STRUCT GameState {
    total_miles: INTEGER,
    miles_traveled: INTEGER,
    turn: INTEGER,
    date: STRING,
    rations: RationAmount,
    is_sick: BOOLEAN,
    is_injured: BOOLEAN,
    inventory: Inventory,
    difficulty: INTEGER
}
```

Primary game state structure holding all relevant game information.

## inventory.rs

### RationAmount

```
ENUM RationAmount {
    Poor,
    Moderate,
    Well
}
```

Used to flag how well the player ate on the current team.

### Inventory

```
STRUCT Inventory {
    oxen: INTEGER,
    food: INTEGER,
    bullets: INTEGER,
    clothing: INTEGER,
    money: INTEGER,
    misc: INTEGER
}
```

Holds all the player inventory details.