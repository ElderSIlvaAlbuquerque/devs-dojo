# React - Orange Belt Lessons

## Lesson 1: React Router

### Core Concepts
- BrowserRouter vs HashRouter
- Route components
- useParams, useNavigate, useLocation
- Nested routes and Outlet
- Protected routes

### Implementation
```jsx
import { BrowserRouter, Routes, Route, Navigate } from 'react-router-dom';

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/products/:id" element={<ProductDetail />} />
        <Route path="/dashboard" element={
          <ProtectedRoute><Dashboard /></ProtectedRoute>
        } />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## Lesson 2: Context API

### State Management
```jsx
const AuthContext = createContext();

function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  
  const login = (credentials) => {
    // Login logic
    setUser(userData);
  };
  
  return (
    <AuthContext.Provider value={{ user, login }}>
      {children}
    </AuthContext.Provider>
  );
}

// Usage
function Profile() {
  const { user } = useContext(AuthContext);
  return <div>{user.name}</div>;
}
```

---

## Lesson 3: Custom Hooks

### Creating Reusable Logic
```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);
  
  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then(setData)
      .catch(setError)
      .finally(() => setLoading(false));
  }, [url]);
  
  return { data, loading, error };
}
```

---

## Lesson 4: Performance Optimization

### Memoization
```jsx
// Memoize expensive calculations
const expensiveValue = useMemo(() => {
  return computeExpensiveValue(a, b);
}, [a, b]);

// Memoize callback functions
const handleClick = useCallback(() => {
  doSomething(a);
}, [a]);

// Memoize components
const MemoizedComponent = React.memo(Component);
```

---

## Lesson 5: Testing with React Testing Library

### Writing Tests
```jsx
import { render, screen, fireEvent } from '@testing-library/react';

test('button click increments counter', () => {
  render(<Counter />);
  const button = screen.getByRole('button');
  fireEvent.click(button);
  expect(screen.getByText('Count: 1')).toBeInTheDocument();
});
```

---

These lessons cover essential React patterns for building production applications!
