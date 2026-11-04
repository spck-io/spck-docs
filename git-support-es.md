# <a name="git-support"></a>Compatibilidad con Git

Spck admite Git en proyectos locales de Android e iOS, en el navegador y en proyectos remotos mediante Spck CLI. Esta guía cubre credenciales, pull requests, inspección de commits, resolución de conflictos y limitaciones de las plataformas.

La integración Git básica, el historial de commits y la resolución de conflictos están disponibles en la versión gratuita. La [integración Git mejorada](#enhanced-git-integration) añade gestión de pull requests y diffs de archivos de commits.

## <a name="git-credentials"></a>Credenciales Git y pull requests

Abre **Git menu → Git Credentials**, selecciona tu proveedor y guarda su token de acceso. Los enlaces de configuración y ayuda se abren en otra pestaña para que puedas volver a Spck y pegar el token.

| Proveedor | Configuración del token | Permisos para Git y pull requests |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">Crear token de GitHub</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">Guía de configuración</a> | Selecciona el repositorio. El enlace preselecciona **Contents: Read and write**, **Pull requests: Read and write** y **Metadata: Read**. |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">Crear token de GitLab</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">Guía de configuración</a> | El enlace preselecciona el ámbito `api` para merge requests. |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">Crear token API</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">Guía de configuración</a> | Elige **Create API token with scopes**, selecciona **Bitbucket** y marca manualmente `read:repository:bitbucket`, `write:repository:bitbucket`, `read:pullrequest:bitbucket` y `write:pullrequest:bitbucket`. La API usa el correo de tu cuenta Atlassian. |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">Guía para crear un PAT</a> | Abre **User settings → Personal access tokens → New Token** en tu organización, selecciona la organización y marca manualmente **Code (Read & write)**. |

Para crear una pull request, haz commit y push de la rama de origen y abre **Git menu → Create PR**. Elige el remoto, las credenciales y una rama de destino diferente, y escribe el título y la descripción. **Generate with AI** puede redactar el mensaje a partir de los cambios confirmados desde el ancestro común de las ramas; primero haz fetch de la rama de destino. Revisa el borrador antes de elegir **Create PR**. GitLab crea una merge request.

Crear y gestionar pull requests es una **función Premium** incluida en la [integración Git mejorada](#enhanced-git-integration). Lite la incluye con la compra única. En la aplicación completa, inicia sesión con una suscripción Supporter, Gold o Node activa, o con la cuenta que posee el desbloqueo de por vida del terminal Spck for NodeJS.

## <a name="pull-request-management"></a>Gestión de pull requests (Premium)

Gestiona pull requests sin salir del editor. Los remotos compatibles son **GitHub.com, GitLab.com, Bitbucket Cloud y Azure DevOps**; GitLab las llama merge requests.

1. Abre un proyecto Git y añade el token en **Git menu → Git Credentials** con los permisos indicados arriba.
2. Abre **Branches menu → Pull Requests** y elige remoto y credenciales para ver las solicitudes abiertas.
3. Selecciona una solicitud para ver título, descripción, autor, ramas de origen y destino y estado.
4. Selecciona un archivo modificado para revisar su diff de solo lectura antes de fusionar.
5. Usa **Merge** para fusionar una solicitud apta o **Close** para cerrarla sin fusionar. Siguen aplicándose revisiones, comprobaciones, permisos del token y reglas de las ramas; los borradores y las solicitudes con conflictos no pueden fusionarse desde este diálogo.

Usa **Refresh** para actualizar la lista tras los cambios en el proveedor. Los detalles también enlazan al proveedor para revisiones, comprobaciones y otras acciones.

Para iniciar una solicitud, usa **Git menu → Create PR** como se explica arriba. Si falta subir la rama de origen, el diálogo ofrece **Push** antes de crearla. La redacción opcional con IA usa el servicio configurado y sus límites; es independiente del acceso a pull requests incluido en Lite.

Si la creación falla por permisos, usa el enlace del proveedor para crear o actualizar el token, guárdalo en **Git Credentials** e inténtalo de nuevo. Se conserva el borrador de la PR.

## <a name="enhanced-git-integration"></a>Integración Git mejorada

La integración Git mejorada añade dos herramientas para revisar y compartir cambios:

- **Gestión de pull requests:** crear solicitudes, consultar las abiertas, revisar archivos y diffs, y fusionar o cerrar solicitudes. Consulta [Gestión de pull requests](#pull-request-management) para configurar y usar la función.
- **Inspección de commits:** revisar archivos modificados y sus diffs sin alterar los archivos de trabajo.

Abre **History** en el panel Git y selecciona un commit para ver archivos añadidos, modificados y eliminados. Selecciona un archivo para abrir un diff de solo lectura respecto al primer padre. En el primer commit se compara con un árbol vacío. El visor usa versiones confirmadas; los cambios sin confirmar no afectan al diff. Los archivos binarios no se muestran como diffs de texto.

También puedes mantener pulsada una entrada del historial, o hacer clic derecho, y elegir **View Commit**.

La integración Git mejorada se incluye con:

- **Spck Editor Lite:** desbloqueada permanentemente con la compra única, sin iniciar sesión.
- **Compra de por vida del terminal Spck for NodeJS:** desbloqueada para siempre para la cuenta propietaria; requiere iniciar sesión.
- **Suscripciones Supporter, Gold o Node:** desbloqueada mientras la suscripción esté activa; requiere iniciar sesión.

La integración Git básica y el historial siguen disponibles en la versión gratuita. Consulta los [precios](https://spck.io/pricing) para conocer los planes.

## <a name="merge-conflict-resolution"></a>Resolver conflictos de fusión

El visor de diffs también ayuda a resolver conflictos en los archivos de trabajo. Forma parte de la integración Git básica y no requiere Premium.

1. Abre un archivo con conflictos desde la lista de cambios Git.
2. Para cada conflicto, elige **Accept Current**, **Accept Incoming** o **Accept Both**. También puedes combinar los cambios editando el archivo manualmente.
3. Revisa el resultado. Cuando no queden marcadores de conflicto, selecciona **Resolve** en el visor para añadir el archivo resuelto al área de preparación.
4. Resuelve los demás archivos y confirma la fusión.

En dispositivos táctiles, mantén pulsado un archivo o una entrada Git para abrir el menú contextual. Las letras de estado Git complementan los colores de los nombres para identificar los cambios.

## <a name="git-limitations"></a>Limitaciones de Git

### <a name="git-limitations-overview"></a>Descripción general

La implementación de Git depende de dónde se guarda el proyecto y de la versión de Spck:

| Entorno | Implementación de Git | Restricciones principales |
| --- | --- | --- |
| Aplicaciones Android e iOS, incluidas Lite y Spck for NodeJS | **libgit2** compilado de forma nativa para proyectos locales | Requiere un proyecto en el almacenamiento del dispositivo; siguen aplicándose sus recursos y restricciones del sistema de archivos. |
| Navegador y editor integrado | [isomorphic-git](https://isomorphic-git.org/) en JavaScript | Límites de memoria, almacenamiento y red del navegador. |
| Proyectos remotos mediante Spck CLI | **Binario Git** del equipo anfitrión | Usa recursos, sistema de archivos, credenciales e instalación de Git del anfitrión. |

Las versiones móviles actuales usan Git nativo en lugar del motor del navegador. Si aparece **Native Git requires a device folder**, mueve el proyecto al almacenamiento del dispositivo. Los proyectos guardados solo en la base de datos del navegador del editor no pueden usar el cliente Git nativo móvil.

La gestión de pull requests llama directamente a la API del proveedor con el token guardado en **Git Credentials**. No usa cookies de sesión del navegador ni almacena respuestas en caché, de modo que una actualización recupera el estado y las ramas más recientes. Consulta [Credenciales Git y pull requests](#git-credentials) para los permisos y [Gestión de pull requests](#pull-request-management) para los proveedores y acciones compatibles.

### <a name="git-limitations-memory"></a>Restricciones de memoria

- Git nativo en Android e iOS opera fuera del motor Git de JavaScript. Las restricciones de ese motor no son un límite fijo de Git móvil.
- Git nativo sigue necesitando memoria y disco disponibles. Los repositorios o archivos pack grandes pueden superar los recursos del dispositivo y causar errores o que el sistema cierre la aplicación.
- Git del navegador sigue limitado por la memoria JavaScript y el almacenamiento del navegador. Los archivos pack grandes pueden necesitar mucha memoria y hacer fallar la clonación o la descarga.

> 💡 **Consejo:** Para repositorios grandes, usa clones superficiales cuando sea posible o trabaja con una parte más pequeña del repositorio.

### <a name="git-limitations-symlinks"></a>Compatibilidad con enlaces simbólicos

- El almacenamiento del navegador y la capa del sistema de archivos del dispositivo usan **enlaces simbólicos emulados** para repositorios con enlaces.
- Cambiar a libgit2 en móviles no elimina las restricciones del sistema de archivos ni garantiza enlaces simbólicos reales del sistema operativo.
- Los enlaces emulados pueden comportarse de forma diferente con herramientas de compilación, gestores de paquetes o scripts que esperan enlaces reales y resuelven sus destinos durante la ejecución.
- Si el proyecto necesita enlaces reales, usa un proyecto remoto en un anfitrión cuyo sistema de archivos y permisos los admitan.

### <a name="git-limitations-cli"></a>Usar la CLI como alternativa

Para repositorios grandes o tareas que necesitan el sistema de archivos y las herramientas Git del anfitrión, usa un **proyecto remoto mediante Spck CLI**. Las operaciones se ejecutan con el **binario Git del anfitrión** mientras editas desde Spck:

- Las operaciones usan la memoria y el disco del anfitrión en lugar de los recursos del móvil o navegador.
- Los enlaces simbólicos dependen del soporte y los permisos del sistema de archivos del anfitrión.
- Usa las herramientas Git del anfitrión para los comandos que no aparecen en los controles del editor.

Consulta [Primeros pasos con Spck CLI](./cli-start) para conectar un anfitrión. Los proyectos remotos requieren una cuenta Spck y están sujetos a los límites del plan; consulta [Proyectos remotos](./editor-lite#remote-projects) para los requisitos de suscripción de Lite. Clonar en el almacenamiento del dispositivo sigue usando el cliente Git nativo móvil.

## <a name="git-related-guides"></a>Guías relacionadas

- [Compatibilidad con lectores de pantalla (experimental)](./screen-reader-support): navegación accesible, controles de versiones y comentarios.
- [Spck Editor Lite](./editor-lite#enhanced-git-integration): herramientas Git incluidas en la compra única.
- [Primeros pasos con Spck CLI](./cli-start): conectar un proyecto remoto para usar las herramientas Git del anfitrión.
