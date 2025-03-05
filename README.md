## Súgó fájlok

> **Backend programozás és tesztelés**

- React-router-dom ()
- Környezeti változók ([Bpt_environment.txt](https://barsonyj.github.io/help/bpt/Bpt_environment.txt))

> [!NOTE]
> **React-router-dom**

* pnpm install react-router-dom
* import { createBrowserRouter, RouterProvider } from "react-router-dom";
* const router = createBrowserRouter([  
  &nbsp;{ element: &lt;Layout />, children: [  
  &nbsp;&nbsp;{ path: "/", element: &lt;Home /> },  
  &nbsp;&nbsp;{ path: "/two", element: &lt;Two /> },  
  &nbsp;&nbsp;{ path: "/about", element: &lt;About /> },  
  &nbsp;&nbsp;{ path: "*", element: &lt;Notfound /> }  
  &nbsp;]}  
  ]);  
* &lt;RouterProvider router={router} />  
  &lt;Outlet />
* &lt;Link to="/about">About</Link> // rá kell kattintani  
  &lt;Navigate to="/about" /> // nem kell rákattintani  
  const navigate = useNavigate();  
  navigate("/about", { replace: true });  
* const { pathname, search, hash } = useLocation();  
  const params = useParams(); // path: "/users/:id" + /users/42 -> { id:42 }

> [!NOTE]
> **Környezeti változók**

* A "process" modul egy Node.js core modul,  
  amit CSAK a node.exe futtatási környezetben tudunk elérni, böngészőben NEM!  
  Egy Vite project a dotenv modul segítségével tud beolvasni környezeti változót,  
  a projektmappa gyökerében lévő .env fájlból, de alapesetben csak a VITE_ előtaggal!
* .env (adjuk meg a .gitignore fájlban!)
   VITE_HOST = "http://localhost:88/"
* const host = import.meta.env.VITE_HOST;

