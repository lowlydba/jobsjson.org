---
layout: default
title: jobs.json Schema Reference
---

> **Prototype Status**: This is a prototype specification (version 0.1) and may change based on community feedback and real-world implementation experience.

The `jobs.json` file must be a valid JSON document conforming to the following schema:

## Root Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `version` | string | Yes | Specification version |
| `company` | object | Yes | Company information object |
| `jobs` | array | Yes | Array of job objects |
| `lastUpdated` | string | No | ISO 8601 timestamp of last update |

## Company Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Company name |
| `url` | string | Yes | Company website URL |
| `logo` | string | No | URL to company logo |
| `description` | string | No | Brief company description |
| `jobs_url` | string | No | URL to company's jobs page or careers site. Can be used instead of or alongside individual jobs listed in the `jobs` array |

## Job Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | string | Yes | Unique identifier for the job |
| `title` | string | Yes | Job title |
| `department` | string | No | Department or team name |
| `description` | string | No | Job description |
| `url` | string | Yes | URL to full job posting |
| `location` | object | No | Single location object |
| `locations` | array | No | Array of location objects (use if multiple locations) |
| `employmentType` | string | No | Employment type. One of: `FULL_TIME`, `PART_TIME`, `CONTRACT`, `TEMPORARY`, `INTERN` |
| `postedDate` | string | No | ISO 8601 date when job was posted |
| `expiresDate` | string | No | ISO 8601 date when posting expires |
| `compensation` | object | No | Compensation information object |
| `otherEmploymentTypes` | array | No | Array of additional employment type strings (for positions with multiple types) |

## Location Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `city` | string | No | City name |
| `state` | string | No | State or province |
| `country` | string | No | Country name or ISO code |
| `remote` | boolean | No | Whether remote work is available |

## Compensation Object

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `currency` | string | Yes | ISO 4217 currency code (e.g., USD, EUR) |
| `min` | number | No | Minimum compensation |
| `max` | number | No | Maximum compensation |
| `period` | string | Yes | Payment period (YEARLY, MONTHLY, HOURLY) |

## Complete Example

```json
{
  "version": "0.1",
  "lastUpdated": "2025-01-20T10:00:00Z",
  "company": {
    "name": "Example Corp",
    "url": "https://example.com",
    "logo": "https://example.com/logo.png",
    "description": "A leading technology company",
    "jobs_url": "https://example.com/careers"
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

## Getting Help

Report specification issues or ask questions on the [GitHub Repository](https://github.com/lowlydba/jobsjson.org).

## Contributing

This specification is open source and welcomes community input. Visit the GitHub repository to propose changes or improvements.

{% include site-footer.html %}
