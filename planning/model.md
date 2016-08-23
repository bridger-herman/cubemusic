# Visualization of a Rubik's Cube in 2D using plaintext

```
// Colors
                   BBB | BBB | BBB
                   BBB | BBB | BBB
                   BBB | BBB | BBB
OOO | OOO | OOO || WWW | WWW | WWW || RRR | RRR | RRR || YYY | YYY | YYY
OOO | OOO | OOO || WWW | WWW | WWW || RRR | RRR | RRR || YYY | YYY | YYY
OOO | OOO | OOO || WWW | WWW | WWW || RRR | RRR | RRR || YYY | YYY | YYY
                   GGG | GGG | GGG
                   GGG | GGG | GGG
                   GGG | GGG | GGG

// Examples: Solved cube after U move
                   BBB | BBB | BBB
                   BBB | BBB | BBB
                   OOO | OOO | OOO
OOO | OOO | GGG || WWW | WWW | WWW || BBB | RRR | RRR || YYY | YYY | YYY
OOO | OOO | GGG || WWW | WWW | WWW || BBB | RRR | RRR || YYY | YYY | YYY
OOO | OOO | GGG || WWW | WWW | WWW || BBB | RRR | RRR || YYY | YYY | YYY
                   RRR | RRR | RRR
                   GGG | GGG | GGG
                   GGG | GGG | GGG

// Examples: Solved cube after R move
                   BBB | BBB | WWW
                   BBB | BBB | WWW
                   BBB | BBB | WWW
OOO | OOO | OOO || WWW | WWW | GGG || RRR | RRR | RRR || BBB | YYY | YYY
OOO | OOO | OOO || WWW | WWW | GGG || RRR | RRR | RRR || BBB | YYY | YYY
OOO | OOO | OOO || WWW | WWW | GGG || RRR | RRR | RRR || BBB | YYY | YYY
                   GGG | GGG | YYY
                   GGG | GGG | YYY
                   GGG | GGG | YYY


// Examples: Solved cube after E move
                   BBB | BBB | BBB
                   OOO | OOO | OOO
                   BBB | BBB | BBB
OOO | GGG | OOO || WWW | WWW | WWW || RRR | BBB | RRR || YYY | YYY | YYY
OOO | GGG | OOO || WWW | WWW | WWW || RRR | BBB | RRR || YYY | YYY | YYY
OOO | GGG | OOO || WWW | WWW | WWW || RRR | BBB | RRR || YYY | YYY | YYY
                   GGG | GGG | GGG
                   RRR | RRR | RRR
                   GGG | GGG | GGG

// Examples: Solved cube after L move
                   YYY | BBB | BBB
                   YYY | BBB | BBB
                   YYY | BBB | BBB
OOO | OOO | OOO || BBB | WWW | WWW || RRR | RRR | RRR || YYY | YYY | GGG
OOO | OOO | OOO || BBB | WWW | WWW || RRR | RRR | RRR || YYY | YYY | GGG
OOO | OOO | OOO || BBB | WWW | WWW || RRR | RRR | RRR || YYY | YYY | GGG
                   WWW | GGG | GGG
                   WWW | GGG | GGG
                   WWW | GGG | GGG

```

# Keeping track of positions
```
// Positional numbering?
                8B | 7B | 6B
                5B | 4B | 3B
                2B | 1B | 0B
6L | 3L | 0L || 0U | 1U | 2U || 2R | 5R | 8R || 8D | 7D | 6D
7L | 4L | 1L || 3U | 4U | 5U || 1R | 4R | 7R || 5D | 4D | 3D
8L | 5L | 2L || 6U | 7U | 8U || 0R | 3R | 6R || 2D | 1D | 0D
                0F | 1F | 2F
                3F | 4F | 5F
                6F | 7F | 8F

// Or positional naming? Yes. This.
                   BLD | BMD | BRD
                   BLE | BME | BRE
                   BLU | BMU | BRU
LDB | LEB | LUB || ULB | UMB | URB || RUB | REB | RDB || DRB | DMB | DLB
LDS | LES | LUS || ULS | UMS | URS || RUS | RES | RDS || DRS | DMS | DLS
LDF | LEF | LUF || ULF | UMF | URF || RUF | REF | RDF || DRF | DMF | DLF
                   FLU | FMU | FRU
                   FLE | FME | FRE
                   FLD | FMD | FRD
```

# Algorithms on the cube
## Methodology
When a move is selected, we'll look up what faces and are affected by such a
move. Then, the move will be applied by changing what colors are at each
position (loop iterating through `positions` in `Cube` class, all flagged
positions will be changed).

## Transitions
*U*
+ LU <- F U
+ F U <- RU
+ RU <- B U
+ B U <- LU

*R*
+ UR <- FR
+ FR <- DR
+ DR <- BR
+ BR <- UR

*E*
+ F E <- RE
+ RE <- B E
+ B E <- LE
+ LE <- F E

*L*
+ UL <- BL
+ BL <- DL
+ DL <- FL
+ FL <- UL
