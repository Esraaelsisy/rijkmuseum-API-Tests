# Rijksmuseum API Tests

This repository contains automated API tests for the Rijksmuseum public API. The tests are written in **Postman** and executed via **Newman** in a continuous integration (CI) pipeline using **GitHub Actions**.

## Repository Structure

```plaintex
RIJKMUSEUM-API-TESTS/
├── .github/
│   └── workflows/
│       └── ci.yml                             # GitHub Actions CI workflow to run tests automatically
├── collections/
│   ├── collection_API.collection.json         # Postman collection to test fetching collections
│   ├── collectionDetails_API.collection.json  # Postman collection to test retrieving collection details
│   └── collectionTiles_API.collection.json    # Postman collection to test retrieving tiles for collections
├── environment/
│   ├── en_production.environment.json         # Postman environment for English
│   ├── nl_production.environment.json         # Postman environment for Dutch
│   └── globals.json                           # Postman global variables (API key, etc.)
├── .gitattributes                             # Git configuration for file attributes
├── .gitignore                                 # Ignore certain files in Git
└── README.md                                  # This readme file
```

## Postman Collections

1. **`collection_API.collection.json`**

   This collection tests fetching collections from the Rijksmuseum API. It verifies the main API endpoints for retrieving collections of art objects.

2. **`collectionDetails_API.collection.json`**

   This collection tests retrieving detailed information about specific art objects from the Rijksmuseum API.

3. **`collectionTiles_API.collection.json`**

   This collection tests retrieving tile images for art objects from the Rijksmuseum API.

## Environments and Globals

- **Environment Files**:
  - `en_production.environment.json`: Environment variables for testing the English version of the Rijksmuseum API.
  - `nl_production.environment.json`: Environment variables for testing the Dutch version of the Rijksmuseum API.

- **Globals**:
  - The `globals.json` file stores global variables, such as the API key and request format.

## Continuous Integration (CI)

This repository uses **GitHub Actions** to automatically run the Postman collections when changes are pushed to the `main` branch. The CI pipeline is defined in the `.github/workflows/ci.yml` file.

### CI Pipeline Steps

1. **Checkout the repository**: Pulls the latest code and files from the repository.
2. **Install Node.js and Newman**: Installs Node.js and Newman, which are required to run the tests.
3. **Run the Postman collections**: Each collection is run twice—once with the **English** environment and once with the **Dutch** environment.
4. **Generate Reports**: HTML reports are generated for each run.
5. **Upload Reports**: The reports are uploaded as build artifacts, which can be downloaded from the GitHub Actions interface.

## Handling Errors

The workflow is configured with `continue-on-error: true`, which means that even if a test fails, the remaining collections will still be executed and their reports will still be generated.

## Running Tests Locally

You can run the Postman collections locally using **Newman**.

### 1. Install Newman

```bash
npm install -g newman
```

### 2. Run a Postman Collection

```bash
newman run collections/collection_API.collection.json \
  --environment environment/en_production.environment.json \
  --globals environment/globals.json \
  --reporters cli,html-extra \
  --reporter-html-extra-export newman-reports/newman-report-collection-EN.html
```
  You can replace `collection_API.collection.json` with any of the other collection files and change the environment to `nl_production.environment.json` to run the Dutch version.

## Viewing Test Results

### GitHub Actions:

1. Navigate to the **Actions** tab in your GitHub repository.
2. Select the latest workflow run.
3. Download the generated HTML reports from the **Artifacts** section.

### Local Run:

- The HTML report will be generated in the file specified with the `--reporter-html-extra-export` flag (e.g., `newman-report-collection-EN.html`).
- Open the HTML file in a web browser to view detailed test results.

## How to Contribute

1. **Fork the repository**.
2. **Create a new branch** (`git checkout -b feature-branch`).
3. **Make your changes**.
4. **Commit your changes** (`git commit -am 'Add some feature'`).
5. **Push to the branch** (`git push origin feature-branch`).
6. Open a **pull request**.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

### Happy Testing!