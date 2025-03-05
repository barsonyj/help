## Súgó fájlok

> **Backend programozás és tesztelés**

- React-router-dom ()
- Környezeti változók ([Bpt_environment.txt](https://barsonyj.github.io/help/bpt/Bpt_environment.txt))

> [!NOTE] React-router-dom

 * pnpm install react-router-dom
 * import { createBrowserRouter, RouterProvider } from "react-router-dom";
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
