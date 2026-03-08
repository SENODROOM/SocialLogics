# ⬡ SocialLogics — Full Stack MERN Video Search Engine

A unified video search engine aggregating **14 platforms** — YouTube, TikTok, Instagram, Facebook, Dailymotion, Twitter/X, Twitch, Reddit, Vimeo, Snapchat, Pinterest, LinkedIn, Rumble, and Odysee.

---

## 🚀 Features

### Search
- 🔍 **Unified Search** — Search across all 14 platforms simultaneously
- 🎯 **Platform Filter** — Target specific platforms
- 💡 **Smart Autocomplete** — Suggestions from trending & past searches
- 🔥 **Category Quick-Search** — Trending, Music, Gaming, Shorts, Sports, etc.

### User System (MERN Auth)
- 🔐 **JWT Authentication** — Register, login, secure sessions
- 👤 **User Profiles** — Bio, avatar, preferred platforms, theme
- 🔑 **Password Management** — Secure bcrypt hashing, change password

### Personal Features
- 📜 **Search History** — Full paginated history, delete & search-again
- ⭐ **Bookmarks** — Save results with notes, collections, edit/delete
- 💾 **Saved Searches** — Pin frequent searches
- 📊 **Dashboard** — Personal stats, top platforms, trending topics

### Technical
- 🛡️ **Security** — Helmet, CORS, rate limiting (200 req/15min)
- ✅ **Validation** — express-validator on all inputs
- 📈 **Trending Engine** — Auto-tracks most searched queries
- 🎨 **Cyberpunk UI** — Orbitron font, scanlines, particle field, neon glow

---

## 📁 Project Structure

```
sociallogics/
├── server/                  # Express + MongoDB API
│   ├── models/
│   │   ├── User.js
│   │   ├── SearchHistory.js
│   │   ├── Bookmark.js
│   │   └── Trending.js
│   ├── routes/
│   │   ├── auth.js          # Register, Login, Profile
│   │   ├── search.js        # Search, Suggestions
│   │   ├── history.js       # Search History CRUD
│   │   ├── bookmarks.js     # Bookmarks CRUD
│   │   ├── trending.js      # Trending queries
│   │   └── users.js         # Stats, Saved Searches
│   ├── middleware/
│   │   └── auth.js          # JWT protect, optionalAuth, adminOnly
│   ├── index.js             # Express server entry
│   └── .env.example
│
└── client/                  # React 18 SPA
    └── src/
        ├── context/
        │   └── AuthContext.js
        ├── utils/
        │   ├── api.js        # Axios API wrappers
        │   └── constants.js  # Platforms, Categories
        ├── components/
        │   ├── Navbar.js
        │   ├── SearchBar.js  # With autocomplete
        │   └── ParticleField.js
        └── pages/
            ├── Home.js       # Landing + platform grid
            ├── Search.js     # Results page
            ├── History.js    # Search history
            ├── Bookmarks.js  # Saved bookmarks
            ├── Dashboard.js  # Stats & analytics
            ├── Profile.js    # User settings
            ├── Login.js
            └── Register.js
```

---

## ⚡ Quick Start

### Prerequisites
- Node.js 18+
- MongoDB (local or Atlas)

### 1. Clone & Install

```bash
# Install all dependencies
npm run install-all
```

### 2. Configure Server

```bash
cd server
cp .env.example .env
# Edit .env with your MongoDB URI and JWT secret
```

**.env:**
```env
PORT=5000
MONGO_URI=mongodb://localhost:27017/sociallogics
JWT_SECRET=your_super_secret_key_here
JWT_EXPIRE=7d
NODE_ENV=development
CLIENT_URL=http://localhost:3000
```

### 3. Run Development

```bash
# From root — runs both server and client
npm run dev
```

- **Client:** http://localhost:3000
- **Server API:** http://localhost:5000
- **Health Check:** http://localhost:5000/api/health

---

## 🌐 API Endpoints

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/api/auth/register` | ❌ | Create account |
| POST | `/api/auth/login` | ❌ | Login |
| GET | `/api/auth/me` | ✅ | Get profile |
| PUT | `/api/auth/profile` | ✅ | Update profile |
| PUT | `/api/auth/change-password` | ✅ | Change password |
| POST | `/api/search` | Optional | Search platforms |
| GET | `/api/search/platforms` | ❌ | List all platforms |
| GET | `/api/search/suggestions?q=` | ❌ | Autocomplete |
| GET | `/api/trending` | ❌ | Trending queries |
| GET | `/api/history` | ✅ | Search history |
| DELETE | `/api/history/:id` | ✅ | Delete one |
| DELETE | `/api/history` | ✅ | Clear all |
| GET | `/api/bookmarks` | ✅ | Get bookmarks |
| POST | `/api/bookmarks` | ✅ | Create bookmark |
| PUT | `/api/bookmarks/:id` | ✅ | Update bookmark |
| DELETE | `/api/bookmarks/:id` | ✅ | Delete bookmark |
| GET | `/api/users/stats` | ✅ | Personal stats |
| POST | `/api/users/saved-searches` | ✅ | Save a search |

---

## 🎨 Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18, React Router v6 |
| Styling | Custom CSS, CSS Variables |
| HTTP | Axios |
| Notifications | react-hot-toast |
| Backend | Node.js, Express 4 |
| Database | MongoDB, Mongoose |
| Auth | JWT + bcryptjs |
| Security | Helmet, CORS, express-rate-limit |
| Validation | express-validator |

---

## 📦 Production Build

```bash
npm run build        # Builds React client
npm start            # Runs Express server
```

Serve the `client/build` folder as static files from Express for a single-server deployment.

---

*Built with ⬡ SocialLogics — Unified Video Intelligence*
