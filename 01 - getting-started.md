### ✅ NGINX Overview and Usage Guide

#### 1. What is NGINX and Why Use It?

NGINX is a high-performance, open-source web server, reverse proxy, load balancer, and HTTP cache. It is designed to handle a large number of concurrent connections efficiently with low memory and CPU usage.

#### Why use NGINX?

NGINX is widely adopted in modern infrastructure because it:

* Handles high concurrency using an event-driven, asynchronous architecture.
* Performs extremely well as a reverse proxy and load balancer.
* Is lightweight and resource-efficient.
* Scales reliably under heavy traffic.
* Integrates cleanly with containerized and cloud-native environments. 

NGINX is commonly used in front of application servers (Node.js, Java, Python, PHP, etc.) to manage traffic, security, and performance.

#### 2. Commands to Install NGINX

#### Ubuntu / Debian
```shell
sudo apt update
sudo apt-get install nginx 
```

#### Start and Enable NGINX
```shell
sudo systemctl start nginx
sudo systemctl enable nginx
```

#### Verify Installation
```shell 
nginx -v
systemctl status nginx
```

#### 3. Apache vs NGINX

| Feature         | Apache                        | NGINX                            |
| --------------- | ----------------------------- | -------------------------------- |
| Architecture    | Process-based / Thread-based  | Event-driven, asynchronous       |
| Performance     | Slower under high concurrency | Excellent under high concurrency |
| Memory Usage    | Higher per connection         | Low and predictable              |
| Static Content  | Good                          | Excellent                        |
| Dynamic Content | Native (mod_php)              | Uses external processors         |
| Configuration   | `.htaccess` supported         | Centralized config only          |
| Reverse Proxy   | Available                     | Core strength                    |
| Load Balancing  | Supported                     | Highly optimized                 |

#### Summary

* Apache is flexible and beginner-friendly, especially for shared hosting.
* NGINX excels in performance, scalability, and modern production environments.

#### 4. Common Use Cases of NGINX

#### Reverse Proxy

* Routes incoming traffic to backend services
* Hides internal architecture from external users

#### Load Balancer

* Distributes traffic across multiple application servers
* Supports round-robin, least-connections, and IP-hash strategies

#### Web Server

* Serves static files (HTML, CSS, JS, images) efficiently
* Commonly used with CDNs

#### SSL/TLS Termination

* Handles HTTPS traffic
* Offloads encryption from application servers

#### API Gateway

* Rate limiting
* Authentication
* Request routing and rewriting

#### Container & Cloud Environments

* Frontend for Docker and Kubernetes services
* Common Ingress controller for Kubernetes
