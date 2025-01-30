## Phase 4: Full-Stack Integration (2-3 Months)
### Goal: Build complete full-stack applications with industry-standard practices

1. **Full-Stack Application Architecture (1 week)**
   - **Project Structure**
     - Monorepo vs separate repos
     - Directory organization
     - Environment configuration
     - Code sharing between front-end and back-end
     - **Code Sample:**
       ```javascript
       // Directory structure example
       my-fullstack-app/
       ├── backend/
       │   ├── src/
       │   │   ├── controllers/
       │   │   ├── models/
       │   │   ├── routes/
       │   │   ├── services/
       │   │   └── app.js
       │   ├── .env
       │   ├── package.json
       │   └── README.md
       ├── frontend/
       │   ├── src/
       │   │   ├── components/
       │   │   ├── pages/
       │   │   ├── services/
       │   │   └── App.js
       │   ├── .env
       │   ├── package.json
       │   └── README.md
       ├── .gitignore
       ├── README.md
       └── docker-compose.yml

       // Environment configuration example
       // backend/.env
       PORT=5000
       DATABASE_URL=mongodb://localhost:27017/myapp
       JWT_SECRET=mysecretkey

       // frontend/.env
       REACT_APP_API_URL=http://localhost:5000/api

       // Docker Compose example
       version: '3.8'
       services:
         backend:
           build: ./backend
           ports:
             - "5000:5000"
           env_file:
             - ./backend/.env
         frontend:
           build: ./frontend
           ports:
             - "3000:3000"
           env_file:
             - ./frontend/.env
       ```

   - **API Integration Patterns**
     - REST API best practices
     - API documentation
     - Error handling strategies
     - Data validation approaches
     - **Code Sample:**
       ```javascript
       // REST API best practices example
       const express = require('express');
       const app = express();
       const Joi = require('joi');

       // Middleware for parsing JSON bodies
       app.use(express.json());

       // Data validation using Joi
       const userSchema = Joi.object({
         name: Joi.string().min(3).required(),
         email: Joi.string().email().required(),
         password: Joi.string().min(6).required()
       });

       // Error handling middleware
       app.use((err, req, res, next) => {
         if (err.isJoi) {
           return res.status(400).json({ error: err.details[0].message });
         }
         res.status(500).json({ error: 'Internal Server Error' });
       });

       // Sample route with validation
       app.post('/api/users', async (req, res, next) => {
         try {
           const { error } = userSchema.validate(req.body);
           if (error) return next(error);
           // ...create user logic...
           res.status(201).json({ message: 'User created successfully' });
         } catch (err) {
           next(err);
         }
       });

       const PORT = process.env.PORT || 5000;
       app.listen(PORT, () => {
         console.log(`Server running on port ${PORT}`);
       });
       ```

   - **State Management**
     - Client-side state
     - Server state management
     - Caching strategies
     - Real-time updates
     - **Code Sample:**
       ```javascript
       // Client-side state management example using React Context
       import React, { createContext, useReducer, useContext } from 'react';

       const initialState = { user: null, loading: false, error: null };

       const reducer = (state, action) => {
         switch (action.type) {
           case 'LOGIN_REQUEST':
             return { ...state, loading: true };
           case 'LOGIN_SUCCESS':
             return { ...state, loading: false, user: action.payload };
           case 'LOGIN_FAILURE':
             return { ...state, loading: false, error: action.payload };
           default:
             return state;
         }
       };

       const StateContext = createContext();

       export const StateProvider = ({ children }) => {
         const [state, dispatch] = useReducer(reducer, initialState);
         return (
           <StateContext.Provider value={{ state, dispatch }}>
             {children}
           </StateContext.Provider>
         );
       };

       export const useStateContext = () => useContext(StateContext);

       // Usage in a component
       import React from 'react';
       import { useStateContext } from './StateProvider';

       const Login = () => {
         const { state, dispatch } = useStateContext();

         const handleLogin = async () => {
           dispatch({ type: 'LOGIN_REQUEST' });
           try {
             // ...login logic...
             dispatch({ type: 'LOGIN_SUCCESS', payload: user });
           } catch (error) {
             dispatch({ type: 'LOGIN_FAILURE', payload: error.message });
           }
         };

         return (
           <div>
             {state.loading ? 'Loading...' : <button onClick={handleLogin}>Login</button>}
             {state.error && <p>{state.error}</p>}
           </div>
         );
       };

       export default Login;
       ```

2. **Advanced Front-End Integration (2 weeks)**
   - **API Integration**
     - Axios/fetch setup
     - Request/response interceptors
     - Custom hooks for API calls
     - Error boundary implementation
     - **Code Sample:**
       ```javascript
       // Axios setup with interceptors
       import axios from 'axios';

       const api = axios.create({
         baseURL: process.env.REACT_APP_API_URL,
       });

       api.interceptors.request.use(
         config => {
           // Add authorization token to headers
           const token = localStorage.getItem('token');
           if (token) {
             config.headers.Authorization = `Bearer ${token}`;
           }
           return config;
         },
         error => Promise.reject(error)
       );

       api.interceptors.response.use(
         response => response,
         error => {
           // Handle errors globally
           if (error.response.status === 401) {
             // Redirect to login if unauthorized
             window.location.href = '/login';
           }
           return Promise.reject(error);
         }
       );

       export default api;
       ```

   - **Data Management**
     - React Query/SWR implementation
       - Caching
       - Optimistic updates
       - Infinite loading
       - Mutations
     - Redux integration with APIs
       - Thunks/Sagas
       - API middleware
       - State normalization
     - **Code Sample:**
       ```javascript
       // React Query setup
       import { useQuery, useMutation, useQueryClient } from 'react-query';
       import api from './api';

       const fetchUser = async (userId) => {
         const { data } = await api.get(`/users/${userId}`);
         return data;
       };

       const useUser = (userId) => {
         return useQuery(['user', userId], () => fetchUser(userId), {
           staleTime: 1000 * 60 * 5, // 5 minutes
         });
       };

       const updateUser = async (user) => {
         const { data } = await api.put(`/users/${user.id}`, user);
         return data;
       };

       const useUpdateUser = () => {
         const queryClient = useQueryClient();
         return useMutation(updateUser, {
           onSuccess: () => {
             queryClient.invalidateQueries('user');
           },
         });
       };

       export { useUser, useUpdateUser };
       ```

   - **Authentication Flow**
     - JWT implementation
     - Protected routes
     - Refresh token handling
     - Persistent login
     - Social authentication
     - **Code Sample:**
       ```javascript
       // ProtectedRoute component
       import React from 'react';
       import { Route, Redirect } from 'react-router-dom';

       const ProtectedRoute = ({ component: Component, ...rest }) => {
         const isAuthenticated = !!localStorage.getItem('token');
         return (
           <Route
             {...rest}
             render={props =>
               isAuthenticated ? (
                 <Component {...props} />
               ) : (
                 <Redirect to="/login" />
               )
             }
           />
         );
       };

       export default ProtectedRoute;
       ```

3. **Backend Integration & Optimization (2 weeks)**
   - **API Optimization**
     - Response compression
     - Database query optimization
     - Caching strategies (Redis)
     - Rate limiting
     - Load balancing
     - **Code Sample:**
       ```javascript
       const express = require('express');
       const compression = require('compression');
       const mongoose = require('mongoose');
       const redis = require('redis');
       const rateLimit = require('express-rate-limit');
       const cluster = require('cluster');
       const os = require('os');

       const app = express();
       const client = redis.createClient();

       // Middleware
       app.use(compression()); // Response compression
       app.use(express.json());

       // Rate limiting
       const limiter = rateLimit({
         windowMs: 15 * 60 * 1000, // 15 minutes
         max: 100 // Limit each IP to 100 requests per windowMs
       });
       app.use(limiter);

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

       // Database query optimization
       mongoose.set('debug', true); // Enable query logging for optimization

       // Example route with caching
       app.get('/user/:id', cache, async (req, res) => {
         const { id } = req.params;
         const user = await User.findById(id);
         client.setex(id, 600, JSON.stringify(user)); // Cache for 10 minutes
         res.json(user);
       });

       // Load balancing with clustering
       if (cluster.isMaster) {
         const numCPUs = os.cpus().length;
         for (let i = 0; i < numCPUs; i++) {
           cluster.fork();
         }
         cluster.on('exit', (worker, code, signal) => {
           console.log(`Worker ${worker.process.pid} died`);
           cluster.fork();
         });
       } else {
         const PORT = process.env.PORT || 3000;
         app.listen(PORT, () => {
           console.log(`Server running on port ${PORT}`);
         });
       }
       ```

   - **File Handling**
     - Image upload and processing
     - File storage (S3/CloudFront)
     - Media streaming
     - File validation

   - **Background Jobs**
     - Queue implementation
     - Scheduled tasks
     - Email services
     - Webhook handling

4. **Database Integration (1 week)**
   - **Data Layer**
     - ORM configuration
     - Migration strategies
     - Seeding data
     - Backup strategies
     - **Code Sample:**
       ```javascript
       // ORM configuration example using Sequelize
       const { Sequelize, DataTypes } = require('sequelize');
       const sequelize = new Sequelize('database', 'username', 'password', {
         host: 'localhost',
         dialect: 'postgres',
       });

       const User = sequelize.define('User', {
         id: {
           type: DataTypes.INTEGER,
           autoIncrement: true,
           primaryKey: true,
         },
         name: {
           type: DataTypes.STRING,
           allowNull: false,
         },
         email: {
           type: DataTypes.STRING,
           allowNull: false,
           unique: true,
         },
         password: {
           type: DataTypes.STRING,
           allowNull: false,
         },
       });

       // Migration strategy example
       const migrateDatabase = async () => {
         try {
           await sequelize.authenticate();
           console.log('Connection has been established successfully.');
           await sequelize.sync({ force: true }); // Use { alter: true } for safe migrations
           console.log('Database synchronized.');
         } catch (error) {
           console.error('Unable to connect to the database:', error);
         }
       };

       // Seeding data example
       const seedDatabase = async () => {
         await User.bulkCreate([
           { name: 'John Doe', email: 'john@example.com', password: 'password123' },
           { name: 'Jane Doe', email: 'jane@example.com', password: 'password123' },
         ]);
         console.log('Database seeded.');
       };

       // Backup strategy example
       const backupDatabase = () => {
         const exec = require('child_process').exec;
         const backupCommand = 'pg_dump -U username -h localhost database > backup.sql';
         exec(backupCommand, (error, stdout, stderr) => {
           if (error) {
             console.error(`Backup error: ${error.message}`);
             return;
           }
           if (stderr) {
             console.error(`Backup stderr: ${stderr}`);
             return;
           }
           console.log('Database backup completed.');
         });
       };

       migrateDatabase().then(() => seedDatabase()).then(() => backupDatabase());
       ```

   - **Performance**
     - Indexing
     - Query optimization
     - Connection pooling
     - Replication setup
     - **Code Sample:**
       ```javascript
       // Indexing example
       User.addIndex('email_index', ['email']);

       // Query optimization example
       const getUsers = async () => {
         const users = await User.findAll({
           attributes: ['id', 'name', 'email'],
           where: {
             active: true,
           },
           limit: 100,
         });
         return users;
       };

       // Connection pooling example
       const sequelize = new Sequelize('database', 'username', 'password', {
         host: 'localhost',
         dialect: 'postgres',
         pool: {
           max: 10,
           min: 0,
           acquire: 30000,
           idle: 10000,
         },
       });

       // Replication setup example
       const sequelize = new Sequelize('database', 'username', 'password', {
         replication: {
           read: [
             { host: 'replica1', username: 'username', password: 'password' },
             { host: 'replica2', username: 'username', password: 'password' },
           ],
           write: { host: 'master', username: 'username', password: 'password' },
         },
         pool: {
           max: 10,
           min: 0,
           acquire: 30000,
           idle: 10000,
         },
       });
       ```

5. **Testing & Quality Assurance (1 week)**
   - **Testing Strategy**
     - Unit tests
     - Integration tests
     - End-to-end tests
     - Performance tests
     - **Code Sample:**
       ```javascript
       // Unit test example using Jest
       const sum = (a, b) => a + b;

       test('adds 1 + 2 to equal 3', () => {
         expect(sum(1, 2)).toBe(3);
       });

       // Integration test example using Jest and Supertest
       const request = require('supertest');
       const express = require('express');
       const app = express();

       app.get('/user', (req, res) => {
         res.status(200).json({ name: 'John Doe' });
       });

       test('GET /user', async () => {
         const response = await request(app).get('/user');
         expect(response.status).toBe(200);
         expect(response.body.name).toBe('John Doe');
       });

       // End-to-end test example using Cypress
       describe('Login Page', () => {
         it('should allow a user to log in', () => {
           cy.visit('/login');
           cy.get('input[name=email]').type('user@example.com');
           cy.get('input[name=password]').type('password123');
           cy.get('button[type=submit]').click();
           cy.url().should('include', '/dashboard');
         });
       });

       // Performance test example using k6
       import http from 'k6/http';
       import { check, sleep } from 'k6';

       export default function () {
         const res = http.get('https://test.k6.io');
         check(res, {
           'is status 200': (r) => r.status === 200,
         });
         sleep(1);
       }
       ```

   - **Tools**
     - Jest
     - React Testing Library
     - Cypress
     - k6 for load testing
   
   - **CI/CD Setup**
     - GitHub Actions
     - Automated testing
     - Deployment pipelines
     - Environment management

6. **Deployment & DevOps (2 weeks)**
   - **Development Environment**
     - Docker setup
     - Development containers
     - Local development workflow
     - **Code Sample:**
       ```dockerfile
       // Dockerfile for Node.js application
       FROM node:14

       # Create app directory
       WORKDIR /usr/src/app

       # Install app dependencies
       COPY package*.json ./
       RUN npm install

       # Bundle app source
       COPY . .

       # Expose port and start application
       EXPOSE 8080
       CMD ["node", "server.js"]
       ```

       ```yaml
       // docker-compose.yml for development environment
       version: '3.8'
       services:
         app:
           build: .
           ports:
             - "8080:8080"
           volumes:
             - .:/usr/src/app
             - /usr/src/app/node_modules
           environment:
             NODE_ENV: development
       ```

   - **Production Deployment**
     - Front-end deployment (Vercel/Netlify)
     - Backend deployment (Heroku/AWS)
     - Database hosting
     - Domain setup & SSL
     - **Code Sample:**
       ```yaml
       // GitHub Actions workflow for CI/CD
       name: CI/CD Pipeline

       on:
         push:
           branches:
             - main

       jobs:
         build:
           runs-on: ubuntu-latest

           steps:
             - name: Checkout code
               uses: actions/checkout@v2

             - name: Set up Node.js
               uses: actions/setup-node@v2
               with:
                 node-version: '14'

             - name: Install dependencies
               run: npm install

             - name: Run tests
               run: npm test

             - name: Build project
               run: npm run build

             - name: Deploy to Heroku
               uses: akhileshns/heroku-deploy@v3.12.12
               with:
                 heroku_api_key: ${{ secrets.HEROKU_API_KEY }}
                 heroku_app_name: 'your-app-name'
                 heroku_email: 'your-email@example.com'
       ```

   - **Monitoring & Logging**
     - Error tracking (Sentry)
     - Performance monitoring
     - Log management
     - Uptime monitoring
     - **Code Sample:**
       ```javascript
       // Sentry setup for error tracking
       const Sentry = require('@sentry/node');
       const express = require('express');
       const app = express();

       Sentry.init({ dsn: 'your-dsn-url' });

       app.use(Sentry.Handlers.requestHandler());

       app.get('/', function mainHandler(req, res) {
         throw new Error('Broke!');
       });

       app.use(Sentry.Handlers.errorHandler());

       app.listen(3000, () => {
         console.log('Server running on port 3000');
       });
       ```

7. **Full-Stack Projects (3-4 weeks)**
   Build one of these comprehensive applications:

   - **E-commerce Platform**
     - Product catalog with search/filter
     - Shopping cart & checkout
     - Payment integration (Stripe)
     - Order management
     - Admin dashboard
     - Email notifications
   
   - **Social Platform**
     - User authentication
     - Profile management
     - Post creation with media
     - Real-time chat
     - Notifications system
     - Social graph (following/followers)
   
   - **Project Management Tool**
     - Team management
     - Task tracking
     - File sharing
     - Calendar integration
     - Real-time updates
     - Activity logging

   **Learning Resources:**
   - Full Stack Open (University of Helsinki)
   - AWS Documentation
   - Docker Documentation
   - Digital Ocean Tutorials
   - TestingJavaScript.com

   **Project Management Tools:**
   - Jira/Trello for task tracking
   - GitHub Projects
   - Notion for documentation

8. **Performance & Optimization (1 week)**
   - **Front-end Performance**
     - Lazy loading
     - Code splitting
     - Bundle optimization
     - Image optimization
     - Performance monitoring
   
   - **Back-end Performance**
     - Database optimization
     - Caching strategies
     - Load balancing
     - Memory management
   
   - **Security**
     - Security headers
     - CORS configuration
     - Rate limiting
     - Input validation
     - XSS/CSRF protection

---