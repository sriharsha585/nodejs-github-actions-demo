# Node.js CI Pipeline with GitHub Actions

## Project Overview

This project demonstrates a complete Continuous Integration (CI) pipeline using GitHub Actions for a Node.js application.

The pipeline automatically:

* Checks out source code
* Installs dependencies
* Runs ESLint code quality checks
* Executes Jest unit tests
* Builds a Docker image

This project helps understand how modern DevOps teams automate validation and packaging of applications before deployment.

---

## Architecture

```text
Developer
    │
    ▼
GitHub Repository
    │
    ▼
GitHub Actions
    │
    ├── Checkout Code
    ├── Install Dependencies
    ├── Run ESLint
    ├── Run Jest Tests
    └── Build Docker Image
```

---

## Technologies Used

* Node.js
* GitHub Actions
* ESLint
* Jest
* Docker
* Git

---

## Project Structure

```text
nodejs-github-actions-demo/
│
├── app.js
├── app.test.js
├── package.json
├── package-lock.json
├── Dockerfile
├── eslint.config.mjs
├── README.md
│
└── .github
    └── workflows
        └── ci.yml
```

---

## Application Code

### app.js

```javascript
function sum(a, b) {
  return a + b;
}

module.exports = sum;
```

### app.test.js

```javascript
const sum = require('./app');

test('adds 1 + 2 to equal 3', () => {
  expect(sum(1, 2)).toBe(3);
});
```

---

## GitHub Actions Workflow

Location:

```text
.github/workflows/ci.yml
```

Workflow Steps:

1. Checkout Source Code
2. Setup Node.js Environment
3. Install Dependencies
4. Run ESLint
5. Execute Unit Tests
6. Build Docker Image

---

## CI Workflow

### Trigger

Pipeline runs automatically on:

```yaml
push:
  branches:
    - main

pull_request:
  branches:
    - main
```

---

### Checkout Code

```yaml
uses: actions/checkout@v4
```

Downloads repository contents into the GitHub-hosted runner.

---

### Setup Node.js

```yaml
uses: actions/setup-node@v4
```

Installs Node.js runtime.

---

### Install Dependencies

```yaml
run: npm ci
```

Uses package-lock.json to install exact dependency versions.

---

### Run ESLint

```yaml
run: npm run lint
```

Performs static code analysis and enforces coding standards.

---

### Run Jest Tests

```yaml
run: npm test
```

Executes unit tests.

Expected output:

```text
PASS app.test.js
```

---

### Build Docker Image

```yaml
uses: docker/build-push-action@v6
```

Builds a Docker image for the application.

Example:

```text
node-demo:latest
```

---

## Dockerfile

```dockerfile
FROM node:22-alpine

WORKDIR /app

COPY package*.json ./

RUN npm ci

COPY . .

CMD ["npm", "test"]
```

---

## Commands Used

### Install Dependencies

```bash
npm install
```

### Run Linting

```bash
npm run lint
```

### Run Unit Tests

```bash
npm test
```

### Build Docker Image

```bash
docker build -t node-demo .
```

### Run Docker Container

```bash
docker run node-demo
```

---

## Challenges Faced

### ESLint Errors

Error:

```text
require is not defined
module is not defined
test is not defined
expect is not defined
```

Root Cause:

ESLint was not configured for Node.js and Jest globals.

Resolution:

Updated eslint.config.mjs and added globals support.

---

### Dependency Conflict

Error:

```text
ERESOLVE could not resolve
```

Root Cause:

Version mismatch between:

```text
@eslint/js 10.x
eslint 9.x
```

Resolution:

Removed unnecessary packages and aligned dependency versions.

---

### GitHub Actions YAML Error

Error:

```text
Unexpected value
```

Root Cause:

Incorrect YAML indentation.

Resolution:

Corrected workflow structure and indentation.

---

## Key Learnings

* GitHub Actions Workflow Creation
* GitHub Hosted Runners
* CI Pipeline Design
* ESLint Integration
* Jest Unit Testing
* Docker Image Build Automation
* Dependency Management
* YAML Troubleshooting
* Git Troubleshooting

---

## Interview Questions

### Why use GitHub Actions?

GitHub Actions provides an integrated CI/CD platform within GitHub, eliminating the need to maintain separate CI servers.

---

### Why use npm ci instead of npm install?

npm ci installs dependencies using package-lock.json, ensuring reproducible and deterministic builds in CI/CD pipelines.

---

### Why run tests before Docker build?

Testing validates application functionality before packaging it into a deployable artifact.

---

### What is a GitHub Runner?

A runner is the execution environment where GitHub Actions jobs run. GitHub-hosted runners are temporary virtual machines created for each workflow execution.

---

## Future Enhancements

* Docker Hub Integration
* Security Scanning
* GitOps Deployment
* Argo CD Integration
* Kubernetes Deployment
* Multi-Environment CI/CD
* SonarQube Integration

---

## Author

Sai Sri Harsha Nandam

DevOps Engineer

Skills:
AWS | GitHub Actions | Jenkins | Docker | Kubernetes | Argo CD | Terraform | Ansible | Linux
