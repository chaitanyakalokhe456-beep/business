# BusinessView

BusinessView is a business management dashboard for tracking sales, expenses, inventory, customers, reports, and alerts. This repository is organized into a frontend, backend, database resources, and project documentation.

## Project structure

```text
businessview/
├── frontend/
│   ├── index.html
│   ├── package.json
│   ├── vite.config.js
│   └── src/
│       ├── App.jsx
│       ├── main.jsx
│       ├── pages/
│       │   ├── Home/Home.jsx
│       │   ├── Dashboard/Dashboard.jsx
│       │   ├── Sales/Sales.jsx
│       │   ├── Expenses/Expenses.jsx
│       │   ├── Inventory/Inventory.jsx
│       │   ├── Customers/Customers.jsx
│       │   ├── Reports/Reports.jsx
│       │   ├── Alerts/Alerts.jsx
│       │   ├── AIInsights/  (reserved; intentionally empty)
│       │   └── Settings/Settings.jsx
│       ├── components/      (business layout, buttons, charts, tables)
│       ├── data/            (shared prototype records)
│       ├── services/        (API client)
│       ├── utils/           (currency and date helpers)
│       └── styles/          (shared CSS)
├── backend/
│   ├── routes/              (sales, expenses, inventory, customers)
│   ├── controllers/         (route handlers; currently return 501)
│   ├── models/              (Product, Sale, Expense, Customer, User)
│   ├── middleware/          (auth and error handling)
│   ├── package.json
│   └── server.js
├── database/                (schema.sql and sample-data.json)
├── docs/                    (features and notes)
└── README.md
```

## Running the frontend

On Windows, double-click `start-website.bat` in the project root. It checks
the required tools, installs missing dependencies, starts the frontend and
account API, and opens the website in your browser. Keep its command window
open while using the site; closing it stops the servers. Startup messages and
errors are shown in that window.

Alternatively, open a terminal in the project root and run:

```sh
npm install
npm install --prefix frontend
npm install --prefix backend
npm run dev
```

The dev command starts both the frontend and account API. Vite prints the
local URL (`http://localhost:5173`) when it is ready.

To run just one service separately, use `npm run dev:web` or
`npm run dev:api` from the project root.

## Running the backend separately

```sh
npm install
npm install --prefix backend
npm run dev:api
```

The API runs at `http://localhost:3000` and creates its SQLite database at
`backend/data/businessview.sqlite`. Keep both frontend and backend running to
create accounts or sign in. Account passwords are stored as scrypt hashes, and
sign-in sessions use an HTTP-only cookie. This is an initial account system,
not a production deployment; configure HTTPS and `FRONTEND_ORIGIN` before
exposing it publicly.

`localhost` is only available on this computer; a public website URL requires
deploying the frontend and API to a hosting provider.

## Status

The frontend includes a responsive sign-in screen, a business dashboard, and working views for sales, expenses, inventory, customers, reports, alerts, and settings. New accounts start with no business records. The dashboard can optionally load clearly labeled fictional City Mart example records for preview; clear them before entering actual records. Business records and profile values are saved in the current browser's local storage. `AIInsights` remains reserved for a later phase and is intentionally not a primary navigation item.

Account registration, sign-in, and account profile updates use the backend and a local SQLite database. Passwords are stored as scrypt hashes, and sessions use HTTP-only cookies. Business records remain in browser storage, separated by signed-in account on that browser; they are not uploaded or synchronized between devices. Sales, expense, inventory, and customer API handlers are still unimplemented and return HTTP 501. This is an initial local-development account system, not a production-ready hosted service.
