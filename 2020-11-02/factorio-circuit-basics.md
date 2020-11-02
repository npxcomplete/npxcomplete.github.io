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
0eNqVUttqwzAM/Rc9O6Mpvc3sbZ8xSnBsdRNz7OBLWSj+98nxGIXB2F4MR9I5OpJ8g9FmnAO5BPIGpL2LIF9uEOnVKVtjaZkRJFDCCQQ4NVVkUJPB0Gk/jeRU8gGKAHIGP0D25SwAXaJE2NRWsAwuTyMGLvhNR8DsI1O9q92r3EbAArLbnx723MRQQN3SWwFsOAVvhxHf1JWYzpwv0YFzZhWKNXqhENPwY64rhZQ58m2pVXTPdaC6jqTqbvoKplmF1aOEJyb4nOb8f8l5YWfZpeES/DSQYw2QF2UjltbStflW1319Apr7NZJpfijoTGmF23Jm7vZvxXyfUuqN1pvKuy8gwKoReRaw/pV0p63X7xy9Yoht46d+d9w9Hg/HfnPYH0r5BBcfxE4=
```
This clock outputs zero or one, alternating every tick. It will form the basis of any complex circuit brain.

_________________

counter:
```
0eNqVkdFqhTAMht8lt6tjylHPvN1jjINUzXYC2kqbyg7Sd19aYTuwi203hTT5/3xJdhjmgKsjw9DtQKM1HrrXHTy9Gz2nP76tCB0Q4wIKjF5SpB3xdUGmsRjtMpDRbB1EBWQm/ICujBcFaJiY8DDMwa03YRnQScEvVgpW60VtTWJIjicFN+iK+vxYS5+JHI5HulIg2Ozs3A941RuJXDTfvr2kp+zlU+KNnOf+x4AbOQ7y8wV2VBQvaSyPySMZedZpV8JvV3T6QIAHkdnAa/ifcYyZ3RyjZLoyPQ6n+6XRlBuO5MZAnMMqXkRb/a1YriGt5CL5iN3dzRXMekChFYxgGNPiN3T+WOy5PLWn57Zpy6embmL8BKVPveI=
```
count till register rollover then reset.

_________________

rs-latch:
```
0eNrNVl1rrDAQ/S/znC2r68c2XC70vU8tfboUiZptBzRKjEuXxf9+E9Na8aOoLNz7IiSTmcmcc8bJFeKs5qVEoYBeAZNCVED/XKHCN8Eys6cuJQcKqHgOBATLzSrlCaZc7pIij1EwVUhoCKBI+QdQp3klwIVChdxGaxeXSNR5zKU+0MUx+RQTqh+IQFlU2rcQJr2OF9z5BC5Ad/7xztdpUpQ8sXaPmBBKFlkU83d2Ru2vnU6YKS5nKjmjVLXe6S5hT+xeTAlJURsown2/mnZfCJu0MqEc85E87VeHqb0PyqRG1S6Nb9OQEQDuOgC8DoBwCEBwQwAeegAcNwJwGAFA4E1yLjYidfhJciOgjp8wBUOY3GmYPmNG2pZiV9sJZaWidbBV3MRY7vRosc5LJttSKPzWZ4palfWK1E82SnmJWtqikyzyCIWOAfTEsoo3y5lzZ6kKWwG4xm/S7i+j0ttEZfjfU/kyovLXBiqfb0jlfNe5t6HSX0Wls/8Xbfm8hcunm7TlZi4nORn8Ut0eHxM/0qHZH5o7AUwIJ5gVzkJhBN9Q5CzLdhnLywlBuN1As5KYEsFXuk4EWzXwNWKB7kfcrmiqCSCnEAi3vm38WSQ2DfPH3jA/LBnmS7RnadcaaV+DtPd4JJCxmOuLgaw06yp511tnfWvb50fHC737MAidfeAHTfMXefGSSA==
```
An RS-Latch is comprised of a set and a reset condition, and a memory cell.
Take in a signal A. If A < L, set S = 1. If A > U, set S = 0; Output S.

_________________

rate-limitter:
```
0eNrFVs2OmzAQfpc5tlAB4WfDodIee9pbL9UKGZjsWrINMiZqFPEAfYs+W5+kAzSEbEIWoo16QRp7/Pmbbz5j7yEVNZaaKwPxHnhWqAriH3uo+Itioh0zuxIhBm5QggWKyTZimptXiYZndlbIlCtmCg2NBVzl+BNit3m2AJXhhmMP2AW7RNUyRU0JA1SOGc9Rj3EsKIuKlhaqJUBw0ZfAgh3EdujQHkTS6EIkKb6yLad8SvqHktBc3q2s2tEN15VJzmrZcm1qGhk49Bn2d+jRK8NaPZw2kCXTHakYvtKCojZlvQDysYcsd8SsVibZ6EImXBEGxBsmKmz6LRVmA2u3/WjMx7pxijzK5DqruenDxjqZ9t9OPxO0N4G1otlmBHDoi/dOi89as363NUegD+hOhS1GcmySTU4qSqQedZzg0w1NIuQFbQiW6OyeJrsTsq+OlCQTwhZMludaBwetA1J9Qu3DboPUNyj9eP0c/Pn1Gxbo5Z7rdUkCf6nzhp9C8HBn53276Dzn1Hif72688COcFtx8wO8u89N/kPlFI6q3UkZXhfbmCR0OLA61zHRzMHm2N1wY1BMX9FXzdpcPcXXGN/R85/nzSo6Wlby+V8lPo5JXc0q+6ILgUtH0rOleQvHo4WSBYCkSMSCXoi24pJS23i0x78r1Hlw/8tdRGLlOGIRN8xeskz5o
```
Given an input signal `I`, an output signal `O`, and a limit signal `L`, Output active `A` if and only if `O - I < L`.

_________________

pulsar:
```
0eNq1VF1vqzAM/S9+nGAqrC0bD1e6v+NqigK4q6V8oCRUqyr++xxYW9TRbd10XxCOnWP7HMcHqFSHrSMToDwA1dZ4KP8dwNOLkSqehX2LUAIF1JCAkTpa0lHYagxUp7XVFRkZrIM+ATINvkKZ9cmXGA3W1KCbB8j75wTQBAqEY0WDsRem0xU6znDCaTu/rboQrGHs1nq+wr+clWGK+1UCeyjT1eP9itEbcliP/jwB7jY4q0SFW7kjzs+XNqQCuisk7MiFjk9OuceI9G+svLZdZDGbkMA9kBcx20Yqj0OQMWMFPuJm8eOwmXZIzVgcubqjMJgDnRP38tL93PeTkCNH+Wdcf+AqW9xI1TuoYF9Dp5Y25HwQt1JnfJCRvUU0dCvdUGMJf/iC7ULb3Q7Z7sUgidg4qwUZxjjq8H0hBg1fHKK59FxowAPLqHmEmQ1/uKLRw7l6LZVKldTtjDb5xSDP6XEs56TH/5DjGnezTecfOZrjYPnFXrk+qsU3R/WM+7tpRVlvI0MeI4w4E5Xys7ctMk9DGXD3g7kdwW8bzk9nLp9bE3EnxT1cTlZ/AkpWqIZlyu+D7R3vwJHQx2xZLJ+KdZEt1qt1378BVrsdGw==
```
Send out a signal only when the input signal changes.

_________________

counter-to-N:
```
```
Count to the input value N, then reset to zero.

_________________

slow-counter-to-N:
```
```
Count to N and reset to 0. Slow the count to rate `R` per ticks `T`.
Note there are approximately 1_000 ticks per second.
