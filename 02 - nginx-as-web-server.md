### NGINX As a Web server

* NGINX directly handles client requests by serving static files (HTML, CSS, JS, Images) from the local disk. 
* It is extremely fast because it uses an event-driven model rather than creating a new process for every request.

#### Practical Implementation

#### Scenario A: Serving a Static Website (Web Server)

**1.** Create your site folder:
```shell
cd /var/www/html 
```
**2.** Add an index file:
```shell
touch index.html
```
```shell
echo "<h1>Hello World</h1>"
```
**3.** Configure NGINX: Create a file at:
```shell 
/etc/nginx/sites-available/default
```
```
server {
    listen 80;
    server_name localhost;
    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

#### Breakdown:

* listen 80; → Listens on HTTP port 80
* server_name localhost; → Domain or IP to respond to
* root → Path where NGINX looks for files
* index → Default file to serve (usually index.html)
* location / → URL path handling

**4.** Reload NGINX:
```shell
systemctl reload nginx
```

**5.** Test: Visit: http://localhost or your server’s IP in browser.

**6.** Common Errors & Fixes:

* 502 Bad Gateway: NGINX is working, but it can't connect to the backend app.
 
**Fix:** Check if your app (Node/Python/Docker) is actually running: 
```
systemctl status my-app 
```

* 403 Forbidden: NGINX doesn't have permission to read the files or the directory index is missing.

**Fix:** Check file permissions and ensure index.html exists. 
```
sudo chmod -R 755 /var/www/html
```

* 504 Gateway Timeout: The backend took too long to respond.

**Fix:** Increase timeout in the location block
```
proxy_read_timeout 300;
```

* Configuration Test Failed: There is a typo in your .conf file.

**Fix:** Always run sudo **nginx -t** before restarting. It will tell you the exact line number of the error.
