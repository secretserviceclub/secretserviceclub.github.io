# paint
An alternative method of creating visuals & graphics on higher level access.\
Instead of using in-game drawing systems, this uses an external version on a separated thread.

---
## Optimizing
When you perform drawing objects, its good practice to localize & reuse data.\
Try to minimize object creation if you can, paint.point.* may be harder to localize.\
This is due to the idea of dynamically changing vectors, which can be a problem but do-able.

```lua
paint.add("example", function(w, h)
    -- don't do this, you are creating a new object every time
    local color = paint.color.rgba(255, 255, 255, 255)
end)

-- instead do this
local white = paint.color.rgba(255, 255, 255, 255)
paint.add("example", function(w, h)
    -- access white here, its now an upvalue
end)

-- if you need to change it at runtime
local dynamic = paint.color.rgba(255, 255, 255, 255)
paint.add("example", function(w, h)
    dynamic.r = (os.clock() % 1) * 255
    -- in here we are just changing the color object's "R" stat
end)
```

---
## Interstate
Paint works everywhere no matter where you call it.\
An example of this is by using linker's ability to attach to certain events.\
This allows you to have a unique way of inline calls for accurate points.
```lua
linker.hook.add("Think", "paint!", function()
    -- perform paint operations here as well
end)
```

---
## Types
Paint uses two different vector types.\
Both types are recognized by their index characteristics.\
Which means using internal game-software mechanics like "Vector", would also work.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.point.vector2(x: number, y: number): paint_point

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.point.vector2(x: number, y: number): paint_point
</code>

- Creates a 2D vector for paint to recognize

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.point.vector3(x: number, y: number, z: number): paint_point

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.point.vector3(x: number, y: number, z: number): paint_point
</code>

- Creates a 3D vector for paint to recognize

---
Paint also uses its own color system due to the fact of interop with other frameworks.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.color.rgb(r: number, g: number, b: number): paint_color

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.color.rgb(r: number, g: number, b: number): paint_color
</code>

- Creates an RGB based color

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.color.rgba(r: number, g: number, b: number, a?: number): paint_color

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.color.rgba(r: number, g: number, b: number, a?: number): paint_color
</code>

- Creates an RGBA based color

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.color.hex(hex: string): paint_color

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.color.hex(hex: string): paint_color
</code>

- Creates an RGBA based color from hex strings
- Accepts format #RRGGBBAA or #RRGGBB

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.color.hsv(h: number, s: number, v: number, a?: number): paint_color

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.color.hsv(h: number, s: number, v: number, a?: number): paint_color
</code>

- Creates an RGBA based color from HSV

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.color.hsl(h: number, s: number, l: number, a?: number): paint_color

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.color.hsl(h: number, s: number, l: number, a?: number): paint_color
</code>

- Creates an RGBA based color from HSL

---
## Functions

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.line(p1: paint_point, p2: paint_point, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.line(p1: paint_point, p2: paint_point, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a line between points A and B

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.circle.filled(center: paint_point, color: paint_color, radius: number, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.circle.filled(center: paint_point, color: paint_color, radius: number, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a circle around a center point that is filled

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.circle.hollow(center: paint_point, color: paint_color, radius: number, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.circle.hollow(center: paint_point, color: paint_color, radius: number, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a circle around a center point that is hollow

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.tri.filled(p1: paint_point, p2: paint_point, p3: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.tri.filled(p1: paint_point, p2: paint_point, p3: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a triangle from three points that is filled

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.tri.hollow(p1: paint_point, p2: paint_point, p3: paint_point, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.tri.hollow(p1: paint_point, p2: paint_point, p3: paint_point, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a triangle from three points that is hollow

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.rect.filled(top_left: paint_point, size: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.rect.filled(top_left: paint_point, size: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a rectangle that is filled

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.rect.hollow(top_left: paint_point, size: paint_point, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.rect.hollow(top_left: paint_point, size: paint_point, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a rectangle that is hollow

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.rect.rfilled(rounding: number, top_left: paint_point, size: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.rect.rfilled(rounding: number, top_left: paint_point, size: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a rectangle that is filled with rounding

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.rect.rhollow(rounding: number, top_left: paint_point, size: paint_point, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.rect.rhollow(rounding: number, top_left: paint_point, size: paint_point, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a rectangle that is hollow with rounding

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.rect.gradient(top_left: paint_point, size: paint_point, up_left: paint_color, up_right: paint_color, bottom_left: color_paint, bottom_right: color_paint, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.rect.gradient(top_left: paint_point, size: paint_point, up_left: paint_color, up_right: paint_color, bottom_left: color_paint, bottom_right: color_paint, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a rectangle using a gradient of colors

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.qrot.filled(center: paint_point, size: paint_point, color: paint_color, rotation: number, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.qrot.filled(center: paint_point, size: paint_point, color: paint_color, rotation: number, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a rectangle that is filled with rotation in degrees
- These rectangles are centered

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.qrot.hollow(center: paint_point, size: paint_point, color: paint_color, rotation: number, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.qrot.hollow(center: paint_point, size: paint_point, color: paint_color, rotation: number, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a rectangle that is hollow with rotation in degrees
- These rectangles are centered

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.quad.filled(p1: paint_point, p2: paint_point, p3: paint_point, p4: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.quad.filled(p1: paint_point, p2: paint_point, p3: paint_point, p4: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a quadrilateral that is filled

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.quad.hollow(p1: paint_point, p2: paint_point, p3: paint_point, p4: paint_point, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.quad.hollow(p1: paint_point, p2: paint_point, p3: paint_point, p4: paint_point, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a quadrilateral that is hollow

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.text.left(point: paint_point, text: string, color: paint_color, outline?: paint_color = {0, 0, 0, 255})

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.text.left(point: paint_point, text: string, color: paint_color, outline?: paint_color = {0, 0, 0, 255})
</code>

- Creates text thats aligned to the left

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.text.center(point: paint_point, text: string, color: paint_color, outline?: paint_color = {0, 0, 0, 255})

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.text.center(point: paint_point, text: string, color: paint_color, outline?: paint_color = {0, 0, 0, 255})
</code>

- Creates text thats aligned to the center

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.text.right(point: paint_point, text: string, color: paint_color, outline?: paint_color = {0, 0, 0, 255})

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.text.right(point: paint_point, text: string, color: paint_color, outline?: paint_color = {0, 0, 0, 255})
</code>

- Creates text thats aligned to the right

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.text.bake(font_name: string, font_data: string, size: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.text.bake(font_name: string, font_data: string, size: number): boolean
</code>

- Bakes a font into memory, so that you can use it
- Fonts already created under a name will simply return true as existing

```lua
local proggy_data = fs.read("proggy_clean.ttf")
if not paint.text.bake("Proggy", proggy_data, 14) then
    error("Couldn't load proggy font!")
end

local point = paint.point.vector2(40, 40)
local white = paint.color.rgb(255, 255, 255)
paint.add("example", function(w, h)
    if paint.text.isbaked("Proggy") then
        paint.text.font("Proggy") -- push the font, otherwise will use 'default'
   		paint.text.left(point, "hello world", white)
	end
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.text.unbake(font_name: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.text.unbake(font_name: string): boolean
</code>

- De-allocates a font from memory, effectively unloading it

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.text.isbaked(font_name: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.text.isbaked(font_name: string): boolean
</code>

- Check if a font has been added

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.text.font(font_name?: string): string

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.text.font(font_name?: string): string
</code>

- Makes all future text renderers use a specific font
- Returns the current font being used currently

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.text.get_size(text: string): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.text.get_size(text: string): table
</code>

- Returns the width and height (in pixels) of the given text using the `default` font.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.text.get_size(font_name: string, text: string): table

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.text.get_size(font_name: string, text: string): table
</code>

- Returns the width and height (in pixels) of the given text using a specified `font`.

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.image.bake(data: string): image | false

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.image.bake(data: string): image | false
</code>

- Bakes an image into memory, so that you can use it
- Images are managed by reference, so if its no longer used in lua, it will eventually de-allocate

```lua
local data = fs.read("sample.jpg")
local image = paint.image.bake(data)
if not image then
    error("Couldn't load image!")
end

local point = paint.point.vector2(50, 50)
local size = paint.point.vector2(128, 128)
local white = paint.color.rgb(255, 255, 255)
paint.add("example", function(w, h)
    paint.image.normal(image, point, size, white)
end)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.image.normal(image: image, top_left: paint_point, size: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255})

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.image.normal(image: image, top_left: paint_point, size: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255})
</code>

- Creates a rectangle image

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.image.round(image: image, rounding: number, top_left: paint_point, size: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255})

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.image.round(image: image, rounding: number, top_left: paint_point, size: paint_point, color: paint_color, outline?: paint_color = {0, 0, 0, 255})
</code>

- Creates a rectangle image with rounding

---

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.poly.filled(vertices: table, color: paint_color, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.poly.filled(vertices: table, color: paint_color, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a filled polygon from a table of vertices. 
- Requires at least 3 vertices

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### paint.poly.hollow(vertices: table, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
paint.poly.hollow(vertices: table, color: paint_color, thickness?: number = 1, outline?: paint_color = {0, 0, 0, 255}, outline_thickness?: number = 0)
</code>

- Creates a hollow polygon from a table of vertices. 
- Requires at least 3 vertices

```lua
local point1 = paint.point.vector2(40, 40)
local point2 = paint.point.vector2(100, 40)
local point3 = paint.point.vector2(70, 100)

local white = paint.color.rgb(255, 255, 255)
local red   = paint.color.rgb(255, 0, 0)

paint.add("example", function(w, h)
    -- filled triangle
    paint.poly.filled({point1, point2, point3}, white)

    -- hollow triangle
    paint.poly.hollow({point1, point2, point3}, red, 2) 
end)
```

---
## Events
Paint uses a slightly different type of **Signal**\
You don't have to provide a name, instead its just an identifier.
```lua
-- instead of:
paint.listener.add("paint", "identity", function(w, h) end)
-- its:
paint.add("identity", function(w, h) end)
```
This is to make it simpler since paint really only has one event handler.

<div hidden>

```ts

```

</div>
