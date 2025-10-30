# jobsjson.org

Website and specification for [jobsjson.org](https://jobsjson.org) - a standardized `jobs.json` file format for publishing job openings.

## About

The jobsjson.org specification defines a well-known file format (similar to `robots.txt` or `humans.txt`) that organizations can use to publish their open job positions in a machine-readable format.

## Development

This is a Jekyll site that is automatically deployed to GitHub Pages on merge to main.

### Local Development

1. Install dependencies:
   ```bash
   bundle install
   ```

2. Run the development server:
   ```bash
   bundle exec jekyll serve
   ```

3. Visit `http://localhost:4000` in your browser

### GitHub Pages Setup

The site is configured to deploy automatically via GitHub Actions. To enable:

1. Go to repository Settings → Pages
2. Under "Build and deployment", set Source to "GitHub Actions"
3. The workflow will automatically build and deploy on push to main

## Contributing

Contributions are welcome! Please open an issue or pull request to suggest improvements to the specification or website.

## License

MIT 
