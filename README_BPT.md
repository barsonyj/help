## Backend programozás és tesztelés
- MySQL ([ugrás](#bpt_mysql))
- Firestore ([ugrás](#bpt_firestore))
- Firebase Authentication ([ugrás](#bpt_firebase_auth))
- Környezeti változók ([ugrás](#bpt_environment))

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

<a name="bpt_firestore"></a>
> [!NOTE]
> **BPT / Firestore**

```
* pnpm install firebase
* import { initializeApp } from "firebase/app";
  import { getFirestore } from "firebase/firestore"; // NEM /lite!!!
  import { firebaseConfig } from "/firebaseConfig.js"; // .gitignore!
  const app = initializeApp(firebaseConfig);
  const db = getFirestore(app);
* const snap = await getDoc(doc(db, "collectionID", "documentID"));
  if (snap.exists()) console.log(snap.data());
  const snap = await getDocs(collection(db, "collectionID"));
  const lst = snap.docs.map(doc => ({ ...doc.data(), id:doc.id }));
  const snap = await getDocs(query(collection(db, "collectionID"), where("field", "==", value)), orderBy("field"));
  const lst = snap.docs.map(doc => ({ ...doc.data(), id:doc.id }));
* await setDoc(doc(db, "collectionID", "documentID"), {field:value, field:value}); // ID!
  await addDoc(collection(db, "collectionID"), {field:value, field:value}); // AutoID
* await updateDoc(doc(db, "collectionID", "documentID"), {field:value});
* await deleteDoc(doc(db, "collectionID", "documentID"));
* useEffect(() => {
    const unsub = onSnapshot(collection(db, 'collectionID'), (snap) => {
      setFunction(snap.docs.map(doc => ({ ...doc.data(), id:doc.id })));
    });
    return unsub;
  },[]);
```

<a name="bpt_environment"></a>
> [!NOTE]
> **BPT / Firebase Authentication**

```
* pnpm install firebase
* import { initializeApp } from "firebase/app";
  import { firebaseConfig } from "/firebaseConfig.js"; // .gitignore!
  const app = initializeApp(firebaseConfig);
* import { getAuth } from "firebase/auth";
  const auth = getAuth(app);
* await signInWithEmailAndPassword(auth, email, password);
  await signInWithPopup(auth, new GoogleAuthProvider());
* const [user, setUser] = useState({});
  const unsubscribe = onAuthStateChanged(auth, (currentUser) => setUser(currentUser));
  {user ? <Valami /> : <Login />}
* await signOut(auth);
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
