# TravelMate

**Explore. Save. Plan.**

TravelMate is a responsive travel web app where users can discover destinations, save their favourite places, find directions, and plan trips with a budget estimator and packing checklist. It is a front-end-only project built with React and Vite, and all user data is stored in the browser's LocalStorage.

---

## Features

| Area | What it does |
| --- | --- |
| **Home** | Hero search bar, featured destinations, travel utilities, quick tips, and a call to action |
| **Authentication** | Register and log in with form validation. The session is kept in LocalStorage |
| **Protected routes** | Planner, Favourites and Profile need a login. Visitors are redirected to Login and sent back afterwards |
| **Explore** | Search the built-in destinations and filter by category (Beach, Mountains, Historical, Adventure, City). If nothing matches, it searches worldwide using OpenStreetMap Nominatim |
| **Favourites** | Save places from Explore, or add your own. Edit, add personal notes, and delete with confirmation |
| **Map** | Type a destination and open turn-by-turn navigation in Google Maps. An OpenStreetMap map is embedded on the page |
| **Trip planner** | Save trip plans with destination, date, budget, notes and a packing checklist |
| **Budget estimator** | Daily spend × number of days, formatted in ₹ |
| **Profile** | Shows account details, counts of favourites and planned trips, and a logout button |
| **Theme** | Light and dark mode, remembered between visits |
| **UX** | Toast messages, empty states, and a layout for mobile, tablet and desktop |

---

## Tech stack

- **React 19** with functional components and hooks
- **React Router 7** for routing and protected routes
- **Vite 8** for the dev server and build
- **lucide-react** for icons
- **Plain CSS** (`src/index.css`) for styling and theming
- **LocalStorage** for data (no backend)
- **OpenStreetMap Nominatim** for live destination search and **Google Maps** for navigation links

---

## Getting started

### Prerequisites

- **Node.js 20.19 or newer** (Node 22 LTS recommended). Check with `node -v`.
- **npm** (comes with Node.js).
- An internet connection for destination images, live search and maps.

### Run locally

```bash
# 1. Install dependencies
npm install

# 2. Start the development server
npm run dev
```

Open the local address printed in the terminal (usually `http://localhost:5173`). `npm start` does the same thing as `npm run dev`.

### Production build

```bash
npm run build     # creates the dist/ folder
npm run preview   # serves the production build locally
```

### Run it in VS Code

1. Choose **File > Open Folder** and select the project folder.
2. Open the terminal with **Terminal > New Terminal**.
3. Run `npm install`, then `npm run dev`.

---

## How to use the app

1. **Register** an account (name, valid email, password of at least 6 characters, matching confirmation), then **log in**.
2. Go to **Explore**, search a place or pick a category, and press **Save place**.
3. Open **Favourites** to add your own places, edit notes, or delete entries.
4. Use **Map** to enter a destination and press **Navigate Now** to open Google Maps directions.
5. In **Planner**, create a trip, add packing items, and save it. Use the budget estimator on the side for a quick total.
6. Open **Profile** to see your totals or log out.

---

## Project structure

```
travelmate/
├── index.html
├── package.json
└── src/
    ├── main.jsx                 # App entry: Router + AppProvider
    ├── App.jsx                  # Route definitions
    ├── index.css                # Global styles, light/dark themes, responsive layout
    ├── components/
    │   ├── Layout.jsx           # Navbar, footer, theme toggle, toast, <Outlet />
    │   ├── ProtectedRoute.jsx   # Redirects to /login when not signed in
    │   └── PlaceCard.jsx        # Destination card with Save button
    ├── context/
    │   └── AppContext.jsx       # Auth, favourites, trips, theme, toast state
    ├── data/
    │   └── places.js            # Built-in destinations
    ├── pages/
    │   ├── Home.jsx
    │   ├── Login.jsx            # Also exports the shared AuthShell layout
    │   ├── Register.jsx
    │   ├── Explore.jsx
    │   ├── Dashboard.jsx        # "Favourites" page (create / edit / delete)
    │   ├── MapPage.jsx
    │   ├── Planner.jsx
    │   └── Profile.jsx
    └── utils/
        └── storage.js           # read / write / uid helpers for LocalStorage
```

### Routes

| Path | Page | Access |
| --- | --- | --- |
| `/` | Home | Public |
| `/explore` | Explore | Public |
| `/map` | Map | Public |
| `/login`, `/register` | Authentication | Public |
| `/planner` | Trip planner | Login required |
| `/dashboard` | Favourites | Login required |
| `/profile` | Profile | Login required |
| `*` | Falls back to Home | Public |

---

## Data storage

Everything is saved in the browser under these LocalStorage keys:

| Key | Contents |
| --- | --- |
| `tm_users` | Registered accounts |
| `tm_session` | The signed-in user |
| `tm_favourites` | Saved and custom favourite places |
| `tm_trips` | Saved trip plans |
| `tm_theme` | `light` or `dark` |

To start fresh, clear the site's data in your browser's developer tools (Application > Local Storage).

> **Security note:** this project uses LocalStorage on purpose, so passwords are stored unencrypted in the browser. That is fine for a demo or learning project, but it is **not suitable for real authentication**. A production app needs a backend with hashed passwords and secure sessions.

---

## Known limitations

- **Map preview is static.** The embedded OpenStreetMap shows a fixed view of India. The destination you type only changes the Google Maps navigation link.
- **Weather is a placeholder.** The Map page marks where a weather API can be connected later.
- **Packing checklist items cannot be ticked yet.** Items are added and listed, but there is no check-off interaction.
- **Planner trips cannot be edited.** They can be created and deleted.
- **Footer items** (Travel tips, Privacy, Instagram, YouTube, Facebook) are plain text, not links.
- **Data is per browser.** Accounts and plans do not sync between devices or browsers.
- **Needs internet.** Images come from Unsplash, and live search uses Nominatim, which has usage limits. If it is unreachable, Explore shows an error message.

---

## Ideas for future improvements

- Connect a weather API on the Map page
- Make the embedded map follow the searched destination
- Add tick-off support to checklists and an edit option for trips
- Replace LocalStorage auth with a real backend (Node/Express, Firebase or Supabase)
- Add image upload for custom favourites

---

## Scripts

| Command | Description |
| --- | --- |
| `npm run dev` / `npm start` | Start the development server |
| `npm run build` | Create a production build in `dist/` |
| `npm run preview` | Preview the production build |
