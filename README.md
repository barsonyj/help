## Súgó fájlok

> **Backend programozás és tesztelés**

- React-router-dom ()
- Környezeti változók ([Bpt_environment.txt](https://barsonyj.github.io/help/bpt/Bpt_environment.txt))

> [!NOTE] React-router-dom
> 

 * pnpm install react-router-dom
 * import { createBrowserRouter, RouterProvider } from "react-router-dom";
 * const router = createBrowserRouter([  
     { element: &lt;Layout />, children: [  
       { path: "/", element: &lt;Home /> },  
       { path: "/two", element: &lt;Two /> },  
       { path: "/about", element: &lt;About /> },  
       { path: "*", element: &lt;Notfound /> }  
     ]}  
   ]);  
 * <RouterProvider router={router} />  
   <Outlet />
 * &lt;Link to="/about">About</Link> // rá kell kattintani  
   &lt;Navigate to="/about" /> // nem kell rákattintani  
   const navigate = useNavigate();  
   navigate("/about", { replace: true });  
 * const { pathname, search, hash } = useLocation();  
   const params = useParams(); // path: "/users/:id" + /users/42 -> { id:42 }
