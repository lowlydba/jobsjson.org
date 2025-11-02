# jobsjson.org

The public website and reference documentation for jobs.json — a small, well-known
JSON file that organizations can publish at their domain root to expose open roles
in a machine-readable way. It’s intentionally simple, vendor‑neutral, and pragmatic.

- Website: <https://jobsjson.org>
- Spec source: `SPECIFICATION.md` (non-rendered)
- Site content: `index.md`, `schema.md`, `examples.md`

## Local development

This site is built with Jekyll and hosted on GitHub Pages.

1) Install Ruby and Bundler
2) Install dependencies
3) Serve locally

```pwsh
bundle install
bundle exec jekyll serve
```

Then open <http://localhost:4000>

## Contributing

Issues and PRs are welcome. Keep the spec small, examples realistic, and JSON valid.
