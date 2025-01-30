## Phase 2: Front-End Development (2-3 Months)
### Goal: Master modern front-end development with React ecosystem

1. **Advanced JavaScript Concepts (2 weeks)**
   - **ES6+ Features**
     - Arrow functions and lexical scope
     - Template literals
     - Destructuring arrays and objects
     - Spread/Rest operators
     - Default parameters
     - Optional chaining
     - Nullish coalescing
     - **Code Sample:**
       ```javascript
       // Arrow functions and lexical scope
       const greet = (name) => `Hello, ${name}`;
       console.log(greet("Alice"));

       // Template literals
       const age = 30;
       console.log(`I am ${age} years old`);

       // Destructuring arrays and objects
       const [a, b] = [1, 2];
       const { x, y } = { x: 10, y: 20 };

       // Spread/Rest operators
       const arr = [1, 2, 3];
       const newArr = [...arr, 4, 5];
       const sum = (...numbers) => numbers.reduce((acc, num) => acc + num, 0);

       // Default parameters
       const multiply = (a, b = 1) => a * b;

       // Optional chaining
       const user = { address: { city: "New York" } };
       console.log(user?.address?.city);

       // Nullish coalescing
       const value = null ?? "default value";
       ```

   - **Asynchronous JavaScript**
     - Callbacks
     - Promises
       - Creating promises
       - Promise chaining
       - Promise.all, Promise.race
       - Error handling with .catch()
     - Async/Await
       - Error handling with try/catch
       - Parallel execution
       - Sequential execution
     - **Code Sample:**
       ```javascript
       // Callbacks
       function fetchData(callback) {
         setTimeout(() => {
           callback("Data fetched");
         }, 1000);
       }

       fetchData((data) => {
         console.log(data);
       });

       // Promises
       const fetchDataPromise = () => {
         return new Promise((resolve, reject) => {
           setTimeout(() => {
             resolve("Data fetched");
           }, 1000);
         });
       };

       fetchDataPromise()
         .then((data) => console.log(data))
         .catch((error) => console.error(error));

       // Async/Await
       const fetchDataAsync = async () => {
         try {
           const data = await fetchDataPromise();
           console.log(data);
         } catch (error) {
           console.error(error);
         }
       };

       fetchDataAsync();
       ```

   - **Modern JavaScript APIs**
     - Fetch API
       - GET, POST, PUT, DELETE requests
       - Headers and body
       - Error handling
       - Response parsing
     - localStorage/sessionStorage
     - Intersection Observer
     - Web Workers
     - **Code Sample:**
       ```javascript
       // Fetch API
       fetch('https://api.example.com/data')
         .then(response => {
           if (!response.ok) {
             throw new Error('Network response was not ok');
           }
           return response.json();
         })
         .then(data => console.log(data))
         .catch(error => console.error('Fetch error:', error));

       // localStorage
       localStorage.setItem('key', 'value');
       const value = localStorage.getItem('key');

       // Intersection Observer
       const observer = new IntersectionObserver((entries) => {
         entries.forEach(entry => {
           if (entry.isIntersecting) {
             console.log('Element is in view');
           }
         });
       });

       observer.observe(document.querySelector('#target'));

       // Web Workers
       const worker = new Worker('worker.js');
       worker.postMessage('Hello, worker');
       worker.onmessage = (event) => {
         console.log('Message from worker:', event.data);
       };
       ```

   - **Practice Projects:**
     - Build a data fetching utility
     - Create a promise-based timer
     - Implement infinite scrolling

2. **React.js Deep Dive (4-6 weeks)**
   - **React Fundamentals**
     - JSX syntax
     - Components (Class vs Functional)
     - Virtual DOM
     - Props and prop types
     - Component lifecycle
     - **Code Sample:**
       ```jsx
       // Functional Component
       import React from 'react';
       import PropTypes from 'prop-types';

       const Greeting = ({ name }) => {
         return <h1>Hello, {name}!</h1>;
       };

       Greeting.propTypes = {
         name: PropTypes.string.isRequired,
       };

       export default Greeting;
       ```

   - **Hooks in Depth**
     - useState
     - useEffect
     - useContext
     - useReducer
     - useCallback
     - useMemo
     - useRef
     - Custom hooks
     - **Code Sample:**
       ```jsx
       import React, { useState, useEffect, useContext, useReducer, useCallback, useMemo, useRef } from 'react';

       // useState
       const Counter = () => {
         const [count, setCount] = useState(0);
         return <button onClick={() => setCount(count + 1)}>Count: {count}</button>;
       };

       // useEffect
       const Timer = () => {
         useEffect(() => {
           const timer = setInterval(() => {
             console.log('Tick');
           }, 1000);
           return () => clearInterval(timer);
         }, []);
         return <div>Check the console for ticks</div>;
       };

       // useContext
       const ThemeContext = React.createContext('light');
       const ThemedComponent = () => {
         const theme = useContext(ThemeContext);
         return <div>Current theme: {theme}</div>;
       };

       // useReducer
       const reducer = (state, action) => {
         switch (action.type) {
           case 'increment':
             return { count: state.count + 1 };
           case 'decrement':
             return { count: state.count - 1 };
           default:
             return state;
         }
       };
       const CounterWithReducer = () => {
         const [state, dispatch] = useReducer(reducer, { count: 0 });
         return (
           <div>
             <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
             <span>{state.count}</span>
             <button onClick={() => dispatch({ type: 'increment' })}>+</button>
           </div>
         );
       };

       // useCallback
       const CallbackComponent = () => {
         const handleClick = useCallback(() => {
           console.log('Button clicked');
         }, []);
         return <button onClick={handleClick}>Click me</button>;
       };

       // useMemo
       const MemoComponent = ({ a, b }) => {
         const result = useMemo(() => a + b, [a, b]);
         return <div>Result: {result}</div>;
       };

       // useRef
       const RefComponent = () => {
         const inputRef = useRef(null);
         const focusInput = () => {
           inputRef.current.focus();
         };
         return (
           <div>
             <input ref={inputRef} type="text" />
             <button onClick={focusInput}>Focus Input</button>
           </div>
         );
       };

       // Custom hook
       const useFetch = (url) => {
         const [data, setData] = useState(null);
         useEffect(() => {
           fetch(url)
             .then((response) => response.json())
             .then((data) => setData(data));
         }, [url]);
         return data;
       };
       const FetchComponent = ({ url }) => {
         const data = useFetch(url);
         return <div>{data ? JSON.stringify(data) : 'Loading...'}</div>;
       };
       ```

   - **State Management**
     - Local state
     - Lifting state up
     - Context API
     - Redux basics
       - Store setup
       - Actions and reducers
       - useSelector and useDispatch
       - Redux Toolkit
     - **Code Sample:**
       ```jsx
       // Redux setup
       import { createStore } from 'redux';
       import { Provider, useSelector, useDispatch } from 'react-redux';

       const initialState = { count: 0 };

       const reducer = (state = initialState, action) => {
         switch (action.type) {
           case 'increment':
             return { count: state.count + 1 };
           case 'decrement':
             return { count: state.count - 1 };
           default:
             return state;
         }
       };

       const store = createStore(reducer);

       const Counter = () => {
         const count = useSelector((state) => state.count);
         const dispatch = useDispatch();
         return (
           <div>
             <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
             <span>{count}</span>
             <button onClick={() => dispatch({ type: 'increment' })}>+</button>
           </div>
         );
       };

       const App = () => (
         <Provider store={store}>
           <Counter />
         </Provider>
       );

       export default App;
       ```

   - **Routing**
     - React Router v6
       - BrowserRouter
       - Routes and Route
       - Link and NavLink
       - URL parameters
       - Nested routes
       - Protected routes
     - **Code Sample:**
       ```jsx
       import { BrowserRouter as Router, Routes, Route, Link, useParams, Navigate } from 'react-router-dom';

       const Home = () => <h2>Home</h2>;
       const About = () => <h2>About</h2>;
       const User = () => {
         const { id } = useParams();
         return <h2>User ID: {id}</h2>;
       };

       const ProtectedRoute = ({ children }) => {
         const isAuthenticated = true; // Replace with actual authentication logic
         return isAuthenticated ? children : <Navigate to="/" />;
       };

       const App = () => (
         <Router>
           <nav>
             <Link to="/">Home</Link>
             <Link to="/about">About</Link>
             <Link to="/user/123">User</Link>
           </nav>
           <Routes>
             <Route path="/" element={<Home />} />
             <Route path="/about" element={<About />} />
             <Route path="/user/:id" element={<User />} />
             <Route path="/protected" element={<ProtectedRoute><h2>Protected</h2></ProtectedRoute>} />
           </Routes>
         </Router>
       );

       export default App;
       ```

   - **Forms and Validation**
     - Controlled components
     - Form libraries (Formik/React Hook Form)
     - Validation libraries (Yup/Zod)
     - **Code Sample:**
       ```jsx
       import React, { useState } from 'react';
       import { useFormik } from 'formik';
       import * as Yup from 'yup';

       const SignupForm = () => {
         const formik = useFormik({
           initialValues: {
             email: '',
             password: '',
           },
           validationSchema: Yup.object({
             email: Yup.string().email('Invalid email address').required('Required'),
             password: Yup.string().min(6, 'Must be 6 characters or more').required('Required'),
           }),
           onSubmit: (values) => {
             console.log(values);
           },
         });

         return (
           <form onSubmit={formik.handleSubmit}>
             <label htmlFor="email">Email</label>
             <input
               id="email"
               name="email"
               type="email"
               onChange={formik.handleChange}
               onBlur={formik.handleBlur}
               value={formik.values.email}
             />
             {formik.touched.email && formik.errors.email ? <div>{formik.errors.email}</div> : null}

             <label htmlFor="password">Password</label>
             <input
               id="password"
               name="password"
               type="password"
               onChange={formik.handleChange}
               onBlur={formik.handleBlur}
               value={formik.values.password}
             />
             {formik.touched.password && formik.errors.password ? <div>{formik.errors.password}</div> : null}

             <button type="submit">Submit</button>
           </form>
         );
       };

       export default SignupForm;
       ```

   - **Performance Optimization**
     - React.memo
     - Lazy loading
     - Code splitting
     - Error boundaries
     - **Code Sample:**
       ```jsx
       import React, { lazy, Suspense } from 'react';

       // React.memo
       const ExpensiveComponent = React.memo(({ data }) => {
         console.log('Rendering ExpensiveComponent');
         return <div>{data}</div>;
       });

       // Lazy loading and code splitting
       const LazyComponent = lazy(() => import('./LazyComponent'));

       // Error boundaries
       class ErrorBoundary extends React.Component {
         constructor(props) {
           super(props);
           this.state = { hasError: false };
         }

         static getDerivedStateFromError(error) {
           return { hasError: true };
         }

         componentDidCatch(error, errorInfo) {
           console.error('ErrorBoundary caught an error', error, errorInfo);
         }

         render() {
           if (this.state.hasError) {
             return <h1>Something went wrong.</h1>;
           }

           return this.props.children;
         }
       }

       const App = () => (
         <div>
           <ExpensiveComponent data="Some data" />
           <ErrorBoundary>
             <Suspense fallback={<div>Loading...</div>}>
               <LazyComponent />
             </Suspense>
           </ErrorBoundary>
         </div>
       );

       export default App;
       ```

   - **Testing**
     - Jest basics
     - React Testing Library
     - Component testing
     - Integration testing
     - **Code Sample:**
       ```jsx
       import React from 'react';
       import { render, screen, fireEvent } from '@testing-library/react';
       import '@testing-library/jest-dom/extend-expect';
       import Counter from './Counter';

       test('increments counter', () => {
         render(<Counter />);
         const button = screen.getByText('Count: 0');
         fireEvent.click(button);
         expect(button).toHaveTextContent('Count: 1');
       });
       ```

3. **Version Control with Git (1 week)**
   - **Basic Commands**
     - init, add, commit
     - branch, checkout, merge
     - pull, push, fetch
     - stash, pop
     - **Code Sample:**
       ```bash
       # Initialize a new Git repository
       git init

       # Add files to staging area
       git add .

       # Commit changes with a message
       git commit -m "Initial commit"

       # Create a new branch
       git branch feature-branch

       # Switch to the new branch
       git checkout feature-branch

       # Merge changes from feature-branch to main
       git checkout main
       git merge feature-branch

       # Push changes to remote repository
       git push origin main

       # Fetch updates from remote repository
       git fetch

       # Stash changes temporarily
       git stash

       # Apply stashed changes
       git stash pop
       ```

   - **GitHub Workflow**
     - Creating repositories
     - Forking
     - Pull requests
     - Code review process
     - Issue tracking
     - **Code Sample:**
       ```bash
       # Clone a repository
       git clone https://github.com/username/repository.git

       # Create a new branch for a feature
       git checkout -b feature-branch

       # Make changes and commit
       git add .
       git commit -m "Add new feature"

       # Push the branch to GitHub
       git push origin feature-branch

       # Create a pull request on GitHub

       # After review, merge the pull request on GitHub

       # Pull the latest changes
       git pull origin main
       ```

   - **Advanced Git**
     - Interactive rebase
     - Cherry-picking
     - Resolving conflicts
     - Git hooks
     - **Code Sample:**
       ```bash
       # Interactive rebase
       git rebase -i HEAD~3

       # Cherry-pick a commit
       git cherry-pick <commit-hash>

       # Resolve merge conflicts
       git merge feature-branch
       # Edit conflicting files
       git add .
       git commit

       # Git hooks (example: pre-commit hook)
       echo "echo 'Running pre-commit checks...'" > .git/hooks/pre-commit
       chmod +x .git/hooks/pre-commit
       ```

   - **Best Practices**
     - Commit message conventions
     - Branching strategies
     - Git workflow models
     - **Code Sample:**
       ```bash
       # Commit message conventions
       git commit -m "feat: add new login feature"
       git commit -m "fix: resolve issue with user authentication"
       git commit -m "docs: update README with setup instructions"

       # Branching strategy (example: Gitflow)
       git checkout -b feature/feature-name
       git checkout -b release/release-name
       git checkout -b hotfix/hotfix-name

       # Git workflow model (example: Feature Branch Workflow)
       git checkout -b feature-branch
       git add .
       git commit -m "Add new feature"
       git push origin feature-branch
       git checkout main
       git merge feature-branch
       git push origin main
       ```

4. **Front-End Tools and Build Process (1 week)**
   - **Package Managers**
     - npm/yarn commands
     - package.json configuration
     - Dependencies vs devDependencies
     - **Code Sample:**
       ```bash
       # Initialize a new project
       npm init -y

       # Install dependencies
       npm install react react-dom

       # Install devDependencies
       npm install --save-dev webpack babel-loader @babel/core @babel/preset-env @babel/preset-react

       # Run scripts defined in package.json
       npm run build
       npm run start
       ```

   - **Build Tools**
     - Vite
     - Webpack basics
     - Babel configuration
     - **Code Sample:**
       ```javascript
       // webpack.config.js
       const path = require('path');

       module.exports = {
         entry: './src/index.js',
         output: {
           path: path.resolve(__dirname, 'dist'),
           filename: 'bundle.js',
         },
         module: {
           rules: [
             {
               test: /\.js$/,
               exclude: /node_modules/,
               use: {
                 loader: 'babel-loader',
                 options: {
                   presets: ['@babel/preset-env', '@babel/preset-react'],
                 },
               },
             },
           ],
         },
         devServer: {
           contentBase: path.join(__dirname, 'dist'),
           compress: true,
           port: 9000,
         },
       };
       ```

   - **Development Tools**
     - Chrome DevTools
     - React Developer Tools
     - Redux DevTools
     - **Code Sample:**
       ```javascript
       // Example of using React Developer Tools
       import React from 'react';
       import { createStore } from 'redux';
       import { Provider } from 'react-redux';
       import { devToolsEnhancer } from 'redux-devtools-extension';

       const store = createStore(reducer, devToolsEnhancer());

       const App = () => (
         <Provider store={store}>
           <div>My App</div>
         </Provider>
       );

       export default App;
       ```

   - **Code Quality**
     - ESLint
     - Prettier
     - Husky pre-commit hooks
     - **Code Sample:**
       ```json
       // .eslintrc.json
       {
         "extends": "eslint:recommended",
         "parserOptions": {
           "ecmaVersion": 2020,
           "sourceType": "module",
           "ecmaFeatures": {
             "jsx": true
           }
         },
         "rules": {
           "semi": ["error", "always"],
           "quotes": ["error", "single"]
         }
       }

       // .prettierrc
       {
         "singleQuote": true,
         "semi": true
       }

       // package.json (Husky setup)
       {
         "husky": {
           "hooks": {
             "pre-commit": "npm run lint"
           }
         },
         "scripts": {
           "lint": "eslint 'src/**/*.{js,jsx}'"
         }
       }
       ```

5. **Practice Projects (2 weeks)**
   - **E-commerce Product Page**
     - Product listing with filters
     - Shopping cart functionality
     - Checkout process
   
   - **Social Media Dashboard**
     - Authentication
     - CRUD operations
     - Real-time updates
   
   - **Task Management App**
     - Drag and drop interface
     - Data persistence
     - User settings
   
   **Learning Resources:**
   - React Documentation
   - React Testing Library docs
   - Kent C. Dodds' blog
   - Redux documentation
   - Epic React by Kent C. Dodds
   - React Router documentation
   - GitHub Learning Lab

   **Practice Platforms:**
   - CodeSandbox
   - Frontend Mentor
   - React Coding Challenges
   - LeetCode Frontend Questions

---