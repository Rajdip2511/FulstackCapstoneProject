# 🚀 Dealership Full-Stack Application - Public Deployment Guide

## 📋 Overview
This is a complete full-stack dealership application with:
- **Frontend**: React.js served by Django
- **Backend**: Django REST API + Node.js microservices  
- **Database**: MongoDB
- **Containerization**: Docker & Kubernetes ready

## 🌐 Live Demo
**Application URL**: `http://YOUR_CLOUD_IP:8000`

## 🐳 Docker Hub Images
- **Main App**: `rajdipdevops/dealership-app:latest`
- **Node API**: `rajdipdevops/dealership-nodeapi:latest`

## 🚀 Quick Deployment (One-Command)

### Option 1: Docker Compose (Recommended)
```bash
# Clone or download the docker-compose.prod.yml file
curl -o docker-compose.prod.yml https://raw.githubusercontent.com/YOUR_REPO/docker-compose.prod.yml

# Start all services
docker-compose -f docker-compose.prod.yml up -d

# Access the application
# http://localhost:8000 (or your server IP)
```

### Option 2: Individual Docker Run Commands
```bash
# 1. Start MongoDB
docker run -d --name dealership_db --network dealership_net -p 27017:27017 mongo:latest

# 2. Start Node.js API
docker run -d --name dealership_api --network dealership_net -p 3030:3030 rajdipdevops/dealership-nodeapi:latest

# 3. Start Django Web App
docker run -d --name dealership_web --network dealership_net -p 8000:8000 \
  -e backend_url=http://dealership_api:3030 \
  rajdipdevops/dealership-app:latest
```

## 🌍 Cloud Deployment Options

### AWS EC2 / Azure VM / Google Compute Engine
1. **Launch a VM** (Ubuntu 20.04+ recommended)
2. **Install Docker & Docker Compose**:
   ```bash
   sudo apt update
   sudo apt install docker.io docker-compose -y
   sudo systemctl start docker
   sudo usermod -aG docker $USER
   ```
3. **Deploy the application**:
   ```bash
   wget https://raw.githubusercontent.com/YOUR_REPO/docker-compose.prod.yml
   docker-compose -f docker-compose.prod.yml up -d
   ```
4. **Configure Security Group/Firewall**:
   - Open port 8000 (HTTP)
   - Open port 3030 (API)
   - Open port 27017 (MongoDB - optional, for admin access)

### Heroku (Alternative)
```bash
# Install Heroku CLI and login
heroku login

# Create new app
heroku create your-dealership-app

# Deploy using Docker
heroku container:push web --app your-dealership-app
heroku container:release web --app your-dealership-app
```

## 🔧 Environment Configuration

### Required Environment Variables
```bash
backend_url=http://api:3030
sentiment_analyzer_url=http://localhost:5050/
ALLOWED_HOSTS=*
DEBUG=False  # For production
```

## 📱 Application Features
- ✅ User Registration & Authentication
- ✅ Dealer Listings with Search
- ✅ Dealer Reviews with Sentiment Analysis
- ✅ Car Inventory Management
- ✅ Responsive Design
- ✅ Admin Panel

## 🔗 API Endpoints
- **GET** `/djangoapp/get_dealers/` - Get all dealers
- **GET** `/djangoapp/dealer/{id}` - Get dealer details
- **GET** `/djangoapp/reviews/dealer/{id}` - Get dealer reviews
- **POST** `/djangoapp/add_review` - Add new review
- **GET** `/djangoapp/get_cars` - Get car models

## 🧪 Testing Endpoints
```bash
# Test API connectivity
curl http://YOUR_IP:8000/djangoapp/get_dealers/

# Test Node.js API directly
curl http://YOUR_IP:3030/fetchDealers
```

## 📊 Monitoring & Logs
```bash
# View container logs
docker-compose -f docker-compose.prod.yml logs -f

# Check container status
docker-compose -f docker-compose.prod.yml ps
```

## 🛠️ Troubleshooting

### Common Issues:
1. **Port conflicts**: Change ports in docker-compose.prod.yml
2. **Network issues**: Ensure all containers are on the same network
3. **Database connection**: Verify MongoDB is running and accessible

### Debug Commands:
```bash
# Check running containers
docker ps

# Inspect network
docker network ls
docker network inspect dealership_network

# Container logs
docker logs dealership_web
docker logs dealership_api
docker logs dealership_db
```

## 📞 Support
Created by: **Rajdip** (DevOps Engineer)
Docker Hub: https://hub.docker.com/u/rajdipdevops

---
**🎉 Ready to deploy? Run the docker-compose command and share your public URL!** 