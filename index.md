layout: default
title: "Home"
description: "A standardized format for organizations to publish open job positions in a human & machine-readable jobs.json file. Tutorial, examples, and complete reference documentation."
keywords: "jobs.json, job postings, careers api, job specification, human-readable jobs, machine-readable jobs, standardized job format"
og_image: /favicon.svg
---

Publish open roles in a simple, standardized `jobs.json` file that tools can discover and parse.

## Overview<!-- omit in toc -->

The `jobs.json` spec uses a well-known file pattern (like `robots.txt` or [`humans.txt`](https://humanstxt.org/)). Put a `jobs.json` at your domain root and make it easy for aggregators, career tools, and scripts to find your roles without scraping.

Today, jobs live across ATS vendors and custom pages with inconsistent HTML. That makes it hard for seekers to search across companies and for builders to index reliably. A small, predictable JSON file at a known URL gives:

- Automatic discovery at a standard location
- A consistent, minimal structure across organizations
- A no-vendor-lock-in option you control
- Flexibility: list individual jobs or just link to your careers page

<div style="padding: 1em; background-color: #d1ecf1; border-left: 4px solid #0c5460; color: #0c5460; margin: 1em 0;">
  <strong>📝 Note:</strong> This is a prototype and, realistically, may remain a niche/experimental standard. It’s still useful as a practical thought experiment: simple to try, easy to abandon, and informative even if adoption stays small. We welcome feedback and real-world trials.
</div>

- [og\_image: /favicon.svg](#og_image-faviconsvg)
- [Tutorial](#tutorial)
  - [Getting Started with jobs.json](#getting-started-with-jobsjson)
- [How-To Guides](#how-to-guides)
  - [Using jobsUrl for Quick Implementation](#using-jobsurl-for-quick-implementation)
- [Reference](#reference)
- [Explanation](#explanation)
  - [Philosophy](#philosophy)
  - [Use Cases](#use-cases)
  - [Relationship to Other Standards](#relationship-to-other-standards)
  - [Future Considerations](#future-considerations)
- [Getting Help](#getting-help)
- [Contributing](#contributing)

## Tutorial

### Getting Started with jobs.json

This tutorial will guide you through creating your first `jobs.json` file and publishing it on your website. You'll learn how to structure the file, where to place it, and how to validate your implementation.

1. Create the file:

   Create a file named `jobs.json` in the root directory of your website (e.g., `https://yourcompany.com/jobs.json`).

2. Add basic structure:

   ```json
   {
     "version": "0.1",
     "company": {
       "name": "Your Company Name",
       "url": "https://yourcompany.com"
    },
     "jobs": []
   }
   ```

3. Add your first job listing

   ```json
   {
     "version": "0.1",
     "company": {
       "name": "Your Company Name",
       "url": "https://yourcompany.com"
     },
     "jobs": [
       {
         "id": "job-001",
         "title": "Software Engineer",
         "department": "Engineering",
          "location": {
           "city": "San Francisco",
           "state": "CA",
           "country": "USA",
           "remote": true
         },
         "url": "https://yourcompany.com/careers/software-engineer"
       }
     ]
   }
   ```

4. Publish and verify

   Upload the file to your website's root directory and verify it's accessible at `https://yourcompany.com/jobs.json`.

## How-To Guides

### Using jobsUrl for Quick Implementation

If maintaining a complete list of individual jobs in your `jobs.json` file is too much overhead, you can use the `jobsUrl` field to simply link to your careers page. This is the fastest way to adopt the specification.

For more detailed examples and common patterns, see the [Examples page](examples.html).

## Reference

For complete schema documentation including all field definitions, data types, and examples, see the [Schema Reference](schema.html) page.

## Explanation

### Philosophy

This project optimizes for small, boring, and useful.

- Simplicity first: A tiny, flat JSON shape most orgs can publish in minutes.
- Well-known location: A predictable URL enables zero-configuration discovery.
- Source of truth: Let your domain speak for itself, independent of vendors or scrapers.
- Pragmatic adoption: If maintaining individual listings is heavy, just set `company.jobsUrl` and you’re still compliant.
- Extensible, not fragile: Add `x-` fields for custom needs without breaking parsers.

What this is not:

- Not an ATS replacement
- Not a competitor to Schema.org markup
- Not trying to capture every job nuance


### Use Cases

- For Organizations: Increase job posting visibility across the web, maintain a single source of truth for open positions, enable integration with multiple job boards automatically, and provide transparent structured data. Start simple with just a `jobsUrl` link and expand to individual listings later if desired.

- For Job Seekers: Use tools to search directly across company websites, get consistent structured information about positions, access up-to-date job listings at their source, and build custom job search and alert systems.

- For Tool Builders: Create job aggregators without screen scraping, build career discovery and comparison tools, develop automated job alert systems, and enable resume matching and recommendation engines.

### Relationship to Other Standards

Similar to `robots.txt`, `humans.txt`, `security.txt`, and `ads.txt` as a well-known file pattern. Works as a lighter alternative to Schema.org's [JobPosting](https://schema.org/JobPosting) markup for HTML structured data.

### Future Considerations

The specification is designed to evolve while maintaining backward compatibility. Potential future additions may include skills requirements, benefits information, application process details, diversity data, and team structure information. Organizations can add custom fields prefixed with `x-` for experimental or proprietary data while maintaining spec compliance.

## Getting Help

Report specification issues or ask questions on the [GitHub Repository](https://github.com/lowlydba/jobsjson.org). For detailed schema documentation and examples, see the [Schema Reference](schema.md) page.

## Contributing

This specification is open source and welcomes community input! Visit the [GitHub repository](https://github.com/lowlydba/jobsjson.org) to propose changes or improvements.
