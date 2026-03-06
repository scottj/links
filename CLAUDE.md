# Links

A single-file bookmarks website. All content lives in `index.html`.

## Architecture

- **Single file**: `index.html` — vanilla HTML/CSS/JS, zero dependencies
- **Data**: `pages` array as JSON in `<script id="pages-data" type="application/json">` in `<head>`, parsed in the module script
- **App logic**: `<script type="module">` in `<body>`

## Data Structure

Each page object:
```js
{ slug, title, category, links: [{ name, url, desc?, children?, internal? }], html? }
```

- `category: null` pages are hidden from category views but reachable via internal links (`#page/<slug>`)
- `html` property is used for pre-formatted content pages (rendered as raw HTML instead of link lists)
- `internal: true` links use `#page/<slug>` for in-app navigation

## Routing

Client-side hash routing:
- `#` — home (category cards grid)
- `#<Category>` — category detail view
- `#<Category>/<slug>` — page detail view
- `#page/<slug>` — direct page access (for uncategorized pages)

## Style Conventions

- Font: Helvetica, Arial, sans-serif; 16px base
- `<style>` uses 2-space indent, starts with `* { box-sizing: border-box; }`
- `<script type="module">` uses 2-space indent; top-level code is not indented
- Layout: 80% width centered container, max-width 1200px; full-width on mobile
- Markdown escape sequences (e.g. `\_`) in source files must be cleaned when importing

## Audit Tool

`audit.html` — standalone page for reviewing all link data. Fetches and parses the JSON data from `index.html` at runtime.

Features:
- Flattens all pages/links into a sortable, filterable table
- Filters: text search, category dropdown, page dropdown, flagged-only toggle
- Grouping: optional "group by page" view with section headers
- Flags detected: `uncategorized`, `empty-url`, `internal`, `has-children`, `has-html`, `empty-page`, `child`, `http` (non-HTTPS)
- Stats summary: total pages, rows, categories, uncategorized count, empty pages, HTTP links
