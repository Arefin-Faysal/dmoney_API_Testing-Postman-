# DMoney API Automation with Postman & Newman

## What is DMoney?

DMoney is a mobile-money (digital wallet) system, similar to bKash or Nagad. Admins create Customer, Agent and Merchant accounts, and users can deposit, send money, cash out and pay bills through a REST API. This project tests those APIs with a Postman collection that runs from the command line with Newman.

## Technology Used

- **Postman** – builds the API requests and writes the test scripts
- **Newman** – runs the Postman collection from the command line
- **newman-reporter-htmlextra** – creates the HTML test report
- **Node.js & npm** – runs Newman and installs the packages
- **JavaScript** – Postman test scripts and the runner script (`report.js`)
- **DMoney Transaction API** – the API under test (Node.js, Express, MySQL, run with Docker)

## Test Coverage

The collection `Assignment SDET` runs these flows in order:

| Module | Scenarios |
|---|---|
| Admin | Login, login with a wrong email |
| Create User | Create Customer 1 & 2, Agent and Merchant; duplicate customer; invalid token |
| Active User | Suspend a user, activate Customer 1 & 2, Agent and Merchant |
| System | System login, deposit to Agent, deposit to Customer (not allowed) |
| Agent | Login, OTP verify, invalid OTP, deposit to Customer |
| Customer 1 | Login, OTP verify, send money to Customer 2, send an invalid amount |
| Customer 2 | Login, OTP verify, cash out, cash out with an empty token, pay bill, pay to an invalid account |

## Project Structure

```
dmoney_newman_API/
├── collection/
│   └── Assignment SDET.postman_collection.json   # Postman collection
├── Reports/
│   └── report.html                               # Generated Newman report
├── report.js                                     # Newman runner script
├── package.json
└── README.md
```

## How to Run

### Prerequisites

- [Node.js](https://nodejs.org/) (includes npm)
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) to run the DMoney API

### 1. Start the DMoney API

The tests call the API at `http://localhost:5000`.

```bash
git clone https://github.com/salmansrabon/dmoney-transaction-api.git
cd dmoney-transaction-api
docker compose up -d --build
```

Wait until `docker compose ps` shows `dmoney-mysql` as `healthy` and `dmoney-api` as `Up`.

### 2. Clone this project and install the packages

```bash
git clone <this-repo-url>
cd dmoney_newman_API
npm install
```

### 3. Run the tests

```bash
node report.js
```

When the run finishes, the console prints `collection run complete!` and the report is saved to `Reports/report.html`. Open that file in a browser to see the results.

You can also run the collection directly with the Newman CLI:

```bash
npx newman run "collection/Assignment SDET.postman_collection.json" -r cli,htmlextra --reporter-htmlextra-export Reports/report.html
```

## Links

- **Test Cases (Excel):** _link coming soon_
- **API Documentation:** _link coming soon_

## Newman Report

_Screenshot coming soon_

<!-- Add the screenshot like this: ![Newman Report](Reports/newman-report.png) -->
