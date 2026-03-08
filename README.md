# Links

A personal bookmarks website — a single-page app for organizing and browsing a curated collection of links across various topics.

## Usage

Open `index.html` in a browser. No build step, no dependencies, no server required.

Browse by category from the home page, or navigate directly to any page via its URL hash.

## Auditing

`audit.html` provides a searchable, filterable table of all link data with automatic flagging of potential issues. It must be served over HTTP (e.g. `bunx serve .`) since it fetches data from `index.html` at runtime.
