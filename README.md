## Súgó fájlok
### Backend programozás és tesztelés
- MySQL ([ugrás](#bpt_mysql))
- Környezeti változók ([ugrás](#bpt_environment))
- Multer ([ugrás](#bpt_multer))
- Vitest ([ugrás](#bpt_vitest))
### Frontend programozás és tesztelés
- React-router-dom ([ugrás](#fpt_react_router_dom))
- Axios ([ugrás](#fpt_axios))
- Firestore ([ugrás](#fpt_firestore))
- Firebase Authentication ([ugrás](#fpt_firebase_auth))
- FormData ([ugrás](#fpt_formdata))
- Vitest ([ugrás](#fpt_vitest))

<a name="bpt_mysql"></a>
> [!NOTE]
> **BPT / MySQL**

```
* pnpm install mysql2
* import mysql from "mysql2/promise";
* con = await mysql.createConnection({ // try-catch
    host: "localhost",
    port: 3306,
    database: "adatbazis",
    user: "root",
    password: ""
  });
* const [ json ] = await con.query(sql); // try-catch
  const [ json ] = await con.execute(sql, [parameterek]); // try-catch
```

<a name="bpt_environment"></a>
> [!NOTE]
> **BPT / Környezeti változók**

```
* A "process" Node.js core modul tartalmaz egy "env" tulajdonságot,
  amely tartalmazza a beállított környezeti változókat: process.env.VARIABLE;
  Beállítani legegyszerűbben a futtatáskor paraméterben átadott .env fájllal lehet:
  - node --env-file=.env index.js
  - node --env-file-if-exists=.env index.js
  // VAGY lehet külső modullal is:
  // * pnpm install dotenv
  // * import dotenv from 'dotenv';
  //   dotenv.config();
* .env (adjuk meg a .gitignore fájlban!)
  PORT = 88
* const port = process.env.PORT;
  const port = process.env.PORT || 88;
```

<a name="bpt_multer"></a>
> [!NOTE]
> **BPT / Multer**

```
* pnpm i multer
* import multer from "multer";
* const upload = multer({ dest: "upload", limits: { fileSize: 8*1024 } }); // v1.0
* const storage = multer.diskStorage({
   destination: (req, file, cb) => cb(null, 'upload'),
   filename: (req, file, cb) => cb(null, file.originalname)
  });
  const upload = multer({ storage:storage, limits: { fileSize: 8*1024 } }); // v2.0
* const storage = multer.memoryStorage();
  const upload = multer({ storage:storage }); // v3.0
* app.post("/upload", upload.single("fieldname"), uploadFajl);
  // console.log(req.file); -> fieldname:, originalname:, mimetype:, filename:, size:, ...
  upload.none() // Nem dolgozza fel a fájlokat
  upload.single("fieldname") // Csak a "fieldname" paraméterben kapottat -> req.file
  upload.array("fieldname", maxCount) // Csak a "fieldname" paraméterben kapottakat -> req.files
  upload.any() // Az összes fájlt feldolgozza -> req.files
* app.use(express.static('upload'));
* import fs from 'fs/promises';
  const files = await fs.readdir('upload');
```

<a name="bpt_vitest"></a>
> [!NOTE]
> **BPT / Vitest**

```
* pnpm install -D vitest
* eredeti.js -> eredeti.test.js:
  import { describe, expect, test } from "vitest";
  import { fuggvenyneve } from "./eredeti.js";  
* describe("Tesztcsoport szöveg", () => {
    test("Teszt szöveg", () => {
      expect(fuggvenyneve(parameterek)).toBe(elvartertek);
    });
  });
* .not.toBe(elvartertek);
  .toBeTruthy(); .toBeFalsy(); .toBeNull();
  .toEqual(objektum);
* beforeEach(() => {}); afterEach(() => {}); // minden 'test' előtt illetve után
  beforeAll(() => {}); afterAll(() => {}); // a 'describe' elején illetve végén
* pnpm vitest
```

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
  <input type="text" onKeyDown={e => { if (e.keyCode == 13) fxHaEnter(); }} />
* const { pathname, search, hash } = useLocation();
  const params = useParams(); // path: "/users/:id" + /users/42 -> { id:42 }
```

<a name="fpt_axios"></a>
> [!NOTE]
> **FPT / Axios**

```
* pnpm install axios
* const response = await axios.get("http://localhost:88/users");
  const { data } = await axios.get("http://localhost:88/users");
* axios.get(url);
  axios.post(url, body);
  axios.put(url, body);
  axios.patch(url, body);
  axios.delete(url);
* response = {
    data: {},
    status: 200,
    statusText: 'OK',
    headers: {},
    config: {},
    request: {}
  };
```

<a name="fpt_firestore"></a>
> [!NOTE]
> **FPT / Firestore**

```
* pnpm install firebase
* import { initializeApp } from "firebase/app";
  import { getFirestore } from "firebase/firestore"; // NEM /lite!!!
  import { firebaseConfig } from "/firebaseConfig.js"; // .gitignore!
  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);
* const snap = await getDoc(doc(db, "collectionID", "documentID"));
  const snap = await getDocs(collection(db, "collectionID"));
  const snap = await getDocs(query(collection(db, "collectionID"), where("field", "==", value)), orderBy("field"));
  const lst = snap.docs.map(doc => ({ ...doc.data(), id:doc.id }));
  let date = new Date(timestamp.seconds * 1000 + timestamp.nanoseconds / 1000000); // .toLocaleString();
* await setDoc(doc(db, "collectionID", "documentID"), {field:value, field:value}); // ID!
  await addDoc(collection(db, "collectionID"), {field:value, field:value}); // AutoID
  let ido = Timestamp.now(); // import { Timestamp } from 'firebase/firestore';
  // Timestamp.now() => { seconds: 1767956338, nanoseconds: 745000000 } // még .toDate(); <- string
* await updateDoc(doc(db, "collectionID", "documentID"), {field:value});
* await deleteDoc(doc(db, "collectionID", "documentID"));
* useEffect(() => {
    // const unsub = onSnapshot(doc(db, "collectionID", "documentID"), (snap) => {
    const unsub = onSnapshot(collection(db, "collectionID"), (snap) => {
      setFunction(snap.docs.map(doc => ({ ...doc.data(), id:doc.id })));
    });
    return unsub;
  },[]);
```

<a name="fpt_firebase_auth"></a>
> [!NOTE]
> **FPT / Firebase Authentication**

```
* pnpm install firebase
* import { initializeApp } from "firebase/app";
  import { firebaseConfig } from "/firebaseConfig.js"; // .gitignore!
  const app = initializeApp(firebaseConfig);
* import { getAuth } from "firebase/auth";
  const auth = getAuth(app);
  // const user = auth.currentUser; de inkább useEffect!
* createUserWithEmailAndPassword(auth, email, password)
* await signInWithEmailAndPassword(auth, email, password);
  await signInWithPopup(auth, new GoogleAuthProvider());
* const [user, setUser] = useState({});
  useEffect(() => {
    const unsube = onAuthStateChanged(auth, (currentUser) => setUser(currentUser));
    return unsub;
  },[]);
* {user ? <Valami /> : <Login />}
* await signOut(auth);
```

<a name="fpt_formdata"></a>
> [!NOTE]
> **FPT / FormData**

```
* <input id='fajl' type='file' accept='.png,.jpg' multiple /> // .hide { display: none; }
  <label htmlFor='fajl'>Megnyitás</label>
* onChange={e => setFajl(e.target.files[0])}
  onChange={e => setFajlok([...e.target.files])}
* const formData = new FormData();
  formData.append('fajl', fajl);
  const resp = await fetch('http://localhost:88/upload', { method: 'POST', body: formData });
```

<a name="fpt_vitest"></a>
> [!NOTE]
> **FPT / Vitest**

```
* pnpm i -D vitest jsdom@26 @testing-library/react @testing-library/jest-dom
  + vite.config.js (defineConfig részbe) -> test: { environment: 'jsdom' }
* import Komponens from "./Komponens";
  render(<Komponens />); // a screen objektumban "jelenik" meg!
  screen.debug(); // a cleanup(); parancs törli!
* screen.getBy*: pontosan EGY elem (különben HIBÁT dob)
  screen.getAllBy*: TÖMBÖT ad vissza, legalább EGY elem (különben HIBÁT dob)
  screen.queryBy*: legfeljebb EGY (az ELSŐ passzoló) elem (vagy null, vagy HIBÁT dob)
  screen.queryAllBy*: TÖMBÖT ad vissza, ami ÜRES, ha nem talál egyet sem
  screen.findBy*: aszinkron (promise!), pontosan EGY elem (különben HIBÁT dob)
  screen.findAllBy*: aszinkron (promise!), TÖMBÖT ad vissza, legalább egy elem (különben HIBÁT dob)
* ByRole('type', {name: /szöveg/i}): adott típusú elemet keres, megadott felirattal
  // type: button, checkbox, radio, option, img, table, form, ...
  ByLabelText: űrlapelemekhez, amihez van label tag (vagy bármi, amihez van aria-label)
  ByPlaceholderText: űrlapelemekhez, amihez van placeholder tulajdonság
  ByText: olyan elem, amelyikben PONTOSAN a megadott szöveg van (innerText!)
  // VAGY regex (idézőjel NÉLKÜL!): screen.getByText(/szöveg/i) = szövegrészt keres ignore case
  ByDisplayValue: űrlapelemekhez, aminek van value tulajdonsága
  ByAltText: bármihez, aminek van alt tulajdonsága (pl. képek)
  ByTitle: bármihez, aminek van title tulajdonsága (pl. képek, ikonok)
  ByTestId: data-testid tulajdonsággal rendelkező elem keresése
* import "@testing-library/jest-dom/vitest";
  import * as matchers from "@testing-library/jest-dom/matchers";
  expect.extend(matchers);
  // .toBeInTheDocument(); .toBeVisible(); .toBeDisabled(); .toBeEnabled(); .toBeChecked();
  // .toHaveValue(value); .toHaveAttribute(attributename, value); .toHaveClass(classname);
* pnpm vitest
```
