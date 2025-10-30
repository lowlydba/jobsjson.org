# jobs.json Technical Specification

**Version**: 1.0  
**Last Updated**: 2025-01-20  
**Status**: Stable

## Abstract

This document defines the technical specification for `jobs.json`, a standardized file format for organizations to publish open job positions in a machine-readable format. The specification defines a JSON document structure that should be accessible at the root of an organization's domain (e.g., `https://example.com/jobs.json`).

## Table of Contents

1. [Introduction](#introduction)
2. [Conformance](#conformance)
3. [File Location and Access](#file-location-and-access)
4. [JSON Schema](#json-schema)
5. [Data Types and Formats](#data-types-and-formats)
6. [Validation Rules](#validation-rules)
7. [Extension Mechanism](#extension-mechanism)
8. [Examples](#examples)
9. [Version History](#version-history)

## 1. Introduction

The `jobs.json` specification provides a standardized way for organizations to publish their open job positions. This specification is designed to:

- Enable machine-readable job listings
- Provide a well-known location for job data
- Support automated job aggregation and discovery
- Maintain simplicity and ease of implementation
- Allow extensibility for future enhancements

## 2. Conformance

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

A conforming `jobs.json` document:
- MUST be valid JSON as defined in RFC 8259
- MUST include all REQUIRED fields
- MUST use the correct data types for all fields
- SHOULD validate against the schema defined in this specification
- MAY include optional fields
- MAY include extension fields prefixed with `x-`

## 3. File Location and Access

### 3.1 File Location

The `jobs.json` file MUST be accessible at the root of the organization's primary domain:

```
https://example.com/jobs.json
```

### 3.2 HTTP Requirements

- The file MUST be served with HTTP status code 200 (OK) when available
- The file SHOULD be served with `Content-Type: application/json`
- The file SHOULD include appropriate caching headers
- The file SHOULD be accessible via HTTPS
- The file MAY return HTTP status code 404 (Not Found) when no jobs are available

### 3.3 Character Encoding

The file MUST use UTF-8 character encoding.

## 4. JSON Schema

### 4.1 Root Object

The root object represents the complete jobs feed for an organization.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `version` | string | **REQUIRED** | Specification version. Current value: "1.0" |
| `company` | object | **REQUIRED** | Company information (see §4.2) |
| `jobs` | array | **REQUIRED** | Array of job objects (see §4.3) |
| `lastUpdated` | string | OPTIONAL | ISO 8601 timestamp of last update |

**Example:**
```json
{
  "version": "1.0",
  "company": { ... },
  "jobs": [ ... ],
  "lastUpdated": "2025-01-20T10:00:00Z"
}
```

### 4.2 Company Object

The company object provides information about the hiring organization.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | **REQUIRED** | Full legal or common name of the company |
| `url` | string | **REQUIRED** | Company website URL (MUST be valid URL) |
| `logo` | string | OPTIONAL | URL to company logo (MUST be valid URL) |
| `description` | string | OPTIONAL | Brief company description (max 500 characters RECOMMENDED) |

**Example:**
```json
{
  "name": "Example Corporation",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png",
  "description": "A leading technology company specializing in innovative solutions"
}
```

### 4.3 Job Object

Each job object represents a single open position.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `id` | string | **REQUIRED** | Unique identifier for the job within this feed |
| `title` | string | **REQUIRED** | Job title |
| `url` | string | **REQUIRED** | URL to the full job posting (MUST be valid URL) |
| `department` | string | OPTIONAL | Department or team name |
| `description` | string | OPTIONAL | Job description or summary |
| `location` | object | OPTIONAL | Single location (see §4.4) |
| `locations` | array | OPTIONAL | Multiple locations (see §4.4) |
| `employmentType` | string | OPTIONAL | Primary employment type (see §5.2) |
| `otherEmploymentTypes` | array | OPTIONAL | Additional employment types when position can be filled under multiple arrangements (e.g., both FULL_TIME and CONTRACT) |
| `postedDate` | string | OPTIONAL | ISO 8601 date when job was posted |
| `expiresDate` | string | OPTIONAL | ISO 8601 date when posting expires |
| `compensation` | object | OPTIONAL | Compensation information (see §4.5) |

**Constraints:**
- `id` MUST be unique within the `jobs` array
- Either `location` OR `locations` MAY be provided, but not both
- If provided, `location` and `locations` MUST conform to Location Object schema
- `postedDate` MUST be in ISO 8601 format (YYYY-MM-DD or full timestamp)
- `expiresDate` MUST be in ISO 8601 format (YYYY-MM-DD or full timestamp)
- `expiresDate`, if provided, SHOULD be later than `postedDate`

**Example:**
```json
{
  "id": "eng-001",
  "title": "Senior Software Engineer",
  "department": "Engineering",
  "description": "We are seeking an experienced software engineer to join our team.",
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
}
```

### 4.4 Location Object

Represents a physical or remote location for a job.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `city` | string | OPTIONAL | City name |
| `state` | string | OPTIONAL | State, province, or region |
| `country` | string | OPTIONAL | Country name or ISO 3166-1 code |
| `remote` | boolean | OPTIONAL | Whether remote work is available |

**Constraints:**
- At least one field SHOULD be provided
- `country` SHOULD use ISO 3166-1 alpha-2 or alpha-3 codes when possible

**Example:**
```json
{
  "city": "New York",
  "state": "NY",
  "country": "USA",
  "remote": false
}
```

### 4.5 Compensation Object

Provides salary or compensation information for a job.

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `currency` | string | **REQUIRED** | ISO 4217 currency code |
| `period` | string | **REQUIRED** | Payment period (see §5.3) |
| `min` | number | OPTIONAL | Minimum compensation amount (as decimal number in major currency units) |
| `max` | number | OPTIONAL | Maximum compensation amount (as decimal number in major currency units) |

**Constraints:**
- `currency` MUST be a valid ISO 4217 three-letter currency code (e.g., USD, EUR, GBP)
- `period` MUST be one of: `YEARLY`, `MONTHLY`, `WEEKLY`, `DAILY`, `HOURLY`
- At least one of `min` or `max` SHOULD be provided
- If both `min` and `max` are provided, `max` MUST be greater than or equal to `min`
- Amounts MUST be positive numbers expressed in major currency units (e.g., dollars, not cents; euros, not euro cents)

**Example:**
```json
{
  "currency": "USD",
  "min": 120000,
  "max": 180000,
  "period": "YEARLY"
}
```

## 5. Data Types and Formats

### 5.1 String Format

- Strings MUST be valid UTF-8
- Empty strings are valid but SHOULD be avoided for required fields
- Strings SHOULD NOT include leading or trailing whitespace

### 5.2 Employment Type Values

The `employmentType` field MUST use one of the following values:

- `FULL_TIME` - Full-time employment
- `PART_TIME` - Part-time employment
- `CONTRACT` - Contract or freelance work
- `TEMPORARY` - Temporary employment
- `INTERN` - Internship position
- `VOLUNTEER` - Volunteer position
- `PER_DIEM` - Per diem work
- `OTHER` - Other employment arrangement

### 5.3 Compensation Period Values

The `period` field in the Compensation Object MUST use one of:

- `YEARLY` - Annual salary
- `MONTHLY` - Monthly salary
- `WEEKLY` - Weekly pay
- `DAILY` - Daily rate
- `HOURLY` - Hourly rate

### 5.4 Date and Time Format

Dates and timestamps MUST use ISO 8601 format:

- Date only: `YYYY-MM-DD` (e.g., `2025-01-20`)
- Date and time: `YYYY-MM-DDTHH:MM:SSZ` (e.g., `2025-01-20T10:00:00Z`)
- Date and time with offset: `YYYY-MM-DDTHH:MM:SS±HH:MM` (e.g., `2025-01-20T10:00:00-05:00`)

### 5.5 URL Format

URLs MUST:
- Be absolute URLs (include scheme and domain)
- Use HTTP or HTTPS scheme
- Be properly percent-encoded as per RFC 3986

## 6. Validation Rules

### 6.1 Document Validation

A valid `jobs.json` document:
1. MUST be well-formed JSON
2. MUST include `version`, `company`, and `jobs` fields
3. MUST have `version` set to "1.0"
4. MUST have a valid `company` object
5. MUST have a `jobs` array (MAY be empty)

### 6.2 Job ID Uniqueness

Within a single `jobs.json` document:
- Each `job.id` MUST be unique
- Job IDs SHOULD remain stable across updates for the same position
- Job IDs SHOULD be opaque identifiers

### 6.3 URL Validation

All URL fields:
- MUST be absolute URLs
- MUST be accessible (RECOMMENDED)
- SHOULD use HTTPS
- MUST NOT contain user credentials

### 6.4 Required Field Validation

Parsers SHOULD reject documents missing required fields or provide appropriate error messages.

## 7. Extension Mechanism

### 7.1 Custom Fields

Organizations MAY add custom fields using the `x-` prefix:

```json
{
  "id": "job-001",
  "title": "Software Engineer",
  "url": "https://example.com/job-001",
  "x-internal-id": "HR-2025-001",
  "x-hiring-manager": "Jane Smith",
  "x-team-size": 8
}
```

### 7.2 Extension Guidelines

- Custom fields MUST be prefixed with `x-`
- Custom fields MUST NOT override standard fields
- Parsers MUST ignore unknown `x-` prefixed fields
- Custom fields SHOULD NOT be relied upon for critical functionality
- Future specification versions MAY standardize common custom fields

## 8. Examples

### 8.1 Minimal Valid Document

```json
{
  "version": "1.0",
  "company": {
    "name": "Example Corp",
    "url": "https://example.com"
  },
  "jobs": []
}
```

### 8.2 Single Job Listing

```json
{
  "version": "1.0",
  "company": {
    "name": "Example Corp",
    "url": "https://example.com"
  },
  "jobs": [
    {
      "id": "job-001",
      "title": "Software Engineer",
      "url": "https://example.com/careers/software-engineer",
      "location": {
        "city": "San Francisco",
        "state": "CA",
        "country": "USA",
        "remote": true
      }
    }
  ]
}
```

### 8.3 Complete Document with All Features

```json
{
  "version": "1.0",
  "lastUpdated": "2025-01-20T10:00:00Z",
  "company": {
    "name": "Example Corporation",
    "url": "https://example.com",
    "logo": "https://example.com/logo.png",
    "description": "A leading technology company"
  },
  "jobs": [
    {
      "id": "eng-001",
      "title": "Senior Software Engineer",
      "department": "Engineering",
      "description": "We are seeking an experienced software engineer to join our platform team.",
      "url": "https://example.com/careers/senior-software-engineer",
      "location": {
        "city": "San Francisco",
        "state": "CA",
        "country": "USA",
        "remote": true
      },
      "employmentType": "FULL_TIME",
      "postedDate": "2025-01-15",
      "expiresDate": "2025-03-15",
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
      "description": "Lead product strategy for our core platform.",
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
      "otherEmploymentTypes": ["CONTRACT"],
      "postedDate": "2025-01-10"
    },
    {
      "id": "intern-003",
      "title": "Software Engineering Intern",
      "department": "Engineering",
      "url": "https://example.com/careers/intern",
      "location": {
        "remote": true
      },
      "employmentType": "INTERN",
      "postedDate": "2025-01-01",
      "compensation": {
        "currency": "USD",
        "min": 25,
        "max": 35,
        "period": "HOURLY"
      }
    }
  ]
}
```

## 9. Version History

### Version 1.0 (2025-01-20)
- Initial specification release
- Core schema definition
- Support for basic job attributes
- Location and compensation data
- Extension mechanism with `x-` prefix

## 10. References

- **RFC 2119**: Key words for use in RFCs to Indicate Requirement Levels
- **RFC 8259**: The JavaScript Object Notation (JSON) Data Interchange Format
- **RFC 3986**: Uniform Resource Identifier (URI): Generic Syntax
- **ISO 8601**: Date and time format
- **ISO 3166-1**: Country codes
- **ISO 4217**: Currency codes

## 11. License

This specification is released under the MIT License.

## 12. Contributing

This specification is maintained at: https://github.com/lowlydba/jobsjson.org

Suggestions and improvements are welcome via GitHub issues and pull requests.

---

**Specification Maintainer**: lowlydba  
**Website**: https://jobsjson.org  
**Repository**: https://github.com/lowlydba/jobsjson.org
