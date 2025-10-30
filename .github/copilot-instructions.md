# GitHub Copilot Instructions for jobsjson.org

## Project Overview

This is the official specification website for **jobs.json** - a standardized file format for organizations to publish open job positions in a machine-readable format. The site is built using **Jekyll** and hosted on **GitHub Pages**.

## Project Structure

- `index.md` - Main documentation page containing the complete specification, tutorials, how-to guides, reference docs, and explanations (follows Diátaxis documentation framework)
- `_config.yml` - Jekyll configuration file
- `.github/workflows/jekyll.yml` - CI/CD workflow for building and deploying the site
- `SPECIFICATION.md` - Technical specification for the jobs.json format
- `Gemfile` - Ruby dependencies (uses github-pages gem)

## Key Technologies

- **Jekyll**: Static site generator (version from github-pages gem)
- **Markdown (kramdown)**: Content format
- **Minima theme**: Default Jekyll theme
- **GitHub Pages**: Hosting platform
- **Ruby 3.2**: Runtime environment

## Coding Standards

### Markdown Files
- Use ATX-style headers (`#` prefix)
- Include frontmatter for Jekyll pages with `layout`, `title`, and other metadata
- Use code fences with language identifiers (e.g., `` ```json ``)
- Follow existing structure: Tutorial → How-To → Reference → Explanation (Diátaxis)
- Keep line length reasonable (~80-100 chars when practical)
- Use relative links for internal navigation
- Ensure proper nesting of lists and headers

### YAML Configuration
- Follow existing `_config.yml` structure
- Use 2-space indentation
- Add comments for clarity where needed
- Keep configuration minimal and focused

### JSON Examples
- All jobs.json examples must be valid JSON
- Use 2-space indentation
- Include required fields: `version`, `company`, `jobs`
- Follow the specification schema precisely
- Provide realistic example data

## Documentation Style

- **Tutorial**: Step-by-step learning for beginners
- **How-To Guides**: Goal-oriented practical instructions
- **Reference**: Technical descriptions and schema specifications
- **Explanation**: Conceptual clarification and design decisions

## Jekyll Specifics

### Building Locally
```bash
bundle install
bundle exec jekyll build
bundle exec jekyll serve  # For local development
```

### File Processing
- Files starting with `_` are special Jekyll files/directories
- Front matter is required for pages to be processed by Jekyll
- Use `include` directive in `_config.yml` for non-standard files (e.g., `humans.txt`)
- Files listed in `exclude` won't be included in the built site

### Permalinks and URLs
- Base URL is empty (site is at domain root)
- Use `{{ site.url }}{{ site.baseurl }}` for absolute URLs
- Relative links work for internal navigation

## Common Tasks

### Adding New Content
1. Create a `.md` file with proper front matter
2. Use appropriate layout (`default` is standard)
3. Follow existing markdown structure and style
4. Link from main navigation if needed

### Updating the Specification
1. Modify `index.md` for documentation changes
2. Update `SPECIFICATION.md` for technical spec changes
3. Ensure examples remain valid and consistent
4. Maintain backward compatibility considerations

### Testing Changes
1. Build the site locally: `bundle exec jekyll build`
2. Serve locally for preview: `bundle exec jekyll serve`
3. Check for build warnings or errors
4. Verify all links work correctly
5. Preview on http://localhost:4000

## GitHub Workflow

### Pull Requests
- The Jekyll workflow runs on PR branches for validation
- Build must succeed before merging
- Check GitHub Actions output for any issues

### Deployments
- Automatic deployment to GitHub Pages on merge to `main`
- Site is deployed via `actions/deploy-pages@v4`
- Uses GitHub Pages environment

## Best Practices

1. **Keep It Simple**: The specification should remain easy to understand and implement
2. **Backward Compatibility**: Changes should not break existing implementations
3. **Clear Examples**: Provide practical, realistic examples for all features
4. **Consistent Formatting**: Follow existing patterns in markdown and code
5. **Validation**: Ensure all JSON examples are valid and match the schema
6. **Accessibility**: Use semantic HTML/markdown structure
7. **Performance**: Keep the site lightweight and fast - optimize images, minimize external dependencies, keep markdown files under 500KB

## jobs.json Specification Principles

1. **Simplicity First**: Easy for any organization to implement quickly
2. **Machine-Readable**: Structured data that tools can parse
3. **Human-Readable**: JSON format developers can understand
4. **Extensible**: Optional fields don't break compatibility
5. **Well-Known Location**: Follows pattern of robots.txt, humans.txt, etc.

## File Naming Conventions

- Use lowercase for file names
- Use hyphens for spaces in URLs (e.g., `my-page.md`)
- Standard files: `README.md`, `LICENSE`, `CNAME`, `humans.txt`
- Configuration: `_config.yml`, `Gemfile`

## When Making Changes

1. Review existing structure and patterns first
2. Maintain consistency with established conventions
3. Test locally before committing
4. Keep changes minimal and focused
5. Update related documentation together
6. Consider impact on existing users of the spec

## Resources

- Jekyll Documentation: https://jekyllrb.com/docs/
- GitHub Pages: https://docs.github.com/pages
- Kramdown Syntax: https://kramdown.gettalong.org/syntax.html
- Minima Theme: https://github.com/jekyll/minima
