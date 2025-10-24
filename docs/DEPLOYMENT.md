# Deployment Guide

This guide covers deploying the Linear Programming Calculator to production environments.

## Table of Contents

- [Overview](#overview)
- [Pre-Deployment Checklist](#pre-deployment-checklist)
- [Deployment Options](#deployment-options)
- [Production Configuration](#production-configuration)
- [Security Considerations](#security-considerations)
- [Monitoring and Maintenance](#monitoring-and-maintenance)

## Overview

The Linear Programming Calculator is a Flask web application that can be deployed on various platforms. This guide covers best practices and platform-specific instructions.

**Important**: Never deploy with `debug=True` in production!

## Pre-Deployment Checklist

Before deploying to production:

- [ ] Set `debug=False` in main.py
- [ ] Configure a production WSGI server (Gunicorn, uWSGI)
- [ ] Set up environment variables for sensitive data
- [ ] Configure reverse proxy (nginx, Apache)
- [ ] Enable HTTPS/SSL
- [ ] Set up logging
- [ ] Configure firewall rules
- [ ] Set up backup strategy
- [ ] Test thoroughly in staging environment

## Deployment Options

### Option 1: Heroku (Easiest)

#### Prerequisites
- Heroku account
- Heroku CLI installed

#### Step 1: Prepare Application

Create `Procfile` in project root:
```
web: gunicorn main:app
```

Create `runtime.txt`:
```
python-3.11.0
```

Update `requirements.txt` to include:
```
gunicorn==21.2.0
```

#### Step 2: Deploy

```bash
# Login to Heroku
heroku login

# Create new app
heroku create your-app-name

# Deploy
git push heroku main

# Open application
heroku open
```

### Option 2: PythonAnywhere

#### Step 1: Upload Files

1. Create account at [pythonanywhere.com](https://www.pythonanywhere.com)
2. Upload project files via Files tab
3. Open Bash console

#### Step 2: Setup Virtual Environment

```bash
mkvirtualenv --python=/usr/bin/python3.10 myenv
pip install -r requirements.txt
```

#### Step 3: Configure Web App

1. Go to Web tab
2. Click "Add a new web app"
3. Select Flask
4. Set source code path: `/home/yourusername/linear-programming-project-flask`
5. Set WSGI file to point to your app
6. Reload web app

### Option 3: AWS EC2

#### Step 1: Launch EC2 Instance

1. Launch Ubuntu 22.04 LTS instance
2. Configure security group (ports 80, 443, 22)
3. SSH into instance

#### Step 2: Install Dependencies

```bash
sudo apt update
sudo apt install python3-pip python3-venv nginx

# Clone repository
git clone https://github.com/Sanchochx/linear-programming-project-flask.git
cd linear-programming-project-flask

# Setup virtual environment
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
pip install gunicorn
```

#### Step 3: Configure Gunicorn

Create `gunicorn_config.py`:
```python
bind = "127.0.0.1:8000"
workers = 4
threads = 2
timeout = 60
```

Create systemd service `/etc/systemd/system/lpapp.service`:
```ini
[Unit]
Description=Linear Programming Calculator
After=network.target

[Service]
User=ubuntu
Group=www-data
WorkingDirectory=/home/ubuntu/linear-programming-project-flask
Environment="PATH=/home/ubuntu/linear-programming-project-flask/venv/bin"
ExecStart=/home/ubuntu/linear-programming-project-flask/venv/bin/gunicorn -c gunicorn_config.py main:app

[Install]
WantedBy=multi-user.target
```

Start service:
```bash
sudo systemctl start lpapp
sudo systemctl enable lpapp
```

#### Step 4: Configure Nginx

Create `/etc/nginx/sites-available/lpapp`:
```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }

    location /static {
        alias /home/ubuntu/linear-programming-project-flask/static;
    }
}
```

Enable site:
```bash
sudo ln -s /etc/nginx/sites-available/lpapp /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

### Option 4: DigitalOcean App Platform

1. Connect GitHub repository
2. Select Python as runtime
3. Configure build command: `pip install -r requirements.txt`
4. Configure run command: `gunicorn main:app`
5. Deploy

### Option 5: Google Cloud Platform (Cloud Run)

#### Create Dockerfile

```dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD exec gunicorn --bind :$PORT --workers 1 --threads 8 main:app
```

#### Deploy

```bash
# Build and push to Container Registry
gcloud builds submit --tag gcr.io/PROJECT-ID/lpapp

# Deploy to Cloud Run
gcloud run deploy lpapp \
    --image gcr.io/PROJECT-ID/lpapp \
    --platform managed \
    --region us-central1 \
    --allow-unauthenticated
```

## Production Configuration

### Modify main.py for Production

```python
from flask import Flask, render_template, request, redirect, url_for
from flask_bootstrap import Bootstrap5
import pulp
import os

app = Flask(__name__)
Bootstrap5(app)

# Production configuration
app.config['DEBUG'] = False
app.config['TESTING'] = False

# Use environment variable for secret key
app.secret_key = os.environ.get('SECRET_KEY', 'your-secret-key-here')

# ... rest of your routes ...

if __name__ == '__main__':
    port = int(os.environ.get('PORT', 5000))
    app.run(host='0.0.0.0', port=port, debug=False)
```

### Environment Variables

Create `.env` file (don't commit to git):
```bash
FLASK_APP=main.py
FLASK_ENV=production
SECRET_KEY=your-very-secret-random-key
PORT=5000
```

### Using Gunicorn (Production WSGI Server)

Install:
```bash
pip install gunicorn
```

Run:
```bash
gunicorn -w 4 -b 0.0.0.0:8000 main:app
```

Configuration file `gunicorn_config.py`:
```python
import multiprocessing

# Server socket
bind = "0.0.0.0:8000"
backlog = 2048

# Worker processes
workers = multiprocessing.cpu_count() * 2 + 1
worker_class = 'sync'
worker_connections = 1000
timeout = 30
keepalive = 2

# Logging
accesslog = '/var/log/gunicorn/access.log'
errorlog = '/var/log/gunicorn/error.log'
loglevel = 'info'

# Process naming
proc_name = 'linear_programming_calculator'

# Server mechanics
daemon = False
pidfile = '/var/run/gunicorn.pid'
user = None
group = None
tmp_upload_dir = None
```

## Security Considerations

### 1. HTTPS/SSL

**Using Let's Encrypt with Nginx**:
```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d your-domain.com
```

### 2. Security Headers

Update nginx configuration:
```nginx
add_header X-Frame-Options "SAMEORIGIN" always;
add_header X-Content-Type-Options "nosniff" always;
add_header X-XSS-Protection "1; mode=block" always;
add_header Strict-Transport-Security "max-age=31536000" always;
```

### 3. Rate Limiting

Install Flask-Limiter:
```bash
pip install Flask-Limiter
```

Update main.py:
```python
from flask_limiter import Limiter
from flask_limiter.util import get_remote_address

limiter = Limiter(
    app=app,
    key_func=get_remote_address,
    default_limits=["200 per day", "50 per hour"]
)

@app.route("/calculator", methods=['POST'])
@limiter.limit("10 per minute")
def calculator():
    # ... your code ...
```

### 4. Input Validation

Already implemented in the application with:
- Maximum variable limits (1-100)
- Maximum constraint limits (1-50)
- Type checking and error handling

### 5. Firewall Configuration

```bash
# UFW (Ubuntu)
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
sudo ufw enable
```

## Monitoring and Maintenance

### Logging

Add logging to main.py:
```python
import logging
from logging.handlers import RotatingFileHandler

if not app.debug:
    file_handler = RotatingFileHandler('logs/app.log', maxBytes=10240, backupCount=10)
    file_handler.setFormatter(logging.Formatter(
        '%(asctime)s %(levelname)s: %(message)s [in %(pathname)s:%(lineno)d]'
    ))
    file_handler.setLevel(logging.INFO)
    app.logger.addHandler(file_handler)
    app.logger.setLevel(logging.INFO)
    app.logger.info('Linear Programming Calculator startup')
```

### Health Check Endpoint

Add to main.py:
```python
@app.route('/health')
def health():
    return {'status': 'healthy'}, 200
```

### Monitoring Tools

- **Application monitoring**: New Relic, Datadog, Sentry
- **Server monitoring**: Nagios, Prometheus, Grafana
- **Uptime monitoring**: UptimeRobot, Pingdom

### Backup Strategy

```bash
# Backup script (backup.sh)
#!/bin/bash
DATE=$(date +%Y%m%d_%H%M%S)
BACKUP_DIR="/backups"
SOURCE_DIR="/home/ubuntu/linear-programming-project-flask"

tar -czf $BACKUP_DIR/lpapp_$DATE.tar.gz $SOURCE_DIR

# Keep only last 7 days of backups
find $BACKUP_DIR -name "lpapp_*.tar.gz" -mtime +7 -delete
```

Add to crontab:
```bash
0 2 * * * /path/to/backup.sh
```

### Updating the Application

```bash
# Pull latest changes
git pull origin main

# Activate virtual environment
source venv/bin/activate

# Install any new dependencies
pip install -r requirements.txt

# Restart service
sudo systemctl restart lpapp
```

## Performance Optimization

### 1. Enable Gzip Compression

Nginx configuration:
```nginx
gzip on;
gzip_vary on;
gzip_types text/plain text/css application/json application/javascript text/xml;
```

### 2. Caching Static Files

```nginx
location /static {
    alias /home/ubuntu/linear-programming-project-flask/static;
    expires 1y;
    add_header Cache-Control "public, immutable";
}
```

### 3. Connection Pooling

For database connections (if you add database support later):
```python
from flask_sqlalchemy import SQLAlchemy

app.config['SQLALCHEMY_POOL_SIZE'] = 10
app.config['SQLALCHEMY_POOL_RECYCLE'] = 3600
```

## Troubleshooting Production Issues

### Application won't start
- Check logs: `sudo journalctl -u lpapp -n 50`
- Verify Python dependencies: `pip list`
- Check file permissions

### 502 Bad Gateway
- Ensure Gunicorn is running
- Check Gunicorn logs
- Verify nginx upstream configuration

### High memory usage
- Reduce number of Gunicorn workers
- Monitor with `htop` or `ps aux`
- Check for memory leaks

### Slow response times
- Increase Gunicorn timeout
- Add more workers
- Monitor with application performance tools

## Support

For deployment issues:
- Email: santiagosanchezmarquez@gmail.com
- GitHub Issues: [Report deployment issues](https://github.com/Sanchochx/linear-programming-project-flask/issues)

---

**Deployment Guide Version**: 1.0.0

**Last Updated**: 2024

**Maintained by**: λ-SanchoDev
