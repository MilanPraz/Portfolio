---
title: 'Deploy Your App on a VPS in Just 5 Steps'
description: 'A simple, repeatable guide to deploying your app on a VPS using Git, PM2, and Nginx — perfect for modern Node.js and Astro-based projects.'
pubDate: 'Jan 01 2026'
heroImage: '../../assets/blog-placeholder-3.jpg'
readTime: '5 min'
tags: ['deployment', 'vps', 'nginx', 'pm2', 'devops']
---

Deploying an app on a VPS often feels intimidating at first — SSH access, Linux commands, server configs, and reverse proxies can look overwhelming. But once your VPS is prepared, deployment becomes a **simple and repeatable workflow**.

In this article, I'll show you **how to deploy your app on a VPS in just 5 steps** using **Git, PM2, and Nginx**. This approach works perfectly for **Astro apps, Node.js APIs, Next.js, and other modern web projects**.

## Why Deploy on a VPS?

Using a VPS gives you:

- Full control over your server
- Better performance than shared hosting
- Freedom to run any stack you want
- Host multiple projects on one server

## Prerequisites

Ensure your VPS has:

- Node.js installed
- PM2 installed (`npm install -g pm2`)
- Nginx installed
- A domain pointing to your VPS IP

## Step 1: Clone Your Project from Git

SSH into your VPS and clone your project:

```bash
ssh user@your-vps-ip
cd /var/www
git clone https://github.com/your-org/your-project.git
cd your-project
```

For private repositories, use SSH cloning instead.

## Step 2: Setup Environment Variables and Install Dependencies

Most apps require environment variables (ports, database URLs, secrets).

```bash
cp .env.example .env
nano .env
```

Example:

```
NODE_ENV=production
PORT=3000
DATABASE_URL=your_db_url
```

Save and exit.

Install dependencies and build the project:

```bash
npm install
npm run build
```

**Don't skip the build step** — production apps should never run unbuilt source code.

## Step 3: Run the App with PM2 (Using an Ecosystem File)

While PM2 allows you to start apps with a single command, the recommended production approach is to use an ecosystem configuration file. This keeps your deployment clean, reproducible, and version-controlled.

### Create `ecosystem.config.js`

Inside your project root, create the file:

```bash
nano ecosystem.config.js
```

### Add the Configuration

Add the following configuration to the file:

```javascript
module.exports = {
  apps: [
    {
      name: 'my-app',
      script: 'npm',
      args: 'start',
      cwd: '/var/www/your-project',
      env: {
        NODE_ENV: 'production',
        PORT: 3000,
      },
    },
  ],
};
```

This file tells PM2:

- What command to run
- Where the app lives
- Which environment variables to use
- How to identify the process

#### Start the App with PM2

Run:

```
pm2 start ecosystem.config.js
```

#### Monitor the App

You can check status and logs anytime:

```
pm2 list
pm2 logs my-app
```

At this point, your app is running in the background and ready to be exposed via Nginx.

## Step 4: Expose the App Using Nginx

Create an Nginx config to route traffic from your domain to the app.

```
sudo nano /etc/nginx/sites-available/my-app
```

Paste this:

```
server {
    listen 80;
    server_name example.com www.example.com;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

Enable and reload:

```
sudo ln -s /etc/nginx/sites-available/my-app /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

🎉 Your app is now live!

## Step 5: Secure Your App with SSL (HTTPS)

Running your app over HTTPS is no longer optional — it improves security, SEO, and user trust.
The easiest way to enable SSL on a VPS is using Certbot with Nginx.

Install Certbot

```
sudo apt update
sudo apt install certbot python3-certbot-nginx -y
```

Generate an SSL Certificate

Replace the domain names with your own:

```
sudo certbot --nginx -d example.com -d www.example.com
```

Certbot will:

- verify your domain
- automatically update your Nginx config
- enable HTTPS

Once completed, your site will be accessible at:

***https://example.com***

## BONUS: Updating Your App Later

After deployment, updating your app is straightforward:

```
git pull origin main
npm install
npm run build
pm2 restart my-app
```

This workflow stays the same for every update.
