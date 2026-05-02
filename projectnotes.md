# Project Notes — Google Search Clone

Personal notes on what was learned and how things work in this project.

---

## 1. HTML Forms

A form is how a webpage sends data somewhere. Every search bar you've ever used is a form.

```html
<form action="https://www.google.com/search" method="GET">
    <input type="text" name="q">
    <button type="submit">Search</button>
</form>
```

- `action` — the URL the form sends data to
- `method="GET"` — data is sent in the URL (you can see it in the address bar)
- `name="q"` — the name of the data being sent. Google reads `q` as the search query
- `type="submit"` — clicking this button sends the form

When you type "cats" and hit search, the browser goes to:
```
https://www.google.com/search?q=cats
```
The `?q=cats` part is called a **query string**. The form built it automatically.

---

## 2. Query Parameters

Query parameters are key=value pairs added to a URL after a `?`.
Multiple parameters are separated by `&`.

```
https://www.google.com/search?q=cats&tbm=isch
                               ↑         ↑
                           search term   image search flag
```

### Parameters used in this project

| Parameter | Value | What it does |
|-----------|-------|--------------|
| `q` | your search | the main search query |
| `tbm` | `isch` | switches to image results (tbm = "to be matched") |
| `btnI` | `I` | "I'm Feeling Lucky" — jumps to the first result |
| `as_q` | words | all these words must appear |
| `as_epq` | phrase | this exact phrase must appear |
| `as_oq` | words | any of these words must appear |
| `as_eq` | words | none of these words should appear |

### Hidden inputs

To send a parameter without showing the user a text box, use a hidden input:

```html
<input type="hidden" name="tbm" value="isch">
```

The browser still sends it — the user just can't see or change it.

---

## 3. Linking Pages Together

Pages link to each other with anchor tags:

```html
<a href="image.html">Images</a>
```

- `href` is the path to the file you want to go to
- Both files must be in the **same folder** for this to work
- If the file were in a subfolder: `href="pages/image.html"`

### Why `href="#"` sometimes

During development you might see `href="#"`. The `#` means "link to nowhere"
— it stops the page jumping anywhere. It's a placeholder until you have a real
destination.

---

## 4. Separate CSS File

Instead of writing CSS inside `<style>` tags in every HTML file, we write it
once in `styles.css` and link it in each page:

```html
<head>
    <link rel="stylesheet" href="styles.css">
</head>
```

- `rel="stylesheet"` tells the browser what kind of file it is
- `href="styles.css"` is the path to the file

**Why this matters:**
- Change the button colour once in `styles.css` → it updates on all three pages
- HTML files stay clean and readable — they only contain content
- This is called **separation of concerns** — HTML for structure, CSS for style

---

## 5. The Box Model

Every HTML element is a rectangular box. The box has four layers:

```
┌──────────────────────────┐
│         margin           │  ← space outside the border
│  ┌────────────────────┐  │
│  │      border        │  │  ← the visible line
│  │  ┌──────────────┐  │  │
│  │  │   padding    │  │  │  ← space inside the border
│  │  │  ┌────────┐  │  │  │
│  │  │  │content │  │  │  │  ← the actual text or element
│  │  │  └────────┘  │  │  │
│  │  └──────────────┘  │  │
│  └────────────────────┘  │
└──────────────────────────┘
```

We used this everywhere:
- `padding: 0 16px` — space inside the search bar so text doesn't touch the edges
- `margin-top: 20px` — space above the buttons
- `border: 1px solid #dfe1e5` — the light grey line around the search bar

### `box-sizing: border-box`

By default, `width` does not include padding or border — which causes sizing
headaches. Adding this at the top of the CSS fixes it:

```css
* {
    box-sizing: border-box;
}
```

Now `width: 500px` means the whole box is 500px, padding included.

---

## 6. Flexbox

Flexbox is a CSS layout tool for arranging things in a row or column.
We used it to centre the search bar and buttons.

```css
.page {
    display: flex;
    flex-direction: column; /* stack children top to bottom */
    align-items: center;    /* centre horizontally */
    justify-content: center;/* centre vertically */
    min-height: 100vh;      /* fill the full screen height */
}
```

- `display: flex` — turns on flexbox for that element
- `flex-direction: column` — children stack vertically (default is row)
- `align-items: center` — centres children on the cross axis (horizontal when column)
- `justify-content: center` — centres children on the main axis (vertical when column)
- `min-height: 100vh` — `vh` means viewport height. `100vh` = full screen height.

---

## 7. Position: Absolute

Normal elements sit in the page flow — each one pushes the next one down.
`position: absolute` removes an element from that flow so it can be placed
anywhere on the page.

```css
nav {
    position: absolute;
    top: 15px;
    right: 20px;
}
```

This pins the nav to exactly 15px from the top and 20px from the right —
regardless of what else is on the page. We used this for the navigation links
so they float in the corner without affecting the centred content below.

---

## 8. CSS Selectors

Selectors choose which HTML elements to style.

```css
/* Element selector — styles ALL <a> tags */
a { color: blue; }

/* Class selector — styles elements with class="btn" */
.btn { background: grey; }

/* Attribute selector — styles <input type="text"> only */
input[type="text"] { border-radius: 24px; }

/* Pseudo-class — styles an element on hover */
.btn:hover { background: darkgrey; }

/* Pseudo-class — styles a focused input */
input:focus { box-shadow: 0 0 0 2px blue; }
```

---

## 9. The Table Layout (Advanced Search)

We used an HTML `<table>` to line up the labels and inputs neatly in two columns.

```html
<table>
    <tr>                                    <!-- table row -->
        <td>all these words:</td>           <!-- left cell (label) -->
        <td><input type="text"></td>        <!-- right cell (input) -->
    </tr>
</table>
```

- `<tr>` = table row
- `<td>` = table data (a cell)
- `text-align: right` on the first `<td>` makes all labels right-align neatly
- `border-collapse: collapse` removes the default gaps between cells

---

## 10. Colour Reference

Google's brand colours used throughout:

| Colour | Hex | Used for |
|--------|-----|----------|
| Google Blue | `#4285F4` | G, second g, links, focus ring |
| Google Red | `#EA4335` | o, e |
| Google Yellow | `#FBBC05` | second o |
| Google Green | `#34A853` | l |
| Dark text | `#202124` | body text, nav links |
| Grey text | `#70757a` | "Images" sub-label |
| Light border | `#dfe1e5` | search bar border |
| Button grey | `#f8f9fa` | default button background |
| Button blue | `#1a73e8` | Advanced Search button |

---

## 11. Things to Remember

- Always write `<!DOCTYPE html>` at the top — tells the browser this is HTML5
- Always add `lang="en"` to `<html>` — helps screen readers and search engines
- Always add a `<title>` — shows in the browser tab
- `method="GET"` puts form data in the URL — good for searches
- `method="POST"` hides form data in the request body — good for passwords
- CSS is read top to bottom — later rules override earlier ones
- When something isn't centring, it's usually a flexbox or width issue