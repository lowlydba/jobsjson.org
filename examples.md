---
layout: default
title: "jobs.json Examples"
description: "Practical examples and common patterns for implementing the jobs.json specification in your organization."
keywords: "jobs.json examples, job posting examples, careers api examples, json examples"
---

This page provides practical examples and common patterns for implementing the jobs.json specification.

## Basic jobs_url Approach

If maintaining a complete list of individual jobs in your `jobs.json` file is too much overhead, you can use the `jobs_url` field to simply link to your careers page or job board. This approach is ideal when you already have a job board with up-to-date listings or want to adopt the specification without the overhead of maintaining individual job entries.

```json
{
  "version": "0.1",
  "company": {
    "name": "Your Company Name",
    "url": "https://yourcompany.com",
    "jobs_url": "https://yourcompany.com/careers"
  },
  "jobs": []
}
```

## Hybrid Approach

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

## Common Patterns

### Multiple Locations

Specify multiple locations for a single position:

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

### Employment Type

Specify full-time, part-time, contract, or other employment types:

```json
{
  "id": "job-003",
  "title": "Marketing Specialist",
  "employmentType": "FULL_TIME",
  "otherEmploymentTypes": ["PART_TIME", "CONTRACT", "TEMPORARY", "INTERN"]
}
```

### Salary Information

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

### Expiration Dates

Add expiration dates to job listings:

```json
{
  "id": "job-005",
  "title": "Data Analyst",
  "postedDate": "2025-01-15",
  "expiresDate": "2025-03-15"
}
```

## Complete Example

Here's a complete example with multiple jobs and various fields:

```json
{
  "version": "0.1",
  "company": {
    "name": "Tech Innovations Inc",
    "url": "https://techinnovations.example.com",
    "logo": "https://techinnovations.example.com/logo.png",
    "description": "Leading technology company focused on innovation",
    "jobs_url": "https://techinnovations.example.com/careers"
  },
  "jobs": [
    {
      "id": "eng-001",
      "title": "Senior Software Engineer",
      "department": "Engineering",
      "location": {
        "city": "San Francisco",
        "state": "CA",
        "country": "USA",
        "remote": true
      },
      "employmentType": "FULL_TIME",
      "compensation": {
        "currency": "USD",
        "min": 150000,
        "max": 200000,
        "period": "YEARLY"
      },
      "url": "https://techinnovations.example.com/careers/senior-software-engineer",
      "postedDate": "2025-01-15"
    },
    {
      "id": "mkt-002",
      "title": "Product Marketing Manager",
      "department": "Marketing",
      "locations": [
        {
          "city": "New York",
          "state": "NY",
          "country": "USA",
          "remote": false
        },
        {
          "city": "Remote",
          "remote": true
        }
      ],
      "employmentType": "FULL_TIME",
      "url": "https://techinnovations.example.com/careers/product-marketing-manager",
      "postedDate": "2025-01-20"
    }
  ],
  "lastUpdated": "2025-01-25T10:30:00Z"
}
```

---

For more information, see the [main specification](/) or the [schema reference](schema.html).
