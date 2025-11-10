# How to Run BITSA Hub

## ✅ Setup Complete!

Your environment files have been created. Here's how to run the application:

## Option 1: Manual Start (Recommended for Development)

### Step 1: Start MongoDB

**If using local MongoDB:**
```bash
# Linux
sudo systemctl start mongod
# or just run: mongod

# Mac
brew services start mongodb-community
# or: mongod

# Windows
# Start MongoDB service from Services, or run: mongod
```

**If using MongoDB Atlas (Cloud):**
- No local setup needed
- Make sure your `backend/.env` has the correct connection string
- Format: `mongodb+srv://username:password@cluster.mongodb.net/bitsa_hub`

### Step 2: Start Backend Server

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

### Step 3: Start Frontend Server

Open a **new terminal** and run:
```bash
npm run dev
```

You should see:
```
✓ Ready in [time]
○ Local: http://localhost:3000
```

### Step 4: Access the Application

Open your browser and go to:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:5000/api/health

## Option 2: Using the Startup Script

You can use the provided startup script (runs both servers):

```bash
./start.sh
```

**Note:** This runs both servers in the background. To stop them, press `Ctrl+C`.

## What to Do Next

1. **Register a User**
   - Go to http://localhost:3000/auth/register
   - Create your account

2. **Create an Admin User** (Optional)
   - After registering, you need to manually set a user as admin
   - Connect to MongoDB and update the user's role:
     ```javascript
     db.users.updateOne(
       { email: "your-email@example.com" },
       { $set: { role: "admin" } }
     )
     ```
   - Or use MongoDB Compass to edit the user document

3. **Explore the Features**
   - Browse the blog
   - View events
   - Check out the gallery
   - Visit the contact page
   - Access admin dashboard (if you're an admin)

## Troubleshooting

### MongoDB Connection Error

**Error:** `MongoDB connection error`

**Solutions:**
1. Make sure MongoDB is running
2. Check your `MONGODB_URI` in `backend/.env`
3. For Atlas, verify your IP is whitelisted
4. Test connection: `mongosh "your-connection-string"`

### Port Already in Use

**Error:** `Port 5000 is already in use`

**Solutions:**
1. Change port in `backend/.env`: `PORT=5001`
2. Or stop the process using the port:
   ```bash
   # Find process
   lsof -i :5000
   # Kill process
   kill -9 <PID>
   ```

### Frontend Can't Connect to Backend

**Error:** `Network Error` or `CORS Error`

**Solutions:**
1. Make sure backend is running on port 5000
2. Check `NEXT_PUBLIC_API_URL` in `.env.local`
3. Verify backend CORS settings allow `http://localhost:3000`

### Module Not Found

**Error:** `Cannot find module`

**Solutions:**
1. Reinstall dependencies:
   ```bash
   # Frontend
   rm -rf node_modules package-lock.json
   npm install
   
   # Backend
   cd backend
   rm -rf node_modules package-lock.json
   npm install
   ```

## Quick Commands Reference

```bash
# Install dependencies
npm install
cd backend && npm install && cd ..

# Start backend
cd backend && npm run dev

# Start frontend (in new terminal)
npm run dev

# Check if MongoDB is running
mongosh --eval "db.adminCommand('ping')"

# Test backend API
curl http://localhost:5000/api/health
```

## Environment Files

### Backend (`backend/.env`)
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/bitsa_hub
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production_min_32_characters_long
JWT_EXPIRE=7d
NODE_ENV=development
FRONTEND_URL=http://localhost:3000
```

### Frontend (`.env.local`)
```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

## Next Steps

1. ✅ Dependencies installed
2. ✅ Environment files created
3. ⏳ Start MongoDB
4. ⏳ Start backend server
5. ⏳ Start frontend server
6. ⏳ Access http://localhost:3000

## Need Help?

- Check `SETUP.md` for detailed setup instructions
- Check `README.md` for API documentation
- Check `PROJECT_SUMMARY.md` for project overview

Happy coding! 🚀

