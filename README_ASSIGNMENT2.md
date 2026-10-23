# SkillSwap

A skill-exchange platform where students teach what they know and learn what they want, with no money involved.
Built with **React 18, React Router 6, Vite, and plain CSS**. Profiles and requests are saved in `localStorage`.

## Run it in VS Code

1. Install **Node.js 18 or newer** from https://nodejs.org (check with `node -v`).
2. In VS Code, choose **File > Open Folder** and select the `skillswap` folder.
3. Open the terminal with **Terminal > New Terminal** (or `` Ctrl + ` ``).
4. Install the dependencies (first time only):
   ```bash
   npm install
   ```
5. Start the development server:
   ```bash
   npm run dev
   ```
6. Open **http://localhost:5173** in your browser (it opens automatically). Edits you save in VS Code appear instantly.

To create a production build, run `npm run build`. To preview it, run `npm run preview`.

## Pages

| Route | What it does |
| --- | --- |
| `/` | Hero, live statistics, popular skills, three-step overview |
| `/explore` | Skill cards, search, category filters, **Request Skill Swap** modal |
| `/offer` | Validated form; the new profile appears in Explore immediately |
| `/requests` | Sent and Received tabs, status filters (Pending, Accepted, Rejected), duplicate prevention |
| `/how-it-works` | Three steps, benefits, FAQ accordion |

## Try the request flow

1. Open **Explore Skills** and press **Request Skill Swap** on any profile. Pending status appears on the card and on the Requests page.
2. Try requesting the same profile again. The card is locked, and the modal also blocks duplicates.
3. On **Swap Requests**, press **Switch user** and enter the name of the profile owner (for example `Meera Nair`).
4. Open the **Received** tab and press **Accept** or **Reject**. Switch back to see the updated status in the Sent tab.
5. The default user `Demo User` already has two incoming requests, so you can try Accept and Reject straight away.
6. **Reset sample data** at the bottom of the Requests page restores the original data.

## Project structure

```
skillswap/
├── index.html
├── package.json
├── vite.config.js
├── public/favicon.svg
└── src/
    ├── main.jsx                  # App entry, router and provider
    ├── App.jsx                   # Layout and routes
    ├── index.css                 # All styles, organised by section
    ├── context/
    │   └── SkillSwapContext.jsx  # Profiles, requests, current user, duplicate checks
    ├── hooks/
    │   └── useLocalStorage.js    # useState that persists to localStorage
    ├── data/
    │   ├── sampleData.js         # Starting profiles and requests
    │   ├── skills.js             # Skill catalog, categories, levels
    │   └── steps.js              # How It Works steps and FAQ
    ├── utils/
    │   ├── helpers.js            # Initials, avatar colours, text helpers
    │   └── validation.js         # Form validation rules
    ├── components/               # Navbar, Footer, Logo, SkillCard, SkillForm,
    │                             # FormField, RequestModal, RequestCard, Toast, ...
    └── pages/                    # Home, Explore, Offer, Requests, HowItWorks, NotFound
```

## Troubleshooting

- **`npm` is not recognized**: install Node.js, then restart VS Code.
- **Port 5173 is busy**: Vite picks the next free port and prints the address in the terminal.
- **Fonts look different offline**: the Google Fonts links need internet; system fonts are used as a fallback.
- **Want a clean slate**: use *Reset sample data*, or clear the site's data in your browser's developer tools.
