# Project Structure Overview
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

---

### `SearchBar.jsx`
```jsx
import React from 'react';

export default function SearchBar({ query, setQuery }) {
  return (
    <input
      type="text"
      placeholder="Search vendors by name or location..."
      value={query}
      onChange={(e) => setQuery(e.target.value)}
      style={{
        padding: '10px',
        width: '100%',
        marginBottom: '20px',
        borderRadius: '8px',
        border: '1px solid #ccc'
      }}
    />
  );
}
```

### `VendorList.jsx`
```jsx
import React, { useEffect, useState } from 'react';
import axios from 'axios';
import SearchBar from './SearchBar';

export default function VendorList() {
  const [vendors, setVendors] = useState([]);
  const [query, setQuery] = useState('');

  useEffect(() => {
    axios.get('/api/vendors')
      .then(res => setVendors(res.data))
      .catch(console.error);
  }, []);

  const filtered = vendors.filter(v =>
    v.name.toLowerCase().includes(query.toLowerCase()) ||
    v.location.toLowerCase().includes(query.toLowerCase())
  );

  return (
    <div>
      <h2>Available Vendors</h2>
      <SearchBar query={query} setQuery={setQuery} />
      <ul>
        {filtered.map(v => (
          <li key={v._id}>
            <strong>{v.name}</strong> – {v.location} – {v.price} ETH
          </li>
        ))}
      </ul>
    </div>
  );
}
```

### `Vendor.js`
```js
const mongoose = require('mongoose');

const vendorSchema = new mongoose.Schema({
  name: String,
  location: String,
  price: Number,
  blockchainAddress: String
});

module.exports = mongoose.model('Vendor', vendorSchema);
```

### `vendors.js` (Express Routes)
```js
const express = require('express');
const router = express.Router();
const Vendor = require('../models/Vendor');

router.get('/vendors', async (req, res) => {
  try {
    const vendors = await Vendor.find();
    res.json(vendors);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

router.post('/vendors', async (req, res) => {
  const { name, location, price, blockchainAddress } = req.body;
  try {
    const vendor = new Vendor({ name, location, price, blockchainAddress });
    await vendor.save();
    res.status(201).json(vendor);
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
});

module.exports = router;
```

### `my_forecast.py`
```python
import pandas as pd
from sklearn.linear_model import LinearRegression
import joblib

def train_forecast(csv_path):
    df = pd.read_csv(csv_path)
    X = df[['month', 'promo']].values
    y = df['sales'].values
    model = LinearRegression().fit(X, y)
    joblib.dump(model, 'ml/forecast_model.pkl')
    print('Model trained and saved to forecast_model.pkl')

if __name__ == '__main__':
    train_forecast('ml/sales_data.csv')
```

### `api.py` (Flask ML API)
```python
from flask import Flask, request, jsonify
import joblib
import numpy as np

app = Flask(__name__)
model = joblib.load('forecast_model.pkl')

@app.route('/predict', methods=['POST'])
def predict():
    data = request.get_json()
    month = data['month']
    promo = data['promo']
    prediction = model.predict(np.array([[month, promo]]))
    return jsonify({'predicted_sales': float(prediction[0])})

if __name__ == '__main__':
    app.run(debug=True)
```

### `VendorPayment.sol`
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract VendorPayment {
    event Paid(address indexed buyer, address indexed vendor, uint amount);

    function payVendor(address payable vendor) external payable {
        require(msg.value > 0, "Must send ETH");
        vendor.transfer(msg.value);
        emit Paid(msg.sender, vendor, msg.value);
    }

    function getBalance() public view returns (uint) {
        return address(this).balance;
    }
}
