Mods:
* Recursive Blueprints
* Ghost Scanner

The first blueprint provides constants, initial state, and clock tick.
```
0eNrdmd1umzAYhu/F0k426GLzl6BpJ+3B7mCbpgoRcBJLYJAx1aKKC9h97Mp2JbOhTQg1xKZpV60Hlfjxa/t9/H3+cO7BOqtxyQjlILwHJCloBcIf96AiWxpn8h7flxiEgHCcAwvQOJdXMSN8l2NOEjsp8jWhMS8YaCxAaIp/ghA21lmNFCckxUwtgDQE5GB5TLlawdFQ2O6KittVElOK+23d5tYCmHLCCe78aC/2Ea3ztXgzhJODsEBZVKJtQWXPQs923SvPAnvRMLjyRD8pYTjpXkCW1OCsyKI13sV3RAiIVhuSccxGYNwRxmtx5zCK7g37Ws4hKWpJE/Zg3La3xSTbPiupBOW/LcOY9udHUjF58S5hSU14eylbN9LLgQVoxEXF5NHo5N1LTP6kfzvBWWZ3HpiZwXA6tMJ/YoWl9szT88w5E0AK7x6cW2kum6NuJB6n5DDFDWEVj7RXEo6TnfSvwlImelzlrZNFiVncjQJ8EC2Lmpe1sXbzjDWJWohIfwlbJ4+XerTcqVQ1jmo5ROWrUT2IXobTEZC/EH/yRl7GrB1qCD7NpiSFyn3UhlG0YUUeESpkQMhZjY0QDiE4ZkgdPWaeeYQhM2zPjrCpdPUk3OxBvL03ITnekxG5HhqtHKkE488G82ZS3+KlU5/CXW8YJZYBGrjQYxPM3ZYQfCts0Cmbd6+zLS3NcthKD8dyNo7Fa+Wwczj8Qax8fB0ehntKoMdjZVgHPJa7CGkVuxepA657GLQbwW5/7xUKn+dwusNsz3eEbi9ZLgTTiQ+605kP6Vbu0BuhLpOnGXazGLxM+TfwvrdVnXD98+v3DLI3E0A3cVbhZvanFDLFp2YEzVPlwiw6L5Uqby5f3h2VzQpxZIRCs/CGyDBcYJ/DiwXIzXRc/JN8p3B5dSbbLcw2NhkXUx/A2lDNDyyc1Tmu/2WdPnQcjW84ivBTeu/OPWNEzkueMX4ZOVazDDS+KjWQkYY8uFbKOLpHx6xu7bFZsS7Uh4W+0Yi+KTUCI43vSo2lyaGlrGisZ32AwOMpSpXHWWZncV5O5nC3XXGqNfbY3yHU5xa3U0lcPK4rLPrICrmc2+Sr75er61cXquLldjGFvd9OLJDFa5x1K0t6IO6IbaLqom8J3cBdBX4AF77nN81fzjW5ew==
```

This can be read as:
```
// D for Done construction
D := (NUM_GHOSTS == 0) ? 1 : 0;

// Clock tick ~ once per second
C := (nanotime % 1_000_000) ? 1 : 0;

if(clock_tick && done)
  then CLEAR(D) and OUTPUT(constants)
```


Next we'll need a global step counter. Later we'll use the global counter to produce individual counters by inverting the equations used to index multidimensional arrays. A quick aside for the novice programmers:

An array is analogous to a vector in linear algebra, similarly a multidimensional array is analogous to a matrix. A 2D matrix maps nicely to memory cells on a euclidean grid. So for a 3x4 matrix `M` we can store and retreive values at `M[0][0]` up to `M[2][3]`. Computer memory is one giant array of machine words. In order for the computer to understand where `M[2][1]` is it has to translate that two dimensional address into a one dimensional address. So for `M[x][y]` the calcualtion looks like:

```
addr = start_of_M + (x * D_1) + y
```

where `D_1` was 4 in our origional example. Typically we'd iterate over a matrix using nested for loops like so:

```
D_1 = 4
D_2 = 3

int M[D_2][D_1] 

for(int i=0; i<D_2; i++){
  for(int j=0; j<D_1; j++){
    doStuff(M[i][j])
  }
}
```

By inverting the above logic we take a global step counter and derive the indexes within each dimension. Thus we only need one for loop:

```
D_1 = 4
D_2 = 3

int M[D_2][D_1] 

for(int k=0; k<D_1 * D_2; k++){
  // take the remainer after division
  int j = k % D_2
  // Integer division drops the remainder (flooring / rounding down)
  int i = k / D_2
  doStuff(M[i][j])
}
```

To get a better feel of the pattern lets look at the same calculation on a 4D matrix

```
int D_1 = 4
int D_2 = 3
int D_3 = 7
int D_4 = 9

int M[D_4][D_3][D_2][D_1] 

for(int k=0; k<(D_1 * D_2 * D_3 * D_4); k++){
  int i_1 = k                     % (D_4 * D_3 * D_2)
  int i_2 = k / (D_1)             % (D_4 * D_3)
  int i_3 = k / (D_1 * D_2)       % (D_4)
  int i_4 = k / (D_1 * D_2 * D_3) 
  doStuff(M[i_4][i_3][i_2][i_1])
}
```

The clock flip flops once per second. In the next print we recurjigger the clock to turn on for only one tick per second and add an incrementing memory cell:
```
0eNrtWktu2zAQvQuBblopEClZkoU2m2TjbbMsAkOWmZiAPgZFBTUCH6D36Ml6kpJyYjuyZHFoOUk/WQSwPkNyHt/MmxEf0Syt6JKzXKDoEbGkyEsUfXtEJbvP41RdE6slRRFigmbIQnmcqV9zmrA55XZSZDOWx6LgaG0hls/pdxThtdVrIOZMLDIqWNJug6xvLURzwQSjmxnVP1bTvMpmlMtBtqbUnEWci31DFloWpXy3yNUMpD3bcy9GFlrJF4OLkRxnzjhNNg8QS9kQvEinM7qIH5g0IN+6Y6mgvMMdD4yLSl7ZzmLzhH2l1pAUlfIn3vPIbX05zzdjlsoSVv/uOaX5/vrYHEWefJbxpGKi/qneXiufNlxAtoPfL4pS2GUSywFaF487F+8NsfgX49sJTVN744OdM4iGMzidN10xOnCF1e4zX89nbs8ObPGdt/HcWHPb7OxO5e052y7xjvFSTLV3Eo2ThfJfSZWZ6fMuR5FjoWJJebyZBfok3ywqsazAttcn7ElSg0j0t7D14jZ29ODyjkWcbqzCJlZ+O1ZPRocBaoeQ78g/dSFbxryeaoQ+G8OkDC1X05pH0zteZFOWSzMoEryiIAzdJoYNUHowdfUwG8Ephv81irVEuiYafifhWl7GRA8b3xgbXUqdjM2xXHIAlI1fIvURglT3SCBWHUdmpAdMAAt0rg9jzCCB7upllGtGuC8GLPl6JLzdxWkJi28YmKRCPWxCIDbeG2Bzs0cPqPf3MLw0wPDGFMMWtoQHAHbIvaAnlQWQ6Bnqikw81tsxYyPZQvAfzuarYdnswNiMNfWJsmtWAxDntZLgvkMPkp7fkCcfzKA6TToex0KTJxgDieI81bGErM9Ijevj1DAJkvSB8pVYsPzeUNBriL6DIAgEDfcVbZpaBhMgqhjGrmGqtgYgXWD/+vHTAO7rAXPiCFQIYE2MXChG+8zr7x8Nl6KgogYPImpO5qtOWGwSlmAoth06hXhdsHvg3OeGfTH3ryzH8UhXijZh6QuzQU+UDTQZDO+zuGMYiYcC9nr42n1nGaYpMSiYajbisW9UvR/q/XMmvMm7r95DGI+Irt43660cypFXrMbwAOjc/Am9FRzCo5gHY89QUWzSGsXI6bXYBJaYxkBV7x/PN0SzdYzHxkg5b4gUjC6nyowJNB/1KMIQlK4G72MReKvEJa8lF41anpMzo9z2YcfpUf0uBGSi+eWUGB+QIO45D0io8yatZyRcjVMj9Up4VU/L5sWsEK2mfMgJA1UrWad1FAkxUxjkDfXfO1QYZ9J/xDX6fnOIzv/vN/1kcrWrZr8nKhJQVHR7RI5u1Nz1R8osTlM7jbPl0Ua0V++Stn3xPN52Xwz/keZS3a5KKsdICxWJ646UPlpYO/SR2mHy6TogR3vHBi30IJPAhiAh9gJvHPgBdvyRv17/Bvbl2A8=
```


We'll use the two dimensional to operate over a grid space. The goal will be a self expanding perimiter that cleans up after two levels.
The procedure to do this is to 

1. Build the outer ring.
2. Destroy the inner ring.
3. Increment ring position
4. Repeat.

Building the outer ring is a chore in itself. So let's start with a fixed ring made of 2 blueprints, a side and a corner. For simplicity we'll place corners first and then fill in the side. Let's cook up some variables:

```
H, W     // the height and width of a blueprint
X_0, Y_0 // the initial values denoting the top left corner
X, Y // the current position we want to place a blue print
M, N // the number of blueprints wide and high of our perimitter.

// Note that this implies that 

for (X=X_0, i=0; i<W; i++) {
  X_(i+1) = X + W
}
```







SR Latches: https://www.youtube.com/watch?v=Hi7rK0hZnfc



