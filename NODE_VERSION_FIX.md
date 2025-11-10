# Node.js Version Fix

## ✅ Problem Solved!

Your Node.js has been upgraded from v18.20.1 to v20.19.5, which is compatible with Next.js 16.

## Important: Loading nvm in New Terminals

When you open a **new terminal**, nvm needs to be loaded. You have two options:

### Option 1: Auto-load nvm (Recommended)

Add this to your `~/.bashrc` file to automatically load nvm in every new terminal:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```

Then reload your shell:
```bash
source ~/.bashrc
```

### Option 2: Manual Load (Each Terminal)

In each new terminal, run:
```bash
source ~/.nvm/nvm.sh
nvm use 20
```

## How to Run the Application Now

### Step 1: Make sure you're using Node.js 20

In your terminal, run:
```bash
source ~/.nvm/nvm.sh
nvm use 20
node --version  # Should show v20.19.5
```

### Step 2: Start MongoDB

Make sure MongoDB is running:
```bash
# Check if MongoDB is running
mongosh --eval "db.adminCommand('ping')" 2>/dev/null || echo "MongoDB not running"
```

If not running, start it:
```bash
# Linux
sudo systemctl start mongod
# or
mongod
```

### Step 3: Start Backend (Terminal 1)

```bash
source ~/.nvm/nvm.sh
nvm use 20
cd backend
npm run dev
```

### Step 4: Start Frontend (Terminal 2)

Open a new terminal and run:
```bash
source ~/.nvm/nvm.sh
nvm use 20
cd ~/Development/bitsa_app
npm run dev
```

### Step 5: Access the Application

Open your browser:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:5000/api/health

## Quick Start Script

You can also use the helper script:

```bash
./run-dev.sh
```

This will check your setup and provide instructions.

## Verify Node.js Version

To check which Node.js version you're using:
```bash
node --version
```

Should show: `v20.19.5`

## Troubleshooting

### "nvm: command not found"

If you get this error in a new terminal, you need to load nvm:
```bash
source ~/.nvm/nvm.sh
```

Or add it to your `~/.bashrc` (see Option 1 above).

### Still seeing Node.js 18

If `node --version` still shows v18:
```bash
source ~/.nvm/nvm.sh
nvm use 20
nvm alias default 20
```

### Next.js still complaining about Node version

1. Make sure you're using Node.js 20:
   ```bash
   source ~/.nvm/nvm.sh
   nvm use 20
   node --version
   ```

2. Clear Next.js cache:
   ```bash
   rm -rf .next
   npm run dev
   ```

## Summary

✅ Node.js upgraded to v20.19.5
✅ Set as default version
✅ Dependencies are compatible

**Next steps:**
1. Make sure nvm loads in new terminals (add to ~/.bashrc)
2. Start MongoDB
3. Start backend server
4. Start frontend server
5. Open http://localhost:3000

Happy coding! 🚀

