# SchemeSaathi

Government scheme discovery and exact eligibility matching platform built with React, Django REST Framework and MySQL.

This project was built with [Lovable](https://lovable.dev).

## Build with Lovable

Open your project in the [Lovable editor](https://lovable.dev) and keep building.

- **Ship faster**: describe what you want to build and Lovable handles the code.
- **Stay in sync**: connect the project to GitHub and every change made in Lovable is committed straight to your repository.
- **Full ownership**: this code is yours. Push to your repository and your changes sync back into Lovable, ready for your next prompt.

## Development

Prefer working locally? You need Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```

## Google sign-in setup

The login and sign-up pages support Google Identity Services. Create an OAuth 2.0 Web Client in Google Cloud, add your local and production origins, then copy `.env.example` to `.env` and set `VITE_GOOGLE_CLIENT_ID`.

When `VITE_API_URL` is configured, accounts use the Django/MySQL backend and Google ID tokens are verified server-side. Browser-only accounts remain available solely as an offline prototype fallback when the API URL is absent.

## Full-stack setup (MySQL)

1. Copy `backend/.env.example` to `backend/.env` and replace its passwords and Google Client ID.
2. Copy `.env.example` to `.env` and use the same Google Client ID.
3. Start MySQL with `docker compose up -d mysql`, or create the same database/user in MySQL Workbench.
4. In `backend`, create a virtual environment and install `requirements.txt`.
5. Run `python manage.py migrate`, then `python manage.py createsuperuser`.
6. Run the API with `python manage.py runserver`.
7. In the project root, run `npm install` and `npm run dev`.

Frontend: `http://localhost:5173`  
API: `http://127.0.0.1:8000/api/`  
Admin: `http://127.0.0.1:8000/admin/`

### Eligibility rule format

Every rule is mandatory. The user is alerted only when all required rules pass. Missing data produces `insufficient_data`; it never produces an eligibility alert.

```json
[
  { "field": "state", "operator": "eq", "value": "Tamil Nadu", "label": "Tamil Nadu resident" },
  { "field": "annual_income", "operator": "lte", "value": 200000, "label": "Income up to ₹2 lakh" },
  { "field": "occupation", "operator": "in", "value": ["farmer", "farm_worker"], "label": "Farmer" }
]
```

Supported operators: `eq`, `in`, `lte`, `gte`, `lt`, `gt`.

## Built with

- TanStack Start
- TypeScript
- React
- Tailwind CSS
