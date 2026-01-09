# Pluto Blocks Web Book

A web-based interactive project book for **Pluto Blocks** - a visual block programming platform for Pluto nano drones. This single-page application provides comprehensive documentation and project tutorials for both **Pluto X** (Primus X2) and **Pluto 1.2** (Primus V4) drones.

## 📋 Table of Contents

- [Project Description](#project-description)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [How to Start the Project](#how-to-start-the-project)
- [JSON Structure](#json-structure)
- [Rules for Modifying JSON Files](#rules-for-modifying-json-files)
- [Understanding index.html](#understanding-indexhtml)
- [Features](#features)
- [Browser Compatibility](#browser-compatibility)

---

## 🎯 Project Description

**Pluto Blocks Web Book** is an interactive documentation platform that serves as a comprehensive guide for users learning to program Pluto drones using the Pluto Blocks visual programming environment. The application provides:

- **Introduction and Platform Overview**: Learn about Pluto drones, their hardware (Primus), and software (Magis)
- **Compatibility Information**: Understand which software versions and drone models are supported
- **Project Tutorials**: Step-by-step projects ranging from basic LED control to advanced flight behaviors
- **Multi-Board Support**: Switch between Pluto X (Primus X2) and Pluto 1.2 (Primus V4) documentation
- **Interactive Navigation**: Easy-to-use sidebar navigation with grouped projects and smooth scrolling

The project is built as a **static single-page application** that requires no build process or server-side rendering. All content is loaded dynamically from JSON configuration files.

---

## 📁 Project Structure

```
Plutoblocks-web-book/
│
├── index.html              # Main HTML file with embedded CSS and JavaScript
├── style.css               # Additional CSS styles
├── README.md               # This file
│
└── assets/
    ├── img/                # Image assets for projects and documentation
    │   ├── 0.jpg
    │   ├── 1.png
    │   └── ... (additional images)
    │
    ├── primus-v4.json      # Content configuration for Pluto 1.2 (Primus V4)
    └── primus-x2.json       # Content configuration for Pluto X (Primus X2)
```

### File Descriptions

- **`index.html`**: Contains the complete application structure, including:
  - HTML markup for sidebar navigation and main content area
  - Embedded CSS styles (dark theme with accent colors)
  - JavaScript for dynamic content loading and navigation
  - Board selector dropdown

- **`style.css`**: Additional CSS rules (currently contains sidebar-specific styles)

- **`assets/primus-v4.json`**: JSON configuration file containing all content for Pluto 1.2 board, including:
  - Introduction sections
  - Platform documentation
  - Project tutorials (p0-p3)

- **`assets/primus-x2.json`**: JSON configuration file containing all content for Pluto X board, including:
  - Introduction sections
  - Platform documentation
  - Project tutorials (p0-p23) organized into Basic and Intermediate groups

- **`assets/img/`**: Directory containing all images referenced in the JSON content files

---

## 🚀 Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Safari, Edge)
- A local web server (optional, but recommended for development)
- Basic understanding of JSON format (for content editing)

### Installation

1. **Clone or download** this repository to your local machine

2. **Navigate** to the project directory:
   ```bash
   cd Plutoblocks-web-book
   ```

3. **No additional dependencies** are required - this is a pure HTML/CSS/JavaScript application!

---

## 🏃 How to Start the Project

### Option 1: Using a Local Web Server (Recommended)

#### Using Python 3
```bash
# Python 3
python3 -m http.server 8000

# Then open in browser:
# http://localhost:8000
```

#### Using Python 2
```bash
# Python 2
python -m SimpleHTTPServer 8000

# Then open in browser:
# http://localhost:8000
```

#### Using Node.js (http-server)
```bash
# Install http-server globally (if not already installed)
npm install -g http-server

# Start the server
http-server -p 8000

# Then open in browser:
# http://localhost:8000
```

#### Using PHP
```bash
php -S localhost:8000
```

### Option 2: Direct File Opening

You can also open `index.html` directly in your browser by:
1. Double-clicking the `index.html` file, or
2. Right-clicking and selecting "Open with" your preferred browser

**Note**: Some browsers may restrict loading JSON files via `file://` protocol. If you encounter issues, use Option 1 (local web server).

### Option 3: Using VS Code Live Server

If you're using Visual Studio Code:
1. Install the "Live Server" extension
2. Right-click on `index.html`
3. Select "Open with Live Server"

---

## 📊 JSON Structure

The JSON files (`primus-v4.json` and `primus-x2.json`) follow a specific structure:

### Basic Structure

```json
{
  "_meta": {
    "order": ["intro", "compatibility", "platform", "p1", "p2"],
    "groups": [
      {
        "id": "basic",
        "title": "Basic Projects",
        "items": ["p1", "p2", "p3"]
      }
    ]
  },
  "intro": {
    "title": "1. Introduction to Pluto",
    "html": "<div class=\"card\">...</div>"
  },
  "p1": {
    "title": "Project 1: Debug APIs",
    "html": "<div class=\"card\">...</div>"
  }
}
```

### Field Descriptions

#### `_meta` Object

- **`order`** (required): Array of section IDs in the order they should appear
  - Used for navigation sequence
  - Determines "Next" and "Previous" button behavior
  - Example: `["intro", "compatibility", "platform", "p1"]`

- **`groups`** (optional): Array of group objects for organizing projects in the sidebar
  - Only present in `primus-x2.json` currently
  - Each group has:
    - `id`: Unique identifier for the group
    - `title`: Display name in the sidebar
    - `items`: Array of section IDs belonging to this group
  - If `groups` is not present, the app falls back to listing all projects starting with "p" followed by a number

#### Section Objects

Each section (like `"intro"`, `"p1"`, etc.) contains:

- **`title`** (required): The section title displayed in:
  - The main content area as `<h1>`
  - The sidebar navigation

- **`html`** (required): HTML content for the section
  - Should be wrapped in a `<div class="card">` for proper styling
  - Can include any valid HTML: paragraphs, lists, images, code blocks, tables, etc.
  - Images should use relative paths: `assets/img/filename.png`
  - Code blocks should use `<pre><code>...</code></pre>`

### Section ID Naming Convention

- **Introduction sections**: Use descriptive IDs like `"intro"`, `"compatibility"`, `"platform"`, `"primus"`, `"magis"`, `"tinkering"`, `"setup"`
- **Project sections**: Use pattern `"p"` followed by a number: `"p0"`, `"p1"`, `"p2"`, etc.
- IDs must be unique within each JSON file
- IDs are used in URL hashes: `#intro`, `#p1`, etc.

---

## ✏️ Rules for Modifying JSON Files

### 1. **JSON Syntax Rules**

- Always use **double quotes** for keys and string values
- No trailing commas after the last item in arrays or objects
- Escape special characters in strings:
  - `"` becomes `\"`
  - `\` becomes `\\`
  - Newlines in HTML should use `\n` or be part of the HTML string

### 2. **Adding a New Section**

1. **Create the section object**:
   ```json
   "new-section-id": {
     "title": "New Section Title",
     "html": "<div class=\"card\"><p>Content here</p></div>"
   }
   ```

2. **Add the ID to `_meta.order`**:
   ```json
   "_meta": {
     "order": ["intro", "compatibility", "new-section-id", "p1"]
   }
   ```

3. **If using groups, add to appropriate group**:
   ```json
   "groups": [
     {
       "id": "basic",
       "title": "Basic Projects",
       "items": ["p1", "new-section-id"]
     }
   ]
   ```

### 3. **Adding a New Project**

1. **Choose a project ID**: Use the next available number (e.g., if last project is `p23`, use `p24`)

2. **Add the project object**:
   ```json
   "p24": {
     "title": "Project 24: Project Name",
     "html": "<div class=\"card\"><h2>Challenge</h2><p>...</p></div>"
   }
   ```

3. **Add to `_meta.order`** in the desired position

4. **Add to appropriate group** (if using groups):
   ```json
   {
     "id": "intermediate",
     "title": "Intermediate Projects",
     "items": ["p9", "p10", "p24"]
   }
   ```

### 4. **Modifying Existing Content**

- **To change a title**: Update the `title` field
- **To change content**: Update the `html` field (preserve the `<div class="card">` wrapper)
- **To reorder sections**: Modify the `_meta.order` array
- **To move a project between groups**: Update the `items` array in the relevant groups

### 5. **Adding Images**

1. **Place image file** in `assets/img/` directory
2. **Reference in HTML**:
   ```html
   <img src="assets/img/filename.png" alt="Description" style="display:block;margin:20px auto;max-width:100%;">
   ```
3. **Use relative paths** starting with `assets/img/`

### 6. **HTML Content Guidelines**

- **Always wrap content** in `<div class="card">` for consistent styling
- **Use semantic HTML**: `<h2>`, `<h3>`, `<p>`, `<ul>`, `<ol>`, `<li>`
- **For code blocks**: Use `<pre><code>...</code></pre>`
- **For styled boxes**: Use inline styles or the existing card structure
- **Escape quotes** in HTML strings: `\"` for double quotes

### 7. **Validation Checklist**

Before saving JSON changes, ensure:
- ✅ JSON is valid (use a JSON validator)
- ✅ All section IDs in `order` array have corresponding section objects
- ✅ All IDs in group `items` arrays exist as section objects
- ✅ No duplicate section IDs
- ✅ Image paths are correct and files exist
- ✅ HTML is properly escaped

### 8. **Testing Changes**

1. **Save the JSON file**
2. **Refresh the browser** (or restart the local server)
3. **Select the board** from the dropdown to load the JSON
4. **Navigate through sections** to verify:
   - Content displays correctly
   - Navigation works
   - Images load
   - Next/Previous buttons work correctly

---

## 🔍 Understanding index.html

The `index.html` file is a **self-contained single-page application** with three main parts:

### 1. **HTML Structure**

```html
<div class="container">
  <aside class="sidebar">
    <!-- Navigation sidebar with board selector -->
  </aside>
  <main class="main">
    <!-- Dynamic content area -->
  </main>
</div>
<div class="nav-buttons">
  <!-- Previous/Next navigation -->
</div>
```

- **Sidebar**: Fixed-width navigation panel (280px) with:
  - Brand header ("Pluto Project Book")
  - Static navigation items (Basics section)
  - Dynamically generated project navigation
  - Board selector dropdown

- **Main Content Area**: Scrollable area that displays the selected section's HTML content

- **Navigation Buttons**: Fixed bottom buttons for Previous/Next navigation

### 2. **CSS Styles (Embedded)**

The styles define:
- **Dark theme** with GitHub-inspired colors
- **CSS Variables** for easy theming:
  - `--bg-dark`: Main background
  - `--bg-side`: Sidebar background
  - `--accent`: Accent color (#ffb627)
- **Responsive layout** with flexbox
- **Card-based content** styling
- **Active navigation** highlighting

### 3. **JavaScript Functionality**

The JavaScript handles:

- **`loadContent()`**: Fetches JSON based on selected board and initializes the app
- **`renderProjectsNav()`**: Dynamically generates sidebar navigation from JSON
  - Supports grouped projects (if `groups` exist in `_meta`)
  - Falls back to simple list if no groups
- **`renderSection(id)`**: Renders a specific section's content
- **`updatePagination(id)`**: Updates Previous/Next button states and links
- **Hash-based routing**: Uses URL hash (`#intro`, `#p1`) for navigation
- **LocalStorage**: Remembers selected board preference

### Key JavaScript Variables

- `boardData`: Stores the loaded JSON content
- `activeOrder`: Array of section IDs in display order
- `boardSelect`: Reference to the board selector dropdown
- `contentArea`: Reference to the main content container

### How Content Loading Works

1. **On page load**: 
   - Checks localStorage for saved board preference
   - Calls `loadContent()` to fetch JSON

2. **On board change**:
   - Saves preference to localStorage
   - Fetches new JSON file
   - Re-renders navigation and content

3. **On hash change**:
   - Extracts section ID from URL hash
   - Calls `renderSection()` to display content
   - Updates active navigation state

---

## ✨ Features

- **📱 Multi-Board Support**: Switch between Pluto X and Pluto 1.2 documentation
- **🎨 Dark Theme UI**: Modern, GitHub-inspired dark theme
- **📑 Organized Navigation**: Grouped projects with collapsible sections
- **🔍 Hash-Based Routing**: Direct links to specific sections via URL hash
- **💾 Persistent Preferences**: Remembers selected board using localStorage
- **📱 Responsive Design**: Works on desktop and tablet devices
- **🖼️ Image Support**: Easy image integration in project content
- **📝 Code Highlighting**: Pre-formatted code blocks for examples
- **⬅️➡️ Navigation Controls**: Previous/Next buttons for sequential browsing

---

## 🌐 Browser Compatibility

This application uses modern web standards and is compatible with:

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

**Required Features**:
- ES6 JavaScript (async/await, arrow functions)
- CSS Grid and Flexbox
- Fetch API
- LocalStorage API
- CSS Custom Properties (variables)

---

## 🛠️ Troubleshooting

### Images Not Loading

- **Check file paths**: Ensure images are in `assets/img/` and paths in JSON are correct
- **Use a local server**: Some browsers block `file://` protocol for security

### JSON Not Loading

- **Check browser console** for errors
- **Validate JSON syntax** using a JSON validator
- **Ensure file names match**: `primus-v4.json` and `primus-x2.json`

### Navigation Not Working

- **Check section IDs**: Ensure all IDs in `_meta.order` exist as section objects
- **Verify hash format**: URLs should be `#section-id` (no spaces, lowercase recommended)

### Styling Issues

- **Clear browser cache**: Old CSS might be cached
- **Check CSS syntax**: Ensure all styles are properly closed

---

## 📝 Notes

- This is a **static website** - no backend or database required
- All content is stored in JSON files for easy editing
- The application works offline once loaded (except for initial JSON fetch)
- Images should be optimized for web (use appropriate formats: PNG for diagrams, JPG for photos)

---

## 🤝 Instructions For Contributors

When contributing content:

1. Follow the JSON structure guidelines
2. Validate JSON before committing
3. Test changes in a local server
4. Ensure images are properly referenced
5. Maintain consistent formatting and style


**Happy Tinkering with Pluto Blocks! 🚁✨**

