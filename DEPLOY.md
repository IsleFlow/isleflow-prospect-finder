# IsleFlow Prospect Finder - Deployment Guide

## Quick Start (5 minutes)

### 1. Create project folder
```bash
mkdir isleflow-prospect-finder
cd isleflow-prospect-finder
```

### 2. Create these 3 files:

---

## File 1: `server.js`

```javascript
const express = require('express');
const cors = require('cors');
const path = require('path');

const app = express();
app.use(cors());
app.use(express.json());
app.use(express.static('public'));

// Proxy endpoint for Claude API
app.post('/api/claude', async (req, res) => {
  try {
    const response = await fetch('https://api.anthropic.com/v1/messages', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'x-api-key': process.env.ANTHROPIC_API_KEY,
        'anthropic-version': '2023-06-01'
      },
      body: JSON.stringify(req.body)
    });
    
    const data = await response.json();
    res.json(data);
  } catch (error) {
    console.error('API Error:', error);
    res.status(500).json({ error: error.message });
  }
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`IsleFlow running at http://localhost:${PORT}`);
});
```

---

## File 2: `package.json`

```json
{
  "name": "isleflow-prospect-finder",
  "version": "1.0.0",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "cors": "^2.8.5"
  }
}
```

---

## File 3: `public/index.html`

Copy the full React app into this HTML file (I'll provide this separately).

---

### 3. Install & Run

```bash
# Install dependencies
npm install

# Set your API key (Mac/Linux)
export ANTHROPIC_API_KEY=sk-ant-xxxxx

# Set your API key (Windows)
set ANTHROPIC_API_KEY=sk-ant-xxxxx

# Run the app
npm start
```

### 4. Open browser
Go to: **http://localhost:3000**

---

## That's it! 

The app will now make real API calls through your backend, keeping your API key secure.

---

## Deploying to the Web

### Vercel (Recommended - Free)
1. Push to GitHub
2. Connect to Vercel
3. Add `ANTHROPIC_API_KEY` in Vercel Environment Variables
4. Deploy

### Railway / Render / Heroku
Same process - add the environment variable in their dashboard.

---

## Cost Estimate

Each full search (15-20 prospects) uses approximately:
- ~50,000 input tokens
- ~15,000 output tokens
- **Cost: ~$0.30-0.50 per search** (using Claude Sonnet)

