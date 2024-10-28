> Before you can use any type of loops, you need to learn [how to escape code](../Escaping.md).

You can use `$sub[1eX;1]` to get as many nines as you want. For example, `$sub[1e10;1]` gives us 10 nines, which is 9999999999. You can then replace each 9 with a piece of code, which will allow you to run the code as many times as you want. However, due to BDFD’s computation limits, this method is limited to 38 nines. For amounts higher than 38, I recommend using [a more advanced method](../Run%20X%20Times/Advanced%20Method.md).

This example deletes the last 3,800 non-pinned messages sent in the last 2 weeks:
```js
$sum[1e38;%{DOL}%clear[100\]]
```

(38 x 100 = 3,800)
