# RegEx
- Literal characters
- Character classes
	- `[abc]` = character class (one of a, b, or c)
	- Meta characters are shortcuts for character classes
		- `.` = any character
		- `\d` = digit, `\D` = non-digit
		- `\s` = whitespace, `\S` = non-whitespace
		- `\w` = word, `\W` = non-word
- Quantifiers:
	- `?` = 0 or 1
	- `\d*` = 0 or more
	- `\d+` = 1 or more
	- `\d{4}` = 4 digits
- Anchors
	- `^` = beginning of the line
	- `$` = end of the line
	- `$^` to match no string
- Capture groups
	- `(abc)` = group (`abc`, `abcabc`, etc.)
	- `|` for "or"
- Non-capture groups
	- `(?:foo|bar)` = matches "foo" or "bar" but doesn't store as a group
- Named capture groups
	- `(?<name>pattern)`
- Lookaheads/behinds
	- Positive lookahead: `X(?=Y)` = X must be followed by Y
	- Negative lookahead: `X(?!Y)` = X cannot be followed by Y
	- Positive lookbehind: `(?<=Y)X` = X must be preceded by Y
	- Negative lookbehind: `(?<!Y)X` = X cannot be preceded by Y

`^[0-9A-Za-z]{8,}$` password containing 8+ characters (either letter or number)
to validate email address
`^[a-zA-Z0-9.-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`
`^[0-9A-Za-z._-]([a-zA-Z0-9.-_]+[a-zA-Z0-9]+)?@[0-9A-Za-z-]+\..[a-z]{2,}$` 
Positive/Negative Lookbehind/Lookahead