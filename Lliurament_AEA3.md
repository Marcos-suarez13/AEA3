# AEA 3: Desplegament Continu i Control de Versions Professional

**Alumne/Grup:** Grup 4

---

## 1. Enllaç al Repositori GitHub

El projecte està gestionat correctament amb control de versions. L'historial de commits reflecteix l'evolució del projecte.

*   **Repositori:** [https://github.com/inspedralbes/tr1-type-racer-royale-grup-4-1](https://github.com/inspedralbes/tr1-type-racer-royale-grup-4-1)

---

## 2. Documentació de Desplegament a Hertzel

S'ha generat un document específic que detalla com accedir al servidor Hertzel i el procediment de desplegament utilitzat per l'equip.

*   [Veure Documentació de Desplegament](./Documentacio_Desplegament.md)

*(Adjunteu aquí el fitxer Documentacio_Desplegament.md o el seu contingut si es demana un únic document)*

---

## 3. Qualitat del Codi (SonarQube) - Qualificació A

S'ha analitzat el codi i s'han realitzat diverses refactoritzacions per eliminar "code smells", bugs i vulnerabilitats, aconseguint una qualificació global d'**A**.

*(Inserir aquí captura de pantalla de SonarQube amb la qualificació A)*

### Modificacions Realitzades (3 Exemples):

Per aconseguir aquesta qualificació, hem aplicat els següents canvis:

#### 1. Eliminació de "Console Log" en Producció (`server.js`)
*   **Problema:** L'ús de `console.log` per depurar embrutava la sortida del servidor i podia exposar informació sensible. SonarQube ho marca com un "Code Smell" de mantenibilitat.
*   **Solució:** S'han eliminat els `console.log` innecessaris de les rutes de l'API o s'han substituït per un sistema de logging adequat (si s'escau).
    *   *Fitxer:* `game/backend/server.js`

#### 2. Ús d'Igualtat Estricta (`===`) (`server.js`)
*   **Problema:** Es detectaven comparacions febles amb `==` (ex: `time == null`), que poden portar a errors de tipus inesperats en JavaScript.
*   **Solució:** S'han substituït per comparacions estrictes (`===`) per garantir que tant el valor com el tipus coincideixen, millorant la fiabilitat del codi.
    *   *Canvi:* De `if (!username || time == null ...)` a `if (!username || time === null ...)`

#### 3. Neteja de Codi Mort (Dead Code) (`App.vue`)
*   **Problema:** Hi havia importacions de components i declaracions de variables (`ref`) que no s'utilitzaven mai en el codi, augmentant la mida del bundle innecessàriament.
*   **Solució:** S'ha eliminat la importació del component `Config` i la variable reactiva `showConfig` que no tenien cap ús.
    *   *Fitxer:* `game/frontend/src/App.vue`
