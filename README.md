# Google Search Clone

A beginner-friendly front-end project that replicates the look and feel of Google Search using plain HTML and CSS — no frameworks, no JavaScript.

## Pages

| File | Description |
|------|-------------|
| `index.html` | Main Google Search page |
| `image.html` | Google Image Search page |
| `advanced.html` | Google Advanced Search page |
| `styles.css` | Shared stylesheet used by all three pages |

## How to Run

1. Download or clone the project folder
2. Make sure all four files are in the **same folder**
3. Open `index.html` in your browser — no server needed

## How the Pages Link Together

```
index.html  ──→  image.html
            ──→  advanced.html

image.html  ──→  index.html
            ──→  advanced.html

advanced.html ──→  index.html
              ──→  image.html
```

Every page has navigation links in the **top-right corner** to reach the other two pages.

## Features

- **Google Search** — type a query and click "Google Search" to see results
- **I'm Feeling Lucky** — skips the results page and goes straight to the first result
- **Image Search** — searches Google Images using the `tbm=isch` parameter
- **Advanced Search** — four filter fields sent to Google as special query parameters:

| Field | Parameter | Meaning |
|-------|-----------|---------|
| All these words | `as_q` | Every word must appear |
| Exact word or phrase | `as_epq` | Matches the phrase exactly |
| Any of these words | `as_oq` | At least one word must appear |
| None of these words | `as_eq` | Excludes these words |

## Project Structure

```
google/
├── index.html       ← Main search page
├── image.html       ← Image search page
├── advanced.html    ← Advanced search page
└── styles.css       ← All CSS, shared across pages
```

## How the CSS is Linked

Each HTML file loads the shared stylesheet in its `<head>`:

```html
<link rel="stylesheet" href="styles.css">
```

Both files must be in the same folder for this to work.

## Key Concepts Used

- **HTML forms** — `<form action="..." method="GET">` sends data to Google
- **Query parameters** — values like `name="q"` become `?q=your+search` in the URL
- **Separate CSS file** — keeps styling out of the HTML for cleaner, reusable code
- **`position: absolute`** — used to place the nav links in the top-right corner
- **Flexbox** — used to centre the search bar and buttons on the page
- **`border-radius`** — gives the search bar its rounded pill shape

## What I Learned / Built This For

This project is part of Harvard's CS50W (Web Programming with Python and JavaScript) — specifically the first assignment on HTML and CSS.
