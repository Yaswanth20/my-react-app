
# **Deploy a React Application on Amazon EC2 Ubuntu VM with Nginx**

This guide provides step-by-step instructions to deploy and run a **This React application** on an **Ubuntu VM** using **Nginx**, making it accessible from a **public IP**.

---

## **1. Launch EC2 on Amazon AWS
Launch an EC2 instance on Amazon. Select the ubuntu VM and in **Security Groups** make sure to allow HTTP and SSH. Create a key pair using pem and save it.

## **2. Connect to EC2
Navigate back to your instances and select the EC2 instance and hit connect. Navigate to SSH and follow the instructions on your command shell

## **3. Install Node.js and npm**  
Since a React application requires both **Node.js** and **npm**, install them first:  

```sh
sudo apt update
sudo apt install -y nodejs npm
```

To verify the installation:  

```sh
node -v
npm -v
```

---

## **4. Install Nginx**  
Update package lists and install **Nginx**:  

```sh
sudo apt install -y nginx
```

Start and enable Nginx:  

```sh
sudo systemctl start nginx
sudo systemctl enable nginx
```
To stop an Nginx server use:

```sh
sudo systemctl stop nginx
```

Check Nginx status:  

```sh
systemctl status nginx
```

---

## **5. Clone the React Application from GitHub**  
Navigate to a temporary directory and **clone the repository**:  

```sh
git clone https://github.com/pravinmishraaws/my-react-app.git
cd my-react-app
```

**Open the App.js file**

Navigate to your React app’s source folder:

```sh
cd my-react-app/src
```

Open the App.js file in a text editor:

```sh
nano App.js
```
(or use vi/vim if you prefer)

Modify the content

```sh
<h2>Deployed by: <strong>Your Full Name</strong></h2>
<p>Date: <strong>DD/MM/YYYY</strong></p>
```

Update your details like: Your Full Name & Date

---

## **4. Install Dependencies and Build the React App**  
Install required dependencies:  

```sh
npm install
```

Build the React application:  

```sh
npm run build
```

This will generate a **`build/`** folder with production-ready static files.

---

## **5. Deploy Build Files to Nginx Web Directory**  
Remove any existing files in the Nginx web directory:  

```sh
sudo rm -rf /var/www/html/*
```

Copy the React **build files** to `/var/www/html/`:  

```sh
sudo cp -r build/* /var/www/html/
```

Set proper permissions:  

```sh
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```

---

## **6. Configure Nginx for React**  
Nginx configuration file:   

```
echo 'server {
    listen 80;
    server_name _;
    root /var/www/html;
    index index.html;
    
    location / {
        try_files $uri /index.html;
    }

    error_page 404 /index.html;
}' | sudo tee /etc/nginx/sites-available/default > /dev/null

```

Restart Nginx to apply the changes:  

```sh
sudo systemctl restart nginx
```

---

## **7. Find Your Public IP and Access the Application**  
Retrieve the **public IP** of your Ubuntu VM:  

```sh
curl ifconfig.me
```

Now, students can **access the React application** in a browser using:  

```
http://<your-public-ip>
```

For example, if the public IP is **203.0.113.25**, visit:  

```
http://203.0.113.25
```

---

## **8. Verify the Deployment**  
Ensure Nginx is correctly serving the React app:  

```sh
curl <your-public-ip>
```

If successful, your **React app is live!**  

---

## **Your React App is Now Live on Ubuntu with Nginx!**  
Now your **React application** is deployed on an **Ubuntu VM with Nginx**, accessible from a **public IP**. 
