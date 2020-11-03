
Compressing a 30 min video into a 3 min blog post.

Requires mods:
  * Pushbutton


Factorio Circuit Network - Medium Difficulty
============================================

Information in a circuit network is not exactly like programming but it has a lot of common characteristics. 
The most important difference is that the circuit network is very sensitive to latency. 
Information takes time to travel and you have to account for that when building your logic.

Blueprints:
```
```


### The short version ###

stable-max:
```
0eNrtWstu4jAU/RdvJ1Q4T4KqSu2+m3Yz0mgUhcQUS8SJHAcVVfmA+ZD5sfmSsQmlNEnJtWFoO+oGEbBvnHPu88ATmi0rUnDKBJo+IZrkrETTH0+opA8sXqrPxLogaIqoIBmyEIszdZWShKaEj5I8m1EWi5yj2kKUpeQRTXFtDRqIORWLjAia9Nuw658WIkxQQUlzos3FOmJVNiNc3mRnqqjKxawSImfSfJGXcot8K28szTjehWehNZqOfPvCk+ZTyknSLLAtJB9X8HwZzcgiXlF5ALlrTpeC8DdQWFEuKvnJ7ubNitF3dfQkrxSMeA8I+RC0jNTd5vGyJJtFjDUnKJVdrF4eOCFs/yFp2hyP8qSiYnMpbdW1AraFgz0AaReS4AWS14C4/YC82I3k1yndnX1OeSkiPYxKomzAN92qTXlBeNycEX2TS/JKFJXQMlLrQK+wtpD95vcBjBrnULh0ecE7XsZ1PxNbM8fRQOJk0XgrK0WsHHasLrIi5puDTdGVAcT3jcliHW2iIJrzPIsokzaeXV+LAGeAAa/NgPV6vwdjyNVjyH3mB5hKPjBfd6Z8cZIey5bdYsuHkeWZkYU/P1mnDS6nzcZh8tzu8j52fD12/PcIpTuTCrQFf4/Cy3NS2BNvfocRC0zdlulhq/hNq8DqF+g5RPgeDnF/+li9PUC04JUOzwGUZ/9wfrV13CCAusEE5gYT3f7UxZqecKr+9HYvO7zyiWPbz2vN9jPQS9AYw5gINScmb/LJJiY8hgGh1pnOTN7ka2bqBT8c8lJg2cBYq264zpaX8Jx149qElptOI3FllkyM6gskh7cLBw67nB3kOIT1ilhbtHB1c9KpAvC5of8XdaGxrTcYQxF2YMl+pzl4QRtY94TJ/u6oZN/TpbgD878L7WIcYFYyUwo8/0sp0FIK8IBUgIFaATYTC7pR8CUW6PWiQLUAm8kF542n/0QuwGC9AGsJBhisGIB7PzPN4Lxe8bE1AwwWDfCAatCepgacAawbYKBwgI2VA7A/fHjl4Ea3PdSVDkIgF6HZUHbWcnpjkq6vO+n6z6/fZkydbizrKjrWwRDSVYg6od77W7NqztVv9tO9/whYaBnPiAQEZfHjaF6xEV+NlrGQjYyFVnIuaFieYDdww8AP8Nj3/Lr+C1whGxk=
```
RS-Latches coupled with memory cells and a circuit function (max)

3 signals
* Reset: will clear both memory cells
* Top input & Bottom input
* Output, the largest value observed by either inputs.

_________________

counter:
```
```
count till register rollover then reset.
