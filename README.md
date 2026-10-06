# React and Express Full-Stack Sample

A Vite React SPA and an Express API deployed as separate components behind one
public hostname.

## Structure

```text
web/  React 19 and Vite 8 static frontend
api/  Express 5 web API
```

Each component has its own `package.json` and lockfile.

## Run locally

Install both components:

```powershell
Set-Location .\api
npm install
Set-Location ..\web
npm install
```

Start the API:

```powershell
Set-Location .\api
$env:PORT = "18089"
npm start
```

In another terminal, start the frontend:

```powershell
Set-Location .\web
npm run dev
```

Vite proxies `/api` to `http://127.0.0.1:18089`, matching the deployed
same-origin route shape.

## Build and verify

```powershell
Set-Location .\api
npm test

Set-Location ..\web
npm run lint
npm run build
npm run preview -- --host 127.0.0.1 --port 8080

Set-Location ..
.\scripts\verify.ps1 -BaseUrl http://127.0.0.1:8080
```

## Builder Apps configuration

The root `builder.yaml` declares:

- A Vite-detected static `web` component at `/`
- An explicit Node.js `api` component at `/api`

The route split keeps SPA fallback behavior out of the API prefix and allows
the browser to call the API without CORS configuration.
