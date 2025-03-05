## Súgó fájlok

### Backend programozás és tesztelés
- Környezeti változók ([Bpt_environment.txt](https://barsonyj.github.io/help/bpt/Bpt_environment.txt))

### Frontend programozás és tesztelés
- React-router-dom ()

> [!NOTE]
> **BPT / Környezeti változók**

```
* A "process" Node.js core modul tartalmaz egy "env" tulajdonságot,
  amely tartalmazza a beállított környezeti változókat: process.env.VARIABLE;
  Beállítani legegyszerűbben a futtatáskor paraméterben átadott .env fájllal lehet:
  - node --env-file=.env index.js
  - node --env-file-if-exists=.env index.js
  - // VAGY lehet külső modullal is:
    // * pnpm install dotenv
    // * import dotenv from 'dotenv';
    //   dotenv.config();
* .env (adjuk meg a .gitignore fájlban!)
  PORT = 88
* const port = process.env.PORT;
  const port = process.env.PORT || 88;
```

> [!NOTE]
> **FPT / React-router-dom**

```
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
* &lt;RouterProvider router={router} />
  &lt;Outlet />
* &lt;Link to="/about">About</Link> // rá kell kattintani
  &lt;Navigate to="/about" /> // nem kell rákattintani
  const navigate = useNavigate();
  navigate("/about", { replace: true });
* const { pathname, search, hash } = useLocation();
  const params = useParams(); // path: "/users/:id" + /users/42 -> { id:42 }
```
