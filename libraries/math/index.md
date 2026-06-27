# math
This is an expansion to the existing Lua Math library.

!!!Expansion Library
This is an expansion to builtins provided by Lua itself, see more about them on the official Lua/LuaJIT wikis.
!!!

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.abs(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.abs(v: number): number
</code>

- Absolute value of v.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.acos(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.acos(v: number): number
</code>

- Arc cosine of v. (Inverse operation of math.cos (v)).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.asin(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.asin(v: number): number
</code>

- Arc sine of v. (Inverse operation of math.sin(v)).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.atan(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.atan(v: number): number
</code>

- Arc tangent of v. (Inverse operation of math.tan (v)).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.atan2(v1: number, v2: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.atan2(v1: number, v2: number): number
</code>

- Arc tangent of v1/v2.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.ceil(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.ceil(v: number): number
</code>

- Smallest integer >= v

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.cos(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.cos(v: number): number
</code>

- Cosine of v radians.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.cosh(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.cosh(v: number): number
</code>

- Hyperbolic cosine of v radians.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.deg(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.deg(v: number): number
</code>

- Convert v from radians to degrees. Note that math.rad is the inverse operation.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.exp(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.exp(v: number): number
</code>

- Compute e to the power v. Note that math.log is the inverse operation.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.floor(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.floor(v: number): number
</code>

- Largest integer <= v

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.fmod(v1: number, v2: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.fmod(v1: number, v2: number): number
</code>

- The modulus (remainder) of doing: v1 / v2

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.frexp(v: number): number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.frexp(v: number): number, number
</code>

- The frexp function breaks down the floating-point value (v) into a mantissa (m) and an exponent (n), such that the absolute value of m is greater than or equal to 0.5 and less than 1.0, and v = m * 2^n.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.huge: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.huge: number
</code>

- The value HUGE_VAL, a value larger than or equal to any other numerical value.
- Note that this is a number, not a function.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.ldexp(m: number, n: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.ldexp(m: number, n: number): number
</code>

- The ldexp function returns the value of m * 2^n.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.log(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.log(v: number): number
</code>

- Natural log of v (that is, to the base e).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.log10(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.log10(v: number): number
</code>

- Log to the base 10 of v.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.max(...: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.max(...: number): number
</code>

- The highest of one or more numbers.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.min(...: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.min(...: number): number
</code>

- The lowest of one or more numbers.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.modf(v: number): number, number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.modf(v: number): number, number
</code>

- Returns two numbers, the integral part of v and the fractional part of v

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.pi: number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.pi: number
</code>

- A variable representing the value of pi (not a function).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.pow(v1: number, v2: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.pow(v1: number, v2: number): number
</code>

- v1 raised to the power v2.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.rad(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.rad(v: number): number
</code>

- Convert v from degrees to radians.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.random(n: number, u: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.random(n?: number, u?: number): number
</code>

- With no arguments, returns a random number in the range [0, 1]. That is, zero up to but excluding 1.
- With 1 argument, returns an integer in the range [1, n]. That is from 1 up to and including n.
- With 2 arguments, returns an integer in the range [n, u]. That is from n up to and including u.
- Use<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.randomseed(n: number)
</code>to seed the generator.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.randomseed(n: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.randomseed(n: number)
</code>

- Seeds the random number generator with an integer.
- Re-seed with the same number to regenerate the same sequences by calling math.random.
- Seeding with os.time () is a common technique to make random numbers different each time.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.sin(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.sin(v: number): number
</code>

- Sine of v radians.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.sinh(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.sinh(v: number): number
</code>

- Hyperbolic sine of v radians.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.sqrt(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.sqrt(v: number): number
</code>

- Square root of v.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.tan(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.tan(v: number): number
</code>

- Tangent of v radians.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### math.tanh(v: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
math.tanh(v: number): number
</code>

- Hyperbolic tangent of v radians.

<div hidden>

```ts

```

</div>
