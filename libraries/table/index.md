# table
This is an expansion to the existing Lua Table library.

!!!Expansion Library
This is an expansion to builtins provided by Lua itself, see more about them on the official Lua/LuaJIT wikis.
!!!

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### table.concat(t: table, sep: string, start?: number, end?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
table.concat(t: table, sep: string, start?: number, end?: number): string
</code>

- Returns the (numeric) entries in the table t, concatenated together with "sep" as the separator, starting at index 'start' and ending at index 'end'.
- The entries are returned as a single string variable.
- Contrast this to the "unpack" function which returns a table as individual variables.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### table.foreach(t: table, f: function(key: any, value: any))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
table.foreach(t: table, f: function(key: any, value: any)): any?
</code>

- Executes f for each element in table t.
- If f returns a non-nil value the loop is broken, and this value is returned as the result from table.foreach.
- Effectively this could be used to find an element inside a table matching a certain condition.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### table.foreachi(t: table, f: function(key: any, value: any))

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
table.foreachi(t: table, f: function(key: any, value: any)): any?
</code>

- Similar to table.foreach, except that only numeric keys in the range 1 to n are processed.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### table.getn(t: table): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
table.getn(t: table): number
</code>

- Returns the size of a numerically-keyed table.
- A table's size (which is only relevant for "numeric" indexed tables) is one less than the first integer index with a nil value.
- If the table has "holes" in it - that is, numeric keys with gaps in the sequence - then the table size is not guaranteed to be the the last gap.
- Lua does a binary search to try to find a gap, it does not necessarily find the first or last one.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### table.insert(t: table, pos: number, value: any)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
table.insert(t: table, pos: number, value: any)
</code>

- Inserts the value at (optional) position 'pos', renumbering existing elements if necessary to make room. Thus the new element becomes the one with index 'pos'.
- If called with 2 arguments, the value is inserted at n+1, that is, the end of the table.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### table.maxn(t: table): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
table.maxn(t: table): number
</code>

- Returns the highest numeric key in the table, by examining each entry in the entire table.
- This will necessarily be slower than doing table.getn, but would be needed if the keys have gaps in the sequence.
- f the table does not have gaps in the keys, it is faster to use<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
table.getn(t: table): number
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### table.remove(t: table, pos?: number): any

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
table.remove(t: table, pos?: number): any
</code>

- Removes the element at position 'pos' from the table, returning the value of the removed element.
- If 'pos' is omitted it defaults to the end of the table (n), thus removing the last element.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### table.sort(t: table, f?: function)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
table.sort(t: table, f?: function)
</code>

- Sorts the table using the supplied function f as the comparison function for each element.
- Function f should return true if the first element is < the second element. If the function omitted it defaults to the operator <.
- Sorting is not stable, that is, the sequence of equal keys is not necessarily preserved.

<div hidden>

```ts

```

</div>
