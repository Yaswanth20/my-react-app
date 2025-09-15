
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
Navigate to a temporary directory and **clone the repository** and change to that directory:  

```sh
git clone https://github.com/Yaswanth20/my-react-app.git
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

Update the page as you like

---

## **6. Install Dependencies and Build the React App**  
Install required npm dependencies:  

```sh
npm install
```

Build the React application:  

```sh
npm run build
```

This will generate a **`build/`** folder with production-ready static files.

---

## **7. Deploy Build Files to Nginx Web Directory**  
Remove any existing files in the Nginx web directory:  

```sh
sudo rm -rf /var/www/html/*
```

Copy the React **build files** to `/var/www/html/`:  

```sh
sudo cp -r build/* /var/www/html/
```
---

## **8. Enable Nginx server
Start and enable your server:

```sh
sudo systemctl start nginx 
sudo systemctl enable nginx
```
---

## **9. Extra content

**Check to see what port your server is running on:
Navigate back to your main directory
```sh
cd ~
```
check your nginx.conf file using cat
```sh
cat \etc/nginx/nginx.conf
```
and look in the html section for the server and specifically the listen to identify the port. It should be defaultly on 80
```sh
server {
    listen 80;
    listen 443 ssl;
    server_name example.com;
    # ... other configurations
}
```

If its not there, you can also use network utilities with the following command

```sh
sudo ss -nltp | grep nginx
```

Try stopping the nginx server and see what happens.


