# 📚 Bookshelf — Reading Tracker

**Bookshelf** is a fast, lightweight, privacy-focused single-page application (SPA) designed to log, structure, and track your personal reading catalog. Operating completely within the browser client, it strips out bulky server setups and tracks your data locally or syncs with your choice of file backups and cloud solutions.

<img width="562" height="875" alt="image" src="https://github.com/user-attachments/assets/dbb3ea76-0c31-4c97-ba40-7b611564d3a5" />
<img width="524" height="249" alt="image" src="https://github.com/user-attachments/assets/bb9b0429-0831-4639-847a-978e98298e31" />
<img width="537" height="877" alt="image" src="https://github.com/user-attachments/assets/44979cc1-e807-4d2d-88c2-fd1a20e9708e" />
<img width="529" height="249" alt="image" src="https://github.com/user-attachments/assets/5e758360-03d8-4253-a399-1d9f730d1f18" />

---

## ✨ Features

* **Multiple Entry Layouts:** 
  * *Manual Input:* Rapidly bind titles and authors to your digital shelves.
  * *Goodreads Import:* Directly paste raw Goodreads HTML/curl data to automatically extract title, author, and native cover images.
* **Automated Metadata Enrichments:** Automatically queries the Open Library API to fetch matching book covers and cross-verify author names.
* **Interactive Shelf Management:** 
  * Organize status groups: *Reading Now*, *To Be Read (TBR)*, and *Already Read*.
  * Native HTML5 Drag-and-Drop handles seamless multi-shelf triage and visual sorting.
  * Built-in fallback controls allow fluid, mobile-friendly click/tap layout sorting.
* **Granular Logs & Tracking:** Log custom star ratings, format preferences (Physical, E-Book, Audio), read status toggles, and formatted inline reading logs/notes.
* **Flexible Storage & Backups:** 
  * Default pipeline auto-commits logs locally to `localStorage`.
  * Native file utility controls allow raw export/import files straight from system storage (iPhone Files app only).
  * Features dedicated cloud synchronization linking support directly into **Google Drive** systems.
* **App-Style Mobile Experience:** Includes responsive mobile styling (`viewport-fit=cover`), standalone apple-mobile configuration flags, and hidden scroll collapsers.

---

## 🛠️ Architecture & Tech Stack

This project is optimized as an zero-dependency standalone web client:
* **Frontend Viewport:** Semantic `HTML5` with custom mobile safe views.
* **Visual Engine:** Modular `CSS3` with native shimmers, radial backdrop color spots, custom fonts (Pirata One, Cormorant Garamond, Quicksand, IBM Plex Mono), and color variables.
* **Client Logic:** Standard modern asynchronous `Vanilla JavaScript (ES6)` handling DOM building, data normalization pipelines, parser implementations, and layout hooks.
* **Integrations:** Google Identity Services client script, Open Library API search hooks.

---

## 📂 Internal Data Shape

Books match a strict layout schema ensuring safe persistence:

```json
{
  "id": "b171923456789xabcdef",
  "title": "Example Book Title",
  "author": "Author Name",
  "cover": "https://openlibrary.org",
  "formats": ["physical", "ebook"],
  "rating": 5,
  "notes": "Custom personal reading log entries...",
  "dateStarted": "2026-07-01",
  "dateCompleted": "2026-07-05"
}
```

Library states split cleanly into three indexed array structures: `{ reading: [], tbr: [], read: [] }`.

---

## 📱 Make one for yourself

1. Download `index.html` and add to your own repo 
1. Host it free on [GitHub pages](https://docs.github.com/en/pages)
2. To use Google Drive for data sync, you'll need to get [Google API Client ID](https://developers.google.com/identity/oauth2/web/guides/get-google-api-clientid)
    * Go to console.cloud.google.com → create a new project (any name, e.g. "Stacks Backup").
    * APIs & Services → Library → search "Google Drive API" → Enable.
    * APIs & Services → OAuth consent screen → User type: External → fill in app name + your email → under Scopes, add .../auth/drive.file → under Test users, add your own Google account email → Save (leave it in Testing mode, that's fine for personal use).
    * APIs & Services → Credentials → Create Credentials → OAuth Client ID → Application type: Web application.
    * Under Authorized JavaScript origins, add your exact GitHub Pages URL (e.g. https://yourusername.github.io, no trailing slash or path).
    * Click Create — copy the Client ID (looks like 123456789-abc.apps.googleusercontent.com).
3. To use Goodreads HTML to add a book
    * Desktop browser: Copy the Response HTML in the Network tab from `GET https://www.goodreads.com/book/show/<book path>`
    * iPhone Shortcut: Build a Shortcut with these steps
        1. "Ask for Input": Ask for <Text> with <Prompt>
        2. "Get URLs from Input": Get URLs from <Ask for Input>
        3. "Get Contents of URL": Get contents of <URLs>
        4. "Make HTML from Rich Text": Make HTML from <Contents of URL>
        5. "Copy to Clipboard": Copy <HTML from Rich Text> to clipboard
