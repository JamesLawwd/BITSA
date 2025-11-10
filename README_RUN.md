# How to Run BITSA Hub - Quick Guide

## ⚠️ Important: Node.js Version

This project requires **Node.js 20.9.0 or higher**. Node.js 20.19.5 is already installed via nvm.

## Quick Start

### Option 1: Use the Dev Script (Easiest)

```bash
./dev.sh
```

This script automatically loads Node.js 20 and starts the dev server.

### Option 2: Manual Setup

**In your current terminal, run these commands:**

```bash
# Load nvm and switch to Node.js 20
source ~/.nvm/nvm.sh
nvm use 20

# Verify you're using Node.js 20
node --version  # Should show v20.19.5

# Now run the dev server
npm run dev
```

### Option 3: Start Fresh Terminal

If you open a **new terminal**, nvm should auto-load (it's in your .bashrc). Then just run:

```bash
cd ~/Development/bitsa_app
npm run dev
```

## Running the Full Application

### Step 1: Load Node.js 20

```bash
source ~/.nvm/nvm.sh
nvm use 20
```

### Step 2: Start MongoDB

```bash
# Check if MongoDB is running
mongosh --eval "db.adminCommand('ping')" 2>/dev/null || echo "Start MongoDB"

# If not running:
sudo systemctl start mongod
# or: mongod
```

### Step 3: Start Backend (Terminal 1)

```bash
source ~/.nvm/nvm.sh
nvm use 20
cd backend
npm run dev
```

### Step 4: Start Frontend (Terminal 2)

```bash
source ~/.nvm/nvm.sh
nvm use 20
cd ~/Development/bitsa_app
npm run dev
```

Or use the script:
```bash
./dev.sh
```

## Troubleshooting

### Still seeing Node.js 18?

**Problem:** Your terminal is using system Node.js 18 instead of nvm Node.js 20.

**Solution:** Load nvm in your current terminal:
```bash
source ~/.nvm/nvm.sh
nvm use 20
node --version  # Should show v20.19.5
```

### "nvm: command not found"

**Problem:** nvm is not loaded in your current terminal.

**Solution:** 
```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
nvm use 20
```

### Make it permanent

Add to your `~/.bashrc` (if not already there):
```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```

Then reload:
```bash
source ~/.bashrc
```

## Quick Commands

```bash
# Load Node.js 20
source ~/.nvm/nvm.sh && nvm use 20

# Check Node version
node --version

# Run dev server (after loading nvm)
npm run dev

# Or use the script
./dev.sh
```

## Summary

✅ Node.js 20.19.5 is installed
✅ Set as default in nvm
✅ Use `./dev.sh` or load nvm manually before running `npm run dev`

**Next:** Run `./dev.sh` or load nvm and run `npm run dev`!

