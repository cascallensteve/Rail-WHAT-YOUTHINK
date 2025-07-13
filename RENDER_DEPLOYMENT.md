# Render Deployment Guide

## Prerequisites
- GitHub repository with your Django code
- Render account (sign up at render.com)

## Deployment Methods

### Method 1: Using render.yaml (Recommended)

1. **Push code to GitHub** (already done)
2. **Go to Render Dashboard**
   - Visit **https://render.com**
   - Sign up/login with GitHub
3. **Deploy via Blueprints**
   - Go to **Blueprints** page
   - Click **New Blueprint Instance**
   - Connect your **What-you-think** repository
   - Give your blueprint a name
   - Click **Apply**

### Method 2: Manual Deployment

1. **Create PostgreSQL Database**
   - In Render Dashboard, create new **PostgreSQL** database
   - Copy the internal database URL

2. **Create Web Service**
   - Click **New Web Service**
   - Connect your Git repository
   - Select **Python 3** as Language

3. **Configure Service Settings**
   - **Build Command:** `./build.sh`
   - **Start Command:** `python -m gunicorn whisperlink_backend.wsgi:application`

4. **Add Environment Variables**
   - `DATABASE_URL`: Paste the database URL
   - `SECRET_KEY`: Click **Generate** for secure key
   - `WEB_CONCURRENCY`: Set to `4`
   - `TOGETHER_API_KEY`: Your Together AI key

## Project Configuration

### Files Created for Render:
- `build.sh` - Build script for dependencies and migrations
- `render.yaml` - Infrastructure as code configuration
- `requirements.txt` - Updated with `dj-database-url`
- `settings.py` - Updated for Render environment

### Key Features:
- Automatic PostgreSQL database provisioning
- Static file serving with WhiteNoise
- Secure secret key generation
- SSL/HTTPS enabled by default
- Custom domain support available

## Post-Deployment

1. **Create Admin User**
   - Use Render Shell: `python manage.py createsuperuser`

2. **Verify Deployment**
   - Check service logs for any errors
   - Test your application functionality

Your Django app will be live at the generated Render URL!
