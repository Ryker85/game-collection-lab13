# Hand trace of the blinker

Generation 0 live cells: (4,10), (5,10), (6,10), a vertical line.
Patch shown: rows 3 to 7 (top to bottom), columns 8 to 12 (left to right).
`#` = alive, `.` = dead. A neighbor beyond the grid edge counts as dead (not
relevant here, the patch is in the middle).

## Generation 0

Cells:

```
        c8 c9 c10 c11 c12
row 3:   .  .  .   .   .
row 4:   .  .  #   .   .
row 5:   .  .  #   .   .
row 6:   .  .  #   .   .
row 7:   .  .  .   .   .
```

Neighbor counts (the cell itself is not counted):

```
        c8 c9 c10 c11 c12
row 3:   0  1  1   1   0
row 4:   0  2  1   2   0
row 5:   0  3  2   3   0
row 6:   0  2  1   2   0
row 7:   0  1  1   1   0
```

Apply the rules to every square:

- (4,10) alive, 1 neighbor -> dies
- (5,10) alive, 2 neighbors -> survives
- (6,10) alive, 1 neighbor -> dies
- (5,9) dead, 3 neighbors -> born
- (5,11) dead, 3 neighbors -> born
- every other square: dead with 0, 1 or 2 neighbors -> stays dead

## Generation 1 (a horizontal line)

Cells: (5,9), (5,10), (5,11)

```
        c8 c9 c10 c11 c12
row 3:   .  .  .   .   .
row 4:   .  .  .   .   .
row 5:   .  #  #   #   .
row 6:   .  .  .   .   .
row 7:   .  .  .   .   .
```

Neighbor counts:

```
        c8 c9 c10 c11 c12
row 3:   0  0  0   0   0
row 4:   1  2  3   2   1
row 5:   1  1  2   1   1
row 6:   1  2  3   2   1
row 7:   0  0  0   0   0
```

Apply the rules to every square:

- (5,9) alive, 1 neighbor -> dies
- (5,10) alive, 2 neighbors -> survives
- (5,11) alive, 1 neighbor -> dies
- (4,10) dead, 3 neighbors -> born
- (6,10) dead, 3 neighbors -> born
- every other square stays dead

## Generation 2 (back to a vertical line)

Cells: (4,10), (5,10), (6,10)

```
        c8 c9 c10 c11 c12
row 3:   .  .  .   .   .
row 4:   .  .  #   .   .
row 5:   .  .  #   .   .
row 6:   .  .  #   .   .
row 7:   .  .  .   .   .
```

Generation 2 equals generation 0, so the blinker has period 2. This is what
the test `blinker_returns_after_two` checks.

