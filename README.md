# Bruno_API_Tests

A collection of API tests for the [Simple Books API](https://simple-books-api.click), built with [Bruno](https://www.usebruno.com/) — an open-source, offline-first API client.

API Documentation by Bruno is available at:  https://shuvamaich.github.io/Bruno_API_Tests/

## About the Project

This project contains automated API tests written in Bruno's YAML-based collection format. The tests cover the full lifecycle of the Simple Books API, including checking service health, browsing the book catalogue, managing orders, and registering API clients.

## What is Bruno?

Bruno is a Git-friendly and offline-first open-source API client aimed at revolutionizing the status quo represented by tools like Postman and Insomnia.
Its absolutely similar to Postman, even the functions and the UI so adaptability is very easy.
Read more at https://www.usebruno.com/compare/bruno-vs-postman

## API Under Test

**Base URL:** `https://simple-books-api.click`

The Simple Books API is a REST API that allows clients to:
- Query the status of the service
- Browse available books
- Place, retrieve, update, and delete orders (requires an API key)

## Test Collection

| Request | Method | Endpoint | Description |
|---|---|---|---|
| Status | GET | `/status` | Verifies the API is up and returns `"OK"` |
| Books | GET | `/books` | Retrieves the list of all available books |
| BookId | GET | `/books/:bookId` | Retrieves a single book by its ID |
| SubmitOrder | POST | `/orders` | Places a new order for a book |
| Order | GET | `/orders` | Retrieves all orders for the authenticated client |
| OrderId | GET | `/orders/:orderId` | Retrieves a single order by its ID |
| UpdateOrder | PATCH | `/orders/:orderId` | Updates an existing order |
| DeleteOrder | DELETE | `/orders/:orderId` | Deletes an existing order |
| Request API Key | POST | `/api-clients` | Registers a new API client and returns an access token |

## Prerequisites

- [Bruno](https://www.usebruno.com/downloads) desktop app **or** the [Bruno CLI](https://docs.usebruno.com/bru-cli/overview) for running tests from the command line.

## Environment Setup

The collection ships with a **Books Environment** that contains the following variables:

| Variable | Description |
|---|---|
| `BaseUrl` | The API base URL (`https://simple-books-api.click`) |
| `Authorization` | Your API bearer token (secret — obtain via the *Request API Key* request) |

To get your API key, run the **Request API Key** request once. Copy the returned `accessToken` value and set it as the `Authorization` environment variable.

## Running the Tests

### Bruno Desktop App
1. Open Bruno and click **Open Collection**.
2. Select this repository folder.
3. Choose the **Books Environment** from the environment picker.
4. Run individual requests or use **Run Collection** to execute the full suite.

### Bruno CLI
```bash
# Install the CLI
npm install -g @usebruno/cli

# Run the full collection
bru run --env "Books Environment"
```
<img width="1591" height="992" alt="image" src="https://github.com/user-attachments/assets/3318f250-5d1a-4ad4-8805-23ad93725744" />


The tests are fully end to end automated and also configured to run on Jenkins where you can also find the test results and HTML Reports:

<img width="3423" height="731" alt="image" src="https://github.com/user-attachments/assets/60183f0c-da96-4fa3-bd5a-42a487936f0e" />

<img width="909" height="657" alt="image" src="https://github.com/user-attachments/assets/fa043d77-8977-46bb-822d-3301361eb7fa" />

<img width="3423" height="915" alt="image" src="https://github.com/user-attachments/assets/559cc4ff-4980-4867-9fdd-f453195a1965" />

<img width="3432" height="3833" alt="screencapture-localhost-8080-job-Bruno-Api-Tests-17-artifact-results-html-2026-03-27-00_21_33" src="https://github.com/user-attachments/assets/4a38fc86-acfa-4ecf-8453-54931990a4d7" />










