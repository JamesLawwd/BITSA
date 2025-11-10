# BITSA Hub

A modern student platform for BITSA activities, events, and community engagement.

## Features

- **User Authentication**: Registration and login system with JWT tokens
- **Blog Section**: Articles, announcements, and updates
- **Events Management**: Discover and register for upcoming events
- **Gallery**: Browse photos from past events
- **Contact Page**: Get in touch with BITSA
- **Admin Dashboard**: Manage users, posts, events, and content
- **Responsive Design**: Mobile and desktop friendly UI

## Tech Stack

### Frontend
- Next.js 16 (App Router)
- TypeScript
- Tailwind CSS
- React Hook Form
- Axios

### Backend
- Node.js
- Express
- TypeScript
- MongoDB (Mongoose)
- JWT Authentication
- Bcrypt for password hashing

## Getting Started

### Prerequisites

- Node.js 18+ and npm
- MongoDB (local or MongoDB Atlas)

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd bitsa_app
```

2. Install frontend dependencies:
```bash
npm install
```

3. Install backend dependencies:
```bash
cd backend
npm install
cd ..
```

4. Set up environment variables:

Create a `.env` file in the `backend` directory:
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/bitsa_hub
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
JWT_EXPIRE=7d
NODE_ENV=development
FRONTEND_URL=http://localhost:3000
```

Create a `.env.local` file in the root directory:
```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

5. Start MongoDB (if using local MongoDB):
```bash
mongod
```

6. Start the backend server:
```bash
cd backend
npm run dev
```

7. Start the frontend development server (in a new terminal):
```bash
npm run dev
```

8. Open [http://localhost:3000](http://localhost:3000) in your browser.

## Project Structure

```
bitsa_app/
├── app/                    # Next.js app directory
│   ├── auth/              # Authentication pages
│   ├── blog/              # Blog pages
│   ├── events/            # Events pages
│   ├── gallery/           # Gallery pages
│   ├── contact/           # Contact page
│   ├── profile/           # User profile
│   ├── admin/             # Admin dashboard
│   └── layout.tsx         # Root layout
├── backend/               # Backend API
│   ├── src/
│   │   ├── config/        # Configuration files
│   │   ├── controllers/   # Route controllers
│   │   ├── models/        # Database models
│   │   ├── routes/        # API routes
│   │   ├── middleware/    # Middleware functions
│   │   └── utils/         # Utility functions
│   └── server.ts          # Server entry point
├── components/            # React components
├── context/               # React context providers
├── lib/                   # Utility libraries
└── public/                # Static assets
```

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register a new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/logout` - Logout user
- `GET /api/auth/me` - Get current user

### Users
- `GET /api/users/profile` - Get user profile
- `PUT /api/users/profile` - Update user profile
- `GET /api/users/all` - Get all users (admin only)

### Blog
- `GET /api/blog` - Get all blog posts
- `GET /api/blog/:id` - Get single blog post
- `POST /api/blog` - Create blog post (authenticated)
- `PUT /api/blog/:id` - Update blog post (author/admin)
- `DELETE /api/blog/:id` - Delete blog post (author/admin)

### Events
- `GET /api/events` - Get all events
- `GET /api/events/:id` - Get single event
- `POST /api/events` - Create event (authenticated)
- `PUT /api/events/:id` - Update event (organizer/admin)
- `DELETE /api/events/:id` - Delete event (organizer/admin)
- `POST /api/events/:id/register` - Register for event (authenticated)

### Gallery
- `GET /api/gallery` - Get all galleries
- `GET /api/gallery/:id` - Get single gallery
- `POST /api/gallery` - Create gallery (authenticated)
- `PUT /api/gallery/:id` - Update gallery (uploader/admin)
- `DELETE /api/gallery/:id` - Delete gallery (uploader/admin)

### Contact
- `GET /api/contact/info` - Get contact information
- `POST /api/contact` - Create contact message
- `GET /api/contact` - Get all messages (admin only)
- `GET /api/contact/:id` - Get single message (admin only)
- `PUT /api/contact/:id` - Update message (admin only)

### Admin
- `GET /api/admin/stats` - Get dashboard statistics (admin only)
- `PUT /api/admin/users/:id/role` - Update user role (admin only)
- `DELETE /api/admin/users/:id` - Delete user (admin only)

## Default Admin User

To create an admin user, you can use MongoDB or create a script. The first user registered will need to have their role manually updated to 'admin' in the database.

## Deployment

### Backend
1. Build the backend:
```bash
cd backend
npm run build
```

2. Start the production server:
```bash
npm start
```

### Frontend
1. Build the frontend:
```bash
npm run build
```

2. Start the production server:
```bash
npm start
```

## License

This project is licensed under the MIT License.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
