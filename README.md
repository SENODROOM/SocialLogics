# ⬡ SocialLogics v2.0 — Production Full-Stack MERN

> Unified video search engine across **18+ platforms** — YouTube, TikTok, Instagram, Facebook, Dailymotion, X/Twitter, Twitch, Reddit, Vimeo, Snapchat, Pinterest, LinkedIn, Rumble, Odysee, Bilibili, Triller, Kwai, PeerTube.

---

## 🚀 Key Features

### Search Engine (Production Level)
| Feature | Details |
|---------|---------|
| **Multi-Platform** | 18+ platforms searched simultaneously |
| **Smart Autocomplete** | Debounced suggestions from trending DB + user history |
| **Query Enhancement** | Auto-expands abbreviations (ai→artificial intelligence) |
| **Score-Based Trending** | Weighted by recency, daily count, total count |
| **Sub-URL Search** | Platform-specific: Shorts, Reels, Live, Clips, Channels |
| **Related Queries** | AI-suggested related searches shown after results |
| **Search Stats** | Response time, total reach (combined monthly users) |

### Results UX
| Feature | Details |
|---------|---------|
| **Result Cards** | Platform color, content types, monthly users, URL preview |
| **Copy URL** | One-click clipboard copy of search URL |
| **Bookmark** | Save to personal collection without leaving page |
| **Expand/Collapse** | Show sub-URLs (Shorts, Live, etc.) per platform |
| **Sort** | By relevance / most users / A–Z |
| **View Modes** | Grid / List / Compact |
| **Category Filter** | Filter results by Video / Social / Shorts / Live etc. |
| **Quick Hide** | Per-platform hide toggle at bottom |
| **Pin to Top** | Pin favorite platforms |
| **Open All** | Opens all platforms simultaneously with stagger |
| **Save Search** | Authenticated users can pin searches |

### User System
| Feature | Details |
|---------|---------|
| **JWT Auth** | Register, login, 7-day token, auto-refresh |
| **Profile** | Bio, avatar URL, preferred platforms, theme |
| **Search History** | Full paginated log, re-search, bulk clear, filter |
| **Bookmarks** | Collections, notes, favorite toggle, sort/filter |
| **Dashboard** | Stats, top platforms bar chart, timeline, trending |
| **Saved Searches** | Pinned searches with labels |
| **Login Streak** | Track daily engagement |

### Keyboard Shortcuts
| Key | Action |
|-----|--------|
| `/` | Focus search bar |
| `?` | Show shortcuts panel |
| `↑↓` | Navigate autocomplete |
| `Esc` | Close dropdown |
| `G + H` | Go to Home |
| `G + S` | Go to Search |
| `G + B` | Go to Bookmarks |

### Security & Performance
- **Helmet** — HTTP security headers
- **CORS** — Whitelisted origins only
- **Rate Limiting** — 200 req/15min API, 10/15min auth endpoints
- **Input Validation** — express-validator on all POST endpoints
- **Mongo Sanitize** — Prevents NoSQL injection
- **Compression** — gzip all responses
- **In-Memory Cache** — Suggestions cached 60s, trending cached 2min
- **Winston Logging** — Structured logs to files
- **Request Timeout** — 15s axios timeout on frontend

---

## 📁 Project Structure

```
sociallogics/
├── backend/                      Node.js + Express API
│   ├── config/
│   │   ├── db.js                 MongoDB connection
│   │   └── logger.js             Winston logger
│   ├── controllers/
│   │   └── searchController.js   Smart search, suggestions, trending, stats
│   ├── middleware/
│   │   ├── auth.js               JWT protect / optionalAuth / adminOnly
│   │   └── index.js              asyncHandler, rateLimiters, errorHandler
│   ├── models/
│   │   ├── User.js               Auth, preferences, saved searches
│   │   ├── SearchHistory.js      Full search log with normalization
│   │   ├── Bookmark.js           Favorites, collections, notes
│   │   ├── Trending.js           Score-weighted trending engine
│   │   ├── Collection.js         Named bookmark collections
│   │   └── SearchAlert.js        Search notification alerts
│   ├── routes/
│   │   └── index.js              All routes in one clean file
│   ├── utils/
│   │   ├── platforms.js          18 platforms with full URL builders
│   │   └── cache.js              In-memory TTL cache
│   └── index.js                  Express server with prod serving
│
└── frontend/                     React 18 SPA
    └── src/
        ├── context/
        │   └── AuthContext.js    Global auth state
        ├── hooks/
        │   └── useSearch.js      Reusable search state hook
        ├── utils/
        │   ├── api.js            Axios instance + all API methods
        │   └── constants.js      18 platforms + categories
        ├── components/
        │   ├── layout/
        │   │   ├── Navbar.js         Sticky, scroll-aware
        │   │   ├── Background.js     Particles + grid + glow
        │   │   └── KeyboardShortcuts.js  Global shortcut overlay
        │   ├── search/
        │   │   └── SearchBar.js  Autocomplete + voice + filters
        │   ├── features/
        │   │   └── PlatformGrid.js
        │   └── ui/index.js
        └── pages/
            ├── Home.js           Hero + stats + trending + platform grid
            ├── Search.js         Full results with all filters/features
            ├── History.js        Paginated history with re-search
            ├── Bookmarks.js      Collections + inline editor
            ├── Dashboard.js      Stats, charts, timeline
            ├── Profile.js        Preferences, platform picker
            ├── Login.js
            └── Register.js
```

---

## ⚡ Quick Start

### Prerequisites
- Node.js 18+
- MongoDB 6+ (local or Atlas)

### 1. Install all dependencies
```bash
cd sociallogics
npm run install-all
```

### 2. Configure environment
```bash
cd backend
cp .env.example .env
# Edit .env:
# MONGO_URI=mongodb://localhost:27017/sociallogics
# JWT_SECRET=your_very_long_random_secret_here
```

### 3. Run in development
```bash
# From root
npm run dev
# Client: http://localhost:3000
# API:    http://localhost:5000
```

### 4. Production build
```bash
npm run build        # builds React
npm start            # serves both from Express on :5000
```

---

## 🌐 API Reference

### Auth
```
POST /api/auth/register     { username, email, password }
POST /api/auth/login        { email, password }
GET  /api/auth/me           → current user
PUT  /api/auth/profile      { bio, avatar, theme, preferredPlatforms }
PUT  /api/auth/change-password
```

### Search
```
POST /api/search            { query, platform, category, contentType }
GET  /api/search/platforms  → all 18 platforms
GET  /api/search/suggestions?q=&limit=
GET  /api/search/trending?limit=&period=daily|weekly|all
GET  /api/search/stats      → total searches, unique queries
POST /api/search/click      { platform, query }
```

### User Data
```
GET    /api/history?page=&q=&platform=
DELETE /api/history/:id
DELETE /api/history
GET    /api/bookmarks?collection=&platform=&sort=&q=
POST   /api/bookmarks       { title, url, platform, notes, tags, collection }
PUT    /api/bookmarks/:id
DELETE /api/bookmarks/:id
POST   /api/bookmarks/:id/toggle-favorite
GET    /api/users/stats     → searchTimeline, topPlatforms, topQueries
POST   /api/users/saved-searches
GET    /api/alerts
POST   /api/alerts          { query, platform, frequency }
```

---

## 🎨 Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18, React Router v6, Axios |
| Styling | CSS Variables, CSS Animations, Syne + JetBrains Mono |
| State | React Context + Hooks |
| Notifications | react-hot-toast |
| Backend | Node.js 18, Express 4 |
| Database | MongoDB 6, Mongoose 8 |
| Auth | JWT + bcryptjs (12 rounds) |
| Caching | In-memory TTL cache |
| Security | Helmet, CORS, express-rate-limit, mongo-sanitize |
| Validation | express-validator |
| Logging | Winston |

---

*⬡ SocialLogics — Built for production. Designed for speed.*
