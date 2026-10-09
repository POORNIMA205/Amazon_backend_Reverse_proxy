# Amazon Backend Reverse Proxy Using NGINX

## 🚀 Project Overview

This project implements an **NGINX Reverse Proxy** for an Amazon-style e-commerce backend built with FastAPI. NGINX acts as an intermediary between clients and the backend application, forwarding incoming HTTP requests to the appropriate backend server and returning responses to clients.

The project demonstrates reverse proxy configuration, HTTP request forwarding, backend integration, and centralized API access.

## ✨ Features

* **NGINX Reverse Proxy:** Routes client requests to the FastAPI backend.
* **Request Forwarding:** Forwards incoming HTTP requests to the configured backend server.
* **Response Handling:** Returns backend responses to clients through NGINX.
* **Centralized API Access:** Provides a single entry point for backend requests.
* **Backend Integration:** Works with an Amazon-style e-commerce API.
* **Scalable Architecture:** Provides a foundation for load balancing and additional backend services.

## 🛠️ Technology Stack

* **NGINX** — Reverse proxy server
* **Python** — Backend application development
* **FastAPI** — REST API framework
* **Uvicorn** — ASGI application server
* **Git & GitHub** — Version control and project hosting

## 🏗️ System Architecture

```text
              Client
                |
                v
        NGINX Reverse Proxy
          Port 80 / 8080
                |
                v
       FastAPI Application
          Uvicorn Server
            Port 8000
                |
                v
       Amazon Backend APIs
   Register | Login | Products
       Cart | Orders | Payments
```

## 📁 Project Structure

Example structure:

```text
Amazon_backend_Reverse_proxy/
├── nginx.conf
├── README.md
└── ...
```

The actual repository may also contain Docker configuration, scripts, or application files depending on your setup.

## ⚙️ Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/POORNIMA205/Amazon_backend_Reverse_proxy.git
cd Amazon_backend_Reverse_proxy
```

### 2. Install NGINX

Install NGINX using the appropriate installation method for your operating system.

For Windows, download it from the official website:

https://nginx.org/en/download.html

Extract the downloaded archive and open Git Bash or a terminal in the NGINX directory.

### 3. Configure the reverse proxy

Create or update `conf/nginx.conf` in your NGINX installation directory with a configuration similar to the following:

```nginx
events {}

http {
    upstream amazon_backend {
        server 127.0.0.1:8000;
    }

    server {
        listen 8080;
        server_name localhost;

        location / {
            proxy_pass http://amazon_backend;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
}
```

This configuration listens on port `8080` and forwards requests to the FastAPI backend on port `8000`.

### 4. Start the Amazon backend

Open a separate terminal in your Amazon backend project and activate its Python environment.

Run:

```bash
uvicorn app.main:app --reload --port 8000
```

Ensure the backend starts successfully before testing NGINX.

### 5. Test and start NGINX

From the NGINX installation directory, test the configuration:

```bash
nginx -t
```

If the configuration test succeeds, start NGINX:

```bash
nginx
```

If NGINX is already running and you have changed its configuration, reload it:

```bash
nginx -s reload
```

### 6. Access the application through NGINX

Send requests through the reverse proxy instead of directly to the backend.

Base URL:

```text
http://localhost:8080
```

FastAPI documentation, if exposed by the backend:

```text
http://localhost:8080/docs
```

## 🧪 Testing

Verify that:

1. The FastAPI backend is running on port `8000`.
2. NGINX starts without configuration errors.
3. Requests sent to port `8080` reach the backend.
4. API responses are returned correctly through the proxy.

The exact API endpoints depend on the routes implemented in the Amazon backend.

## 🔒 Security Considerations

* Do not expose passwords, API keys, JWT secrets, or `.env` files in GitHub.
* Use HTTPS for production deployments.
* Configure appropriate request size limits and timeouts.
* Apply authentication and authorization in the backend.
* Restrict access to internal backend ports when deploying in production.

## 🔮 Future Enhancements

* Load balancing across multiple FastAPI instances
* HTTPS configuration with TLS certificates
* Rate limiting and request throttling
* Health checks and monitoring
* Docker-based deployment
* Centralized access and error logging

## 🎯 Learning Outcomes

* Understanding NGINX reverse proxy architecture
* Configuring HTTP request forwarding
* Integrating NGINX with FastAPI
* Managing client-server communication
* Testing backend APIs through a reverse proxy
* Using Git and GitHub for project version control

## 👩‍💻 Author

**Poornima H B**

* GitHub: https://github.com/POORNIMA205
* LinkedIn: https://www.linkedin.com/in/poornima-h-b-36bb3a2aa/

---

*This project demonstrates NGINX reverse proxy integration with an Amazon-style FastAPI backend.*
