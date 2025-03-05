### Frontend programozás és tesztelés
- React-router-dom ([ugrás](#fpt_react_router_dom))

<a name="fpt_react_router_dom"></a>
> [!NOTE]
> **FPT / React-router-dom**

```
* pnpm install react-router-dom
* import { createBrowserRouter, RouterProvider } from 'react-router-dom';
* const router = createBrowserRouter([
   { element: <Layout />, children: [
    { path: "/", element: <Home /> },
    { path: "/two", element: <Two /> },
    { path: "/about", element: <About /> },
    { path: "*", element: <Notfound /> }
   ]}
  ]);
* <RouterProvider router={router} />
  <Outlet />
* <Link to="/about">About</Link> // rá kell kattintani
  <Navigate to="/about" /> // nem kell rákattintani
  const navigate = useNavigate();
  navigate("/about", { replace: true });
* const { pathname, search, hash } = useLocation();
  const params = useParams(); // path: "/users/:id" + /users/42 -> { id:42 }
```
