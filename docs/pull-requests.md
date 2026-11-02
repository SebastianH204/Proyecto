# Pull Requests

Aquí dejo lo que respondí en cada PR del proyecto, con la plantilla de `.github/pull_request_template.md`.

## PR #1 · README con la insignia de Proyecto y la URL de Vercel

### Qué cambia

Cambié la insignia del CI del README para que apunte a este repositorio y puse la URL de Vercel en "Pruébalo aquí".

### Por qué

La insignia todavía apuntaba al repositorio viejo, entonces no mostraba el estado real del CI de este proyecto, y el README no tenía el enlace a la página publicada.

### Cómo probarlo

1. Abre la URL de preview que Vercel comenta en este PR.
2. Abre el README en la pestaña de archivos del PR.
3. La insignia de CI debe salir en verde y el enlace "Pruébalo aquí" debe abrir https://proyecto-pearl-two.vercel.app con los Pokémon.

### Lista de chequeo

- [x] El CI está en verde
- [x] Probé la preview en el celular (o en DevTools a 375 px)
- [x] La consola no muestra errores
- [x] Puedo explicar cada línea que cambié

## PR #2 · Lighthouse

### Qué cambia

Agregué la plantilla para los PR, la captura de Lighthouse de la página ya publicada en Vercel y la URL real en el README.

### Por qué

La plantilla es para que todos mis PR expliquen lo mismo (qué cambia, por qué y cómo probarlo), la captura queda como evidencia de las notas de Lighthouse en producción y no en local, y el README tenía la URL de ejemplo en vez de la de Vercel.

### Cómo probarlo

1. Abre la URL de preview que Vercel comenta en este PR.
2. Abre docs/lighthouse-despues.png en los archivos del PR: salen 100 en rendimiento, 96 en accesibilidad, 100 en buenas prácticas y 100 en SEO.
3. En el README, el enlace "Pruébalo aquí" debe abrir https://proyecto-pearl-two.vercel.app con los Pokémon.

### Lista de chequeo

- [x] El CI está en verde
- [x] Probé la preview en el celular (o en DevTools a 375 px)
- [x] La consola no muestra errores
- [x] Puedo explicar cada línea que cambié
