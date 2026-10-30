# Containerized React Application

This project demonstrates how to containerize a React (TypeScript) web application using Docker multi-stage builds and serve it via Nginx for production deployment.

---

## Key Technical Highlights

* **Framework:** React + TypeScript (Bootstrapped with Create React App)
* **Build Engine:** Multi-stage Dockerfile using Node.js and Nginx
* **Web Server:** Nginx (`1.27.0-alpine`) serving lightweight static assets
* **Development:** Local npm dev server with Hot Module Reloading (HMR)

---

## 🛠️ Multi-Stage Dockerfile Architecture

The build process uses a **2-stage multi-stage Docker build** to keep the final image size minimal:

1. **Stage 1: Build Phase (`node:22-alpine`)**
   * Installs production dependencies using `npm ci`.
   * Compiles TypeScript and React source code into static production assets (`npm run build`).

2. **Stage 2: Production Serving Phase (`nginx:1.27.0`)**
   * Copies only the compiled static build output from Stage 1 into Nginx's public directory (`/usr/share/nginx/html`).
   * Runs lightweight Nginx web server to serve the React single-page application (SPA).

---

## 🚀 How to Run Locally

### Option 1: Development Mode (Without Docker)

1. **Install dependencies:**
   ```bash
   npm install
   1.npm start(Start dev server)
   2.docker build -t react-app:nginx . (Build the Docker Image)
   3.docker run -p 9001:80 --rm react-app:nginx
   docker run -p 9000:80 --rm react-app:blue
   (Run the Container Port Mapping Examples)
   4.Open http://localhost:9001 (or http://localhost:9000 (Access Application:)
