# 🎵 MusicApp

> A full-stack music discovery platform where users can explore artists, albums and tracks, build a personal library of favourites, rate music, comment on articles, follow concerts and connect with a community of music lovers.

Built as a group project (LEI-111641 - My contributions), MusicApp combines a **Django REST API** backend with a **React (Vite)** frontend, and integrates with the **Deezer Public API** to populate the catalogue with real artist, album and track data.

> 📦 **Project repository (with original commits):** [github.com/LEI-122664/Music](https://github.com/LEI-122664/Music)


---

## 📑 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Running the Project](#-running-the-project)
- [Configuration](#-configuration)
- [Database Schema](#-database-schema)
- [API Reference](#-api-reference)
- [Authentication](#-authentication)
- [Staff Dashboard](#-staff-dashboard)
- [Deezer Integration](#-deezer-integration)

---

## ✨ Features

### 👥 For Everyone (Public)
- 🏠 **Homepage** — landing page with welcome message and navigation
- 🎤 **Browse Artists** — view all artists with their photos
- 💿 **Browse Albums** — explore the full album catalogue
- 🎵 **Track Listings** — open an album to see all its tracks
- 📰 **Articles** — read music news and editorial pieces
- 🎟️ **Concerts** — see upcoming concerts with date, venue and ticket links
- 👥 **Members Directory** — discover other users in the community
- 🔍 **Global Search** — search across artists, albums and music with live results in the top nav

### 🔐 For Logged-In Users
- 📝 **Account Management** — sign up, log in and log out with token-based auth
- 👤 **Personal Profile** — set a bio and upload a profile photo
- ⭐ **Favourites System** — add or remove favourite **artists**, **albums** and **music**
- 💬 **Comment on Articles** — share thoughts on editorial content
- ⭐ **Rate Music & Albums** — leave 1–5 star ratings with an optional comment
- 👍 **Like Ratings** — engage with other users' reviews
- 🗑️ **Manage Own Content** — delete your own comments and ratings

### 🛠️ For Staff Users
- 🎛️ **Staff Dashboard** — central control panel (gated by `is_staff`)
- 💿 **Import from Deezer** — 4-step wizard to import artists, albums and tracks straight from Deezer
- ✍️ **Article Editor** — create and delete articles with cover images
- 🎤 **Concert Management** — add upcoming concerts
- 💬 **Comment Moderation** — review and remove user comments
- ⭐ **Rating Moderation** — review and remove user ratings

---

## 🛠 Tech Stack

### Backend
- **Python 3.x**
- **Django 6.0.4** — web framework
- **Django REST Framework** — REST API
- **DRF Authtoken** — token-based authentication
- **django-cors-headers** — CORS handling for the React frontend
- **SQLite** — default development database
- **Requests** — HTTP client for the Deezer API
- **Pillow** — image handling (profile photos, article covers)

### Frontend
- **React 18** with **Vite** as the build tool
- **React Router DOM** — client-side routing
- **Axios** — HTTP client
- **Vanilla CSS** — custom styling (no UI framework)

### External APIs
- **Deezer Public API** (`api.deezer.com`) — catalogue source for artists, albums and tracks

---

## 📁 Project Structure

The Django backend lives at the **project root**, while the React frontend lives inside the **`MusicApp-frontend/`** subfolder.

```
project-root/                        # ← Django backend root (run manage.py from here)
├── Music/                           # Django project
│   ├── __init__.py
│   ├── asgi.py
│   ├── wsgi.py
│   ├── settings.py                  # Django settings (CORS, DRF, DB, media)
│   └── urls.py                      # Root URL config (mounts MusicApp/)
│
├── MusicApp/                        # Main Django app
│   ├── __init__.py
│   ├── admin.py                     # Admin registration for all models
│   ├── apps.py
│   ├── deezer.py                    # Deezer API helper functions
│   ├── models.py                    # Database models
│   ├── serializers.py               # DRF serializers
│   ├── views.py                     # API views / endpoints
│   ├── urls.py                      # API routes
│   └── tests.py
│
├── media/                           # Uploaded files (profile photos, article covers)
├── db.sqlite3                       # SQLite database
├── manage.py
│
└── MusicApp-frontend/               # ← React frontend (cd here for npm commands)
    ├── src/
    │   ├── components/
    │   │   ├── Homepage.jsx
    │   │   ├── TopNav.jsx
    │   │   ├── AuthModal.jsx
    │   │   ├── Artists.jsx
    │   │   ├── ArtistCard.jsx
    │   │   ├── Albuns.jsx           # Albums of a single artist
    │   │   ├── AllAlbums.jsx        # Full album grid
    │   │   ├── Tracks.jsx           # Tracks inside an album
    │   │   ├── Articles.jsx
    │   │   ├── Concertos.jsx
    │   │   ├── Members.jsx
    │   │   ├── MemberProfilePage.jsx
    │   │   ├── UserProfile.jsx
    │   │   ├── EditProfileModal.jsx
    │   │   ├── StaffDashboard.jsx
    │   │   ├── ImportFromDeezer.jsx
    │   │   ├── CreateArticle.jsx
    │   │   ├── AddConcerto.jsx
    │   │   ├── AnalyzeComments.jsx
    │   │   └── ManageRatings.jsx
    │   │
    │   ├── constants/
    │   │   └── config.js            # API_BASE_URL constant
    │   ├── utils/
    │   │   └── auth.js              # getAuthHeader() helper
    │   ├── css/
    │   │   └── styles.css           # Global styles
    │   ├── App.jsx                  # Routes
    │   ├── App.css
    │   ├── index.css
    │   └── main.jsx
    │
    ├── package.json
    └── vite.config.js
```

---

## 📋 Prerequisites

Make sure you have these installed:

- **Python 3.10+**
- **Node.js 18+** and **npm**
- **pip** and **virtualenv** (recommended)
- **Git**

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/LEI-122664/Music.git
cd Music
```

### 2. Backend setup (Django)

Run these from the **project root** (where `manage.py` lives):

```bash
# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate          # macOS / Linux
venv\Scripts\activate             # Windows

# Install dependencies
pip install django==6.0.4
pip install djangorestframework
pip install django-cors-headers
pip install requests
pip install Pillow

# Or, if you have a requirements.txt:
# pip install -r requirements.txt

# Run database migrations
python manage.py makemigrations
python manage.py migrate

# Create a superuser (gives you staff access)
python manage.py createsuperuser
```

### 3. Frontend setup (React + Vite)

The frontend lives in the `MusicApp-frontend/` subfolder:

```bash
cd MusicApp-frontend

# Install dependencies
npm install
```

If you're starting from scratch, the main packages are:

```bash
npm install react react-dom react-router-dom axios
npm install -D vite @vitejs/plugin-react
```

---

## ▶️ Running the Project

You need **two terminals** open at the same time.

### Terminal 1 — Backend (from project root)

```bash
# from the project root
source venv/bin/activate          # activate venv
python manage.py runserver
```

The Django API will be available at **`http://127.0.0.1:8000`**.

### Terminal 2 — Frontend (from `MusicApp-frontend/`)

```bash
cd MusicApp-frontend
npm run dev
```

The React app will be available at **`http://localhost:5173`**.

### Quick health-check

- Visit `http://localhost:5173` → you should see the MusicApp homepage.
- Visit `http://127.0.0.1:8000/admin/` → Django admin, log in with your superuser.

---

## 🔧 Configuration

### Backend

Key settings in `Music/settings.py`:

| Setting | Value | Notes |
|---|---|---|
| `DEBUG` | `True` | ⚠️ **Set to `False` in production** |
| `SECRET_KEY` | hard-coded | ⚠️ **Move to an env var in production** |
| `ALLOWED_HOSTS` | `[]` | Add your domain(s) for production |
| `CORS_ALLOWED_ORIGINS` | `localhost:5173`, `127.0.0.1:5173` | Frontend dev URLs |
| `DATABASES` | SQLite | Swap for PostgreSQL/MySQL in production |
| `MEDIA_URL` / `MEDIA_ROOT` | `/media/` | Uploads (profile photos, article covers) |

### Frontend

The frontend keeps the API base URL in `MusicApp-frontend/src/constants/config.js`:

```js
export const API_BASE_URL = 'http://127.0.0.1:8000'
```

> ⚠️ **Note:** many components still call `http://127.0.0.1:8000/MusicApp/api/...` directly instead of using the `API_BASE_URL` constant. Consider refactoring to use the constant everywhere before deploying.

The auth helper lives in `MusicApp-frontend/src/utils/auth.js`:

```js
export const getAuthHeader = () => ({
    'Authorization': `Token ${localStorage.getItem('authToken')}`
});
```

---

## 🗄 Database Schema

### Core models

| Model | Description | Key fields |
|---|---|---|
| **Genre** | Music genre | `name`, `description` |
| **Artist** | Performer | `name`, `biography`, `photo_url`, `genre` (M2M), `deezer_id` |
| **Album** | Album by an artist | `title`, `artist` (FK), `release_date`, `cover_url`, `deezer_id` |
| **Music** | Individual track | `title`, `artist` (FK), `album` (FK), `deezer_track_id`, `duration`, `deezer_id` |
| **Concerto** | Live concert | `artista` (FK), `local`, `data`, `link_bilhetes` |
| **Artigo** | Editorial article | `titulo`, `conteudo`, `autor`, `data_publicacao`, `capa_artigo` (image) |

### Social / user models

| Model | Description | Key fields |
|---|---|---|
| **Perfil** | Extended user profile | `user` (OneToOne), `bio`, `foto`, `fav_artists` (M2M), `albuns_preferidos` (M2M), `musicas_preferidas` (M2M) |
| **Comentario** | Comment on an article | `user`, `artigo`, `texto`, `data_criacao` |
| **Avaliacao** | 1–5 star rating | `user`, `album` (nullable), `musica` (nullable), `nota`, `comentario`, `data_criacao` |
| **Like** | Like on a rating | `user`, `avaliacao` (unique together) |

**Relationships overview:**
- An `Artist` has many `Album`s; each `Album` has many `Music` tracks.
- A `User` has one `Perfil`, which holds their favourites across artists, albums and music.
- `Avaliacao` can target either an `Album` *or* a `Music` (both nullable so one is set at a time).
- `Like` is uniquely scoped per `(user, avaliacao)` pair — one like per user per rating.

---

## 🌐 API Reference

All endpoints are prefixed with `/MusicApp/`.

### 🔐 Authentication

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| `POST` | `/api/auth/signup/` | Create a new account | ❌ |
| `POST` | `/api/auth/login/` | Log in, returns auth token | ❌ |
| `POST` | `/api/auth/logout/` | Invalidate current token | ✅ |
| `GET`  | `/api/auth/user/` | Get current authenticated user | ✅ |

### 👤 Profiles

| Method | Endpoint | Description | Auth |
|---|---|---|---|
| `GET` | `/api/perfis/` | List all profiles | ❌ |
| `GET` / `PUT` | `/api/perfil/` | Get / update own profile | ✅ |
| `GET` | `/api/users/<user_id>/` | Public profile of a user (with their comments & ratings) | ❌ |
| `POST` | `/api/perfil/favorite-artist/<id>/add/` | Add artist to favourites | ✅ |
| `POST` | `/api/perfil/favorite-artist/<id>/remove/` | Remove artist from favourites | ✅ |
| `POST` | `/api/perfil/favorite-album/<id>/add/` | Add album to favourites | ✅ |
| `POST` | `/api/perfil/favorite-album/<id>/remove/` | Remove album from favourites | ✅ |
| `POST` | `/api/perfil/favorite-music/<id>/add/` | Add track to favourites | ✅ |
| `POST` | `/api/perfil/favorite-music/<id>/remove/` | Remove track from favourites | ✅ |

### 🎤 Catalogue

| Method | Endpoint | Description |
|---|---|---|
| `GET` / `POST` | `/api/artists/` | List / create artists |
| `GET` / `PUT` / `DELETE` | `/api/artists/<id>/` | Artist detail |
| `GET` / `POST` | `/api/artists/<id>/albums/` | Albums by artist |
| `GET` / `POST` | `/api/albums/` | List / create albums |
| `GET` / `PUT` / `DELETE` | `/api/albums/<id>/` | Album detail |
| `GET` / `POST` | `/api/albums/<id>/music/` | Tracks in an album |
| `GET` / `POST` | `/api/music/` | List / create tracks |
| `GET` / `PUT` / `DELETE` | `/api/music/<id>/` | Track detail |
| `GET` | `/api/music/<id>/preview/` | Track preview URL |
| `GET` / `POST` | `/api/genres/` | List / create genres |
| `GET` | `/api/genres/<id>/` | Genre detail |

### 🎟️ Concerts

| Method | Endpoint | Description |
|---|---|---|
| `GET` / `POST` | `/api/concertos/` | List / create concerts |
| `GET` / `PUT` / `DELETE` | `/api/concertos/<id>/` | Concert detail |
| `GET` | `/api/artistas/<artist_id>/concertos/` | Concerts by artist |

### 📰 Articles & Comments

| Method | Endpoint | Description |
|---|---|---|
| `GET` / `POST` | `/api/artigos/` | List / create articles |
| `GET` / `PUT` / `DELETE` | `/api/artigos/<id>/` | Article detail |
| `GET` / `POST` | `/api/artigos/<id>/comentarios/` | Comments on an article |
| `GET` | `/api/comentarios/` | List all comments (staff) |
| `GET` / `DELETE` | `/api/comentarios/<id>/` | Comment detail / delete |

### ⭐ Ratings & Likes

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/avaliacoes/` | List all ratings |
| `GET` / `PUT` / `DELETE` | `/api/avaliacoes/<id>/` | Rating detail |
| `POST` | `/api/avaliacoes/<id>/like/` | Toggle a like on a rating |
| `GET` / `POST` | `/api/albums/<id>/avaliacoes/` | Ratings for an album |
| `GET` / `POST` | `/api/music/<id>/avaliacoes/` | Ratings for a track |

### 🔍 Search & Deezer

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/search/?q=<query>` | Global search (artists, albums, music) |
| `GET` | `/api/deezer_search/?q=<query>` | Search Deezer for an artist |
| `GET` | `/api/deezer_artist_albums/<deezer_id>/` | Albums of a Deezer artist |
| `GET` | `/api/deezer_artist_tracks/<album_id>/` | Tracks of a Deezer album |

---

## 🔑 Authentication

MusicApp uses **DRF Token Authentication**.

### 🧪 Test Accounts

The seeded database ships with the following accounts ready to use:

| Role | Username | Password |
|---|---|---|
| 🛠️ **Staff** | `test` | `test12345` |
| 👤 User | `bob`  | `123` |
| 👤 User | `rui`  | `123` |
| 👤 User | `Ana`  | `123` |

> 💡 Log in with **`test` / `test12345`** to access the **Staff Dashboard** (Deezer import, articles, concerts, moderation). The other accounts are regular users for testing the social features (favourites, comments, ratings, likes).

### Login flow

1. User submits credentials to `POST /api/auth/login/`.
2. Backend returns a JSON payload containing the token and user info:
   ```json
   {
     "token": "abc123...",
     "id": 1,
     "username": "alice",
     "email": "alice@example.com",
     "is_staff": false
   }
   ```
3. The frontend stores `token` in `localStorage.authToken` and the user object in `localStorage.userData`.
4. Every subsequent authenticated request includes the header:
   ```
   Authorization: Token abc123...
   ```

The helper `getAuthHeader()` in `MusicApp-frontend/src/utils/auth.js` builds this header automatically.

### Logout flow

`POST /api/auth/logout/` invalidates the token server-side, and the frontend clears both `localStorage` entries.

---

## 🛠 Staff Dashboard

The Staff Dashboard is only accessible to users with `is_staff = True`. The "Staff" link in the navigation bar is hidden for everyone else, and the dashboard route itself does a client-side gate that shows **"🚫 Acesso Negado"** to non-staff users.

Sub-sections (all under `/staff-dashboard/...`):

| Path | Component | Purpose |
|---|---|---|
| `/staff-dashboard/import` | `ImportFromDeezer` | 4-step Deezer import wizard |
| `/staff-dashboard/article` | `CreateArticle` | Create & delete articles |
| `/staff-dashboard/concertos` | `AddConcerto` | Add concerts |
| `/staff-dashboard/comments` | `AnalyzeComments` | Moderate user comments |
| `/staff-dashboard/ratings` | `ManageRatings` | Moderate user ratings |

> 💡 You can create a staff user with `python manage.py createsuperuser`, or by toggling `is_staff` in `/admin/` for any existing user. The included **`test` / `test12345`** account already has staff privileges.

---

## 🎶 Deezer Integration

The catalogue can be populated automatically by importing real data from Deezer.

### How it works

The backend uses `MusicApp/deezer.py`, which exposes three helpers that call the Deezer public API:

```python
search_artist(query)         # → GET https://api.deezer.com/search/artist?q=<query>
get_artist_albums(deezer_id) # → GET https://api.deezer.com/artist/<id>/albums
get_album_tracks(deezer_id)  # → GET https://api.deezer.com/album/<id>/tracks
```

These are exposed via the `/api/deezer_*` endpoints listed above.

### Import wizard (frontend)

`ImportFromDeezer.jsx` walks staff through a 4-step flow:

1. **Search Artist** — type an artist name, pick from Deezer results.
2. **Select Albums** — choose which of the artist's albums to import.
3. **Select Tracks** — choose which tracks from those albums to import.
4. **Review & Save** — confirms and persists everything to the database, automatically:
   - Reuses an existing `Artist` if its `deezer_id` already exists, otherwise creates a new one.
   - Creates each selected `Album` linked to that artist.
   - Creates each selected `Music` track linked to its album.

No Deezer API key is required — the public API is used.

---

🎵 *Made with love by a group of music enthusiasts.*
