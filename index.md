---
layout: default
title: "jobs.json Specification - Machine-Readable Job Postings"
description: "A standardized format for organizations to publish open job positions in a machine-readable jobs.json file. Tutorial, examples, and complete reference documentation."
keywords: "jobs.json, job postings, careers api, job specification, machine-readable jobs, standardized job format"
og_image: /favicon.svg
---

A specification for a standardized `jobs.json` file to describe open positions at an organization.

## Overview<!-- omit in toc -->

The `jobs.json` specification defines a well-known file format, similar to `robots.txt` or [`humans.txt`](https://humanstxt.org/), that organizations can use to publish their open job positions in a machine-readable format. By placing a `jobs.json` file at the root of your domain, you make it easy for job aggregators, career tools, and automated systems to discover and parse your available positions.

Job postings are scattered across various platforms, formats, and systems. Organizations maintain careers pages with inconsistent structures and vendors, making it difficult for job seekers to programmatically search across companies, aggregators to reliably collect listings, and tools to provide unified search experiences.

A standardized, [well-known file format][well-known] placed at a predictable location enables automatic discovery, consistent structure across organizations, simple implementation, no proprietary platform lock-in, and flexibility to list individual jobs or simply link to your careers page.

<div style="padding: 1em; background-color: #d1ecf1; border-left: 4px solid #0c5460; color: #0c5460; margin: 1em 0;">
  <strong>📝 Note:</strong> This is a prototype specification and may change based on community feedback and real-world implementation experience. We encourage early adopters to try it out and share their feedback.
</div>


- [Tutorial](#tutorial)
  - [Getting Started with jobs.json](#getting-started-with-jobsjson)
- [How-To Guides](#how-to-guides)
  - [How to Use jobs\_url for a Lower-Lift Approach](#how-to-use-jobs_url-for-a-lower-lift-approach)
  - [Common Patterns](#common-patterns)
- [Reference](#reference)
- [Explanation](#explanation)
  - [Design Principles](#design-principles)
  - [Use Cases](#use-cases)
  - [Relationship to Other Standards](#relationship-to-other-standards)
  - [Future Considerations](#future-considerations)
- [Getting Help](#getting-help)
- [Contributing](#contributing)

## Tutorial

### Getting Started with jobs.json

This tutorial will guide you through creating your first `jobs.json` file and publishing it on your website. You'll learn how to structure the file, where to place it, and how to validate your implementation.

Step 1: Create the file

Create a file named `jobs.json` in the root directory of your website (e.g., `https://yourcompany.com/jobs.json`).

Step 2: Add basic structure

Start with a minimal structure:

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

Step 3: Add your first job listing

Add a job entry to the `jobs` array:

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

Step 4: Publish and verify

Upload the file to your website's root directory and verify it's accessible at `https://yourcompany.com/jobs.json`.

## How-To Guides

### How to Use jobs_url for a Lower-Lift Approach

If maintaining a complete list of individual jobs in your `jobs.json` file is too much overhead, you can use the `jobs_url` field to simply link to your careers page or job board. This approach is ideal when you already have a job board with up-to-date listings or want to adopt the specification without the overhead of maintaining individual job entries.

<details>
<summary>Example: Basic jobs_url approach</summary>

{% highlight json %}
{
  "version": "0.1",
  "company": {
    "name": "Your Company Name",
    "url": "https://yourcompany.com",
    "jobs_url": "https://yourcompany.com/careers"
  },
  "jobs": []
}
{% endhighlight %}

</details>

You can also use both approaches together - list some key positions individually while also providing a `jobs_url` for the complete listing:

```json
{
  "version": "0.1",
  "company": {
    "name": "Your Company Name",
    "url": "https://yourcompany.com",
    "jobs_url": "https://yourcompany.com/careers"
  },
  "jobs": [
    {
      "id": "featured-001",
      "title": "Senior Software Engineer (Featured)",
      "url": "https://yourcompany.com/careers/senior-software-engineer"
    }
  ]
}
```

### Common Patterns

<details>
<summary>Multiple Locations</summary>

Specify multiple locations for a single position:

{% highlight json %}
{
  "id": "job-002",
  "title": "Product Manager",
  "locations": [
    {
      "city": "New York",
      "state": "NY",
      "country": "USA",
      "remote": false
    },
    {
      "city": "London",
      "country": "UK",
      "remote": false
    }
  ]
}
{% endhighlight %}

</details>

<details>
<summary>Employment Type</summary>

Specify full-time, part-time, contract, or other employment types:

{% highlight json %}
{
  "id": "job-003",
  "title": "Marketing Specialist",
  "employmentType": "FULL_TIME",
  "otherEmploymentTypes": ["PART_TIME", "CONTRACT", "TEMPORARY", "INTERN"]
}
{% endhighlight %}

</details>

<details>
<summary>Salary Information</summary>

Include transparent salary information:

{% highlight json %}
{
  "id": "job-004",
  "title": "Senior Developer",
  "compensation": {
    "currency": "USD",
    "min": 120000,
    "max": 180000,
    "period": "YEARLY"
  }
}
{% endhighlight %}

</details>

<details>
<summary>Expiration Dates</summary>

Add expiration dates to job listings:

{% highlight json %}
{
  "id": "job-005",
  "title": "Data Analyst",
  "postedDate": "2025-01-15",
  "expiresDate": "2025-03-15"
}
{% endhighlight %}

</details>

## Reference

For complete schema documentation including all field definitions, data types, and examples, see the [Schema Reference](schema.md) page.

## Explanation

### Design Principles

The specification prioritizes simplicity for quick implementation, machine-readable structured data, human-readable JSON format, extensibility through optional fields, and follows the well-known file location pattern of `robots.txt` and `humans.txt`.


### Use Cases

For Organizations: Increase job posting visibility across the web, maintain a single source of truth for open positions, enable integration with multiple job boards automatically, and provide transparent structured data. Start simple with just a `jobs_url` link and expand to individual listings later if desired.

For Job Seekers: Use tools to search directly across company websites, get consistent structured information about positions, access up-to-date job listings at their source, and build custom job search and alert systems.

For Tool Builders: Create job aggregators without screen scraping, build career discovery and comparison tools, develop automated job alert systems, and enable resume matching and recommendation engines.

### Relationship to Other Standards

Similar to `robots.txt`, `humans.txt`, `security.txt`, and `ads.txt` as a well-known file pattern.

Works as a lighter alternative to Schema.org's [JobPosting](https://schema.org/JobPosting) markup for HTML structured data.

### Future Considerations

The specification is designed to evolve while maintaining backward compatibility. Potential future additions may include skills requirements, benefits information, application process details, diversity data, and team structure information. Organizations can add custom fields prefixed with `x-` for experimental or proprietary data while maintaining spec compliance.

---

## Getting Help

Report specification issues or ask questions on the [GitHub Repository](https://github.com/lowlydba/jobsjson.org). For detailed schema documentation and examples, see the [Schema Reference](schema.md) page.

## Contributing

This specification is open source and welcomes community input. Visit the GitHub repository to propose changes or improvements.

{% include footer.html %}

[well-known]: https://tools.ietf.org/html/rfc5785
