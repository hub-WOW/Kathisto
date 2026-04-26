# Kathisto
- **Kathisto** is an easy to use, highly customisable markdown engine, meant for beginners to create their own websites. 
- *Kathisto* means *Καθιστώ* in Greek, meaning 'to render'.
- It handles LaTeX, Code Syntax Highlighting, Spacing, Navigation Bars, Colours, Styles, and Headers making it very convinient for making good static web-pages quickly.

## 🍱 Layout Engine (`layout.js`)

The `Layout` component manages global UI elements like the sidebar, top navigation bar, and hero sections.

### `Layout.init(config?)`
Initializes the core UI. It injects the sidebar, sets up the resize handle logic, and handles active link highlighting.

**Configuration Options:**
- `topBarLinks` (Array): An optional array to override the global top-navigation links for a specific page.

### `Layout.renderHero(containerId, options)`
Renders a stylized hero section with a gradient title and tagline.
- `logo`: Path to a logo image.
- `title`: Primary heading (rendered with a blue-green gradient).
- `subtitle`: Descriptive paragraph.
- `tagline`: Bold monospace footer text (red).

---

## 🧠 Markdown Engine (`md-engine.js`)

The rendering engine transforms raw Markdown into accessible, interactive HTML sections.

### `MdEngine.render(markdownText, rootEl, tocEl)`
- **Parsing**: Uses `markdown-it` for reliable GFM support.
- **Math**: Native LaTeX support via `KaTeX` (use `$$` for blocks, `$` for inline).
- **Syntax Highlighting**: Automated block detection using `highlight.js`.
- **Auto-TOC**: Automatically generates a nested Table of Contents based on `#` headers.
- **Animations**: Wraps content in `.section-box` containers for entry transitions.
- **Scroll Spy**: Updates the sidebar navigation automatically as the user scrolls.

### `MdEngine.setupDragDrop(callback)`
- Utility to allow local `.md` file testing by dragging files directly into the browser window.
- It is useful for testing your markdown files locally.

---

## 🔗 Navigation Configuration

Each page manages its own top navigation via a simple data structure. This allows for complex, nested menus without modifying the core scripts.

### Data Structure Example
```javascript
const TOP_BAR_LINKS = [
    { name: 'Home', url: 'home.html' },
    {
        name: 'Dropdown', url: '#',
        children: [
            { name: 'Page A', url: 'a.html' },
            { 
                name: 'Nested', url: '#', 
                children: [
                    { name: 'Sub Page', url: 'sub.html' }
                ]
            }
        ]
    }
];
```

---

## 🎨 Design System (`styles.css`)

The look and feel is managed through CSS Variables (Custom Properties). To maintain consistency, use these variables:

| Variable | Purpose |
| :--- | :--- |
| `--bg-color` | Main background color (Black) |
| `--sidebar-bg` | Sidebar and panel backgrounds |
| `--accent-blue` | Primary brand/action color |
| `--accent-green` | Secondary / Success / Italic highlights |
| `--accent-red` | Warning / Critical / Bold highlights |
| `--text-primary` | Main body text |
| `--font-sans` | Primary UI font (Inter) |
| `--font-mono` | Technical/Data font (Roboto Mono) |

The CSS **can be modified** according to your needs. By default, it is *optimised for hub-WOW*.

### Custom Components

Kathisto includes built-in styling for custom components that you can embed directly in your Markdown using raw HTML:

- **`.btn-green`**: A stylish, interactive green button that fully supports embedded Markdown, KaTeX, and hyperlinks.
  - *Example Usage*: `<a href="#" class="btn-green">**Click Me** with $E=mc^2$ Math</a>`

---

## 📦 External Dependencies

The system relies on the following CDNs (ensure these are in your `<head>`):
1. **KaTeX**: Math typesetting.
2. **Markdown-it**: Markdown parsing.
3. **Highlight.js**: Code syntax highlighting.
4. **DOMPurify**: Security and XSS prevention.
5. **Google Fonts**: Inter & Roboto Mono.
