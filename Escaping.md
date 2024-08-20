# Escaping
Imagine you want to send “$nomention” but BDFD doesn’t let you because it’s a function. Escaping allows you to do that!

The “escaped version” of `$nomention` is `%{DOL}%nomention`, so, in order to send “$nomention” you should do `$sendMessage[%{DOL}%nomention]`.

`$` => `%{DOL}%` or `$$c[]` \
`[` doesn’t need to be changed. \
`;` => `\;` \
`]` => `\]` \
`\` => `\\`

For example, to send `$addButton[New row;Custom ID;Label;Style;Disabled;Emoji;Message ID]`, you could do:
```
$sendMessage[$$c[]addButton[New Row\;Custom Id\;Label\;Style\;Disabled\;Emoji\;Message Id\]]
```

> BDFD thinks `\\]` means “Backslash followed by an escaped `]`” instead of “Escaped backslash followed by a `]`” so it can break your code. You can instead use `$url[decode;%5C]` as an escaped backslash in these situations.
> 
> Example: \
> `$replaceText[\\;\\;\\]` throws an error, but `$replaceText[\\;\\;$url[decode;%5C]]` doesn’t.

# Other
If your code has a lot of `%{DOL}%` or `$$c[]`, you could use a symbol like and `/` then replace them with `$`.

Example:
```
$replaceText[/nomention /maybemention /yesmention;/;$]
```

#

If you put your code in an `$async` block (which can be retrieved with `$await`) you don't need to escape anything besides `$`.

Example:
```
$async[]
    $$c[]addButton[New Row;Custom Id;Label;Style;Disabled;Emoji;Message Id]
$endasync

$sendMessage[$await[]]
```
> Note:
> In the above example, `$await[]` returns a line-break character, 4 spaces, the escaped code, then another new line, but Discord automatically removes spaces at the start and end of messages, so in this `$sendMessage` example, there’s no need to use `$trimSpace`, but in other situations, you might need it.

# Example of combining a few of the tricks above
```
$async[]
    /if[/discriminator[]==0]
        It seems like you have switched to the new username system. You probably hate your new username, but I hope you like it.
    /else
        Why haven’t you switched to the new username system yet? The sooner you do, the more likely you are to get a username you like.
    /endif
$endasync

$eval[$replaceText[$trimSpace[$await[]];/;$]]
```
