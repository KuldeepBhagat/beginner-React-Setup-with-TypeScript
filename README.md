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
import { useState } from "react";

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
