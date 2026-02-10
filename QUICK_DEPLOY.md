# 🚀 Quick Deployment Steps

Follow these steps to deploy your full-stack application:

## 1. Database - MongoDB Atlas (5 minutes)
1. Sign up at https://www.mongodb.com/cloud/atlas/register
2. Create a free M0 cluster
3. Create database user (save username & password)
4. Allow network access from anywhere (0.0.0.0/0)
5. Get connection string:
   ```
   mongodb+srv://username:password@cluster.xxxxx.mongodb.net/scalable-web
   ```

## 2. Backend - Render.com (10 minutes)
1. Sign up at https://render.com with GitHub
2. New Web Service → Connect repository
3. Settings:
   - Root Directory: `backend`
   - Build: `npm install`
   - Start: `npm start`
4. Environment Variables:
   ```
   NODE_ENV=production
   MONGODB_URI=<your-mongodb-connection-string>
   JWT_SECRET=<generate-random-32-char-string>
   JWT_EXPIRE=7d
   PORT=5000
   CLIENT_URL=https://amitdayma0011.github.io
   ```
5. Deploy → Copy your backend URL (e.g., `https://scalable-web-api.onrender.com`)

## 3. Frontend - GitHub Pages (Already done! ✅)
1. Update `.env.production` with your Render backend URL:
   ```
   VITE_API_URL=https://your-backend-name.onrender.com/api
   ```
2. Rebuild and deploy:
   ```bash
   cd frontend
   npm run build
   cd ..
   git add .
   git commit -m "Update production API URL"
   git push origin main
   git subtree push --prefix frontend/dist origin gh-pages
   ```

## 4. Test Your App
Visit: https://amitdayma0011.github.io/scalable-web/

- Sign up for an account
- Log in
- Create a task
- Test file uploads
- Verify everything works!

---

## 📋 Environment Variables Checklist

### Backend (.env on Render)
- [ ] NODE_ENV=production
- [ ] MONGODB_URI=(from Atlas)
- [ ] JWT_SECRET=(random string)
- [ ] JWT_EXPIRE=7d
- [ ] PORT=5000
- [ ] CLIENT_URL=https://amitdayma0011.github.io

### Frontend (.env.production)
- [ ] VITE_API_URL=(your Render backend URL)

---

## 🔄 Update Workflow

### Update Backend:
```bash
git add backend/
git commit -m "Update backend"
git push origin main
# Render auto-deploys
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

## 📊 Your Live URLs

- **Frontend**: https://amitdayma0011.github.io/scalable-web/
- **Backend**: https://your-app.onrender.com
- **Database**: MongoDB Atlas

---

Need help? Check [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md) for detailed instructions.
