# 🚀 BlogSpace - Full-Stack Production-Ready Blogging Platform

BlogSpace is a modern, responsive, full-stack blogging platform built with **Node.js, Express, SQLite, HTML5, CSS3, and Vanilla JavaScript**. Users can sign up, log in, create and format blog posts, follow other writers, like posts, comment on articles, manage user profiles, search & filter stories by topic, receive real-time notifications, and manage platform content via a built-in Admin Dashboard.

---

## 📸 Key Features

- **User Authentication**: Secure JWT-based authentication with bcrypt password hashing, persistent sessions (`localStorage`), and protected API routes.
- **Rich Blog Editor**: Format posts with Bold, Italic, Headings (H2/H3), Lists, Links, Quotes, Tags, Cover Images, and a **Live Preview** mode. Save drafts or publish directly.
- **Social Interactions**: Real database-backed likes, threaded comment system with replies, user follow/unfollow system, and personalized following feed.
- **Notifications System**: Real-time notification badge and dropdown for new followers, post likes, and comments.
- **Search & Explore**: Full-text search across titles, content, tags, and authors, with category filtering pills and sorting by popularity or recency.
- **User Profiles**: Custom bio, avatar URL, join date, follower count, total published blogs, saved drafts, and editable profile settings.
- **Admin Dashboard**: Overview statistics (total users, posts, comments, likes) with moderation controls to view and delete users, posts, or comments.
- **Modern UI & Dark Mode**: Glassmorphism navbar, smooth CSS animations, dark mode toggle, mobile bottom navigation bar, toast alerts, and responsive grid layouts.

---

## 🛠️ Technology Stack

- **Frontend**: HTML5, CSS3 (Custom CSS variables, Dark Mode, Responsive Design), Vanilla JavaScript (ES6 Modules/Fetch API).
- **Backend**: Node.js, Express.js (REST API architecture, CORS, JSON middleware).
- **Authentication**: JSON Web Tokens (jwt) & `bcryptjs` for secure password hashing.
- **Database**: SQLite3 with strict Foreign Key constraints, parameterized queries, and auto-seeding.

---

## 📁 Project Structure

```
blogspace/
│
├── frontend/
│   ├── index.html          # Main social feed page
│   ├── login.html          # User login page
│   ├── register.html       # User registration page
│   ├── create-post.html    # Blog editor & live preview page
│   ├── post.html           # Single blog post detail view
│   ├── profile.html        # User profile & settings page
│   ├── explore.html        # Search, filter, and discover page
│   ├── admin.html          # Admin management dashboard
│   ├── css/
│   │   └── style.css       # Production CSS design system
│   └── js/
│       ├── api.js          # API client & local token manager
│       ├── app.js          # Global UI, theme toggle, navbar, notifications
│       ├── auth.js         # Auth form validation & handlers
│       ├── posts.js        # Posts feed, editor & comment interactions
│       ├── profile.js      # User profile & edit modal
│       └── admin.js        # Admin dashboard controller
│
├── backend/
│   ├── server.js           # Express app entrypoint & static server
│   ├── database/
│   │   └── database.js     # SQLite connection & schema initialization
│   ├── routes/
│   │   ├── auth.js         # /api/auth routes
│   │   ├── posts.js        # /api/posts routes
│   │   ├── likes.js        # /api/posts/:id/like routes
│   │   ├── comments.js     # /api/posts/:id/comments routes
│   │   ├── users.js        # /api/users routes
│   │   ├── notifications.js# /api/notifications routes
│   │   └── admin.js        # /api/admin routes
│   ├── middleware/
│   │   └── auth.js         # JWT auth & admin guard middleware
│   └── package.json        # Backend dependencies & npm scripts
│
├── database/
│   └── schema.sql          # Relational SQLite database schema
│
├── .env.example            # Environment variables template
└── README.md               # Complete setup documentation
```

---

## 🚀 Quick Start Guide

### Prerequisites
- **Node.js** (v16.0.0 or higher)
- **npm** (v7.0.0 or higher)

### Installation Steps

1. **Navigate to the backend directory**:
   ```bash
   cd backend
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Start the application**:
   ```bash
   npm start
   ```

4. **Access the application**:
   Open your browser and navigate to:
   ```
   http://localhost:3000
   ```

*(The SQLite database and demo data will automatically initialize upon first launch!)*

---

## 🔑 Pre-seeded Demo Credentials

To test the application immediately, you can log in with any of these pre-configured accounts:

### 1. Administrator Account
- **Email**: `admin@blogspace.com` (or username `admin`)
- **Password**: `Password123!`
- **Access**: Full platform access + Admin Dashboard (`/admin.html`)

### 2. Regular Author Accounts
- **Account 1**: `alex@example.com` / Username: `alexrivera` / Password: `Password123!`
- **Account 2**: `sarah@example.com` / Username: `sarahj` / Password: `Password123!`

---

## 🔌 REST API Endpoint Reference

### Authentication (`/api/auth`)
- `POST /api/auth/register` - Create a new user account
- `POST /api/auth/login` - Authenticate user & receive JWT token
- `GET /api/auth/me` - Get current authenticated user profile

### Blog Posts (`/api/posts`)
- `GET /api/posts` - List published posts (supports `category`, `search`, `sort`, `feed`, `page`, `limit`)
- `GET /api/posts/:id` - Fetch single post details (increments view count)
- `POST /api/posts` - Create blog post (Requires Auth)
- `PUT /api/posts/:id` - Update blog post (Author / Admin)
- `DELETE /api/posts/:id` - Delete blog post (Author / Admin)

### Likes (`/api/posts/:id`)
- `POST /api/posts/:id/like` - Toggle like/unlike on post (Requires Auth)
- `GET /api/posts/:id/liked` - Check if logged-in user liked post

### Comments (`/api`)
- `GET /api/posts/:id/comments` - List comments for a post (with nested replies)
- `POST /api/posts/:id/comments` - Add comment to post (Requires Auth)
- `DELETE /api/comments/:id` - Delete comment (Comment Author / Post Author / Admin)

### Users & Followers (`/api/users`)
- `GET /api/users/:identifier` - Get public profile by ID or username
- `PUT /api/users/:id` - Edit user profile (Requires Auth)
- `GET /api/users/:id/posts` - Get posts written by user (Requires Auth for drafts)
- `POST /api/users/:id/follow` - Follow user (Requires Auth)
- `DELETE /api/users/:id/follow` - Unfollow user (Requires Auth)

### Notifications (`/api/notifications`)
- `GET /api/notifications` - Get user notifications (Likes, Comments, Followers, Direct Messages)
- `PUT /api/notifications/read` - Mark notifications as read

### Direct Messaging (`/api/messages`)
- `GET /api/messages/conversations` - Get list of active chat conversations with recent messages & unread counts
- `GET /api/messages/:user_id` - Fetch chat history transcript with target user & mark incoming as read
- `POST /api/messages/:user_id` - Send direct message to target user
- `GET /api/messages/unread/count` - Get total unread messages count for navbar badge

### Admin Dashboard (`/api/admin`)
- `GET /api/admin/stats` - Platform overview stats (Users, Posts, Comments, Likes, User Logs)
- `GET /api/admin/logs` - List user authentication activity logs (Login, Logout, Register timestamps & IP address)
- `GET /api/admin/users` - List all users (Requires Admin)
- `GET /api/admin/posts` - List all posts (Requires Admin)
- `GET /api/admin/comments` - List all comments (Requires Admin)
- `DELETE /api/admin/users/:id` - Delete user account (Requires Admin)

---

## ⚙️ Environment Variables Configuration

Create a `.env` file inside the `backend/` directory:

```env
PORT=3000
JWT_SECRET=your_jwt_secret_key_here
DB_PATH=../database/blogspace.db
```

---

## 💻 Running in VS Code

1. Open VS Code and open the `blogspace` directory.
2. Open the built-in terminal (`Ctrl + ~` or `Cmd + ~`).
3. Run:
   ```bash
   cd backend
   npm start
   ```
4. Click on `http://localhost:3000` in the terminal to view the application in your browser.

---

## 🔒 Security Measures Included

- **SQL Injection Protection**: Parameterized SQL queries across all endpoints.
- **XSS Protection**: HTML sanitization and entity escaping on user content.
- **Authorization Verification**: Middleware enforcing post/comment ownership and admin role verification.
- **Password Security**: Omitted from all API outputs, hashed with 10 salt rounds of `bcryptjs`.
