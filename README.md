# Bug Tracker – Production Deployment & DevOps

This repository contains a full MERN stack bug tracker application.
The goal of this assignment is to deploy the app to production, implement CI/CD, configure environment variables securely, and set up monitoring.

## MongoDB Production Setup & Environment Variables

- Managed Database: Uses [MongoDB Atlas](https://www.mongodb.com/atlas) for secure, scalable, and reliable cloud database hosting.
- Replica Set: Atlas cluster with at least a 3-node replica set for high availability.
- User Permissions: Database users have minimum privileges (RBAC).
- IP Whitelisting: Only trusted backend servers and CI/CD runners are allowed via Atlas IP Access List.
- Connection Pooling: Mongoose is configured for efficient resource usage.
- Backups: Continuous backups enabled and restore procedures tested.

### Environment Variable Configuration

- Sensitive Data: All secrets (like the MongoDB URI) are stored in environment variables, never hardcoded.
- Local Development: Use a `.env` file (not committed to git) with:
  `
  MONGO_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/<dbname>?retryWrites=true&w=majority
  `
- Production: Environment variables are set securely in the cloud provider’s dashboard (Render, Railway, Heroku, etc.), not in code or `.env` files.
- Backend Usage Example:
  `js
  // Connect to MongoDB using environment variable
  const mongoose = require('mongoose');
  mongoose.connect(process.env.MONGO_URI, {
    useNewUrlParser: true,
    useUnifiedTopology: true
  })
  .then(() => console.log('Connected to MongoDB'))
  .catch(err => console.error('MongoDB connection error:', err));
  `
- Multiple Environments: Separate variables are used for development, staging, and production.

> Tip: See `.env.example` for required environment variables.

## 🌐 Deployment URLs

- Frontend: [YOUR_FRONTEND_URL_HERE](#)
- Backend API: [YOUR_BACKEND_URL_HERE](#)

## 🛠️ CI/CD Pipeline Screenshots

_Add screenshots of your GitHub Actions workflows running tests, builds, and deployments._

## 📈 Monitoring Setup

- Health check endpoints implemented.
- Uptime monitoring configured.
- Error tracking (e.g., Sentry) integrated.
- Performance monitoring enabled via hosting provider dashboards.

## 📝 Deployment & Rollback Documentation

- Deployment automated via GitHub Actions.
- Rollback possible via cloud provider dashboard or redeploying previous commit.
