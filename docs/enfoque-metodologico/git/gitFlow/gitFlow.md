# Flujo de Trabajo Diario con Git y GitHub

## Introducción 
Este flujo describe las buenas prácticas al trabajar con Git y GitHub, desde la creación de una rama `feature` para desarrollar una nueva funcionalidad, hasta la creación de un pull request para fusionar cambios en producción. Los ambientes definidos son:

- **`main`:** Representa el ambiente productivo. Los cambios aquí deben estar completamente probados y listos para desplegar.
- **`hotfix`:** Usada para resolver errores críticos detectados en producción.
- **`release`:** Rama utilizada para preparar una versión para su despliegue. Permite realizar pruebas finales antes de integrarla en `main`.
- **`develop`:** Contiene el código en desarrollo que aún no está listo para producción. Aquí se integran las ramas `feature`.
- **`feature/<id-jira>`:** Usada para desarrollar nuevas funcionalidades. El nombre de la rama debe incluir el ID del ticket de Jira para facilitar el seguimiento.

---

## Personal Access Token (PAT)

Un PAT es una clave segura y específica para tu entorno de desarrollo, que te permite autenticarte sin exponer tu contraseña principal. Puedes limitarle los permisos (por ejemplo, solo para leer o escribir en repositorios) y establecer una fecha de caducidad, lo que lo hace mucho más seguro que tu contraseña.

## Cómo agregar el PAT a Git

La primera vez que realices una operación de Git que necesite conectarse al repositorio remoto desde Visual Studio Code (como un git pull, git push o git clone), se te pedirá que te autentiques.

1. Genera tu PAT: Primero, ve a la configuración de tu cuenta en la web (GitHub, GitLab, etc.) y crea un nuevo token.

2. Copia el token: Asegúrate de copiar el token en ese momento, ya que no podrás verlo de nuevo.

3. Pega el token: Cuando Visual Studio Code te pida la contraseña para autenticarte, en lugar de tu contraseña principal, pega el Personal Access Token.

Una vez hecho esto, el gestor de credenciales de Git almacenará el token de forma segura en tu sistema, y no necesitarás volver a ingresarlo para futuras interacciones.


#### Para configurar un Personal Access Token (PAT) en GitHub, sigue estos pasos:

1. Accede a la Configuración de tu Cuenta
Inicia sesión en tu cuenta de GitHub.

-  Haz clic en tu foto de perfil en la esquina superior derecha de la página.

- En el menú desplegable, selecciona Settings (Configuración).

2. Ve a la Sección de Tokens
En la barra lateral izquierda, busca y haz clic en Developer settings (Configuración de desarrollador).

- En el nuevo menú lateral, selecciona Personal access tokens (Tokens de acceso personal).

- Luego, haz clic en Tokens (classic).

3. Genera un Nuevo Token
Haz clic en el botón Generate new token (classic) (Generar nuevo token (clásico)).

- Te pedirá que vuelvas a ingresar tu contraseña para confirmar tu identidad.

- Ahora, completa los siguientes campos:

- Note: Dale un nombre descriptivo a tu token, por ejemplo, "VS Code - Mi PC".

- Expiration: Elige una fecha de vencimiento. Te recomiendo una duración de 30 o 90 días por seguridad. Si expira, simplemente tendrás que generar uno nuevo.

- Select scopes: Aquí, defines los permisos del token. Para el uso común con Git, activa la casilla de repo para tener acceso completo a tus repositorios.

4. Guarda y Copia el Token
Haz clic en el botón verde Generate token (Generar token) al final de la página.

!!! TIP  En la siguiente pantalla, se mostrará el token por única vez. Cópialo de inmediato y guárdalo en un lugar seguro (como un gestor de contraseñas) o pégalo directamente en Visual Studio Code.


Una vez que cierres esta página, ya no podrás ver el token. Si lo pierdes, tendrás que generar uno nuevo.









## Flujo de Trabajo

### 1. Crear una Rama `feature`
- Asegúrate de estar en la rama `develop` (o la rama base según corresponda):
```bash
   git checkout develop
   git pull origin develop
```
- Crea y cambia a una nueva rama `feature`:
```bash
   git checkout -b feature/<id-ticketJira>
```
- Comienza a desarrollar la funcionalidad requerida.

### 2. Realizar Cambios y Commits
- Verifica los cambios realizados:
```bash
   git status
```
- Selecciona los archivos para agregar al área de staging:
```bash
   git add archivo1 archivo2
   # O de forma interactiva:
   git add -i
```
- Realiza un commit con una descripción clara:
```bash
   git commit -m "[<id-ticketJira>] Implementación de nueva funcionalidad."
```
- Repite este paso hasta completar la funcionalidad.

### 3. Actualizar la rama `feature` con `develop`

Antes de pedir revisión, traé los últimos cambios de `develop` a tu rama. Así el PR nace sin quedar atrás.

```bash
git checkout feature/<id-ticketJira>
git fetch origin
git merge origin/develop
```

Si hay conflictos, resolvelos en la rama `feature`, hacé commit y seguí. No fusionés `feature` en `develop` en tu máquina: eso lo hace el Pull Request.

### 4. Subir la rama `feature` al remoto

```bash
git push -u origin feature/<id-ticketJira>
```

La primera vez usá `-u` para dejar el tracking. Después alcanza con `git push`.

### 5. Crear un Pull Request en GitHub

- Abrí el repositorio en GitHub.
- Creá un Pull Request **desde** `feature/<id-ticketJira>` **hacia** `develop`.
- La base es `develop`. El compare es tu `feature`. Nunca al revés.

Incluí en la descripción:

- Qué funcionalidad añade.
- Enlace al ticket de Jira.
- Pruebas hechas y dependencias.

Asigná revisores antes de pedir el merge.

!!! warning "Dirección del PR"
    El PR de una funcionalidad va de `feature/<id>` → `develop`. El PR a producción (por ejemplo este sitio de docs) va de `develop` → `main`. No abras un PR de `develop` hacia `feature`.

### 6. Revisar y fusionar el Pull Request

- Los revisores validan y aprueban en GitHub.
- El merge se hace **en GitHub**, sobre el PR, hacia `develop`.
- Después del merge, actualizá tu `develop` local y borré la rama `feature`:

```bash
git checkout develop
git pull origin develop
git branch -d feature/<id-ticketJira>
git push origin --delete feature/<id-ticketJira>
```

### 7. Crear una rama `release` (cuando proceda)

Si el conjunto de cambios en `develop` está listo para pruebas finales:

```bash
git checkout develop
git pull origin develop
git checkout -b release/<version>
git push -u origin release/<version>
```

Aplicá ajustes menores en esa rama. Cuando esté aprobada, abrí un PR de `release/<version>` hacia `main` (y otro hacia `develop` si hace falta reintegrar hotfixes de la release).

### 8. Integración en `main`

Cuando una versión está lista para producción, el merge a `main` se hace por Pull Request (no con `git push` directo a `main` desde la notebook).

En este repositorio de documentación el flujo habitual es: trabajo en `feature` → PR a `develop` → PR de `develop` a `main` → GitHub Actions publica el sitio.

---




## Notas y Buenas Prácticas
- **Actualización constante:** Antes de trabajar en una rama, asegúrate de sincronizarla con su rama base para evitar conflictos.
- **Commits pequeños y descriptivos:** Facilita la revisión y depuración.
- **Uso de etiquetas Jira:** Incluye siempre el ID del ticket de Jira en el nombre de la rama y en los mensajes de commit.
- **Revisión de código:** Realiza revisiones exhaustivas para mantener la calidad del código.
- **Pruebas:** Antes de fusionar en `main`, asegúrate de que todas las pruebas estén completas y aprobadas.