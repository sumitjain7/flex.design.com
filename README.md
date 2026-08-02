# How to Run the Flex Design System Web Showcase Locally

This package contains the production-ready static assets for the **Flex Design System Web Showcase** (built using Kotlin WebAssembly). 

Since the application runs on WebAssembly, opening the `index.html` file directly in your browser (`file://` protocol) will fail due to browser security restrictions (CORS). You must serve these files using a local HTTP server.

Below are the easiest ways to run this locally:

---

## Method 1: Using Node.js (Recommended)
If you have Node.js installed, you can use `npx` to serve the folder instantly without installing any global packages:

1. Open your terminal in this directory.
2. Run:
   ```bash
   npx serve
   ```
3. Open the URL shown in the terminal (usually `http://localhost:3000`).

---

## Method 2: Using Python
If you don't have Node.js but have Python installed, you can use Python's built-in HTTP server:

### Python 3:
1. Open your terminal in this directory.
2. Run:
   ```bash
   python3 -m http.server 8080
   ```
3. Open [http://localhost:8080](http://localhost:8080) in your browser.

### Python 2:
1. Open your terminal in this directory.
2. Run:
   ```bash
   python -m SimpleHTTPServer 8080
   ```
3. Open [http://localhost:8080](http://localhost:8080) in your browser.

---

## Method 3: Using Docker
If you prefer running via Docker, you can spin up a lightweight Nginx web server:

1. Open your terminal in this directory.
2. Run:
   ```bash
   docker run --name flex-showcase -v "$PWD":/usr/share/nginx/html:ro -p 8080:80 -d nginx:alpine
   ```
3. Open [http://localhost:8080](http://localhost:8080) in your browser.
4. To stop the server later, run: `docker stop flex-showcase && docker rm flex-showcase`

---

## ⚠️ Hosting Requirements (For Production)
When uploading these static assets to a production hosting provider (e.g., AWS S3 + CloudFront, Nginx, Netlify, Vercel, or Apache):
1. **Directory Root**: Configure your server to use `index.html` as the entrypoint.
2. **MIME-Type for WASM**: Ensure that your web server serves `.wasm` files with the header `Content-Type: application/wasm`. (If this header is missing or incorrect, browsers will refuse to instantiate the WebAssembly module).
