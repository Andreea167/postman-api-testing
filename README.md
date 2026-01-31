# Postman API Testing with Newman

This repository contains a Postman collection including automated API tests, designed to run with Newman in GitHub Actions.

## Test Collection

The collection includes 13 API tests covering:

- **Auth API Tests**: Token creation with valid/invalid credentials
- **Booking API Tests**: CRUD operations for booking management
  - Health check (Ping)
  - Get all bookings
  - Create, read, update, and delete bookings
  - Error handling (404, 403 responses)

## GitHub Actions Workflow

The workflow automatically runs on:
- Push to `main` or `master` branch
- Pull requests to `main` or `master` branch
- Manual trigger via GitHub Actions UI

### What the workflow does:

1. Checks out the repository
2. Sets up Node.js environment
3. Installs Newman and HTML reporters
4. Runs all API tests
5. Generates HTML test reports
6. Uploads reports as artifacts (available for 30 days)

## Viewing Test Reports

After a workflow run completes:

1. Go to the **Actions** tab in your GitHub repository
2. Click on the latest workflow run
3. Scroll down to **Artifacts**
4. Download `newman-test-reports`
5. Extract and open `newman-detailed-report.html` in your browser

## Running Tests Locally

### Prerequisites
```bash
npm install -g newman
npm install -g newman-reporter-htmlextra
```

### Run the tests
```bash
newman run api-postman-automation.json --reporters cli,htmlextra --reporter-htmlextra-export report.html
```

## Project Structure

```
.
├── .github/
│   └── workflows/
│       └── newman-tests.yml    # GitHub Actions workflow
├── api-postman-automation.json # Postman collection
└── README.md                   # This file
```

## API Endpoints Tested

Base URL: `https://restful-booker.herokuapp.com`

- `POST /auth` - Authentication
- `GET /ping` - Health check
- `GET /booking` - Get all bookings
- `POST /booking` - Create booking
- `GET /booking/:id` - Get booking by ID
- `PUT /booking/:id` - Update booking (requires auth)
- `PATCH /booking/:id` - Partial update (requires auth)
- `DELETE /booking/:id` - Delete booking (requires auth)

## Features

- Automated test execution on every push
- Detailed HTML reports with pass/fail statistics
- Request/response logging
- Authentication token management
- Dynamic test data generation
- Error scenario testing

## Notes

- Tests run against a public API (Restful Booker)
- No sensitive credentials required
- Reports are automatically archived for 30 days
- Tests can be triggered manually from the Actions tab

