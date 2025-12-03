# Copilot Instructions for Flask Codespaces

## Project Overview
This is a minimal Flask starter application designed for GitHub Codespaces. It demonstrates Flask basics with server-side template rendering and static file serving. The app is intentionally lightweight to serve as a learning foundation.

**Key Components:**
- `app.py` - Single Flask application instance with one route handler
- `templates/index.html` - Jinja2 template using Flask's `url_for()` for static file references
- `static/main.css` - Styling using CSS Grid and flexbox for the centered header layout
- `requirements.txt` - Pinned Flask 2.3.2 dependency

## Architecture & Data Flow

### Route Structure
The application has one entry point: `GET /` returns `index.html` with a `title="Hello"` context variable.
- **Pattern:** Use `render_template(filename, **context)` to pass data to templates
- **Context variables** are accessible in templates via Jinja2 syntax: `{{ variable_name }}`

### Template & Static Asset Management
- **Static files:** Reference via `{{ url_for('static', filename='path/to/file') }}` — this generates correct URLs in development and production
- **Templates:** Store in `templates/` directory; Flask auto-discovers this folder
- **CSS/Images:** Store in `static/` directory with the same convention

## Development Workflow

### Running the Application
```bash
flask --debug run
```
- Debug mode enables auto-reload on file changes and the interactive debugger
- Application serves on `http://localhost:5000` by default

### Making Changes
1. **Route handlers** (`.py` files) - Flask auto-reloads the server
2. **Templates** (`templates/*.html`) - Refresh browser; Flask recompiles on request
3. **Static assets** (`static/*`) - Browser may cache; do a hard refresh (Ctrl+Shift+R) if needed

### Environment
- Python 3.x (standard Codespaces environment)
- Run `pip install -r requirements.txt` if dependencies need updating

## Project Conventions

### Naming Conventions
- Route functions use descriptive names matching their purpose (e.g., `hello_world`)
- HTML templates use lowercase filenames (e.g., `index.html`)
- CSS uses kebab-case class names (e.g., `.App-header`, `.App-logo`)

### Code Patterns to Follow
- Keep routes simple; delegate logic to helper functions or services as the app grows
- Use Jinja2 context variables for dynamic content; avoid hardcoding in templates
- Group related CSS classes in logical sections (e.g., `.App-*` for the main container)

## Extending the Codebase

### Adding a New Route
```python
@app.route("/about")
def about_page():
    return render_template("about.html", page_title="About Us")
```

### Adding Static Files
Place images, fonts, or additional stylesheets in `static/`. Reference them consistently via `url_for()`.

### Adding More Templates
Create files in `templates/` (e.g., `about.html`, `contact.html`). Extend `index.html` layout if needed for consistency.

## Important Reminders
- This is a starter template; no database, authentication, or complex logic is included by design
- Flask's development server is not suitable for production; use a production WSGI server (Gunicorn, uWSGI)
- Always use `url_for()` for static file references to avoid hardcoded paths breaking in different environments
