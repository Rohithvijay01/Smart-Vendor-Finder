# Smart Vendor Finder – Blockchain-Based Supply Chain Management

**Smart Vendor Finder** is an intelligent, blockchain-powered platform designed to streamline local vendor discovery, enable secure payments, and deliver demand-driven purchasing decisions using AI-powered forecasting. This solution integrates Web3 technology with traditional supply chain workflows to build trust, transparency, and efficiency.

---

## ✅ Key Features

- 🛒 **Vendor Marketplace**  
  Discover and verify nearby vendors offering the best products at the lowest price.

- 🔐 **Blockchain-Backed Payments**  
  Enables decentralized transactions with Ethereum using WalletConnect and Alchemy.

- 📦 **Smart Inventory Management**  
  Seamless tracking of purchased products and dynamic stock updates.

- 📊 **Sales Prediction (AI + ML)**  
  Predicts future demand using historical data and suggests restocking decisions.

- 📍 **Geo-Based Vendor Search (Extensible)**  
  Can be integrated with maps to locate nearby suppliers in real-time.

- 🧠 **AI-Powered Insights**  
  Recommends vendors and products based on demand forecasting and usage patterns.

---

## ⚙️ Tech Stack

### 💻 Web Application (MERN Stack)
- **MongoDB** – Database
- **Express.js** – Backend APIs
- **React.js** – Frontend Interface
- **Node.js** – Server Runtime

### 🔗 Blockchain & Web3
- **Solidity** – Smart Contracts
- **Foundry** – Contract Testing & Deployment
- **Wagmi + WalletConnect** – Wallet Integrations
- **Alchemy** – Ethereum Node Provider

### 🤖 Machine Learning & Forecasting
- **Flask** – ML API Server
- **Scikit-learn** – Forecasting Algorithms
- **NumPy & Pandas** – Data Processing
- **Jupyter Notebooks** – Model Development

---


## 🧭 Project Workflow

```
Smart-Vendor-Finder/
├── client/              # Frontend (React)
│   └── src/
│       └── components/
│           └── VendorList.jsx
│           └── SearchBar.jsx
│       └── App.jsx
├── server/              # Backend (Node.js + Express)
│   └── routes/
│       └── vendors.js
│   └── models/
│       └── Vendor.js
│   └── index.js or app.js
├── contracts/           # Blockchain (Solidity)
│   └── VendorPayment.sol
├── ml/                  # Machine Learning scripts
│   └── my_forecast.py
│   └── api.py
│   └── sales_data.csv
└── README.md
```
