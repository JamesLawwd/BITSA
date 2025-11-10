# Quick Start Guide - BITSA Hub

## Step 1: Install Dependencies

### Frontend (if not already installed):
```bash
npm install
```

### Backend:
```bash
cd backend
npm install
cd ..
```

## Step 2: Set Up Environment Variables

### Backend Environment File

Create a file `backend/.env` with the following content:

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/bitsa_hub
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production_min_32_characters_long
JWT_EXPIRE=7d
NODE_ENV=development
FRONTEND_URL=http://localhost:3000
```

**Quick command to create it:**
```bash
cat > backend/.env << 'EOF'
PORT=5000
MONGODB_URI=mongodb://localhost:27017/bitsa_hub
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production_min_32_characters_long
JWT_EXPIRE=7d
NODE_ENV=development
FRONTEND_URL=http://localhost:3000
EOF
```

### Frontend Environment File

Create a file `.env.local` in the root directory with:

```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

**Quick command to create it:**
```bash
cat > .env.local << 'EOF'
NEXT_PUBLIC_API_URL=http://localhost:5000/api
EOF
```

## Step 3: Start MongoDB

### Option A: Local MongoDB
Make sure MongoDB is running on your system:

**Linux:**
```bash
sudo systemctl start mongod
# or
mongod
```

**Mac:**
```bash
brew services start mongodb-community
# or
mongod
```

**Windows:**
Start MongoDB service from Services or run `mongod` in a terminal.

### Option B: MongoDB Atlas (Cloud)
If using MongoDB Atlas, update the `MONGODB_URI` in `backend/.env` with your connection string.

## Step 4: Start the Backend Server

Open a terminal and run:

```bash
cd backend
npm run dev
```

You should see:
```
MongoDB Connected Successfully
Server is running on port 5000
```

## Step 5: Start the Frontend Server

Open a **new terminal** and run:

```bash
npm run dev
```

You should see:
```
✓ Ready in [time]
○ Local: http://localhost:3000
```

## Step 6: Access the Application

Open your browser and go to:
- **Frontend**: http://localhost:3000
- **Backend API Health Check**: http://localhost:5000/api/health

## Troubleshooting

### MongoDB Connection Error
- Make sure MongoDB is running
- Check the `MONGODB_URI` in `backend/.env`
- For Atlas, verify your IP is whitelisted

### Port Already in Use
- Change the port in `backend/.env` (PORT=5001)
- Or stop the process using the port

### Module Not Found
- Delete `node_modules` and `package-lock.json`
- Run `npm install` again

### Frontend Can't Connect to Backend
- Make sure backend is running on port 5000
- Check `NEXT_PUBLIC_API_URL` in `.env.local`
- Verify CORS settings in backend

## Next Steps

1. **Register a User**: Go to http://localhost:3000/auth/register
2. **Create Admin User**: Update the user's role to 'admin' in MongoDB
3. **Explore Features**: Browse blog, events, gallery, and contact pages

## Quick Commands Summary

```bash
# Install dependencies
npm install
cd backend && npm install && cd ..

# Create environment files (run these commands)
cat > backend/.env << 'EOF'
PORT=5000
MONGODB_URI=mongodb://localhost:27017/bitsa_hub
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production_min_32_characters_long
JWT_EXPIRE=7d
NODE_ENV=development
FRONTEND_URL=http://localhost:3000
EOF

cat > .env.local << 'EOF'
NEXT_PUBLIC_API_URL=http://localhost:5000/api
EOF

# Start MongoDB (if using local)
sudo systemctl start mongod  # Linux
# or
mongod

# Start backend (Terminal 1)
cd backend
npm run dev

# Start frontend (Terminal 2)
npm run dev
```

