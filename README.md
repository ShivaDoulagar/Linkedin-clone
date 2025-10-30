# LinkedIn Clone 

This repository contains a small LinkedIn-like application split into two parts:

- `server/` — Express.js backend (API, auth, MongoDB, file uploads)
- `client/` — React front-end (Create React App)

This README explains how to set up and run both parts locally (development) and how to build the client for production.

## Prerequisites

- Node.js (>= 16) and npm
- MongoDB (local instance or a hosted cluster URI)
- Optional: nodemon for server auto-reload (dev dependency in `server/package.json`)

## Quick start (development)

1. Open two terminals/tabs.

2. Start the backend server:

```bash
cd server
# install server deps
npm install

# create a .env file in server/ (see example below)
# then start in dev mode (auto-restart on change):
npm run dev
```

3. Start the React client (in the other terminal):

```bash
cd client
npm install
npm start
```

The React app should open at http://localhost:3000 and the server will run on the port you set in `server/.env` (commonly `5000`).

## Environment variables (server/.env)

Create a `.env` file in the `server/` folder with the following variables (example):

```
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/linkedin
JWT_SECRET=your_jwt_secret_here
```

Adjust `MONGO_URI`, `PORT`, and `JWT_SECRET` for your environment.

## Build & Production

1. Build the React app:

```bash
cd client
npm run build
```

2. Serve the built files from a static server or integrate them into the Express server. An easy option is to use a static file server (e.g., `serve`) or to copy `client/build` into a folder served by the backend and configure Express to serve static files.

Example using `serve`:

```bash
npm install -g serve
serve -s client/build -l 3000
```

Or modify the Express server to serve static assets from `client/build` (not included by default in this repo).

## Useful scripts

- Server

  - `npm run dev` — start server with nodemon (development)
  - `npm start` — start server with node (production)

- Client (inside `client/`)
  - `npm start` — start CRA dev server
  - `npm run build` — build production bundle

## Common issues & troubleshooting

- "react-scripts is not recognized": make sure you ran `npm install` inside `client/` and that `react-scripts` is present in `client/package.json` dependencies.
- Backend errors about JWT or DB connection: verify `.env` values and that MongoDB is reachable.
- If you added local changes to build tooling (webpack, etc.), revert to CRA defaults unless you intentionally ejected.

## Notes

- The client uses AOS (Animate On Scroll) for some UI animations — you can initialize it from the React components via the `aos` npm package or via CDN. This project includes examples of initializing AOS in components.
- File uploads are saved to `server/uploads` (the server creates these folders on startup).

## Contact / Next steps

If you want, I can:

- Add a single command to run both client and server concurrently (using `concurrently` or `npm-run-all`).
- Configure the server to serve the client `build` automatically.
- Add a `.env.example` file to the repo.

Happy hacking!
