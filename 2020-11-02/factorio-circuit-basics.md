Compressing a 30 min video into a 3 min blog post.

Requires mods:
  * Pushbutton


Factorio Circuit Network - Basics
==================================

Information in a circuit network is not exactly like programming but it has a lot of common characteristics. 
The most important difference is that the circuit network is very sensitive to latency. 
Information takes time to travel and you have to account for that when building your logic.

Vanilla Blueprint Book:
```
```

Push Button Book:
```
```


### The short version ###

logic-clock:
```
```
This clock outputs zero or one, alternating every tick. It will form the basis of any complex circuit brain.

counter:
```
```
count till register rollover then reset.

slow-counter-to-N:
```
```
Count to N and reset to 0. Slow the count to rate `R` per ticks `T`.
Note there are approximately 1_000 ticks per second.

counter-to-N:
```
```
Count to the input value N, then reset to zero.

rs-latch:
```
```
An RS-Latch is comprised of a set and a reset condition, and a memory cell.
Take in a signal A. If A < L, set S = 1. If A > U, set S = 0; Output S.

rate-limitter:
```
```
Given an input signal `I`, an output signal `O`, and a limit signal `L`, Output active `A` if and only if `O - I < L`.

pulsar:
```
```
For boundary conditions upper `U` and lower `L`: 
If input `A` rises above `U` output `1` for a single tick. 
If input `A` falls below `L`, output `0` for a single tick.
