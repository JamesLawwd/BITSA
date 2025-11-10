# BITSA Hub Setup Guide

This guide will help you set up the BITSA Hub application step by step.

## Prerequisites

Before you begin, make sure you have the following installed:

1. **Node.js** (version 18 or higher)
   - Download from [nodejs.org](https://nodejs.org/)
   - Verify installation: `node --version`

2. **npm** (comes with Node.js)
   - Verify installation: `npm --version`

3. **MongoDB**
   - Option 1: Local MongoDB
     - Download from [mongodb.com](https://www.mongodb.com/try/download/community)
     - Install and start MongoDB service
   - Option 2: MongoDB Atlas (Cloud)
     - Sign up at [mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)
     - Create a free cluster
     - Get your connection string

## Step-by-Step Setup

### 1. Clone or Navigate to the Project

```bash
cd bitsa_app
```

### 2. Install Frontend Dependencies

```bash
npm install
```

### 3. Install Backend Dependencies

```bash
cd backend
npm install
cd ..
```

### 4. Set Up Environment Variables

#### Backend Environment Variables

Create a `.env` file in the `backend` directory:

```bash
cd backend
touch .env
```

Add the following content to `backend/.env`:

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/bitsa_hub
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production_min_32_characters
JWT_EXPIRE=7d
NODE_ENV=development
FRONTEND_URL=http://localhost:3000
```

**Important Notes:**
- Replace `MONGODB_URI` with your MongoDB connection string
  - Local: `mongodb://localhost:27017/bitsa_hub`
  - Atlas: `mongodb+srv://username:password@cluster.mongodb.net/bitsa_hub?retryWrites=true&w=majority`
- Replace `JWT_SECRET` with a strong, random secret (at least 32 characters)
- In production, use a secure random string for `JWT_SECRET`

#### Frontend Environment Variables

Create a `.env.local` file in the root directory:

```bash
touch .env.local
```

Add the following content to `.env.local`:

```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

### 5. Start MongoDB

#### If using Local MongoDB:

**Linux/Mac:**
```bash
sudo systemctl start mongod
# or
mongod
```

**Windows:**
```bash
# Start MongoDB service from Services
# or run: mongod
```

#### If using MongoDB Atlas:

No local setup needed. Make sure your connection string in `.env` is correct.

### 6. Start the Backend Server

```bash
cd backend
npm run dev
```

The backend server should start on `http://localhost:5000`.

You should see:
```
MongoDB Connected Successfully
Server is running on port 5000
```

### 7. Start the Frontend Development Server

Open a new terminal window and run:

```bash
npm run dev
```

The frontend should start on `http://localhost:3000`.

### 8. Access the Application

Open your browser and navigate to:
- Frontend: http://localhost:3000
- Backend API: http://localhost:5000/api/health

## Creating an Admin User

To create an admin user, you have two options:

### Option 1: Using MongoDB Compass or MongoDB Shell

1. Connect to your MongoDB database
2. Navigate to the `users` collection in the `bitsa_hub` database
3. Find the user you want to make admin
4. Update the `role` field from `student` to `admin`

### Option 2: Using a Script

Create a file `backend/scripts/createAdmin.js`:

```javascript
const mongoose = require('mongoose');
const User = require('../src/models/User');
require('dotenv').config();

mongoose.connect(process.env.MONGODB_URI)
  .then(async () => {
    const user = await User.findOne({ email: 'admin@example.com' });
    if (user) {
      user.role = 'admin';
      await user.save();
      console.log('User updated to admin');
    } else {
      console.log('User not found');
    }
    process.exit(0);
  })
  .catch((error) => {
    console.error('Error:', error);
    process.exit(1);
  });
```

Run the script:
```bash
node backend/scripts/createAdmin.js
```

## Troubleshooting

### Backend Issues

1. **MongoDB Connection Error**
   - Verify MongoDB is running
   - Check the `MONGODB_URI` in `.env`
   - For Atlas, verify your IP is whitelisted

2. **Port Already in Use**
   - Change the `PORT` in `backend/.env`
   - Or stop the process using port 5000

3. **Module Not Found**
   - Run `npm install` in the `backend` directory
   - Delete `node_modules` and `package-lock.json`, then reinstall

### Frontend Issues

1. **API Connection Error**
   - Verify backend server is running
   - Check `NEXT_PUBLIC_API_URL` in `.env.local`
   - Check CORS settings in backend

2. **Build Errors**
   - Delete `.next` folder and rebuild
   - Check TypeScript errors: `npm run lint`

## Development Workflow

1. **Backend Changes**: The backend server auto-reloads on changes (using `ts-node-dev`)
2. **Frontend Changes**: Next.js hot-reloads on changes
3. **Database Changes**: Restart the backend server if you modify models

## Production Deployment

### Backend

1. Build the TypeScript code:
```bash
cd backend
npm run build
```

2. Start the production server:
```bash
npm start
```

### Frontend

1. Build the Next.js application:
```bash
npm run build
```

2. Start the production server:
```bash
npm start
```

## Additional Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [Express.js Documentation](https://expressjs.com/)
- [MongoDB Documentation](https://docs.mongodb.com/)
- [Mongoose Documentation](https://mongoosejs.com/)

## Support

If you encounter any issues, please check:
1. All dependencies are installed
2. Environment variables are set correctly
3. MongoDB is running and accessible
4. Ports 3000 and 5000 are available

For more help, refer to the main README.md file.

