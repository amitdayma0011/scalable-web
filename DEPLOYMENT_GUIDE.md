# 🚀 Full-Stack Deployment Guide

This guide will help you deploy your full application with Frontend + Backend + Database all connected.

## Architecture Overview

- **Frontend**: GitHub Pages (Static React App)
- **Backend**: Render.com (Free Node.js API)
- **Database**: MongoDB Atlas (Free Cloud Database)

---

## Step 1: Set Up MongoDB Atlas (Database)

### 1.1 Create MongoDB Atlas Account
1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas/register)
2. Sign up for a free account
3. Click "Create" to create a new cluster

### 1.2 Configure Database
1. Choose **M0 Free** tier
2. Select a cloud provider (AWS/Google/Azure) and region closest to you
3. Click "Create Cluster" (takes 3-5 minutes)

### 1.3 Create Database User
1. Click "Database Access" in left sidebar
2. Click "Add New Database User"
3. Choose "Password" authentication
4. Username: `adminUser` (or your choice)
5. Password: Generate a secure password (save it!)
6. Database User Privileges: "Read and write to any database"
7. Click "Add User"

### 1.4 Configure Network Access
1. Click "Network Access" in left sidebar
2. Click "Add IP Address"
3. Click "Allow Access from Anywhere" (0.0.0.0/0)
4. Click "Confirm"

### 1.5 Get Connection String
1. Click "Database" in left sidebar
2. Click "Connect" on your cluster
3. Choose "Connect your application"
4. Copy the connection string (looks like):
   ```
   mongodb+srv://adminUser:<password>@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority
   ```
5. Replace `<password>` with your actual password
6. Add database name after `.net/`: `scalable-web`
   ```
   mongodb+srv://adminUser:yourpassword@cluster0.xxxxx.mongodb.net/scalable-web?retryWrites=true&w=majority
   ```

---

## Step 2: Deploy Backend to Render

### 2.1 Create Render Account
1. Go to [Render.com](https://render.com/)
2. Sign up using your GitHub account (easiest)

### 2.2 Create New Web Service
1. Click "New +" → "Web Service"
2. Connect your GitHub repository: `amitdayma0011/scalable-web`
3. Configure the service:
   - **Name**: `scalable-web-api`
   - **Region**: Choose closest to you
   - **Branch**: `main`
   - **Root Directory**: `backend`
   - **Environment**: `Node`
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Instance Type**: Free

### 2.3 Add Environment Variables
Click "Advanced" → "Add Environment Variable" and add these:

| Key | Value |
|-----|-------|
| `NODE_ENV` | `production` |
| `MONGODB_URI` | Your MongoDB Atlas connection string from Step 1.5 |
| `JWT_SECRET` | Generate a random 32+ character string |
| `JWT_EXPIRE` | `7d` |
| `PORT` | `5000` |
| `CLIENT_URL` | `https://amitdayma0011.github.io` |

**Generate JWT_SECRET:**
```bash
# Run in terminal to generate random string
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

### 2.4 Deploy
1. Click "Create Web Service"
2. Wait for deployment (5-10 minutes)
3. Your backend will be live at: `https://scalable-web-api.onrender.com`
4. **Save this URL!** You'll need it for the frontend

### 2.5 Test Backend
Visit: `https://scalable-web-api.onrender.com/api/auth/signup` - should return an error (it's working!)

---

## Step 3: Update Frontend Configuration

### 3.1 Update API URL in Frontend
1. Create production environment file

### 3.2 Update Backend CORS
The backend needs to allow requests from your GitHub Pages URL.

---

## Step 4: Redeploy Frontend

After updating the API URL:

```bash
cd frontend
npm run build
cd ..
git add .
git commit -m "Update API URL for production deployment"
git push origin main
git subtree push --prefix frontend/dist origin gh-pages
```

---

## Step 5: Testing Your Deployment

1. **Frontend**: https://amitdayma0011.github.io/scalable-web/
2. **Backend**: https://your-app-name.onrender.com/api
3. **Database**: MongoDB Atlas (connected to backend)

### Test the Full Flow:
1. Open your frontend URL
2. Click "Sign Up"
3. Create a new account
4. Log in
5. Create a task
6. Verify data persistence

---

## 🔧 Troubleshooting

### Backend Logs (Render)
1. Go to Render dashboard
2. Click your service
3. Click "Logs" to see real-time output

### CORS Errors
Make sure backend CORS is configured with your GitHub Pages URL:
```javascript
app.use(
  cors({
    origin: process.env.CLIENT_URL || 'http://localhost:5173',
    credentials: true,
  })
);
```

### MongoDB Connection Errors
- Verify connection string format
- Check database user password
- Ensure network access allows 0.0.0.0/0

### Render Free Tier Notes
- Service spins down after 15 minutes of inactivity
- First request after sleep takes 30-50 seconds
- Upgrade to paid tier ($7/month) for always-on service

---

## 🔄 Future Updates

### Update Backend:
```bash
git add .
git commit -m "Update backend"
git push origin main
# Render auto-deploys from GitHub
```

### Update Frontend:
```bash
cd frontend
npm run build
cd ..
git add frontend/dist -f
git commit -m "Update frontend"
git subtree push --prefix frontend/dist origin gh-pages
```

---

## 📊 Monitoring

### Render Dashboard
- View deployment logs
- Monitor service health
- Check resource usage

### MongoDB Atlas Dashboard
- View database size
- Monitor connections
- Check query performance

---

## 🎉 Your Application is Now Live!

- ✅ Frontend hosted on GitHub Pages
- ✅ Backend API on Render
- ✅ Database on MongoDB Atlas
- ✅ All connected and working!

**Share your app:** `https://amitdayma0011.github.io/scalable-web/`
