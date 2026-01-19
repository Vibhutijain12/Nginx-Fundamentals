#### NGINX as a Reverse Proxy

NGINX acts as an intermediary. It accepts a request from a client, forwards it to a "backend" server (like a Node.js, Python, or Java app), receives the response, and sends it back to the client. The client never talks to the backend directly.

NGINX is one of the most popular tools used as a reverse proxy in production.

#### Why Use NGINX as a Reverse Proxy?

* Protect backend services from direct access
* Centralized SSL termination
* Load balancing backend apps
* Path-based routing (/api → backend1, /app → backend2)
* Easy caching and compression

#### Reverse Proxy Configuration (Ubuntu/Linux)

**File:** ```/etc/nginx/sites-available/default```

Update the existing server block or create a new one:

```js
server {
    listen 80;
    server_name localhost;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

#### Breakdown:
* proxy_pass → forwards requests to your backend app
* proxy_set_header → preserves original request metadata (like IP and host)

#### Practical Implementation

#### Step1: Install NodeJS
```js
sudo apt update
sudo apt install nodejs npm -y
```

#### Step2: Create a simple app
```
mkdir backend 
cd backend 
touch server.js
```

```js
const http = require('http');
http.createServer((req, res) => {
  res.end('Hello from Node.js backend!');
}).listen(3000);
```

Run it:
```js
node server.js
```

#### Step3: Configure NGINX as reverse proxy

```js
location / {
    proxy_pass http://localhost:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
}
```
#### Step4: Reload the NGINX: 
```
systemctl reload nginx
```

#### Step5: Test in Browser: 
```
www.localhost:80
```
✅ You should see: Hello from Node.js backend!

<img width="819" height="273" alt="nginx" src="https://github.com/user-attachments/assets/31603349-f80d-4736-8a1a-c7de4b332b92" />
