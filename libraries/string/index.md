# string
This is an expansion to the existing Lua String library.

!!!Expansion Library
This is an expansion to builtins provided by Lua itself, see more about them on the official Lua/LuaJIT wikis.
!!!

---
## Format
```
%c - convert a number to a single character (like string.char)
%d and %i - output as an integer number
%o - convert to octal
%u - convert to an unsigned number
%x - hex (lower-case)
%X - hex (upper-case)
%e - scientific notation, "e" in lower case:
%E - scientific notation, "E" in upper case:
%f - floating point, default to 6 decimal places:
%g - Signed value printed in %f or %e format, whichever is more compact for the given value. To make it compact, only the required number of decimal places (if any) are shown.
%G - Same as %g except that an upper-case E is used where appropriate.
%q - formats a string in such a way Lua can read it back in (eg. as Lua source).
%s - output a string (or something that can be converted to a string, such as a number).
%% - output a single % character
```

---
## Patterns
```
 . --- (a dot) represents all characters. 
%a --- all letters. 
%c --- all control characters. 
%d --- all digits. 
%l --- all lowercase letters. 
%p --- all punctuation characters. 
%s --- all space characters. 
%u --- all uppercase letters. 
%w --- all alphanumeric characters. 
%x --- all hexadecimal digits. 
%z --- the character with hex representation 0x00 (null). 
%% --- a single '%' character.
%1 --- captured pattern 1.
%2 --- captured pattern 2 (and so on).
%f[s]  transition from not in set 's' to in set 's'.
%b()   balanced nested pair ( ... ( ... ) ... ) 
```

### Sets
```
[abc] ---> matches a, b or c
[a-z] ---> matches lowercase letters (same as %l)
[^abc] ---> matches anything except a, b or c
[%a%d] ---> matches all letters and digits
[%a%d_] ---> matches all letters, digits and underscore
[%[%]] ---> matches square brackets (had to escape them with %)
```

### Repetition
```
+  ---> 1 or more repetitions (greedy)
*  ---> 0 or more repetitions (greedy)
-  ---> 0 or more repetitions (non greedy)
?  ---> 0 or 1 repetition only
```

### Anchor
```
^  ---> anchor to start of subject string (must be the very first character)
$  ---> anchor to end of subject string   (must be the very last character)
```

### Special
```
(...) ---> captures the contents inside the parenthesis
print (string.find ("You see dogs and dogs", "You see (.*) and %1")) --> 1 21 dogs
```

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.byte(s: string, n?: number = 1): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.byte(s: string, n?: number = 1): number
</code>

- Returns the ASCII code for the nth character of the string s. The inverse operation is carried out by string.char.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.char(...: number): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.char(...: number): string
</code>

- Receives 0 or more numbers and converts them to the corresponding characters. The inverse operation is carried out by string.byte.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.dump(f: function): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.dump(f: function): string
</code>

- Converts a function f into binary representation, which can be subsequently processed by loadstring to retrieve the function.
- The function must be a Lua function without upvalues.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.find(str: string, pattern: string, index?: number = 1, plain?: boolean = false): number?, number?, ...?: string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.find(str: string, pattern: string, index?: number = 1, plain?: boolean = false): number?, number?, ...?: string
</code>

- Find the first match of the regular expression "pattern" in "str", starting at position "index".
- The starting position (index) is optional, and defaults to 1 (the start of the string).
- If found, returns the start and end position, and any captures as additional results.
- If "plain" is true, the search string is plain text, not a regular expression. (The "plain" argument is optional, and defaults to false).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.format(fstr: string, ...: any): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.format(fstr: string, ...: any): string
</code>

- Formats the supplied values (v1, v2 etc.) using format string 'fstr', similar to the C function printf.
- It is an error to supply too few variables for the format string.
- The format string comprises literal text, and directives starting with %. Each directive controls the format of the next argument.
- Directives can include flags, width and precision controls.
- To literally incorporate `%` in the output you need to put `%%` in the format string.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.gmatch(str: string, pattern: string): function

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.gmatch(str: string, pattern: string): function
</code>

- Returns an iterator function for returning the next capture from a pattern over a string.
- If there is no capture, the whole match is produced.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.gsub(str: string, pattern: string, replacement: string | function | table, n?: number): string, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.gsub(str: string, pattern: string, replacement: string | function | table, n?: number): string, number
</code>

- Returns a copy of str with matches to 'pattern' replaced by 'replacement', for a maximum of n times, as a second result it returns the number of matches made.
- 'replacement' can be a string in which case it simply replaces the matching pattern.
- However `%1` through to `%9` in the replacement pattern can refer to captured strings in the source pattern. `%%` becomes `%`.
- Also, `%0` in the replacement pattern refers to the entire matching string.
- If 'replacement' is a function it is called for each match with the matching string as an argument.
- It should return a string which is the string to replace it with. If it returns nil the original string is retained.
- If 'replacement' is a table then the matching string is looked up in the table for each match, and if found, the replacement is substituted.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.len(str: string): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.len(str: string): number
</code>

- Returns the length of the string, including any imbedded zero (0x00) bytes.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.lower(str: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.lower(str: string): string
</code>

- Returns the string converted to lower-case.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.match(str: string, pattern: string, index?: number): ...string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.match(str: string, pattern: string, index?: number): ...string
</code>

- Find the first match of the regular expression "pattern" in "str", starting at position "index".
- The starting position (index) is optional, and defaults to 1 (the start of the string).
- If found, returns any captures in the pattern. If no captures were specified the entire matching string is returned.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.rep(str: string, n: number): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.rep(str: string, n: number): string
</code>

- Returns a string which is n copies of the source string concatenated together.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.reverse(str: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.reverse(str: string): string
</code>

- Returns a string that is the string str reversed.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.sub(str: string, start: number, end?: number): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.sub(str: string, start: number, end?: number): string
</code>

- Returns a substring of the string, starting at index 'start' and ending at index 'end'. Both may be negative to indicate counting from the right. The end point is optional and defaults to -1, which is the entire rest of the string.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### string.upper(str: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
string.upper(str: string): string
</code>

- Returns the string converted to upper-case.
<div hidden>

```ts

```

</div>
