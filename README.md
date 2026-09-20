# Notes Master

A polished, responsive **offline-first Notes Master App** built with HTML, CSS and vanilla JavaScript.

The application is designed as a complete personal note-taking workspace rather than a simple textarea demo. Notes are persisted in the browser with `localStorage`, so the core experience works without a backend or database.

## Features

### Note management
- Create notes instantly
- Edit title and rich note body
- Autosave changes locally
- Duplicate notes
- Pin important notes
- Favorite notes
- Archive notes
- Move notes to trash
- Permanently delete notes from trash
- Move notes between folders

### Rich editor
- Bold
- Italic
- Underline
- Strikethrough
- Heading 2
- Bulleted lists
- Numbered lists
- Blockquotes
- Checklist insertion
- Code block
- Links
- Clear formatting

### Organization
- All notes
- Pinned
- Favorites
- Archive
- Trash
- Custom folders
- Folder note counts

### Search and sorting
Searches across:
- Note titles
- Note body text
- Tags stored with the note

Sorting options:
- Recently updated
- Recently created
- Title A–Z
- Favorites first
- Pinned first

### Workspace features
- Dark / light theme
- Focus mode
- Responsive mobile layout
- Keyboard shortcuts
- Word count
- Relative update times
- Empty states
- Toast notifications
- Print note
- Copy note text

### Backup
Notes and folders can be:
- Exported to JSON
- Imported from a JSON backup

This makes it possible to move the local note collection between browsers/devices manually.

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl/Cmd + N` | Create a new note |
| `/` | Focus search |
| `Esc` | Close modal / mobile editor |

## Project Structure

```text
Notes-Master/
├── index.html
├── README.md
├── css/
│   └── style.css
├── js/
│   └── app.js
└── assets/
    └── icons/
        └── favicon.svg
```

### `index.html`
Defines the application shell:
- Sidebar navigation
- Search and toolbar
- Notes list
- Editor
- Modals
- Import control

### `css/style.css`
Contains:
- Design tokens
- Light/dark themes
- Sidebar styling
- Notes cards
- Editor styling
- Rich text presentation
- Responsive breakpoints
- Focus mode
- Modals and toast UI

### `js/app.js`
Contains the complete application logic:
- LocalStorage persistence
- CRUD operations
- Search
- Sorting
- Folder management
- Note state changes
- Rich text commands
- Import/export
- Keyboard shortcuts
- Theme persistence
- Responsive editor behavior

## Data Model

A note is stored approximately as:

```js
{
  id: "unique-id",
  title: "My note",
  body: "<p>Rich text content</p>",
  tags: [],
  folderId: "work",
  pinned: false,
  favorite: true,
  archived: false,
  trashed: false,
  createdAt: "2026-09-20T00:00:00.000Z",
  updatedAt: "2026-09-20T00:00:00.000Z"
}
```

Folders are stored separately:

```js
{
  id: "work",
  name: "Work"
}
```

## Storage

The app uses browser `localStorage`.

Storage keys:
- `notes-master-v1-notes`
- `notes-master-v1-folders`
- `notes-theme`

Because the app is client-side, clearing browser storage will remove locally stored notes. Use **Export** regularly when the notes matter.

## Architecture

The project intentionally avoids frameworks and build tooling.

```text
Browser
   │
   ├── index.html
   │      └── UI structure
   │
   ├── css/style.css
   │      └── visual system + responsive layout
   │
   └── js/app.js
          ├── State
          ├── LocalStorage
          ├── Search / Sort
          ├── Folder management
          ├── Rich editor commands
          └── Rendering
```

## How Autosave Works

Whenever the note title or body changes:
1. The selected note is updated in memory.
2. `updatedAt` is refreshed.
3. The state is saved to `localStorage`.
4. The note list is refreshed.
5. The UI briefly shows `Saving…`, then `Saved`.

No server round trip is required.

## Search Behavior

The search field performs a client-side case-insensitive match against:
- title
- plain-text note body
- tag values

This makes the search immediate even when the application is running offline.

## Rich Text Behavior

The editor uses the browser's `contenteditable` capability and `document.execCommand` for simple formatting operations.

This keeps the application dependency-free. It also means the stored body is HTML rather than Markdown or a document format.

## Backup / Restore

### Export
The **Export** action produces a JSON file containing:
- application metadata
- folders
- notes

### Import
The **Import** action accepts a compatible JSON backup and replaces the current local note collection with the imported one.

For production use, validate backups carefully before importing them.

## Security and Privacy

The application does not send note contents to a server.

Notes are stored locally in the user's browser.

The app therefore provides local privacy by default, but it should not be treated as an encrypted vault. Browser storage is not the same as end-to-end encryption.

## Running Locally

No dependency installation is necessary.

You can open `index.html` directly in a browser.

For local development, a simple static server is also suitable:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

## Browser Support

Use a modern browser with support for:
- `localStorage`
- `contenteditable`
- Fetch/Blob APIs
- CSS Grid
- CSS variables
- Modern JavaScript

## Future Enhancements

Natural next additions for a larger production version include:
- Markdown mode
- Rich tag management UI
- Note color themes
- Drag-and-drop folders
- Encrypted local storage
- IndexedDB for much larger note collections
- Cloud sync
- Account authentication
- Cross-device synchronization
- Collaborative notes
- Attachments
- Voice notes
- PWA installation
- Service-worker offline caching
- Version history and undo snapshots

## License

Use a license appropriate to the way you plan to distribute or publish the project.

---

**Notes Master** is designed to be a clean portfolio-quality static application that demonstrates client-side state management, UI architecture, rich text editing, persistence, search, organization and backup workflows.
