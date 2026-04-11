# React + TypeScript Setup Guide (Vite)
A guide to setup React working environent with Typescript/Javascript alongside vite + tailwindcss

## Prerequisites
Make sure Node.js is installed on your system.

---

## 📁 Client Setup

### 1. Initialize Project
```bash
npm init -y
```

---

### 2. Edit `package.json`

Add:
```json
"type": "module",
"scripts": {
  "dev": "vite",
  "build": "vite build",
  "preview": "vite preview"
}
```

---

### 3. Install React

```bash
npm install react react-dom
```

---

### 4. Install TypeScript

```bash
npm install -D typescript @types/react @types/react-dom
```

---

### 5. Install Vite + React Plugin

```bash
npm install -D vite @vitejs/plugin-react
```

---

### 6. (Optional) Install TailwindCSS

```bash
npm install tailwindcss @tailwindcss/vite
```

---

## ⚙️ Vite Configuration

Create `vite.config.ts`:

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
  server: {
    port: 5173
  }
});
```

---

## ⚙️ TypeScript Configuration

Generate config:

```bash
npx tsc --init
```

Update `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "lib": ["DOM", "ES2020"],
    "moduleResolution": "Bundler",
    "esModuleInterop": true,
    "noUncheckedSideEffectImports": false
  }
}
```

---

## 🧱 HTML Setup

Create `index.html` in root/client folder:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />

    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <meta name="theme-color" content="#000000" />

    <meta name="description" content="Your description" />

    <title>React + TS App</title>
  </head>

  <body>
    <div id="root"></div>

    <script type="module" src="src/main.tsx"></script>
  </body>
</html>
```

---

## ⚛️ React App Setup

### `src/App.tsx`

```tsx
export default function App() {
  return <h1>Hello World</h1>;
}
```

---

### `src/main.tsx`

```tsx
import { createRoot } from "react-dom/client";
import App from "./App";
import "./styles.css";

const root = createRoot(document.getElementById("root")!);
root.render(<App />);
```

---

### `src/styles.css`

```css
@import "tailwindcss";
```

---

## 🚀 Run Development Server

```bash
npm run dev
```

---

## 📦 Build for Production

```bash
npm run build
```

---

## 👀 Preview Production Build

```bash
npm run preview
```



## 📦 Server Setup

```bash
npm init -y
```

---

## 📥 Install Dependencies

```bash
npm install express cors dotenv
```

---

## 📥 Install Dev Dependencies (TypeScript)

```bash
npm install -D typescript @types/express @types/node @types/cors tsx
```

---

## ⚙️ Update `package.json`

Add:

```json
"type": "module",
"scripts": {
  "dev": "tsx watch src/index.ts",
  "build": "tsc",
  "start": "node dist/index.js"
}
```

---

## ⚙️ TypeScript Configuration

Generate config:

```bash
npx tsc --init
```

Update `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "moduleResolution": "bundler",
    "outDir": "./dist",
    "rootDir": "./src",
    "esModuleInterop": true
  }
}
```

---

## 📁 Server Entry Point

Create `src/index.ts`:

```ts
import express, { type Request, type Response } from "express";
import cors from "cors";
import dotenv from "dotenv";

// Initialize environment variables
dotenv.config();

const app = express();
const PORT = 5000;

// Middleware
app.use(cors());
app.use(express.json());

// Health Check Route
app.get("/", (req: Request, res: Response) => {
  res.status(200).json({ message: "Server is healthy" });
});

// Test API Route
app.get("/api/test", (req: Request, res: Response) => {
  res.json({
    message: "Backend is connected!",
    timestamp: new Date().toISOString()
  });
});

// Start Server
app.listen(PORT, () => {
  console.log(`🚀 Server running on http://localhost:${PORT}`);
});
```

---

# 🔗 Connecting Frontend to Backend

## Update `App.tsx`

```tsx
import { useEffect, useState } from "react";

export default function App() {
  const [message, setMessage] = useState<string>("Loading...");

  useEffect(() => {
    const fetchTestData = async () => {
      try {
        const response = await fetch("/api/test");
        const data = await response.json();
        setMessage(data.message);
      } catch (error) {
        console.error("Error fetching data:", error);
        setMessage("Failed to connect to backend.");
      }
    };

    fetchTestData();
  }, []);

  return (
    <div className="p-8">
      <h1 className="text-2xl font-bold text-blue-600">BookMyRoom Frontend</h1>
      <div className="mt-4 p-4 bg-gray-100 rounded-lg shadow">
        <p className="text-gray-700">
          Backend Status:{" "}
          <span className="font-mono font-bold">{message}</span>
        </p>
      </div>
    </div>
  );
}
```

---

## ⚙️ Add Proxy in `vite.config.ts`

```ts
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
  plugins: [react(), tailwindcss()],
  server: {
    port: 5173,
    proxy: {
      "/api": {
        target: "http://localhost:5000",
        changeOrigin: true
      }
    }
  }
});
```

---

## 🚀 Run Server

```bash
npm run dev
```

---

## 🧪 Test

- Backend: http://localhost:5000/api/test  
- Frontend: http://localhost:5173  

---
