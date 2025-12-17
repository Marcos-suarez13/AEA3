# Documentació de Desplegament: Servidor Hertzel

**Projecte:** TR1 - Type Racer Royale
**Data de Desplegament:** 17/12/2025
**Responsables:** Marcos Suarez
**URL:** https://github.com/Marcos-suarez13/AEA3

## 1. Accés al Servidor (Hertzel)

Per accedir al servidor de desplegament, utilitzem les següents credencials i mètodes d'accés segur:

*   **Host:** `hertzel.inspedralbes.cat`
*   **Port:** `22` (SSH estàndard)
*   **Protocol:** SSH
*   **Usuari:** `msuarez_2daw`
*   **Mètode d'Autenticació:** Clau Pública SSH (RSA 4096 bits)
    *   **Clau pública:** `~/.ssh/id_rsa_hertzel.pub`
    *   *Nota: La clau privada es troba emmagatzemada de manera segura al keychain local i no es comparteix mai.*

### Com connectar-se:
```bash
ssh -i ~/.ssh/id_rsa_hertzel msuarez_2daw@hertzel.inspedralbes.cat
```

## 2. Arquitectura del Desplegament

El projecte es desplega utilitzant contenidors Docker per garantir la consistència entre entorns.

*   **Frontend:** Servit via Nginx (port 80/443).
*   **Backend:** Node.js API (port 3000).
*   **Base de Dades:** MySql/MariaDB (port 3306).

### Estructura de fitxers al servidor:
```
/home/msuarez_2daw/tr1-production/
├── docker-compose.yml
├── .env
├── data/
│   └── mysql/
├── logs/
└── backups/
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
# Base de dades
DB_HOST=mysql
DB_PORT=3306
DB_NAME=typing_game
DB_USER=tr1_user
DB_PASS=Tr1P4ssw0rd!2024

# Backend
PORT=3000
NODE_ENV=production

# Frontend
VITE_API_URL=https://hertzel.inspedralbes.cat/api
```
