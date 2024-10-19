# API Testing Project

## Overview
This repository hosts a comprehensive suite of tests for the Cat Facts API and PoetryDB API, built with Postman and seamlessly integrated into a GitHub Actions pipeline for automated testing.


## Project Structure
```
├── .github/
│   └── workflows/
│       └── api-tests.yml
├── collections/
│   ├── Cat_Facts_API_Tests.postman_collection.json
│   └── PoetryDB_API_Tests.postman_collection.json
├── environments/
│   ├── dev.postman_collection.json
└── README.md
```

## Test Cases

### PoetryDB API Tests

| Test ID | Test Case | Steps | Expected Result | Validation Method |
|---------|-----------|--------|-----------------|-------------------|
| POE_001 | Get Random Poem | 1. Send GET request to `/random` <br> 2. Verify response status <br> 3. Validate response schema | - Status code: 200 <br> - Response contains valid poem object <br> - Required fields present | - Status code assertion <br> - JSON schema validation <br> - Response time check |
| POE_002 | Search Poem by Author | 1. Send GET request to `/author/{author}` <br> 2. Verify response <br> 3. Validate data structure | - Status code: 200 <br> - Poems by specified author returned <br> - Correct data format | - Status code assertion <br> - Author field validation <br> - Array structure check |
| POE_003 | Invalid Author Search | 1. Send GET request with non-existent author <br> 2. Verify error handling | - Status code: 404 <br> - Appropriate error message | - Status code assertion <br> - Error message validation |

### Cat Facts API Tests

| Test ID | Test Case | Steps | Expected Result | Validation Method |
|---------|-----------|--------|-----------------|-------------------|
| CAT_001 | Get Random Fact | 1. Send GET request to `/facts/random` <br> 2. Verify response <br> 3. Validate fact structure | - Status code: 200 <br> - Single fact returned <br> - Valid fact object | - Status code assertion <br> - JSON schema validation <br> - Response format check |
| CAT_002 | Get Multiple Facts | 1. Send GET request with amount parameter <br> 2. Verify response array | - Status code: 200 <br> - Correct number of facts <br> - Valid array structure | - Status code assertion <br> - Array length validation <br> - Data structure check |
| CAT_003 | Invalid Parameter | 1. Send GET request with invalid amount <br> 2. Verify error handling | - Status code: 400 <br> - Error message present | - Status code assertion <br> - Error response validation |

## Validation Approach

### Schema Validation
- JSON Schema validation ensures response structure consistency
- Required fields presence validation
- Data type validation for each field

### Response Validation
- Status code assertions for different scenarios
- Response time threshold checks
- Content-Type header validation
- Response body structure verification

### Data Validation
- Data format verification
- Field value validation
- Array length validation where applicable
- Error message format validation

## Setup Instructions

1. Clone the repository
2. Install dependencies:
```bash
npm install -g newman
npm install -g newman-reporter-htmlextra
```

3. Run tests locally:
```bash
newman run collections/PoetryDB_API_Tests.postman_collection.json -e environments/dev.json -r cli,htmlextra
newman newman run collections/Cat_Facts_API_Tests.postman_collection.json -e environments/dev.json -r cli,htmlextra
```

## GitHub Actions Integration

Tests are automatically executed on:
- Push to main branch
- Pull request to main branch
- Manual trigger

Results are available in GitHub Actions artifacts.
