# StellAura — Stellar Wallet Explorer dApp

A decentralized application (dApp) built on the **Stellar Testnet** that lets anyone look up a Stellar wallet address and instantly see its XLM balance, account statistics, and full transaction history — powered entirely by the Stellar Horizon API.

---

## What is this project?

StellAura is a **read-only blockchain explorer** for the Stellar network. You enter a Stellar public key (wallet address), and the app fetches real, live data directly from the Stellar blockchain — no backend server, no database, no login required.

It was built as a submission for the **Stellar Philippines UniTour Hackathon 2026** at the University of the East, Caloocan Campus.

---

## Live Demo

> Replace this with your GitHub Pages URL after deployment  
> Example: `https://your-username.github.io/stellarscope`

---

## Features

- Look up any Stellar testnet wallet address instantly
- View native XLM balance, subentry count, and recent operation count
- Browse the last 20 transactions with type, amount, and date
- Each transaction links to Stellar.Expert for full on-chain details
- One-click copy of the full wallet address
- Clean split-panel UI with a sticky sidebar and scrollable dashboard
- All custom SVG icons — no emoji, no icon libraries
- Fully responsive for mobile and desktop

---

## How the System Works

This section explains what actually happens when you use StellAura — step by step.

### 1. What is a Stellar Wallet Address?

A Stellar wallet address (also called a **public key**) is a unique 56-character identifier that looks like this:

```
GAAZI4TCR3TY5OJHCTJC2A4QSY6CJWJH5IAJTGKIN2ER7LBNVKOCCWN
```

It always starts with the letter `G`. This is your account's public identity on the Stellar blockchain. It is safe to share — anyone can look it up, but no one can move your funds without the matching **private key** (which StellAura never touches or asks for).

---

### 2. What is the Stellar Blockchain?

Stellar is a **distributed ledger** — a record of every account and transaction that is shared across thousands of computers (called nodes) around the world. No single person or company owns or controls it. Every time a payment is made, it gets recorded permanently across all these nodes simultaneously.

The Stellar **Testnet** is a separate, identical copy of the network used for development and testing. It uses fake XLM with no real monetary value, which makes it safe for hackathon projects and learning.

---

### 3. What is the Horizon API?

Horizon is Stellar's official **REST API** — a publicly available web service that acts as a bridge between apps and the Stellar network. Instead of running your own Stellar node (which is complex and expensive), developers simply send HTTP requests to Horizon and receive blockchain data as JSON.

StellAura uses two Horizon endpoints:

| Endpoint | What it returns |
|---|---|
| `GET /accounts/{address}` | Balance, subentry count, account flags |
| `GET /accounts/{address}/operations` | List of recent operations (payments, account creation, etc.) |

The Testnet Horizon base URL is:
```
https://horizon-testnet.stellar.org
```

---

### 4. How StellAura Fetches Data

Here is the exact flow of what happens when you click "Explore Wallet":

```
Step 1 — Input validation
  The app checks that the address starts with G
  and is exactly 56 characters long.

Step 2 — Two parallel API requests are sent
  → GET /accounts/{address}
      Returns: XLM balance, subentry count, account metadata

  → GET /accounts/{address}/operations?limit=20&order=desc
      Returns: The 20 most recent blockchain operations

Step 3 — The responses arrive as JSON
  The app parses the data and extracts what it needs.

Step 4 — The dashboard is rendered
  Balance, stats, and the transaction list are displayed
  in the browser — no page reload, no server involved.
```

All of this happens directly in the **browser using JavaScript**. There is no backend. StellAura talks to the Stellar network directly from your browser tab.

---

### 5. What is an "Operation" on Stellar?

On Stellar, a **transaction** can contain one or more **operations**. An operation is a single action, such as:

| Operation Type | Meaning |
|---|---|
| `payment` | XLM or another asset was sent from one account to another |
| `create_account` | A new Stellar account was created and funded |
| `change_trust` | A trustline was set up for a non-XLM asset |
| `manage_sell_offer` | A sell order was placed on the Stellar DEX |
| `path_payment` | A cross-asset payment was made via the DEX |

StellAura displays all operation types with readable labels and directional arrows (incoming / outgoing / other).

---

### 6. Why is this a "dApp"?

A **decentralized application (dApp)** is an app that reads from or writes to a blockchain instead of a traditional centralized server.

StellAura qualifies as a dApp because:
- All data comes directly from the **Stellar blockchain** via the Horizon API
- There is no central database storing user data
- No login, no account, no tracking — the blockchain is the only source of truth
- The app is deployed as a **static file** — anyone can host it or verify the code

---

## Tech Stack

| Technology | Role |
|---|---|
| HTML / CSS / JavaScript | Frontend (no frameworks needed) |
| Stellar Horizon REST API | Blockchain data source |
| Stellar Testnet | The blockchain network |
| GitHub Pages | Static hosting |
| Google Fonts (Syne + DM Mono + Cabinet Grotesk) | Typography |
| Custom inline SVG | All icons and the logo |

---

## Setup & Running Locally

### Requirements

- Any modern web browser (Chrome, Firefox, Edge, Safari)
- No Node.js, no npm, no build tools required

### Steps

**1. Clone the repository**

```bash
git clone https://github.com/YOUR_USERNAME/stellarscope.git
cd stellarscope
```

**2. Open the app**

Simply open `index.html` in your browser:

```bash
# On macOS
open index.html

# On Windows (PowerShell)
start index.html

# Or just double-click the file
```

That is it. The app is a single HTML file with no dependencies to install.

---

## Deploying on GitHub Pages (Testnet Deployment)

Since the Stellar Testnet is a live public network, running the app on GitHub Pages counts as deploying on the testnet — the app connects directly to `horizon-testnet.stellar.org` from any browser.

**Steps:**

1. Push your repository to GitHub
2. Go to your repository → **Settings** → **Pages**
3. Under "Source", select **main branch** and **/ (root)**
4. Click **Save**
5. GitHub will give you a URL like: `https://your-username.github.io/stellarscope`

Your dApp is now live and accessible to anyone.

---

## Testing the App

Use any of these funded testnet addresses to explore real blockchain data:

```
GAAZI4TCR3TY5OJHCTJC2A4QSY6CJWJH5IAJTGKIN2ER7LBNVKOCCWN
```

To create your own testnet wallet:
1. Go to [Stellar Laboratory](https://laboratory.stellar.org/)
2. Click **Generate Keypair** to create a new address
3. Click **Fund Account with Friendbot** to add testnet XLM
4. Paste your new public key into StellAura

---

## Project Structure

```
stellarscope/
├── index.html      ← The complete dApp (single file)
└── README.md       ← This file
```

The entire application is contained in one HTML file. This was intentional — it keeps deployment simple (just one file to host) and makes the code easy to read and audit.

---

## Submission Checklist

- [x] Unique dApp — a Stellar wallet explorer with custom design, SVG icons, and a split-panel layout not found in any existing Stellar template
- [x] GitHub repository with README (this file)
- [x] README written in English
- [x] App communicates with the Stellar Testnet (`horizon-testnet.stellar.org`)

---

## License

MIT License — free to use, study, modify, and distribute.

---

## Author

Built by a CS student at the **University of the East — Caloocan Campus**  
Submitted for the **Stellar Philippines UniTour Hackathon 2026**