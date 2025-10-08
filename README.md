# 🚀 **Modern Full-Stack Setup Guide (React + Express + Mobile)**

Welcome to your complete guide for launching a full-stack web app with **React (Vite)** on the frontend, **Express** on the backend, and an optional **React Native (Expo)** mobile app using **Nativewind**. This setup includes modern tools like **TailwindCSS**, **MongoDB**, **Prisma**, **Cloudinary**, and optional **local AI models**, making it perfect for scalable, high-performance applications.

<div align="center">

![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat-square&logo=vite&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white)
![Expo](https://img.shields.io/badge/Expo-000020?style=flat-square&logo=expo&logoColor=white)

</div>

---

## 📚 **Table of Contents**

* [🎨 Frontend Setup (React + Vite)](#frontend-setup-react--vite)
* [🔧 Backend Setup (Express)](#backend-setup-express)
* [📱 Mobile App Setup (React Native + Expo)](#mobile-app-setup-react-native--expo)
* [🗄️ Database Setup (Prisma)](#database-setup-prisma)
* [⚙️ Running the App Locally](#running-the-app-locally)
* [🛠️ GitHub Integration](#github-integration)
* [📦 `package.json` Files](#packagejson-files)
* [☁️ Cloudinary Integration](#cloudinary-integration)
* [🔐 Authentication Middleware](#authentication-middleware)
* [💻 Linux Development Setup](#linux-development-setup)
* [💡 Bonus: Local AI Models](#bonus-local-ai-models)

---

## 🎨 **Frontend Setup (React + Vite)**

Build a blazing-fast frontend with Vite, styled with TailwindCSS, and enhanced with modern libraries.

### 🛠️ Steps

1. **Create the App**

   ```bash
   npm create vite@latest
   ```

2. **Install Dependencies**

   ```bash
   npm install
   npm install tailwindcss @tailwindcss/vite
   npm install @google/generative-ai @react-three/drei @react-three/fiber axios chart.js chartjs-plugin-datalabels framer-motion jspdf jspdf-autotable keen-slider lucide-react qrcode.react react react-calendar react-chartjs-2 react-datepicker react-dom react-icons react-pdf react-qr-code react-responsive react-router-dom react-slick slick-carousel socket.io-client
   npm install --dev @eslint/js @types/react @types/react-dom eslint eslint-plugin-react-hooks eslint-plugin-react-refresh globals vite
   ```

3. **Configure Vite**

   Update `vite.config.ts`:

   ```ts
   import { defineConfig } from 'vite';
   import react from '@vitejs/plugin-react';
   import tailwindcss from '@tailwindcss/vite';

   export default defineConfig({
     plugins: [react(), tailwindcss()],
   });
   ```

4. **Configure TailwindCSS**

   In your CSS file (e.g., `src/index.css`):

   ```css
   @import "tailwindcss";
   ```

---

## 🔧 **Backend Setup (Express)**

A robust backend with Express, MongoDB, authentication, and file upload support.

### 🛠️ Steps

1. **Initialize Project**

   ```bash
   npm init -y
   ```

2. **Install Dependencies**

   ```bash
   npm install @google/generative-ai axios bcrypt bcryptjs cloudinary cors dotenv express express-fileupload firebase firebase-admin fs jsonwebtoken jspdf mongodb mongoose multer node-fetch nodemailer qrcode sanitize-filename socket.io validator
   npm install -g nodemon
   ```

3. **Set Up `index.js`**

   ```js
   import express from 'express';
   import mongoose from 'mongoose';
   import dotenv from 'dotenv';
   import cors from 'cors';

   dotenv.config();

   const app = express();

   app.use(cors());
   app.use(express.json());

   mongoose.connect(process.env.MONGO_URI)
     .then(() => console.log('MongoDB connected'))
     .catch(err => console.log(err));

   const PORT = process.env.PORT || 5000;
   app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
   ```

4. **Run the Backend**

   ```bash
   nodemon index.js
   ```

---

## 📱 **Mobile App Setup (React Native + Expo)**

Build a mobile app with Expo and style it with Nativewind (TailwindCSS for React Native).

### 🛠️ Steps

1. **Create the App**

   ```bash
   npx create-expo-app@latest --template
   ```

2. **Install Dependencies**

   ```bash
   npm install nativewind react-native-reanimated@~3.17.4 react-native-safe-area-context@5.4.0
   npm install --dev tailwindcss@^3.4.17 prettier-plugin-tailwindcss@^0.5.11
   npx tailwindcss init
   ```

3. **Configure Nativewind**

   * Update `tailwind.config.js`:

     ```js
     /** @type {import('tailwindcss').Config} */
     module.exports = {
       content: ["./App.tsx", "./components/**/*.{js,jsx,ts,tsx}"],
       presets: [require("nativewind/preset")],
       theme: {
         extend: {},
       },
       plugins: [],
     };
     ```

   * Create `global.css`:

     ```css
     @tailwind base;
     @tailwind components;
     @tailwind utilities;
     ```

   * Update `babel.config.js`:

     ```js
     module.exports = function (api) {
       api.cache(true);
       return {
         presets: [
           ["babel-preset-expo", { jsxImportSource: "nativewind" }],
           "nativewind/babel",
         ],
       };
     };
     ```

   * Update `metro.config.js`:

     ```js
     const { getDefaultConfig } = require("expo/metro-config");
     const { withNativeWind } = require('nativewind/metro');

     const config = getDefaultConfig(__dirname);

     module.exports = withNativeWind(config, { input: './global.css' });
     ```

   * Add to `_layout.tsx`:

     ```tsx
     import "./global.css";
     ```

4. **Run the Mobile App**

   ```bash
   npx expo start
   ```

5. **Export the Expo App**

   ```bash
   npm install -g expo-cli
   expo login
   eas build:configure
   eas build -p android --profile preview
   ```

> **Note**: Remove default files and use `_layout.tsx` as the main app file. Place screens in the `app/screens` folder or similar.

---

## 🗄️ **Database Setup (Prisma)**

Use Prisma for efficient database management with MongoDB or other databases.

### 🛠️ Steps

1. **Install Prisma**

   ```bash
   npm install prisma --save-dev
   npm install @prisma/client
   npx prisma init
   ```

2. **Push Schema to Database**

   ```bash
   npx prisma db push
   ```

3. **Generate Prisma Client**

   ```bash
   npx prisma generate
   ```

4. **View Prisma Studio**

   ```bash
   npx prisma studio
   ```

---

## ⚙️ **Running the App Locally**

* **Frontend**

  ```bash
  npm run dev
  ```

* **Backend**

  ```bash
  nodemon index.js
  ```

* **Mobile App**

  ```bash
  npx expo start
  ```

---

## 🛠️ **GitHub Integration**

### 🔄 Push to GitHub

```bash
git add .
git commit -m "Added new features"
git push origin main --force
```

### ⬇️ Pull from GitHub

```bash
git pull
```

---

## 📦 **`package.json` Files**

### 📁 Frontend

<details>
<summary><code>client/package.json</code></summary>

```json
{
  "name": "client",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint .",
    "preview": "vite preview"
  },
  "dependencies": {
    "@google/generative-ai": "^0.24.0",
    "@react-three/drei": "^10.0.6",
    "@react-three/fiber": "^9.1.2",
    "@tailwindcss/vite": "^4.0.10",
    "axios": "^1.8.1",
    "chart.js": "^4.4.9",
    "chartjs-plugin-datalabels": "^2.2.0",
    "client": "file:",
    "dotenv": "^16.5.0",
    "framer-motion": "^12.5.0",
    "jspdf": "^3.0.1",
    "jspdf-autotable": "^5.0.2",
    "keen-slider": "^6.8.6",
    "lucide-react": "^0.488.0",
    "qrcode.react": "^4.2.0",
    "react": "^19.0.0",
    "react-calendar": "^5.1.0",
    "react-chartjs-2": "^5.3.0",
    "react-datepicker": "^8.3.0",
    "react-dom": "^19.0.0",
    "react-icons": "^5.5.0",
    "react-pdf": "^9.2.1",
    "react-qr-code": "^2.0.15",
    "react-responsive": "^10.0.1",
    "react-router-dom": "^7.2.0",
    "react-slick": "^0.30.3",
    "router-dom": "^3.0.3",
    "slick-carousel": "^1.8.1",
    "socket.io-client": "^4.8.1",
    "tailwindcss": "^4.0.10"
  },
  "devDependencies": {
    "@eslint/js": "^9.21.0",
    "@types/react": "^19.0.10",
    "@types/react-dom": "^19.0.4",
    "@vitejs/plugin-react": "^4.3.4",
    "eslint": "^9.21.0",
    "eslint-plugin-react-hooks": "^5.1.0",
    "eslint-plugin-react-refresh": "^0.4.19",
    "globals": "^15.15.0",
    "vite": "^6.2.0"
  }
}
```

</details>

### 📁 Backend

<details>
<summary><code>server/package.json</code></summary>

```json
{
  "name": "server",
  "version": "1.0.0",
  "type": "module",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "nodemon --quiet index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": "",
  "dependencies": {
    "@google/generative-ai": "^0.24.1",
    "axios": "^1.8.3",
    "bcrypt": "^5.1.1",
    "bcryptjs": "^3.0.2",
    "cloudinary": "^2.6.0",
    "cors": "^2.8.5",
    "dotenv": "^16.4.7",
    "express": "^4.21.2",
    "express-fileupload": "^1.5.1",
    "firebase": "^11.6.0",
    "firebase-admin": "^13.2.0",
    "fs": "^0.0.1-security",
    "jsonwebtoken": "^9.0.2",
    "jspdf": "^3.0.1",
    "mongodb": "^6.14.2",
    "mongoose": "^8.12.1",
    "multer": "^2.0.1",
    "node-fetch": "^3.3.2",
    "nodemailer": "^6.10.0",
    "qrcode": "^1.5.4",
    "sanitize-filename": "^1.6.3",
    "server": "file:",
    "socket.io": "^4.8.1",
    "validator": "^13.12.0"
  }
}
```

</details>

### 📁 Mobile (Expo)

<details>
<summary><code>mobile/package.json</code></summary>

```json
{
  "name": "mobile",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "expo start",
    "android": "expo start --android",
    "ios": "expo start --ios",
    "web": "expo start --web"
  },
  "dependencies": {
    "expo": "^51.0.0",
    "nativewind": "^4.0.0",
    "react": "^19.0.0",
    "react-native": "^0.74.5",
    "react-native-reanimated": "~3.17.4",
    "react-native-safe-area-context": "5.4.0"
  },
  "devDependencies": {
    "babel-preset-expo": "^10.0.0",
    "tailwindcss": "^3.4.17",
    "prettier-plugin-tailwindcss": "^0.5.11"
  },
  "private": true
}
```

</details>

---

## ☁️ **Cloudinary Integration**

Set up Cloudinary for image and video uploads.

### 🛠️ Steps

1. **Create `cloudinary.js`**

   ```js
   import { v2 as cloudinary } from 'cloudinary';
   import dotenv from 'dotenv';

   dotenv.config();

   cloudinary.config({
     cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
     api_key: process.env.CLOUDINARY_API_KEY,
     api_secret: process.env.CLOUDINARY_API_SECRET,
   });

   export const uploadToCloudinary = async (file, resourceType = 'image') => {
     try {
       if (!file) {
         return null;
       }
       const uploadResult = await new Promise((resolve, reject) => {
         const stream = cloudinary.uploader.upload_stream(
           {
             folder: 'website',
             resource_type: resourceType,
             allowed_formats: resourceType === 'video' ? ['mp4'] : ['jpg', 'png'],
             public_id: `${resourceType}_${Date.now()}`,
           },
           (error, result) => {
             if (error) return reject(error);
             resolve(result);
           }
         );
         stream.end(file.buffer);
       });
       return uploadResult.secure_url;
     } catch (error) {
       console.error(`Cloudinary ${resourceType} upload error:`, error);
       throw new Error(`Failed to upload ${resourceType} to Cloudinary`);
     }
   };

   export const deleteFromCloudinary = async (publicId, resourceType = 'image') => {
     try {
       const result = await cloudinary.uploader.destroy(publicId, { resource_type: resourceType });
       return result;
     } catch (error) {
       console.error(`Cloudinary ${resourceType} delete error:`, error);
       throw new Error(`Failed to delete ${resourceType} from Cloudinary`);
     }
   };
   ```

2. **Set Environment Variables**

   Add to `.env`:

   ```env
   CLOUDINARY_CLOUD_NAME=your_cloud_name
   CLOUDINARY_API_KEY=your_api_key
   CLOUDINARY_API_SECRET=your_api_secret
   ```

---

## 🔐 **Authentication Middleware**

Protect routes with JWT-based authentication.

### 🛠️ Steps

1. **Create `middleware.js`**

   ```js
   import jwt from 'jsonwebtoken';
   import { asyncHandler } from '../utils/asyncHandler.js';
   import User from '../models/User.js';

   export const protect = asyncHandler(async (req, res, next) => {
     let token;
     if (req.headers.authorization && req.headers.authorization.startsWith('Bearer')) {
       try {
         token = req.headers.authorization.split(' ')[1];
         const decoded = jwt.verify(token, process.env.JWT_SECRET);
         req.user = await User.findById(decoded.id).select('-password');
         next();
       } catch (error) {
         res.status(401).json({ message: 'Not authorized, token failed' });
       }
     } else {
       res.status(401).json({ message: 'Not authorized, no token' });
     }
   });

   export const admin = (req, res, next) => {
     if (req.user && (req.user.usertype === 'admin' || req.user.usertype === 'superadmin')) {
       next();
     } else {
       res.status(401).json({ message: 'Not authorized as admin' });
     }
   };

   export const superadmin = (req, res, next) => {
     if (req.user && req.user.usertype === 'superadmin') {
       next();
     } else {
       res.status(401).json({ message: 'Not authorized as superadmin' });
     }
   };
   ```

2. **Set JWT Secret**

   Add to `.env`:

   ```env
   JWT_SECRET=your_jwt_secret
   ```

---

## 💻 **Linux Development Setup**

For Linux users, compile and run C programs with the following steps:

```bash
touch program.c
nano program.c
# Write code, save with Ctrl+X, Y, Enter
ls
gcc -o program.exe program.c
chmod +x program.exe
./program.exe
```

---

## 💡 **Bonus: Local AI Models (Optional)**

Integrate AI features locally using [**Ollama**](https://ollama.com):

```bash
ollama run llama3.2
ollama run deepseek-coder
ollama run deepseek-coder:6.7b
```

### Additional Notes

* **DNS Configuration (Optional)**: To set Google DNS on Windows for better connectivity:

  ```bash
  netsh interface ip set dns "Wi-Fi" static 8.8.8.8
  netsh interface ip add dns "Wi-Fi" 8.8.4.4 index=2
  ```

* **Prisma Note**: Ensure your `prisma/schema.prisma` is configured for MongoDB or your preferred database before running `npx prisma db push`.

---

## ✨ Happy Building!

> *“Code like a poet. Deploy like an engineer.”*

---
