# flex-control

**flex-control** is a lightweight FSCSS-based plugin for flexbox layout utilities. It provides a collection of single-call macros that cover the most common flex patterns — centering, alignment, direction, wrapping, spacing, and responsive layouts — without writing repetitive boilerplate.

* **Alignment shortcuts:** instant centering on both axes (`flex-center`), horizontal-only (`flex-x`), vertical-only (`flex-y`), or no alignment (`flex`).
* **Distribution helpers:** `flex-between`, `flex-around`, and `flex-even` for common `justify-content` patterns, all with `align-items: center` included.
* **Direction variants:** `flex-col`, `flex-col-center`, and `flex-row-center` for explicit direction control.
* **Wrap support:** `flex-wrap` and `flex-wrap-center` for wrapping containers.
* **Gap utilities:** `flex-gap(size)`, `flex-col-gap(size)`, and `flex-stack(gap)` for spaced layouts.
* **Power macros:** `flex-layout(dir, justify, align, gap)` for full control in one call, `flex-equal(gap)` for equal-width children, and `flex-responsive(gap)` for wrap + gap combos.
* **Edge cases:** `flex-inline` for inline-flex, `flex-stretch`, `flex-start`, and `flex-end`.

flex-control is implemented entirely in FSCSS, following the same **FSCSS plugin logic** as libraries like [st-core](https://github.com/fscss-ttr/st-core.fscss).

## Installation

Include FSCSS v1.1.24 or higher, then import **flex-control** via `@import`:

```html
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.24/exec.min.js" defer></script>
```

This (better)

```
@import(exec(_init flex-control))
```

Or this

```
@import((*) from flex-control)
```

The library supports FSCSS **1.1.24+**. Once imported, all `flex-*` macros are available in your stylesheet.

## Usage

### Basic centering

```css
.hero {
  @flex-center()
}

.header {
  @flex-between()
}

.icon-wrap {
  @flex-inline()
}
```

### Direction and stacking

```css
.sidebar {
  @flex-col()
}

.modal {
  @flex-col-center()
}

.card-list {
  @flex-stack(16px)
}
```

### Gap utilities

```css
.toolbar {
  @flex-gap(12px)
}

.form-fields {
  @flex-col-gap(8px)
}
```

### Wrapping and responsive

```css
.tag-list {
  @flex-wrap()
}

.grid {
  @flex-responsive(20px)
}
```

### Equal-width children

```css
.tabs {
  @flex-equal(2px)
}
```

All children of `.tabs` will have `flex: 1`, making them share available space equally.

### Full control with `flex-layout`

```css
.custom {
  @flex-layout(row, space-between, flex-start, 24px)
}
```

This expands to:

```css
.custom {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: flex-start;
  gap: 24px;
}
```

## Example

```html
<script src="https://cdn.jsdelivr.net/npm/fscss@1.1.24/exec.min.js" defer></script>
<style>
@import(exec(*) from flex-control)

body {
  @flex-col()
  min-height: 100vh;
}

header {
  @flex-between()
  padding: 0 24px;
  height: 60px;
}

.nav-links {
  @flex-gap(24px)
}

main {
  @flex-center()
  flex: 1;
}

.card-grid {
  @flex-responsive(20px)
}

.card {
  @flex-col-gap(12px)
  padding: 20px;
  border-radius: 12px;
}

.card-footer {
  @flex-between()
}

.badge {
  @flex-inline()
  gap: 6px;
}

.tabs {
  @flex-equal(1px)
}
</style>

<header>
  <span class="logo">Figsh</span>
  <nav class="nav-links">
    <a href="#">Docs</a>
    <a href="#">Plugins</a>
    <a href="#">GitHub</a>
  </nav>
</header>

<main>
  <div class="card-grid">
    <div class="card">
      <h3>Revenue</h3>
      <p>$1.2M</p>
      <div class="card-footer">
        <span class="badge">↑ 5%</span>
        <small>vs last month</small>
      </div>
    </div>
  </div>
</main>
```

In this example, every layout concern is handled by a single `flex-*` call. No manually written `display: flex` blocks anywhere.

## Plugin Reference

| Macro | Output summary |
|---|---|
| `@flex()` | `display: flex` |
| `@flex-center()` | flex + center both axes |
| `@flex-x()` | flex + `justify-content: center` |
| `@flex-y()` | flex + `align-items: center` |
| `@flex-between()` | flex + space-between + center |
| `@flex-around()` | flex + space-around + center |
| `@flex-even()` | flex + space-evenly + center |
| `@flex-col()` | flex + column direction |
| `@flex-col-center()` | flex + column + centered |
| `@flex-row-center()` | flex + row + centered |
| `@flex-wrap()` | flex + wrap |
| `@flex-wrap-center()` | flex + wrap + centered |
| `@flex-start()` | flex + flex-start + center |
| `@flex-end()` | flex + flex-end + center |
| `@flex-stretch()` | flex + stretch |
| `@flex-inline()` | inline-flex + center |
| `@flex-gap(size)` | flex + gap |
| `@flex-col-gap(size)` | flex + column + gap |
| `@flex-stack(gap)` | flex + column + gap (alias) |
| `@flex-responsive(gap)` | flex + wrap + gap |
| `@flex-equal(gap)` | flex + gap + `> * { flex: 1 }` |
| `@flex-layout(dir, justify, align, gap)` | full flex shorthand |

## License

flex-control is open source and free to use under the MIT License.
