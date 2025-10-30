---
layout: default
title: jobsjson.org - A Standard for Publishing Job Opportunities
---

# jobsjson.org

A specification for a standardized `jobs.json` file to describe open positions at an organization.

## Overview

The `jobs.json` specification defines a well-known file format, similar to `robots.txt` or `humans.txt`, that organizations can use to publish their open job positions in a machine-readable format. By placing a `jobs.json` file at the root of your domain, you make it easy for job aggregators, career tools, and automated systems to discover and parse your available positions.

---

## Tutorial

### Getting Started with jobs.json

This tutorial will guide you through creating your first `jobs.json` file and publishing it on your website.

**What you'll learn:**
- How to structure a basic `jobs.json` file
- Where to place the file on your website
- How to validate your implementation

**Step 1: Create the file**

Create a file named `jobs.json` in the root directory of your website (e.g., `https://yourcompany.com/jobs.json`).

**Step 2: Add basic structure**

Start with a minimal structure:

```json
{
  "version": "1.0",
  "company": {
    "name": "Your Company Name",
    "url": "https://yourcompany.com"
  },
  "jobs": []
}
```

**Step 3: Add your first job listing**

Add a job entry to the `jobs` array:

```json
{
  "version": "1.0",
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

**Step 4: Publish and verify**

Upload the file to your website's root directory and verify it's accessible at `https://yourcompany.com/jobs.json`.

---

## How-To Guides

### How to Add Multiple Locations

To specify multiple locations for a single position:

```json
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
```

### How to Include Employment Type

Specify full-time, part-time, contract, or other employment types:

```json
{
  "id": "job-003",
  "title": "Marketing Specialist",
  "employmentType": "FULL_TIME",
  "otherEmploymentTypes": ["PART_TIME", "CONTRACT", "TEMPORARY", "INTERN"]
}
```

### How to Add Salary Information

Include transparent salary information:

```json
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
```

### How to Set Expiration Dates

Add expiration dates to job listings:

```json
{
  "id": "job-005",
  "title": "Data Analyst",
  "postedDate": "2025-01-15",
  "expiresDate": "2025-03-15"
}
```

---

## Reference

### Schema Specification

The `jobs.json` file must be a valid JSON document conforming to the following schema:

#### Root Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `version` | string | Yes | Specification version (currently "1.0") |
| `company` | object | Yes | Company information object |
| `jobs` | array | Yes | Array of job objects |
| `lastUpdated` | string | No | ISO 8601 timestamp of last update |

#### Company Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Company name |
| `url` | string | Yes | Company website URL |
| `logo` | string | No | URL to company logo |
| `description` | string | No | Brief company description |

#### Job Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | string | Yes | Unique identifier for the job |
| `title` | string | Yes | Job title |
| `department` | string | No | Department or team name |
| `description` | string | No | Job description |
| `url` | string | Yes | URL to full job posting |
| `location` | object | No | Single location object |
| `locations` | array | No | Array of location objects (use if multiple locations) |
| `employmentType` | string | No | Employment type (FULL_TIME, PART_TIME, CONTRACT, TEMPORARY, INTERN) |
| `postedDate` | string | No | ISO 8601 date when job was posted |
| `expiresDate` | string | No | ISO 8601 date when posting expires |
| `compensation` | object | No | Compensation information object |

#### Location Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `city` | string | No | City name |
| `state` | string | No | State or province |
| `country` | string | No | Country name or ISO code |
| `remote` | boolean | No | Whether remote work is available |

#### Compensation Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `currency` | string | Yes | ISO 4217 currency code (e.g., USD, EUR) |
| `min` | number | No | Minimum compensation |
| `max` | number | No | Maximum compensation |
| `period` | string | Yes | Payment period (YEARLY, MONTHLY, HOURLY) |

### Complete Example

```json
{
  "version": "1.0",
  "lastUpdated": "2025-01-20T10:00:00Z",
  "company": {
    "name": "Example Corp",
    "url": "https://example.com",
    "logo": "https://example.com/logo.png",
    "description": "A leading technology company"
  },
  "jobs": [
    {
      "id": "eng-001",
      "title": "Senior Software Engineer",
      "department": "Engineering",
      "description": "We are seeking an experienced software engineer...",
      "url": "https://example.com/careers/senior-software-engineer",
      "location": {
        "city": "San Francisco",
        "state": "CA",
        "country": "USA",
        "remote": true
      },
      "employmentType": "FULL_TIME",
      "postedDate": "2025-01-15",
      "compensation": {
        "currency": "USD",
        "min": 150000,
        "max": 200000,
        "period": "YEARLY"
      }
    },
    {
      "id": "pm-002",
      "title": "Product Manager",
      "department": "Product",
      "url": "https://example.com/careers/product-manager",
      "locations": [
        {
          "city": "New York",
          "state": "NY",
          "country": "USA",
          "remote": false
        },
        {
          "city": "Austin",
          "state": "TX",
          "country": "USA",
          "remote": false
        }
      ],
      "employmentType": "FULL_TIME",
      "postedDate": "2025-01-10"
    }
  ]
}
```

---

## Explanation

### Why jobs.json?

**The problem:** Job postings are scattered across various platforms, formats, and systems. Organizations maintain careers pages with inconsistent structures, making it difficult for:
- Job seekers to programmatically search across companies
- Aggregators to reliably collect and update job listings
- Tools to provide unified job search experiences

**The solution:** A standardized, well-known file format placed at a predictable location enables:
- **Discoverability**: Tools can automatically find job listings
- **Consistency**: All organizations use the same structure
- **Simplicity**: Easy to implement and maintain
- **Openness**: No proprietary platform lock-in

### Design Principles

1. **Simplicity First**: The specification should be simple enough for any organization to implement quickly
2. **Machine-Readable**: Structured data that can be easily parsed by tools
3. **Human-Readable**: JSON format that developers can understand and debug
4. **Extensible**: Allows for optional fields without breaking compatibility
5. **Well-Known Location**: Following the pattern of `robots.txt` and `humans.txt`

### Use Cases

**For Organizations:**
- Increase job posting visibility across the web
- Maintain a single source of truth for open positions
- Enable integration with multiple job boards automatically
- Provide transparent, structured data about opportunities

**For Job Seekers:**
- Use tools to search directly across company websites
- Get consistent, structured information about positions
- Access up-to-date job listings at their source
- Build custom job search and alert systems

**For Tool Builders:**
- Create job aggregators without screen scraping
- Build career discovery and comparison tools
- Develop automated job alert systems
- Enable resume matching and recommendation engines

### Relationship to Other Standards

**Similar to:**
- `robots.txt`: Well-known file for web crawler instructions
- `humans.txt`: Information about the people behind a website
- `security.txt`: Security contact information
- `ads.txt`: Authorized digital sellers declaration

**Complements:**
- Schema.org JobPosting markup: Can be used alongside HTML structured data
- RSS/Atom feeds: Provides richer structured data than traditional feeds
- Job board APIs: Offers a simpler, standardized alternative

### Future Considerations

The specification is designed to evolve while maintaining backward compatibility. Potential future additions may include:
- Skills and qualifications requirements
- Benefits and perks information
- Application process details
- Diversity and inclusion data
- Team structure information

Organizations can add custom fields prefixed with `x-` for experimental or proprietary data while maintaining spec compliance.

---

## Getting Help

- **Specification Issues**: [GitHub Repository](https://github.com/lowlydba/jobsjson.org)
- **Questions**: Open a discussion on GitHub
- **Examples**: See the reference section above

## Contributing

This specification is open source and welcomes community input. Visit the GitHub repository to propose changes or improvements.

---

**Version**: 1.0  
**Last Updated**: 2025-01-20  
**License**: MIT
