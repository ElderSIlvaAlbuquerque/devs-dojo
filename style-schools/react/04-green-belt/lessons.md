# React - Green Belt Lessons

## Lesson 1: Next.js and Server-Side Rendering

### Core Concepts
- File-based routing
- SSR vs SSG vs ISR
- API routes
- Middleware
- Image optimization

### Implementation
```jsx
// pages/products/[id].js
export async function getStaticProps({ params }) {
  const product = await fetchProduct(params.id);
  return {
    props: { product },
    revalidate: 60, // ISR: Revalidate every 60 seconds
  };
}

export async function getStaticPaths() {
  const products = await fetchAllProducts();
  return {
    paths: products.map(p => ({ params: { id: p.id } })),
    fallback: 'blocking',
  };
}
```

---

## Lesson 2: TypeScript with React

### Typing Components
```tsx
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
  disabled?: boolean;
}

const Button: React.FC<ButtonProps> = ({ 
  label, 
  onClick, 
  variant = 'primary',
  disabled = false 
}) => {
  return (
    <button 
      onClick={onClick}
      disabled={disabled}
      className={`btn btn-${variant}`}
    >
      {label}
    </button>
  );
};
```

---

## Lesson 3: Advanced State Management

### Redux Toolkit
```tsx
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';

export const fetchUsers = createAsyncThunk(
  'users/fetchUsers',
  async () => {
    const response = await api.get('/users');
    return response.data;
  }
);

const usersSlice = createSlice({
  name: 'users',
  initialState: { data: [], loading: false },
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchUsers.pending, (state) => {
        state.loading = true;
      })
      .addCase(fetchUsers.fulfilled, (state, action) => {
        state.data = action.payload;
        state.loading = false;
      });
  },
});
```

---

## Lesson 4: Performance Optimization

### Bundle Analysis
```bash
# Analyze bundle size
npm run build -- --analyze

# Code splitting
const LazyComponent = lazy(() => import('./LazyComponent'));

// Virtualization for long lists
import { FixedSizeList } from 'react-window';
```

---

## Lesson 5: Accessibility (a11y)

### Best Practices
```jsx
// Semantic HTML
<nav aria-label="Main navigation">
  <button 
    aria-expanded={isOpen}
    aria-controls="menu"
  >
    Menu
  </button>
</nav>

// Keyboard navigation
const handleKeyDown = (e) => {
  if (e.key === 'Enter' || e.key === ' ') {
    handleClick();
  }
};

// Focus management
const firstInputRef = useRef();
useEffect(() => {
  firstInputRef.current?.focus();
}, []);
```

---

## Lesson 6: Testing Strategies

### Integration Tests
```tsx
import { render, screen, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';

test('user can complete checkout flow', async () => {
  render(<App />);
  
  await userEvent.click(screen.getByText('Add to Cart'));
  await userEvent.click(screen.getByText('Checkout'));
  
  await userEvent.type(screen.getByLabelText('Name'), 'John Doe');
  await userEvent.click(screen.getByText('Submit'));
  
  await waitFor(() => {
    expect(screen.getByText('Order confirmed')).toBeInTheDocument();
  });
});
```

---

These advanced lessons prepare you for building production React applications!
