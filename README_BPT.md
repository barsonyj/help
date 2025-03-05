## Backend programozás és tesztelés
- Környezeti változók ([ugrás](#bpt_environment))

<a name="bpt_environment"></a>
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
