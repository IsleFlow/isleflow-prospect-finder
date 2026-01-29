# IsleFlow Prospect Finder

AI-powered prospect research tool for finding construction executives who are ideal book-writing candidates.

## Deploy to Vercel (Easiest - 5 minutes)

### Step 1: Get the code on GitHub
1. Create a new GitHub repository
2. Upload these files:
   - `server.js`
   - `package.json`
   - `public/index.html`

### Step 2: Deploy on Vercel
1. Go to [vercel.com](https://vercel.com) and sign in with GitHub
2. Click "New Project"
3. Import your GitHub repository
4. **Important:** Add your API key:
   - Go to Settings → Environment Variables
   - Add: `ANTHROPIC_API_KEY` = `sk-ant-your-key-here`
5. Click Deploy

### Step 3: Done!
Your app will be live at `your-project.vercel.app`

---

## Run Locally

```bash
# Install dependencies
npm install

# Set your API key
export ANTHROPIC_API_KEY=sk-ant-xxxxx

# Run
npm start

# Open http://localhost:3000
```

---

## Cost

Each search uses approximately:
- ~50,000 input tokens
- ~15,000 output tokens
- **~$0.30-0.50 per search** (Claude Sonnet)

---

## Files

```
isleflow-prospect-finder/
├── server.js          # Express backend (proxies API calls)
├── package.json       # Dependencies
├── public/
│   └── index.html     # React frontend (all-in-one)
└── README.md
```
