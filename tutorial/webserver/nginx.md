---
tags: []
howto: false
title: NGINX - A High Performance Web Server
description: Learn what NGINX is, how it works, and explore its major use cases with detailed configuration examples including reverse proxy, load balancing, SSL termination, caching, and more.
---

# NGINX - A High Performance Web Server

NGINX (pronounced as "engine-x") is an open-source web server that is also used as a **reverse proxy**, **load balancer**, **mail proxy**, and **HTTP cache**. It was originally developed by **Igor Sysoev** in 2004 to solve the **C10k problem**—handling 10,000 simultaneous client connections on a single server.

NGINX is renowned for its high performance, stability, rich feature set, simple configuration, and low resource consumption.

---

## Why NGINX?

- **Event-driven architecture**: Handles multiple connections with a single thread using non-blocking I/O.
- **Efficient resource usage**: Uses less memory and CPU even under heavy load.
- **High concurrency**: Easily handles thousands of simultaneous connections.
- **Modular architecture**: Supports load balancing, reverse proxying, media streaming, and more.

---

## Core Use Cases of NGINX

NGINX is extremely versatile. Here's a breakdown of its primary use cases:

### 1. Web Server

NGINX can serve static content (HTML, CSS, JS, images, etc.) with blazing speed. It is optimized for performance, making it a preferred choice for high-traffic websites.

**Example Configuration:**

```nginx
server {
  listen 80;
  server_name example.com;

  root /var/www/html;
  index index.html;
}
```

### 2. Reverse Proxy

Forward client requests to backend servers (e.g., Node.js, Django) while hiding the backend details.

```nginx
server {
  listen 80;
  server_name example.com;

  location / {
    proxy_pass http://localhost:3000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
}
```

### 3. Load Balancer

NGINX can distribute traffic across multiple servers using different algorithms.

#### Round Robin Load Balancing

```nginx
upstream backend {
  server backend1.example.com;
  server backend2.example.com;
}

server {
  listen 80;
  server_name example.com;

  location / {
    proxy_pass http://backend;
  }
}
```

#### Least Connections Load Balancing

```nginx
upstream backend {
  least_conn;
  server backend1.example.com;
  server backend2.example.com;
}

server {
  listen 80;
  server_name example.com;

  location / {
    proxy_pass http://backend;
  }
}
```

### 4. SSL/TLS Termination

Terminate HTTPS at NGINX, then forward to internal HTTP services.

```nginx
server {
  listen 443 ssl;
  server_name example.com;

  ssl_certificate /etc/nginx/ssl/example.com.crt;
  ssl_certificate_key /etc/nginx/ssl/example.com.key;

  location / {
    proxy_pass http://localhost:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  }
}
```

Redirect HTTP to HTTPs:

```nginx
server {
  listen 80;
  server_name example.com;
  return 301 https://$host$request_uri;
}
```

### 5. HTTP Caching

Improve performance and reduce backend load using proxy caching.

```nginx
proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=my_cache:10m max_size=1g inactive=60m use_temp_path=off;

server {
  listen 80;
  server_name example.com;

  location /api/ {
    proxy_pass http://api_backend;
    proxy_cache my_cache;
    proxy_cache_valid 200 302 10m;
    proxy_cache_valid 404 1m;
    add_header X-Cache-Status $upstream_cache_status;
  }
}
```

### 6. Mail Proxy

NGINX can act as a proxy for email protocols like SMTP, IMAP, and POP3.

```nginx
mail {
  server {
    listen 587;
    protocol smtp;
    proxy on;
  }

  auth_http localhost:9000/cgi-bin/auth;
  smtp_capabilities "SIZE 10485760" "STARTTLS";
}
```

### 6. Media streaming

NGINX can stream video/audio using modules like RTMP.

```nginx
rtmp {
  server {
    listen 1935;
    chunk_size 4096;

    application live {
      live on;
      record off;
    }
  }
}

http {
  server {
    listen 8080;

    location /stat {
      rtmp_stat all;
      rtmp_stat_stylesheet stat.xsl;
    }

    location /stat.xsl {
      root /usr/local/nginx/html;
    }
  }
}
```
