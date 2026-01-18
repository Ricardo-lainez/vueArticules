# PLOS Articles Application - Deployment Guide

## 🚀 Deployment to Render

This application consists of two services:
- **Backend**: Node.js/Express API
- **Frontend**: Vue.js Static Site

### Prerequisites
- Git repository (GitHub, GitLab, or Bitbucket)
- Render account (free tier available at https://render.com)

### Environment Variables

#### Backend (.env)
```
PORT=3000
PLOS_API_URL=https://api.plos.org/search
CORS_ORIGIN=*
NODE_ENV=production
```

#### Frontend (.env)
```
VITE_API_URL=https://your-backend-url.onrender.com/api
```

### Deployment Steps

1. **Push to Git Repository**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

2. **Create Render Account**
   - Go to https://render.com
   - Sign up with GitHub/GitLab/Bitbucket

3. **Deploy Backend**
   - Click "New +" → "Web Service"
   - Connect your repository
   - Configure:
     - Name: `plos-articles-backend`
     - Environment: `Node`
     - Region: `Oregon (US West)`
     - Branch: `main`
     - Root Directory: `backend`
     - Build Command: `npm install`
     - Start Command: `npm start`
   - Add Environment Variables (see above)
   - Click "Create Web Service"

4. **Deploy Frontend**
   - Click "New +" → "Static Site"
   - Connect your repository
   - Configure:
     - Name: `plos-articles-frontend`
     - Branch: `main`
     - Root Directory: `frontend`
     - Build Command: `npm install && npm run build`
     - Publish Directory: `dist`
   - Add Environment Variable:
     - `VITE_API_URL`: Use your backend URL from step 3
   - Click "Create Static Site"

### Post-Deployment

1. Update backend CORS_ORIGIN with your frontend URL
2. Test all endpoints
3. Verify PDF export functionality

### Local Development

Backend:
```bash
cd backend
npm install
npm run dev
```

Frontend:
```bash
cd frontend
npm install
npm run dev
```

## 📝 Notes

- Free tier services may spin down after inactivity
- First request after inactivity may take 30-60 seconds
- Backend URL will be: `https://plos-articles-backend.onrender.com`
- Frontend URL will be: `https://plos-articles-frontend.onrender.com`
