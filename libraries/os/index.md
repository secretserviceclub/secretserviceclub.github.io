# os
This is an expansion to the existing Lua OS library.

!!!Expansion Library
This is an expansion to builtins provided by Lua itself, see more about them on the official Lua/LuaJIT wikis.
!!!

---
## Format

```
%a - Abbreviated weekday name (eg. Wed)
%A - Full weekday name (eg. Wednesday)
%b - Abbreviated month name (eg. Sep)
%B - Full month name (eg. September)
%c - Date and time representation appropriate for locale (eg. 23/04/07 10:20:41)
         (Standard date and time string ) - see below for using os.setlocale to get the correct locale.
%d - Day of month as decimal number (01 - 31)
%H - Hour in 24-hour format (00 - 23)
%I - Hour in 12-hour format (01 - 12)
%j - Day of year as decimal number (001 - 366)
%m - Month as decimal number (01 - 12)
%M - Minute as decimal number (00 - 59)
%p - Current locale’s A.M./P.M. indicator for 12-hour clock (eg. AM/PM)
%S - Second as decimal number (00 - 59)
%U - Week of year as decimal number, with Sunday as first day of week 1 (00 - 53)
%w - Weekday as decimal number (0 - 6; Sunday is 0)
%W - Week of year as decimal number, with Monday as first day of week 1 (00 - 53)
%x - Date representation for current locale (Standard date string)
%X - Time representation for current locale (Standard time string)
%y - Year without century, as decimal number (00 - 99)  (eg. 07)
%Y - Year with century, as decimal number (eg. 2007)
%Z - Time-zone name or abbreviation; no characters if time zone is unknown
%% - Percent sign
```

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### os.clock(): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
os.clock(): number
</code>

- Returns the approximate amount of CPU time used by the current process in seconds.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### os.date(format: string, time?: number): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
os.date(format: string, time?: number): string
</code>

- Returns a string with the date and time formatted according to the format given. If no time is supplied defaults to the current time.
- The format string can consist of "*t" on its own, or literal strings, mixed with other directives

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### os.difftime(t1: number, t2: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
os.difftime(t1: number, t2: number): number
</code>

- Returns the number of seconds from time t1 to time t2.
- In other words, the result is t1 - t2.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### os.time(t?: number | table): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
os.time(t?: table): number
</code>

- Returns the current time if no argument supplied.
- The time is in seconds from the start of the current epoch.
- On Windows, the function returns the number of seconds elapsed since midnight (00:00:00), January 1, 1970, coordinated universal time, according to the system clock.

```lua
print (os.time {
    year = 2004,
    month = 8,
    day = 30,
    hour = 6,
    min = 32,
    sec = 1,
    dst = true
})
--> 1093811521

print (os.date ("%x %X", 1093811521)) 
--> 30/08/04 06:32:01         
```
<div hidden>

```ts

```

</div>
