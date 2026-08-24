# Bobathon Tools Guide Template

A small static site skeleton for participant setup guides and MCP labs.

## Preview locally

```bash
./script/preview
```

Then open <http://127.0.0.1:4173/>.

## Publish with GitHub Pages

1. Create an empty GitHub repository.
2. Push this folder to its `main` branch.
3. In GitHub, open Settings > Pages.
4. Set Source to GitHub Actions.

Every push to `main` builds and deploys the site automatically.

## Customize

- Replace the event title and contact details in each HTML file.
- Duplicate `guides/notion-mcp.html` when adding another tool lab.
- Add the new page to the card grid in `index.html`.
- Keep participant instructions short and provide a visible success check.
