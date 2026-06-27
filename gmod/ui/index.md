# ui
Create and manage menu elements (groupboxes, checkboxes, sliders, buttons, etc.) in the cheat interface. Use `config_name` with [config](/gmod/config/) get/set to read and save values.

---
## Creation

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.create_groupbox(tab: string, side: string, name: string, height: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.create_groupbox(tab: string, side: string, name: string, height: number)
</code>

- Creates a groupbox within the specified tab of the menu.

```lua
secret.ui.create_groupbox("lua", "right", "elements", 200)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.create_checkbox(tab: string, groupbox: string, name: string, config_name: string): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.create_checkbox(tab: string, groupbox: string, name: string, config_name: string): number
</code>

- Creates a checkbox UI element within the specified tab and groupbox of the menu. 
- Returns a numeric ID for the created element that can be used to update or remove it later.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.create_button(tab: string, groupbox: string, name: string, callback: function): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.create_button(tab: string, groupbox: string, name: string, callback: function): number
</code>

- Creates a **button** UI element within the specified tab and groupbox of the menu.
- Returns a numeric ID for the created element that can be used to update or remove it later.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.create_slider(tab: string, groupbox: string, name: string, min: number, max: number, config_name: string): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.create_slider(tab: string, groupbox: string, name: string, min: number, max: number, config_name: string): number
</code>

- Creates a slider UI element within the specified tab and groupbox of the menu.
- Returns a numeric ID for the created element that can be used to update or remove it later.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.create_colorpicker(tab: string, groupbox: string, name: string, config_name: string): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.create_colorpicker(tab: string, groupbox: string, name: string, config_name: string): number
</code>

- Creates a colorpicker UI element within the specified tab and groupbox of the menu.
- Returns a numeric ID for the created element that can be used to update or remove it later.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.create_inputbox(tab: string, groupbox: string, name: string, config_name: string): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.create_inputbox(tab: string, groupbox: string, name: string, config_name: string): number
</code>

- Creates an inputbox UI element within the specified tab and groupbox of the menu.
- Returns a numeric ID for the created element that can be used to update or remove it later.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.create_hotkey(tab: string, groupbox: string, name: string, config_name: string): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.create_hotkey(tab: string, groupbox: string, name: string, config_name: string): number
</code>

- Creates a hotkey UI element within the specified tab and groupbox of the menu.
- Returns a numeric ID for the created element that can be used to update or remove it later.

```lua
secret.ui.create_groupbox("lua", "right", "elements", 200) -- create a groupbox called "elements"

-- create and check lua hotkeys
secret.ui.create_hotkey("lua", "elements", "my hotkey", "lua_hotkey")
if secret.config.get("lua_hotkey") then
    print("our lua hotkey is on!")
end
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.create_dropdown(tab: string, groupbox: string, name: string, config_name: string, items: table, multi: boolean): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.create_dropdown(tab: string, groupbox: string, name: string, config_name: string, items: table, multi: boolean): number
</code>

- Creates a dropdown UI element within the specified tab and groupbox of the menu.
- Returns a numeric ID for the created element that can be used to update or remove it later.

```lua
secret.ui.create_groupbox("lua", "right", "elements", 200) -- create a groupbox called "elements"

secret.ui.create_dropdown("lua", "elements", "My Lua Dropdown", "lua_dropdown", {"Item1", "Item2", "Item3"}, false)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.create_playerlist_text(text: string, index: number): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.create_playerlist_text(text: string, index: number): number
</code>

- Creates a text UI element in the 'advanced' tab of the player identified by the given index.
- Returns a numeric ID for the created element that can be used to update or remove it later.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.create_playerlist_button(name: string, index: number, callback: function): number

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.create_playerlist_button(name: string, index: number, callback: function): number
</code>

- Creates a button UI element in the 'advanced' tab of the player identified by the given index.
- Do note that the callback will return the index as a param.
- Returns a numeric ID for the created element that can be used to update or remove it later.

---
## Updates & removal

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.update(index: number, new_value: string|table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.update(index: number, new_value: string|table)
</code>

- Updates the UI element at the given index.

```lua
secret.ui.update(checkbox_id, "New Checkbox Label")        -- update checkbox/button/inputbox label
secret.ui.update(button_id, "New Button Label")
secret.ui.update(inputbox_id, "New Input Label")

secret.ui.update(dropdown_id, {"NewItem1", "NewItem2"})

secret.ui.update(slider_id, { min = 0, max = 100 })
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.remove(index: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.remove(index: number)
</code>

- Removes the UI element at the given index.

```lua
secret.ui.remove(checkbox_id)
```

---
## Groupbox

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.update_groupbox(tab: string, groupbox_name: string, update_value: string|table|number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.update_groupbox(tab: string, groupbox_name: string, update_value: string|table|number)
</code>

- Updates properties of an existing groupbox.

```lua
-- update groupbox name
secret.ui.update_groupbox("lua", "elements", "new_elements")

-- update multiple properties
secret.ui.update_groupbox("lua", "elements", { name = "new_elements", side = "left", height = 150 })

-- update height only
secret.ui.update_groupbox("lua", "elements", 300)
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.remove_groupbox(tab: string, groupbox_name: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.remove_groupbox(tab: string, groupbox_name: string)
</code>

- Removes the specified groupbox.

```lua
secret.ui.remove_groupbox("lua", "elements")
```

---
## State & notifications

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.clear_elements()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.clear_elements()
</code>

- Clears all the current elements made with lua, such as secret.ui.create_checkbox, etc.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.menu_open(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.menu_open(): boolean
</code>

- Returns a boolean value of the menu being open.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.console_open(): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.console_open(): boolean
</code>

- Returns a boolean value of the console being open.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.notify(text: string, type: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.notify(text: string, type: number)
</code>

- Creates a new notification at the top left corner of the screen with the specified text and type.
- 0 = Default
- 1 = Warning
- 2 = Error

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.is_keybind_active(keybind_name: string, absolute?: boolean = false): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.is_keybind_active(keybind_name: string, absolute?: boolean = false): boolean
</code>

- Checks if a specified keybind is currently active/pressed.
- Only works with built-in cheat features, not Lua-specific keybinds.

```lua
-- check thirdperson with absolute=false (default) - returns true if in "always" mode or not bound
if secret.config.get("misc_thirdperson") and secret.ui.is_keybind_active("thirdperson") then
    print("thirdperson is enabled (always mode or key not bound)")
end

-- check thirdperson with absolute=true - only returns true if key is physically pressed --> this is what the 'hotkeys' uses.
if  secret.config.get("misc_thirdperson") and secret.ui.is_keybind_active("thirdperson", true) then
    print("thirdperson key is currently being pressed")
end
```

---
## Advanced script windows

This is the callback-based UI API for custom script windows.
Use it when you want to build your own menu layout with Lua.

### Quickstart

```lua
local ui = secret.ui

local window_id = "quickstart_window"
local state = { enabled = false }

local function render_window()
    local changed
    changed, state.enabled = ui.checkbox("enabled", state.enabled)
    ui.tooltip("this is a quickstart tooltip")
end

if not ui.window_exists(window_id) then
    ui.window_register(window_id, "quickstart", render_window, {
        visible = true,
        open = true,
        size = { x = 320, y = 180 }
    })
end
```

---
## Window lifecycle

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_register(id: string, title: string, callback: function, options?: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_register(id: string, title: string, callback: function, options?: table)
</code>

- Creates or replaces a script window and callback.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_bind_draw(id: string, callback: function)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_bind_draw(id: string, callback: function)
</code>

- Replaces the draw callback for an already registered window.
- Useful when the window metadata was created earlier and you only need to update what it renders.
- The window must already exist (`ui.window_register` first).

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_remove(id: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_remove(id: string)
</code>

- Removes one script window.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_exists(id: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_exists(id: string): boolean
</code>

- Checks if a window id is currently registered.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_clear_all()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_clear_all()
</code>

- Removes all script windows created by Lua.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_set_visible(id: string, visible: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_set_visible(id: string, visible: boolean)
</code>

- Sets visibility.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_set_open(id: string, open: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_set_open(id: string, open: boolean)
</code>

- Sets open/closed state.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_get_open(id: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_get_open(id: string): boolean
</code>

- Gets open/closed state.

---
## Window options, style, colors

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_set_options(id: string, options: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_set_options(id: string, options: table)
</code>

- Updates options after registration.
- Full supported `options` fields:

```lua
{
    -- state
    visible = true,
    open = true,

    -- glow/shadow toggle
    glow = true,   -- alias: shadow
    shadow = true, -- alias of glow

    -- transform
    position = { x = 120, y = 120 }, -- or {120, 120}
    size = { x = 420, y = 360 },     -- or {420, 360}
    position_cond = 2, -- ImGuiCond number (optional)
    size_cond = 2,     -- ImGuiCond number (optional)

    -- window flags
    flags = 0, -- raw ImGuiWindowFlags number (optional)
    no_title_bar = false,
    no_resize = false,
    no_move = false,
    no_scrollbar = false,
    no_scroll_with_mouse = false,
    no_collapse = false,
    always_auto_resize = false,
    no_background = false,
    no_saved_settings = false,
    no_focus_on_appearing = false,
    no_bring_to_front_on_focus = false
}
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_set_style(id: string, style: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_set_style(id: string, style: table)
</code>

- Sets per-window style overrides (padding, spacing, rounding, border size, alignments).
- Full supported `style` keys:

```lua
{
    -- vec2
    window_padding = { x = 13, y = 13 },
    item_spacing = { x = 10, y = 10 },
    item_inner_spacing = { x = 8, y = 8 },
    window_title_align = { x = 0.0, y = 0.5 },
    button_text_align = { x = 0.5, y = 0.5 },
    selectable_text_align = { x = 0.0, y = 0.0 },

    -- float
    window_rounding = 6,
    child_rounding = 6,
    frame_rounding = 6,
    popup_rounding = 6,
    tab_rounding = 6,
    scrollbar_rounding = 6,
    grab_rounding = 6,
    window_border_size = 1,
    child_border_size = 1,
    frame_border_size = 1,
    popup_border_size = 1,
    indent_spacing = 8,
    scrollbar_size = 12,
    grab_min_size = 10
}
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_clear_style(id: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_clear_style(id: string)
</code>

- Clears style overrides.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_set_color(id: string, color_name: string, color: table|r: number, g: number, b: number, a?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_set_color(id: string, color_name: string, color: table|r: number, g: number, b: number, a?: number)
</code>

- Sets one color override for a window.
- `Shadow` and `BorderShadow` target the same outside glow color.
- Full supported `color_name` values:

```lua
{
    "Text", "TextDisabled",
    "WindowBg", "ChildBg", "PopupBg",
    "Border", "BorderShadow", "Shadow",
    "FrameBg", "FrameBgHovered", "FrameBgActive",
    "TitleBg", "TitleBgActive", "TitleBgCollapsed",
    "MenuBarBg",
    "ScrollbarBg", "ScrollbarGrab", "ScrollbarGrabHovered", "ScrollbarGrabActive",
    "CheckMark",
    "SliderGrab", "SliderGrabActive",
    "Button", "ButtonHovered", "ButtonActive",
    "Header", "HeaderHovered", "HeaderActive",
    "Separator", "SeparatorHovered", "SeparatorActive",
    "ResizeGrip", "ResizeGripHovered", "ResizeGripActive",
    "Tab", "TabHovered", "TabActive", "TabUnfocused", "TabUnfocusedActive",
    "PlotLines", "PlotLinesHovered",
    "PlotHistogram", "PlotHistogramHovered",
    "TableHeaderBg", "TableBorderStrong", "TableBorderLight",
    "TableRowBg", "TableRowBgAlt",
    "TextSelectedBg",
    "DragDropTarget",
    "NavHighlight", "NavWindowingHighlight", "NavWindowingDimBg",
    "ModalWindowDimBg",
    "Scheme"
}
```

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.window_clear_colors(id: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.window_clear_colors(id: string)
</code>

- Clears all window color overrides.

---
## Widgets

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.text(text: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.text(text: string)
</code>

- Draws text.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.text_colored(color: table, text: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.text_colored(color: table, text: string)
</code>

- Draws colored text.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.button(label: string, width?: number, height?: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.button(label: string, width?: number, height?: number): boolean
</code>

- Draws a button. Returns `true` when clicked.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.checkbox(label: string, value: boolean): (changed: boolean, value: boolean)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.checkbox(label: string, value: boolean): (changed: boolean, value: boolean)
</code>

- Draws a checkbox.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.toggle(...)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.toggle(...) -- alias of ui.checkbox(...)
</code>

- Alias for `ui.checkbox`.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.slider_float(label: string, value: number, min: number, max: number, format?: string): (changed: boolean, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.slider_float(label: string, value: number, min: number, max: number, format?: string): (changed: boolean, value: number)
</code>

- Float slider.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.slider_int(label: string, value: number, min: number, max: number, format?: string): (changed: boolean, value: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.slider_int(label: string, value: number, min: number, max: number, format?: string): (changed: boolean, value: number)
</code>

- Int slider.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.input_text(label: string, value: string, max_length?: number): (changed: boolean, value: string)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.input_text(label: string, value: string, max_length?: number): (changed: boolean, value: string)
</code>

- Text input.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.combo(label: string, current_index_0_based: number, items: table): (changed: boolean, index_0_based: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.combo(label: string, current_index_0_based: number, items: table): (changed: boolean, index_0_based: number)
</code>

- Combo using zero-based index.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.combo_simple(label: string, current_index_1_based: number, items: table): (changed: boolean, index_1_based: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.combo_simple(label: string, current_index_1_based: number, items: table): (changed: boolean, index_1_based: number)
</code>

- Combo using one-based index.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.tabs(id: string, current_index_1_based: number, labels: table): (changed: boolean, index_1_based: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.tabs(id: string, current_index_1_based: number, labels: table): (changed: boolean, index_1_based: number)
</code>

- Tab selector.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.color_edit4(label: string, r: number, g: number, b: number, a: number, flags?: number): (changed: boolean, r: number, g: number, b: number, a: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.color_edit4(label: string, r: number, g: number, b: number, a: number, flags?: number): (changed: boolean, r: number, g: number, b: number, a: number)
</code>

- Color editor. Returns channels in 0-255.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.color_picker(label: string, ...): (changed: boolean, color: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.color_picker(label: string, color_or_channels..., picker_options?: table|number, layout_options?: table|boolean): (changed: boolean, color: table)
</code>

- Color picker helper.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.color_picker_inline(label: string, ...): (changed: boolean, color: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.color_picker_inline(label: string, color_or_channels..., picker_options?: table|number, layout_options?: table|boolean): (changed: boolean, color: table)
</code>

- Inline color picker helper.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.hotkey(label: string, key: number, mode?: number, allow_mode?: boolean, inline?: boolean, spacing?: number, align_right?: boolean): (changed: boolean, key: number, mode: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.hotkey(label: string, key: number, mode?: number, allow_mode?: boolean, inline?: boolean, spacing?: number, align_right?: boolean): (changed: boolean, key: number, mode: number)
</code>

- Hotkey widget.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.hotkey_inline(label: string, key: number, mode?: number, allow_mode?: boolean, spacing?: number): (changed: boolean, key: number, mode: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.hotkey_inline(label: string, key: number, mode?: number, allow_mode?: boolean, spacing?: number): (changed: boolean, key: number, mode: number)
</code>

- Inline hotkey widget.

---
## Helpers, layout, draw

### Layout helpers

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.tooltip(text: string): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.tooltip(text: string): boolean
</code>

- Shows a tooltip if the previously rendered item is hovered.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.help_marker_inline(text: string, spacing?: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.help_marker_inline(text: string, spacing?: number): boolean
</code>

- Draws inline `(?)` and shows tooltip on hover.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.separator()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.separator()
</code>

- Draws a horizontal separator line.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.spacing(amount?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.spacing(amount?: number)
</code>

- Adds one or more spacing rows.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.same_line(offset?: number, spacing?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.same_line(offset?: number, spacing?: number)
</code>

- Places the next item on the same line.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.begin_group()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.begin_group()
</code>

- Starts a group block.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.end_group()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.end_group()
</code>

- Ends a group block.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.begin_child(id: string, width: number, height: number, border?: boolean, flags?: number): boolean

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.begin_child(id: string, width: number, height: number, border?: boolean, flags?: number): boolean
</code>

- Begins a child/groupbox section. Returns opened state.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.end_child()

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.end_child()
</code>

- Ends the current child/groupbox section.

### Style stack helpers

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.push_color(color_name: string, color: table)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.push_color(color_name: string, color: table)
</code>

- Pushes a temporary ImGui color.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.pop_color(count?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.pop_color(count?: number)
</code>

- Pops one or more pushed colors.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.push_style_var(style_name: string, ...values)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.push_style_var(style_name: string, ...values)
</code>

- Pushes a temporary style var.

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.pop_style_var(count?: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.pop_style_var(count?: number)
</code>

- Pops one or more pushed style vars.

### Draw helpers

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.draw_line(x1, y1, x2, y2, color, thickness?)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.draw_line(x1, y1, x2, y2, color, thickness?)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.draw_rect(x, y, w, h, color, rounding?, thickness?)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.draw_rect(x, y, w, h, color, rounding?, thickness?)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.draw_rect_filled(x, y, w, h, color, rounding?)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.draw_rect_filled(x, y, w, h, color, rounding?)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.draw_circle(x, y, radius, color, segments?, thickness?)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.draw_circle(x, y, radius, color, segments?, thickness?)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.draw_circle_filled(x, y, radius, color, segments?)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.draw_circle_filled(x, y, radius, color, segments?)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.draw_text(x, y, color, text)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.draw_text(x, y, color, text)
</code>

- Draw-list primitives in current window space.

### Cursor/window helpers

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.get_cursor_pos(): (x: number, y: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.get_cursor_pos(): (x: number, y: number)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.set_cursor_pos(x: number, y: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.set_cursor_pos(x: number, y: number)
</code>

<div style="opacity: 0; height: 0; width: 0; overflow: hidden; pointer-events: auto;">

### ui.get_window_size(): (w: number, h: number)

</div>

<code class="language-typescript" style="text-align:center; font-size:16px; white-space:pre-wrap; word-break:break-word;">
ui.get_window_size(): (w: number, h: number)
</code>

- Cursor/window helper functions.

---

### example 1: simple (checkbox + slider)

```lua
local ui = secret.ui

local window_id = "example_simple_window"
local state = {
    enabled = false,
    power = 40
}

local function render_simple()
    local changed_enabled
    changed_enabled, state.enabled = ui.checkbox("enabled", state.enabled)
    ui.tooltip("turn this on or off")

    local changed_power
    changed_power, state.power = ui.slider_int("power", state.power, 0, 100, "%d%%")
    ui.tooltip("controls the power level")
end

if not ui.window_exists(window_id) then
    ui.window_register(window_id, "simple menu", render_simple, {
        visible = true,
        open = true,
        size = { x = 320, y = 180 },
        no_collapse = true
    })
end
```

### example 2: tabs + checkboxes + colors + tooltips

```lua
local ui = secret.ui

local window_id = "example_tabs_window"
local state = {
    left_tab = 1,
    right_tab = 1,
    legit = true,
    visuals = true,
    bhop = false,
    accent = { r = 120, g = 170, b = 255, a = 255 },
    glow = { r = 255, g = 120, b = 80, a = 160 },
    mode = 1
}

local function render_tabs()
    local window_w, window_h = ui.get_window_size()
    local child_w = (window_w - 42) * 0.5

    local left_open = ui.begin_child("left group##example2", child_w, 0, true)
    if left_open then
        local left_tab_changed
        left_tab_changed, state.left_tab = ui.tabs("left_tabs", state.left_tab, { "main", "extra" })
        ui.separator()

        if state.left_tab == 1 then
            local changed_legit
            changed_legit, state.legit = ui.checkbox("legit enabled", state.legit)
            ui.tooltip("main legit toggle")

            local changed_visuals
            changed_visuals, state.visuals = ui.checkbox("visuals enabled", state.visuals)
            ui.tooltip("main visuals toggle")
        else
            local changed_bhop
            changed_bhop, state.bhop = ui.checkbox("auto bhop", state.bhop)
            ui.tooltip("example extra movement option")

            local changed_mode
            changed_mode, state.mode = ui.combo_simple("mode", state.mode, { "silent", "balanced", "aggressive" })
            ui.help_marker_inline("switches behavior mode")
        end
    end
    ui.end_child()

    ui.same_line()

    local right_open = ui.begin_child("right group##example2", child_w, 0, true)
    if right_open then
        local right_tab_changed
        right_tab_changed, state.right_tab = ui.tabs("right_tabs", state.right_tab, { "colors", "glow" })
        ui.separator()

        if state.right_tab == 1 then
            ui.text("accent")
            local changed_accent
            changed_accent, state.accent = ui.color_picker_inline("accent_inline", state.accent, {
                compact = true,
                use_inputs = false
            }, {
                inline = true,
                spacing = 8
            })
            ui.tooltip("menu accent color")

            if changed_accent then
                ui.window_set_color(window_id, "Scheme", state.accent)
            end
        else
            ui.text("shadow glow")
            local changed_glow
            changed_glow, state.glow = ui.color_picker_inline("shadow_inline", state.glow, {
                compact = true,
                use_inputs = false
            }, {
                inline = true,
                spacing = 8
            })
            ui.tooltip("outside glow color")

            if changed_glow then
                ui.window_set_color(window_id, "Shadow", state.glow)
            end
        end
    end
    ui.end_child()
end

if not ui.window_exists(window_id) then
    ui.window_register(window_id, "tabs menu", render_tabs, {
        visible = true,
        open = true,
        size = { x = 430, y = 310 },
        no_collapse = true
    })
end
```

### example 3: tung tung menu (simple custom theme)

```lua
local ui = secret.ui

local window_id = "tung_tung_menu"
local state = {
    tab = 1,
    enabled = true,
    tung_power = 65,
    mode = 1,
    accent = { r = 255, g = 145, b = 82, a = 255 },
    shadow = { r = 255, g = 126, b = 72, a = 145 }
}

local theme_applied = false

local function apply_theme()
    ui.window_set_options(window_id, { glow = true })

    ui.window_set_style(window_id, {
        window_padding = { x = 14, y = 14 },
        item_spacing = { x = 9, y = 9 },
        item_inner_spacing = { x = 7, y = 6 },
        window_rounding = 8,
        child_rounding = 7,
        frame_rounding = 6,
        tab_rounding = 6,
        grab_rounding = 5,
        window_border_size = 1,
        child_border_size = 1,
        frame_border_size = 1
    })

    ui.window_set_color(window_id, "Text", 236, 226, 212, 255)
    ui.window_set_color(window_id, "TextDisabled", 154, 142, 130, 255)
    ui.window_set_color(window_id, "WindowBg", 24, 18, 16, 245)
    ui.window_set_color(window_id, "ChildBg", 35, 26, 22, 255)
    ui.window_set_color(window_id, "Border", 88, 64, 52, 255)
    ui.window_set_color(window_id, "FrameBg", 51, 37, 31, 255)
    ui.window_set_color(window_id, "FrameBgHovered", 74, 52, 42, 255)
    ui.window_set_color(window_id, "FrameBgActive", 92, 64, 52, 255)
    ui.window_set_color(window_id, "Button", 66, 47, 39, 255)
    ui.window_set_color(window_id, "ButtonHovered", 93, 64, 52, 255)
    ui.window_set_color(window_id, "ButtonActive", 112, 76, 61, 255)
    ui.window_set_color(window_id, "Header", 72, 51, 42, 255)
    ui.window_set_color(window_id, "HeaderHovered", 101, 69, 55, 255)
    ui.window_set_color(window_id, "HeaderActive", 120, 81, 64, 255)
    ui.window_set_color(window_id, "Tab", 58, 42, 35, 255)
    ui.window_set_color(window_id, "TabHovered", 87, 60, 48, 255)
    ui.window_set_color(window_id, "TabActive", 107, 72, 57, 255)
    ui.window_set_color(window_id, "CheckMark", state.accent)
    ui.window_set_color(window_id, "SliderGrab", state.accent)
    ui.window_set_color(window_id, "Scheme", state.accent)
    ui.window_set_color(window_id, "Shadow", state.shadow)
end

local function render_custom()
    if not theme_applied then
        apply_theme()
        theme_applied = true
    end

    local window_w, window_h = ui.get_window_size()

    local tab_changed
    tab_changed, state.tab = ui.tabs("tung_tabs", state.tab, { "main", "colors" })
    ui.separator()

    if state.tab == 1 then
        local changed_enabled
        changed_enabled, state.enabled = ui.checkbox("enable tung tung", state.enabled)
        ui.tooltip("master toggle for tung tung mode")

        local changed_power
        changed_power, state.tung_power = ui.slider_int("tung power", state.tung_power, 0, 100, "%d%%")
        ui.tooltip("how strong the tung tung effect is")

        local changed_mode
        changed_mode, state.mode = ui.combo_simple("sahur mode", state.mode, { "chill", "normal", "loud" })
    else
        ui.text("accent")
        local changed_accent
        changed_accent, state.accent = ui.color_picker_inline("accent_picker", state.accent, {
            compact = true,
            use_inputs = false
        }, {
            inline = true,
            spacing = 8
        })

        ui.text("shadow glow")
        local changed_shadow
        changed_shadow, state.shadow = ui.color_picker_inline("shadow_picker", state.shadow, {
            compact = true,
            use_inputs = false
        }, {
            inline = true,
            spacing = 8
        })

        if changed_accent then ui.window_set_color(window_id, "Scheme", state.accent) end
        if changed_accent then ui.window_set_color(window_id, "CheckMark", state.accent) end
        if changed_accent then ui.window_set_color(window_id, "SliderGrab", state.accent) end
        if changed_shadow then ui.window_set_color(window_id, "Shadow", state.shadow) end
    end

    ui.draw_text(12, window_h - 22, { r = 165, g = 146, b = 124, a = 255 }, "current user: tung tung")
end

if not ui.window_exists(window_id) then
    ui.window_register(window_id, "tung tung menu", render_custom, {
        visible = true,
        open = true,
        size = { x = 460, y = 320 },
        no_collapse = true
    })
end
```

<div hidden>

```ts

```

</div>
