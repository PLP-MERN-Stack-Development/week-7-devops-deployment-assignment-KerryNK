# MongoDB Production Setup & Environment Variables

## MongoDB Atlas Production Best Practices

- Managed Database:The app uses [MongoDB Atlas](https://www.mongodb.com/atlas) for secure, scalable, and reliable cloud database hosting.
- Replica Set: The Atlas cluster is configured with at least a 3-node replica set for high availability and fault tolerance.
- User Permissions: Database users are created with the minimum privileges required (using Role-Based Access Control).
- IP Whitelisting: Only trusted backend servers and CI/CD runners are allowed to connect via Atlas IP Access List.
- Connection Pooling: Mongoose (or native MongoDB driver) is configured to use connection pooling for efficient resource usage.
- Backups: Continuous backups are enabled in Atlas, and restore procedures are tested regularly.

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
