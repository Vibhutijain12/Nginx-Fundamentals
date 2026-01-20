#### NGINX as a Load balancer 

In a DevOps infrastructure, NGINX acts as a Load Balancer by sitting between the internet and a "cluster" of backend servers. Its job is to distribute incoming traffic across these servers to ensure no single server is overwhelmed, providing both **high availability** and **redundancy**.

#### 1. Why Use NGINX for Load Balancing?
* Scalability: Easily add or remove backend servers as your traffic grows.

* High Availability: If one backend server fails, NGINX detects the failure and automatically redirects traffic to the healthy servers.

* Performance: It can distribute traffic based on server capacity, ensuring optimal resource utilization.

#### 2. Load Balancing Methods (Algorithms)

**1.** round-robin: Default — rotates through all backends equally

**2.** least_conn: Sends traffic to the backend with the fewest active connections

**3.** ip_hash:	Uses client IP to consistently route requests to the same backend

#### 3. Practical Configuration

To set up a load balancer, you use the upstream directive in your configuration file.

```js
# Define the cluster of servers
upstream backend_app {
    server 10.0.0.1:3001;
    server 10.0.0.2:3002;
}

server {
    listen 80;
    server_name localhost;

    location / {
        # Pass the traffic to the upstream cluster
        proxy_pass http://backend_app;
    }
}
```
#### Demo: Load Balance Two Local Backend Servers

#### Step1: Create Backend Servers

```
mkdir load-test
cd load-test
```

#### server1.js

```js 
require('http').createServer((req, res) => {
  res.end('Response from Server 1');
}).listen(3001);
```
#### server2.js

```js
require('http').createServer((req, res) => {
  res.end('Response from Server 2');
}).listen(3002);
```

#### Step2: Run both the servers

```js
node server1.js
node server2.js
```

#### Step3: Reload the NGINX
```
sudo nginx -t
sudo systemctl reload nginx
```

#### Step4: Test the Load Balancer
```
curl http://localhost
```

Run it multiple times — you should see the response alternate between:
<img width="416" height="224" alt="image" src="https://github.com/user-attachments/assets/c82bb48a-d6f1-4dfb-9303-8c139ce723f7" />
<img width="534" height="238" alt="image" src="https://github.com/user-attachments/assets/5a5e35c8-e41a-4aa7-a1d2-29b77acac019" />

