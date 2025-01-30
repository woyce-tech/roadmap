## Phase 3: Back-End Development (2-3 Months)
### Goal: Master server-side programming, databases, and API development

1. **Node.js Fundamentals (2 weeks)**
   - **Node.js Basics**
     - Event Loop and Asynchronous Programming
     - Modules and require/import
     - File System Operations
     - Streams and Buffers
     - Error Handling
     - CommonJS vs ES Modules
     - **Code Sample:**
       ```javascript
       // Importing modules
       const fs = require('fs');
       const path = require('path');

       // Asynchronous file read with error handling
       fs.readFile(path.join(__dirname, 'example.txt'), 'utf8', (err, data) => {
         if (err) {
           console.error('Error reading file:', err);
           return;
         }
         console.log('File content:', data);
       });

       // Using Promises for better readability
       const readFileAsync = (filePath) => {
         return new Promise((resolve, reject) => {
           fs.readFile(filePath, 'utf8', (err, data) => {
             if (err) {
               reject(err);
             } else {
               resolve(data);
             }
           });
         });
       };

       readFileAsync(path.join(__dirname, 'example.txt'))
         .then(data => console.log('File content:', data))
         .catch(err => console.error('Error reading file:', err));

       // Using async/await for even cleaner code
       const readFile = async (filePath) => {
         try {
           const data = await readFileAsync(filePath);
           console.log('File content:', data);
         } catch (err) {
           console.error('Error reading file:', err);
         }
       };

       readFile(path.join(__dirname, 'example.txt'));
       ```

   - **NPM (Node Package Manager)**
     - Package.json management
     - Dependencies vs DevDependencies
     - Script commands
     - Version control
     - Publishing packages
     - **Code Sample:**
       ```json
       // package.json example
       {
         "name": "example-project",
         "version": "1.0.0",
         "description": "An example project to demonstrate Node.js best practices",
         "main": "index.js",
         "scripts": {
           "start": "node index.js",
           "test": "echo \"Error: no test specified\" && exit 1"
         },
         "dependencies": {
           "express": "^4.17.1"
         },
         "devDependencies": {
           "nodemon": "^2.0.7"
         },
         "author": "Your Name",
         "license": "ISC"
       }
       ```

   - **Core Modules**
     - http/https
     - fs (File System)
     - path
     - os
     - events
     - util
     - **Code Sample:**
       ```javascript
       const http = require('http');

       const server = http.createServer((req, res) => {
         res.statusCode = 200;
         res.setHeader('Content-Type', 'text/plain');
         res.end('Hello, World!\n');
       });

       const PORT = process.env.PORT || 3000;
       server.listen(PORT, () => {
         console.log(`Server running at http://localhost:${PORT}/`);
       });
       ```

   - **Resources:**
     - Node.js Official Documentation
     - Node.js Design Patterns Book
     - NodeSchool.io tutorials

2. **Express.js Framework (3 weeks)**
   - **Express Basics**
     - Application Setup
     - Routing
     - Middleware concept
     - Static files
     - Template engines
     - **Code Sample:**
       ```javascript
       const express = require('express');
       const app = express();
       const path = require('path');
       const morgan = require('morgan');

       // Middleware
       app.use(morgan('dev')); // Logging
       app.use(express.json()); // Parse JSON bodies
       app.use(express.urlencoded({ extended: true })); // Parse URL-encoded bodies

       // Static files
       app.use(express.static(path.join(__dirname, 'public')));

       // Routes
       app.get('/', (req, res) => {
         res.send('Hello, World!');
       });

       app.get('/users/:id', (req, res) => {
         const userId = req.params.id;
         res.send(`User ID: ${userId}`);
       });

       // Error handling middleware
       app.use((err, req, res, next) => {
         console.error(err.stack);
         res.status(500).send('Something broke!');
       });

       const PORT = process.env.PORT || 3000;
       app.listen(PORT, () => {
         console.log(`Server is running on port ${PORT}`);
       });
       ```

   - **Request Handling**
     - Route parameters
     - Query strings
     - Request body parsing
     - File uploads
     - Headers and cookies
     - **Code Sample:**
       ```javascript
       // Route parameters
       app.get('/users/:id', (req, res) => {
         const userId = req.params.id;
         res.send(`User ID: ${userId}`);
       });

       // Query strings
       app.get('/search', (req, res) => {
         const query = req.query.q;
         res.send(`Search query: ${query}`);
       });

       // Request body parsing
       app.post('/submit', (req, res) => {
         const { name, email } = req.body;
         res.send(`Name: ${name}, Email: ${email}`);
       });

       // File uploads
       const multer = require('multer');
       const upload = multer({ dest: 'uploads/' });
       app.post('/upload', upload.single('file'), (req, res) => {
         res.send(`File uploaded: ${req.file.originalname}`);
       });

       // Headers and cookies
       app.get('/headers', (req, res) => {
         res.set('Custom-Header', 'value');
         res.cookie('name', 'value');
         res.send('Headers and cookies set');
       });
       ```

   - **Middleware Development**
     - Custom middleware
     - Error handling middleware
     - Third-party middleware
     - Validation middleware
     - Authentication middleware
     - **Code Sample:**
       ```javascript
       // Custom middleware
       app.use((req, res, next) => {
         console.log(`${req.method} ${req.url}`);
         next();
       });

       // Error handling middleware
       app.use((err, req, res, next) => {
         console.error(err.stack);
         res.status(500).send('Something broke!');
       });

       // Third-party middleware
       const helmet = require('helmet');
       app.use(helmet());

       // Validation middleware
       const { body, validationResult } = require('express-validator');
       app.post('/register', [
         body('email').isEmail(),
         body('password').isLength({ min: 6 })
       ], (req, res) => {
         const errors = validationResult(req);
         if (!errors.isEmpty()) {
           return res.status(400).json({ errors: errors.array() });
         }
         res.send('User registered');
       });

       // Authentication middleware
       const passport = require('passport');
       app.use(passport.initialize());
       app.post('/login', passport.authenticate('local', { session: false }), (req, res) => {
         res.send('Logged in');
       });
       ```

   - **REST API Development**
     - RESTful principles
     - API versioning
     - Route organization
     - Controller patterns
     - Response formatting
     - Status codes
     - Error handling
     - **Code Sample:**
       ```javascript
       // RESTful principles
       const router = express.Router();

       // Controller patterns
       const userController = {
         getAllUsers: (req, res) => {
           res.json([{ id: 1, name: 'John Doe' }]);
         },
         getUserById: (req, res) => {
           const userId = req.params.id;
           res.json({ id: userId, name: 'John Doe' });
         },
         createUser: (req, res) => {
           const { name } = req.body;
           res.status(201).json({ id: 2, name });
         },
         updateUser: (req, res) => {
           const userId = req.params.id;
           const { name } = req.body;
           res.json({ id: userId, name });
         },
         deleteUser: (req, res) => {
           const userId = req.params.id;
           res.status(204).send();
         }
       };

       // Route organization
       router.get('/users', userController.getAllUsers);
       router.get('/users/:id', userController.getUserById);
       router.post('/users', userController.createUser);
       router.put('/users/:id', userController.updateUser);
       router.delete('/users/:id', userController.deleteUser);

       app.use('/api/v1', router);

       // Error handling
       app.use((err, req, res, next) => {
         console.error(err.stack);
         res.status(500).json({ error: 'Internal Server Error' });
       });
       ```

   - **Practice Projects:**
     - Basic CRUD API
     - File upload service
     - Authentication service

3. **Database Management (4 weeks)**
   - **SQL (PostgreSQL) (2 weeks)**
     - **Database Design**
       - Tables and relationships
       - Primary and foreign keys
       - Constraints
       - Normalization
       - **Code Sample:**
         ```sql
         -- Create tables with relationships
         CREATE TABLE users (
           id SERIAL PRIMARY KEY,
           username VARCHAR(50) UNIQUE NOT NULL,
           email VARCHAR(100) UNIQUE NOT NULL
         );

         CREATE TABLE posts (
           id SERIAL PRIMARY KEY,
           user_id INT REFERENCES users(id),
           title VARCHAR(100) NOT NULL,
           content TEXT NOT NULL,
           created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
         );
         ```

     - **SQL Operations**
       - CRUD operations
       - Joins
       - Aggregations
       - Transactions
       - Indexes
       - Views
       - **Code Sample:**
         ```sql
         -- CRUD operations
         INSERT INTO users (username, email) VALUES ('john_doe', 'john@example.com');
         SELECT * FROM users WHERE id = 1;
         UPDATE users SET email = 'john.doe@example.com' WHERE id = 1;
         DELETE FROM users WHERE id = 1;

         -- Joins
         SELECT users.username, posts.title
         FROM users
         JOIN posts ON users.id = posts.user_id;

         -- Aggregations
         SELECT user_id, COUNT(*) AS post_count
         FROM posts
         GROUP BY user_id;

         -- Transactions
         BEGIN;
         INSERT INTO users (username, email) VALUES ('jane_doe', 'jane@example.com');
         INSERT INTO posts (user_id, title, content) VALUES (1, 'Post Title', 'Post Content');
         COMMIT;

         -- Indexes
         CREATE INDEX idx_user_email ON users(email);

         -- Views
         CREATE VIEW user_posts AS
         SELECT users.username, posts.title, posts.content
         FROM users
         JOIN posts ON users.id = posts.user_id;
         ```

     - **PostgreSQL Specific**
       - JSON operations
       - Full-text search
       - Triggers
       - Stored procedures
       - **Code Sample:**
         ```sql
         -- JSON operations
         CREATE TABLE products (
           id SERIAL PRIMARY KEY,
           details JSONB NOT NULL
         );

         INSERT INTO products (details) VALUES ('{"name": "Product1", "price": 100}');
         SELECT details->>'name' AS name FROM products;

         -- Full-text search
         CREATE TABLE documents (
           id SERIAL PRIMARY KEY,
           content TEXT NOT NULL,
           tsvector_content TSVECTOR
         );

         CREATE INDEX idx_tsvector_content ON documents USING GIN(tsvector_content);
         UPDATE documents SET tsvector_content = to_tsvector(content);
         SELECT * FROM documents WHERE tsvector_content @@ to_tsquery('search_term');

         -- Triggers
         CREATE FUNCTION update_tsvector() RETURNS TRIGGER AS $$
         BEGIN
           NEW.tsvector_content := to_tsvector(NEW.content);
           RETURN NEW;
         END;
         $$ LANGUAGE plpgsql;

         CREATE TRIGGER tsvector_update BEFORE INSERT OR UPDATE ON documents
         FOR EACH ROW EXECUTE FUNCTION update_tsvector();

         -- Stored procedures
         CREATE OR REPLACE FUNCTION add_user(username VARCHAR, email VARCHAR) RETURNS VOID AS $$
         BEGIN
           INSERT INTO users (username, email) VALUES (username, email);
         END;
         $$ LANGUAGE plpgsql;
         ```

   - **MongoDB (2 weeks)**
     - **NoSQL Concepts**
       - Document model
       - Collections
       - BSON format
       - Embedded vs Referenced documents
       - **Code Sample:**
         ```javascript
         // Document model
         const userSchema = new mongoose.Schema({
           username: { type: String, required: true, unique: true },
           email: { type: String, required: true, unique: true },
           posts: [{ type: mongoose.Schema.Types.ObjectId, ref: 'Post' }]
         });

         const postSchema = new mongoose.Schema({
           user: { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
           title: { type: String, required: true },
           content: { type: String, required: true },
           createdAt: { type: Date, default: Date.now }
         });

         const User = mongoose.model('User', userSchema);
         const Post = mongoose.model('Post', postSchema);
         ```

     - **CRUD Operations**
       - insertOne/insertMany
       - find/findOne
       - update operations
       - delete operations
       - **Code Sample:**
         ```javascript
         // Insert operations
         const user = new User({ username: 'john_doe', email: 'john@example.com' });
         await user.save();

         // Find operations
         const foundUser = await User.findOne({ username: 'john_doe' });

         // Update operations
         await User.updateOne({ username: 'john_doe' }, { email: 'john.doe@example.com' });

         // Delete operations
         await User.deleteOne({ username: 'john_doe' });
         ```

     - **Advanced Features**
       - Aggregation pipeline
       - Indexing
       - Transactions
       - Schema validation
       - **Code Sample:**
         ```javascript
         // Aggregation pipeline
         const postCounts = await User.aggregate([
           { $lookup: { from: 'posts', localField: '_id', foreignField: 'user', as: 'posts' } },
           { $project: { username: 1, postCount: { $size: '$posts' } } }
         ]);

         // Indexing
         userSchema.index({ email: 1 });

         // Transactions
         const session = await mongoose.startSession();
         session.startTransaction();
         try {
           const user = new User({ username: 'jane_doe', email: 'jane@example.com' });
           await user.save({ session });
           const post = new Post({ user: user._id, title: 'Post Title', content: 'Post Content' });
           await post.save({ session });
           await session.commitTransaction();
         } catch (error) {
           await session.abortTransaction();
           throw error;
         } finally {
           session.endSession();
         }

         // Schema validation
         const productSchema = new mongoose.Schema({
           name: { type: String, required: true },
           price: { type: Number, required: true, min: 0 }
         });
         const Product = mongoose.model('Product', productSchema);
         ```

     - **Mongoose ODM**
       - Schema definition
       - Model operations
       - Middleware
       - Validation
       - Population
       - **Code Sample:**
         ```javascript
         // Schema definition
         const userSchema = new mongoose.Schema({
           username: { type: String, required: true, unique: true },
           email: { type: String, required: true, unique: true }
         });

         // Model operations
         const User = mongoose.model('User', userSchema);
         const user = new User({ username: 'john_doe', email: 'john@example.com' });
         await user.save();

         // Middleware
         userSchema.pre('save', function(next) {
           this.email = this.email.toLowerCase();
           next();
         });

         // Validation
         userSchema.path('email').validate((email) => {
           return email.includes('@');
         }, 'Invalid email format');

         // Population
         const postSchema = new mongoose.Schema({
           user: { type: mongoose.Schema.Types.ObjectId, ref: 'User' },
           title: { type: String, required: true },
           content: { type: String, required: true }
         });
         const Post = mongoose.model('Post', postSchema);
         const posts = await Post.find().populate('user');
         ```

4. **Authentication & Security (2 weeks)**
   - **User Authentication**
     - Password hashing (bcrypt)
     - JWT implementation
     - Session management
     - OAuth 2.0
     - Refresh tokens
     - **Code Sample:**
       ```javascript
       const express = require('express');
       const bcrypt = require('bcrypt');
       const jwt = require('jsonwebtoken');
       const session = require('express-session');
       const passport = require('passport');
       const OAuth2Strategy = require('passport-oauth2');

       const app = express();
       const users = []; // Example user storage

       // Middleware
       app.use(express.json());
       app.use(session({ secret: 'your-secret-key', resave: false, saveUninitialized: true }));

       // Password hashing
       app.post('/register', async (req, res) => {
         const { username, password } = req.body;
         const hashedPassword = await bcrypt.hash(password, 10);
         users.push({ username, password: hashedPassword });
         res.status(201).send('User registered');
       });

       // JWT implementation
       app.post('/login', async (req, res) => {
         const { username, password } = req.body;
         const user = users.find(u => u.username === username);
         if (user && await bcrypt.compare(password, user.password)) {
           const token = jwt.sign({ username }, 'your-jwt-secret', { expiresIn: '1h' });
           res.json({ token });
         } else {
           res.status(401).send('Invalid credentials');
         }
       });

       // Protecting routes with JWT
       const authenticateJWT = (req, res, next) => {
         const token = req.headers.authorization?.split(' ')[1];
         if (token) {
           jwt.verify(token, 'your-jwt-secret', (err, user) => {
             if (err) {
               return res.sendStatus(403);
             }
             req.user = user;
             next();
           });
         } else {
           res.sendStatus(401);
         }
       };

       app.get('/protected', authenticateJWT, (req, res) => {
         res.send('This is a protected route');
       });

       // OAuth 2.0 setup
       passport.use(new OAuth2Strategy({
         authorizationURL: 'https://provider.com/oauth2/authorize',
         tokenURL: 'https://provider.com/oauth2/token',
         clientID: 'your-client-id',
         clientSecret: 'your-client-secret',
         callbackURL: 'http://localhost:3000/auth/callback'
       }, (accessToken, refreshToken, profile, cb) => {
         // Find or create user in your database
         return cb(null, profile);
       }));

       app.use(passport.initialize());

       app.get('/auth/provider', passport.authenticate('oauth2'));

       app.get('/auth/callback', passport.authenticate('oauth2', { failureRedirect: '/' }), (req, res) => {
         res.redirect('/protected');
       });

       const PORT = process.env.PORT || 3000;
       app.listen(PORT, () => {
         console.log(`Server running on port ${PORT}`);
       });
       ```

   - **Security Best Practices**
     - Input validation
     - XSS protection
     - CSRF prevention
     - Rate limiting
     - Helmet security
     - SQL injection prevention
     - Environment variables
     - **Code Sample:**
       ```javascript
       const express = require('express');
       const helmet = require('helmet');
       const rateLimit = require('express-rate-limit');
       const xss = require('xss-clean');
       const mongoSanitize = require('express-mongo-sanitize');
       const csrf = require('csurf');

       const app = express();

       // Middleware
       app.use(helmet()); // Security headers
       app.use(xss()); // XSS protection
       app.use(mongoSanitize()); // Prevent NoSQL injection
       app.use(express.json());
       app.use(csrf({ cookie: true })); // CSRF protection

       // Rate limiting
       const limiter = rateLimit({
         windowMs: 15 * 60 * 1000, // 15 minutes
         max: 100 // Limit each IP to 100 requests per windowMs
       });
       app.use(limiter);

       // Input validation example
       const { body, validationResult } = require('express-validator');
       app.post('/submit', [
         body('email').isEmail(),
         body('password').isLength({ min: 6 })
       ], (req, res) => {
         const errors = validationResult(req);
         if (!errors.isEmpty()) {
           return res.status(400).json({ errors: errors.array() });
         }
         res.send('Data is valid');
       });

       const PORT = process.env.PORT || 3000;
       app.listen(PORT, () => {
         console.log(`Server running on port ${PORT}`);
       });
       ```

   - **Authorization**
     - Role-based access control
     - Permission systems
     - API keys
     - Middleware guards
     - **Code Sample:**
       ```javascript
       const express = require('express');
       const jwt = require('jsonwebtoken');

       const app = express();
       const users = [
         { username: 'admin', role: 'admin' },
         { username: 'user', role: 'user' }
       ];

       // Middleware
       app.use(express.json());

       // Role-based access control
       const authenticateJWT = (req, res, next) => {
         const token = req.headers.authorization?.split(' ')[1];
         if (token) {
           jwt.verify(token, 'your-jwt-secret', (err, user) => {
             if (err) {
               return res.sendStatus(403);
             }
             req.user = user;
             next();
           });
         } else {
           res.sendStatus(401);
         }
       };

       const authorizeRole = (role) => {
         return (req, res, next) => {
           if (req.user.role !== role) {
             return res.sendStatus(403);
           }
           next();
         };
       };

       app.get('/admin', authenticateJWT, authorizeRole('admin'), (req, res) => {
         res.send('Admin content');
       });

       app.get('/user', authenticateJWT, authorizeRole('user'), (req, res) => {
         res.send('User content');
       });

       const PORT = process.env.PORT || 3000;
       app.listen(PORT, () => {
         console.log(`Server running on port ${PORT}`);
       });
       ```

5. **Advanced API Development (2 weeks)**
   - **API Features**
     - Pagination
     - Filtering
     - Sorting
     - Field selection
     - Population/Eager loading
     - **Code Sample:**
       ```javascript
       const express = require('express');
       const mongoose = require('mongoose');

       const app = express();
       app.use(express.json());

       // Mongoose models
       const UserSchema = new mongoose.Schema({
         name: String,
         age: Number,
         email: String
       });

       const User = mongoose.model('User', UserSchema);

       // Pagination
       app.get('/users', async (req, res) => {
         const { page = 1, limit = 10 } = req.query;
         const users = await User.find()
           .limit(limit * 1)
           .skip((page - 1) * limit)
           .exec();
         const count = await User.countDocuments();
         res.json({
           users,
           totalPages: Math.ceil(count / limit),
           currentPage: page
         });
       });

       // Filtering
       app.get('/users/filter', async (req, res) => {
         const { age } = req.query;
         const users = await User.find({ age: { $gte: age } });
         res.json(users);
       });

       // Sorting
       app.get('/users/sort', async (req, res) => {
         const { sortBy = 'name', order = 'asc' } = req.query;
         const users = await User.find().sort({ [sortBy]: order === 'asc' ? 1 : -1 });
         res.json(users);
       });

       // Field selection
       app.get('/users/fields', async (req, res) => {
         const { fields } = req.query;
         const users = await User.find().select(fields.split(',').join(' '));
         res.json(users);
       });

       // Population/Eager loading
       const PostSchema = new mongoose.Schema({
         title: String,
         content: String,
         author: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
       });

       const Post = mongoose.model('Post', PostSchema);

       app.get('/posts', async (req, res) => {
         const posts = await Post.find().populate('author', 'name email');
         res.json(posts);
       });

       const PORT = process.env.PORT || 3000;
       app.listen(PORT, () => {
         console.log(`Server running on port ${PORT}`);
       });
       ```

   - **API Documentation**
     - Swagger/OpenAPI
     - API versioning
     - Documentation generation
     - **Code Sample:**
       ```javascript
       const swaggerJsDoc = require('swagger-jsdoc');
       const swaggerUi = require('swagger-ui-express');

       const swaggerOptions = {
         swaggerDefinition: {
           openapi: '3.0.0',
           info: {
             title: 'API Documentation',
             version: '1.0.0',
             description: 'API Information'
           },
           servers: [
             {
               url: 'http://localhost:3000',
               description: 'Development server'
             }
           ]
         },
         apis: ['./routes/*.js']
       };

       const swaggerDocs = swaggerJsDoc(swaggerOptions);
       app.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocs));
       ```

   - **Performance**
     - Caching strategies
     - Database optimization
     - Query optimization
     - Load balancing basics
     - **Code Sample:**
       ```javascript
       const redis = require('redis');
       const client = redis.createClient();

       // Caching middleware
       const cache = (req, res, next) => {
         const { id } = req.params;
         client.get(id, (err, data) => {
           if (err) throw err;
           if (data) {
             res.send(JSON.parse(data));
           } else {
             next();
           }
         });
       };

       app.get('/user/:id', cache, async (req, res) => {
         const { id } = req.params;
         const user = await User.findById(id);
         client.setex(id, 600, JSON.stringify(user)); // Cache for 10 minutes
         res.json(user);
       });

       // Database and query optimization
       UserSchema.index({ email: 1 }); // Indexing for faster queries

       // Load balancing basics (example with PM2)
       // pm2 start app.js -i max
       ```

   - **Error Handling**
     - Error classes
     - Global error handling
     - Async error handling
     - Logging
     - Monitoring
     - **Code Sample:**
       ```javascript
       // Error classes
       class AppError extends Error {
         constructor(message, statusCode) {
           super(message);
           this.statusCode = statusCode;
           this.status = `${statusCode}`.startsWith('4') ? 'fail' : 'error';
           this.isOperational = true;
           Error.captureStackTrace(this, this.constructor);
         }
       }

       // Global error handling middleware
       app.use((err, req, res, next) => {
         err.statusCode = err.statusCode || 500;
         err.status = err.status || 'error';
         res.status(err.statusCode).json({
           status: err.status,
           message: err.message
         });
       });

       // Async error handling
       const catchAsync = fn => (req, res, next) => {
         fn(req, res, next).catch(next);
       };

       app.get('/user/:id', catchAsync(async (req, res, next) => {
         const user = await User.findById(req.params.id);
         if (!user) {
           return next(new AppError('User not found', 404));
         }
         res.json(user);
       }));

       // Logging and monitoring (example with Winston and Morgan)
       const winston = require('winston');
       const morgan = require('morgan');

       const logger = winston.createLogger({
         level: 'info',
         format: winston.format.json(),
         transports: [
           new winston.transports.File({ filename: 'error.log', level: 'error' }),
           new winston.transports.File({ filename: 'combined.log' })
         ]
       });

       app.use(morgan('combined', { stream: { write: message => logger.info(message.trim()) } }));
       ```

6. **Integration & Testing (1 week)**
   - **Testing**
     - Unit tests with Jest
     - Integration tests
     - API testing with Supertest
     - Mock databases
     - Test coverage
     - **Code Sample:**
       ```javascript
       // Jest unit test example
       const sum = (a, b) => a + b;

       test('adds 1 + 2 to equal 3', () => {
         expect(sum(1, 2)).toBe(3);
       });

       // Integration test example
       const request = require('supertest');
       const express = require('express');
       const app = express();

       app.get('/user', (req, res) => {
         res.status(200).json({ name: 'John Doe' });
       });

       request(app)
         .get('/user')
         .expect('Content-Type', /json/)
         .expect(200, { name: 'John Doe' });

       // Mock database example
       const mongoose = require('mongoose');
       const { MongoMemoryServer } = require('mongodb-memory-server');

       let mongoServer;
       beforeAll(async () => {
         mongoServer = await MongoMemoryServer.create();
         const uri = mongoServer.getUri();
         await mongoose.connect(uri, { useNewUrlParser: true, useUnifiedTopology: true });
       });

       afterAll(async () => {
         await mongoose.disconnect();
         await mongoServer.stop();
       });

       // Test coverage example
       // Add the following script to package.json
       // "scripts": {
       //   "test": "jest --coverage"
       // }
       ```

   - **Deployment Preparation**
     - Environment configuration
     - Process management (PM2)
     - Logging setup
     - Monitoring setup
     - CI/CD basics
     - **Code Sample:**
       ```bash
       # Environment configuration
       export NODE_ENV=production
       export PORT=3000

       # Process management with PM2
       pm2 start app.js --name "my-app"

       # Logging setup with PM2
       pm2 logs my-app

       # Monitoring setup (example with New Relic)
       # Install New Relic agent
       npm install newrelic --save
       # Add the following line to the top of your main file (e.g., app.js)
       require('newrelic');

       # CI/CD basics (example with GitHub Actions)
       # .github/workflows/ci.yml
       name: CI

       on: [push]

       jobs:
         build:
           runs-on: ubuntu-latest

           steps:
           - uses: actions/checkout@v2
           - name: Set up Node.js
             uses: actions/setup-node@v2
             with:
               node-version: '14'
           - run: npm install
           - run: npm test
           - run: npm run build
       ```

7. **Final Projects (2 weeks)**
   Build one of these complete backend systems:
   - **E-commerce API**
     - Product management
     - User authentication
     - Order processing
     - Payment integration
   
   - **Social Media API**
     - User profiles
     - Posts and comments
     - Follow system
     - Feed generation
   
   - **Task Management API**
     - Project organization
     - Task CRUD
     - User assignments
     - Real-time updates

   **Learning Resources:**
   - Express.js Documentation
   - MongoDB University
   - PostgreSQL Tutorial
   - JWT.io
   - Web Security Academy
   - Testing JavaScript by Kent C. Dodds

---