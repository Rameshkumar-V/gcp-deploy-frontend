# 🚀 Beginner-Friendly Guide: Host Your GitHub Frontend on a Google Cloud VM

This guide helps you host your frontend website from GitHub on a Google Cloud Ubuntu VM using **Nginx**.

You can copy and paste each command directly into your VM terminal.

---

# 📌 Before You Start

Make sure you already have:

- A Google Cloud VM running Ubuntu
- SSH access to the VM
- Your frontend code pushed to GitHub
- A static IP attached to your VM

---

# 1️⃣ Connect to Your VM

Open your VM using SSH from Google Cloud Console.

---

# 2️⃣ Update the Server and Install Required Software

Install:

- `git` → to download your code from GitHub
- `nginx` → web server to host your site

Run this command:

```bash
sudo apt update
sudo apt install -y git nginx
```

---

# 3️⃣ Remove Default Nginx Website Files

Nginx comes with a default webpage. Remove it first.

```bash
sudo rm -rf /var/www/html/*
```

---

# 4️⃣ Download Your GitHub Repository

Replace:

```text
[YOUR_REPO_URL]
```

with your GitHub repository URL.

Example:

```text
https://github.com/username/my-project.git
```

Now run:

```bash
cd ~

git clone [YOUR_REPO_URL] my-website

cd my-website
```

---

# 5️⃣ Switch to the Correct Branch

If your frontend is inside the `gh-pages` branch, run:

```bash
git checkout gh-pages
```

If your project uses the `main` branch instead, skip this step.

---

# 6️⃣ Create Required Website Folder Structure

Some frontend projects expect files to exist inside a subfolder.

This step fixes CSS and JavaScript loading issues.

Run:

```bash
sudo mkdir -p /var/www/html/web-mindhatch-ai-frontend
```

---

# 7️⃣ Copy Website Files to Nginx Folder

Copy your frontend files into the web server directory.

```bash
sudo cp -r * /var/www/html/web-mindhatch-ai-frontend/

sudo cp -r * /var/www/html/
```

---

# 8️⃣ Set Correct File Permissions

Allow Nginx to access your website files.

```bash
sudo chown -R www-data:www-data /var/www/html

sudo chmod -R 755 /var/www/html
```

---

# 9️⃣ Restart Nginx

Apply all changes.

```bash
sudo systemctl restart nginx
```

---

# 🔟 Open Your Website

Open your browser and visit your VM static IP address:

```text
http://ip
```

Replace this IP with your own VM IP if different.

---

# 🔄 How to Update Your Website Later

Whenever you push new code to GitHub:

## Step 1 — Open Your Project Folder

```bash
cd ~/my-website
```

---

## Step 2 — Pull Latest Code

```bash
git pull origin gh-pages
```

If you use the `main` branch:

```bash
git pull origin main
```

---

## Step 3 — Copy Updated Files

```bash
sudo cp -r * /var/www/html/web-mindhatch-ai-frontend/

sudo cp -r * /var/www/html/
```

---

## Step 4 — Restart Nginx

```bash
sudo systemctl restart nginx
```

---

# ✅ Useful Commands

## Check Nginx Status

```bash
sudo systemctl status nginx
```

---

## Restart Nginx

```bash
sudo systemctl restart nginx
```

---

## Stop Nginx

```bash
sudo systemctl stop nginx
```

---

## Start Nginx

```bash
sudo systemctl start nginx
```

---

# ⚠️ Common Problems

## Website Not Opening

Make sure:

- VM is running
- Firewall allows HTTP traffic
- Nginx is running

Enable HTTP traffic in Google Cloud:

```text
VM Instance → Edit → Allow HTTP Traffic
```

---

## CSS or JS Not Loading

Usually caused by incorrect asset paths.

The folder setup step (`web-mindhatch-ai-frontend`) fixes this for most projects.

---

# 🎉 Done!

Your frontend website is now hosted on your Google Cloud VM using Nginx.
