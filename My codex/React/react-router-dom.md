```Jsx
// HeaderLayout.jsx
const HeaderLayout = () => (
  <>
    <header>
      <nav>{/* Navigation links */}</nav>
    </header>
    <main>
      <Outlet />
    </main>
  </>
);

// routes.js
const router = createBrowserRouter([
  {
    element: <HeaderLayout />,
    errorElement: <ErrorPage />, // ← Thêm error handling
    children: [
    {
       index: true,
       element: <Navigate to="/A" replace />,
      },
      { path: "/", element: <div>Home</div> },
      // ... other routes
    ],
  },
]);

// App.jsx
function App() {
  return <RouterProvider router={router} />;
}
```


