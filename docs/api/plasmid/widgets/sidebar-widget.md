# Sidebar Widget

Provides a sidebar using Vanilla scoreboards.  
Has a limit of 15 lines at once, which can be bypassed by using a [ScrollableSidebarWidget](scrollable-sidebar-widget.md)

--8<-- [start:content]

### Constructors

---

- SidebarWidget()
- SidebarWidget(Predicate&lt;ServerPlayer&gt;)
- SidebarWidget(Component)
- SidebarWidget(Component, Predicate&lt;ServerPlayer&gt;)

### getPriority()

---

Returns the priority that this sidebar will display as

### setPriority()

---

Sets the priority that this sidebar will display as

### getDefaultNumberFormat()

---

Gets the number format used for this sidebar

### setDefaultNumberFormat(NumberFormat)

---

Sets the number format used for this sidebar (usually used to hide the index of each line)

### getUpdateRate()

---

How often this sidebar will update in ticks

### setUpdateRate(int)

---

Sets how often the sidebar will update in ticks

### getTitle()

---

Gets the title used for this sidebar

### setTitle(Component)

---

Sets the title used for this sidebar

### setLine(int, Component)

### setLine(SidebarLine)

---

Sets the content of the line at the given index  
Can also be called with a NumberFormat to set the number format of this specific line

### addLines(SidebarLine)

### addLines(Component...)

---

Adds lines in bulk

### removeLine(SidebarLine)

### removeLine(int)

---

Removes the specified line, either by SidebarLine or its index

### getLine(int)

---

Gets the line at this index

### replaceLines(Component...)

### replaceLines(SidebarLine...)

### replaceLines(LineBuilder)

---

Clears previous lines and replaces them with the arguments

### clearLines()

---

Clears all lines

### set(Consumer&lt;LineBuilder&gt;)

---

Replaces all lines with the result of the LineBuilder

<!-- prettier-ignore -->
??? info "Game Widget inherited methods"
    --8<-- "api/plasmid/widgets/game-widget.md:content"
--8<-- [end:content]
