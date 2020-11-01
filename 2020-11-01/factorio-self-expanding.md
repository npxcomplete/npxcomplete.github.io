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

