# Documentació de Desplegament: Servidor Hertzel

**Projecte:** TR1 - Type Racer Royale
**Data de Desplegament:** 17/12/2025
**Responsables:** Equip de Desenvolupament

## 1. Accés al Servidor (Hertzel)

Per accedir al servidor de desplegament, utilitzem les següents credencials i mètodes d'accés segur:

*   **Host:** `hertzel.inspedralbes.cat` (Exemple)
*   **Protocol:** SSH
*   **Usuari:** `alumne` (o l'assignat)
*   **Mètode d'Autenticació:** Clau Pública SSH (`id_rsa.pub`)
    *   *Nota: La clau privada es troba distribuïda de manera segura entre els membres autoritzats de l'equip.*

### Com connectar-se:
```bash
ssh alumne@hertzel.inspedralbes.cat
```

## 2. Arquitectura del Desplegament

El projecte es desplega utilitzant contenidors Docker per garantir la consistència entre entorns.

*   **Frontend:** Servit via Nginx (port 80/443).
*   **Backend:** Node.js API (port 3000).
*   **Base de Dades:** MySql/MariaDB (port 3306).

### Estructura de fitxers al servidor:
```
/home/alumne/deploy/
├── docker-compose.yml
├── .env
└── data/
```

## 3. Procediment de Desplegament Automàtic (CI/CD)

El flux de treball està configurat per desplegar automàticament quan es fa un merge a la branca `main`.

1.  **GitHub Actions:** Detecta el `push` a `main`.
2.  **Build:** Construeix les imatges de Docker.
3.  **Deploy:**
    *   Es connecta via SSH a Hertzel.
    *   Fa `git pull` dels últims canvis.
    *   Reinicia els contenidors amb:
        ```bash
        docker-compose down
        docker-compose up -d --build
        ```

## 4. Variables d'Entorn (.env)
*El fitxer .env no es puja al repositori per seguretat. S'ha de crear manualment al servidor.*

```env
DB_HOST=mysql
DB_USER=admin
DB_PASS=secret_password_here
PORT=3000
```
