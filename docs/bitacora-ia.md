# Bitácora de IA - Explorador PokeSearch

## 2026-10-06 · Modal de detalle

**Herramienta:** Claude

**Spec que usé:**

```
QUÉ: modal de detalle de un Pokémon para mi Explorador (PokeSearch).

ESTRUCTURA
- Elemento nativo <dialog id="modal-detalle">, abierto con showModal().
- Arriba una franja roja con la imagen del Pokémon en círculo con borde blanco.
- <h2> con el nombre, lista <dl> con número, tipo, altura, peso y habilidades,
  y un botón "Cerrar".

ESTILO
- Tailwind CSS v4 (NO v3): sin tailwind.config.js, sin CSS propio, sin style="".
- Mis colores: rojo #EF5350 (bg-[#EF5350]) y rojo oscuro #C62828 para los hover.
- rounded-2xl, max-w-md, shadow-2xl, fondo del backdrop oscuro semitransparente.
- Dark mode con dark: (fondo gray-800, textos claros).

COMPORTAMIENTO
- Se abre desde cualquier botón "Ver detalle" de las tarjetas (clase btn-detalle).
- Se cierra con Esc, con el botón Cerrar (usa <form method="dialog">)
  y al hacer clic en el fondo oscuro.

RESTRICCIONES
- HTML + JS vanilla en el mismo archivo. Sin librerías. Comentarios en español.
- aria-labelledby apuntando al h2. alt en la imagen.

CONTEXTO (datos reales de mi API, https://pokeapi.co/api/v2/pokemon/25):
{"id":25,"name":"pikachu","types":[{"type":{"name":"electric"}}],
 "height":4,"weight":60,
 "abilities":[{"ability":{"name":"static"}},{"ability":{"name":"lightning-rod"}}],
 "sprites":{"front_default":
 "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/25.png"}}
```

**Auditoría contra la spec:**
- [x] Usa `<dialog>` y `showModal()`
- [x] Cierra con Esc y con el botón Cerrar (`<form method="dialog">`)
- [x] Cierra con clic en el fondo (`e.target === modal`). Funciona porque el dialog tiene `p-0`
- [x] Tiene `m-auto`: sin eso el reset de Tailwind lo deja pegado arriba a la izquierda
- [x] `aria-labelledby="modal-nombre"` apunta al h2 y la imagen tiene alt
- [ ] Altura y peso: la API los da en decímetros y hectogramos. Revisé que quedaran divididos entre 10 (4 → 0.4 m, 60 → 6 kg)
- [ ] El botón Cerrar no tenía estilo de mi proyecto. Le puse el mismo de mis enlaces del menú: texto rojo y al pasar el mouse fondo `#C62828` con letra blanca

**Clases o sintaxis inventadas que encontré:**
- Ninguna. No había sintaxis de v3 (`bg-opacity-50`, `@tailwind base`): usa `backdrop:bg-gray-900/60`.
- `btn-detalle` no es de Tailwind: es una clase mía solo para buscar los botones desde JavaScript. No genera CSS y está bien que IntelliSense no la reconozca.

**Qué no entendí y cómo lo resolví:**
- `backdrop:` → es la variante que le da estilo al fondo oscuro que sale detrás del dialog (`::backdrop`).
- `bg-[#EF5350]` → los corchetes dejan usar un valor exacto que no está en la escala de Tailwind. Es la misma sintaxis de `aspect-[3/2]` que usé en la semana 5.

**¿Puedo explicar cada línea?** Sí.

---

## 2026-10-06 · Dark mode

**Herramienta:** Claude

**Spec que usé:**

```
QUÉ: agregar modo oscuro a todos los componentes de mi Explorador
(formulario, tarjetas, modal y footer).

ESTILO
- Tailwind CSS v4. Solo variantes dark:, sin JavaScript y sin CSS propio.
  El modo oscuro sigue la preferencia del sistema operativo.
- Usa SIEMPRE estas parejas claro/oscuro:
  Fondo de la página ........ bg-gray-50      → dark:bg-gray-900
  Superficie (tarjeta, modal,
  caja de búsqueda) ......... bg-white        → dark:bg-gray-800
  Texto principal ........... text-gray-700   → dark:text-gray-100
  Texto secundario .......... text-gray-500   → dark:text-gray-400
  Bordes .................... border-gray-200 → dark:border-gray-600

RESTRICCIONES
- No cambies las clases que ya existen, solo agrega las dark:.
- El rojo de mi marca (#EF5350) se queda igual en los dos modos:
  navbar, bienvenida, títulos y botones no cambian.
- Los chips de tipo se quedan iguales.
- Ningún texto puede quedar ilegible ni ningún elemento blanco en modo oscuro.
```

**Auditoría contra la spec:**
- [x] Body, tarjetas, caja de búsqueda, modal y footer con sus parejas
- [x] Input y select con `dark:border-gray-600 dark:bg-gray-800 dark:text-gray-100`
- [x] El rojo de la marca y los chips no se tocaron
- [ ] El círculo de fondo de las imágenes (`bg-gray-50`) quedaba como una mancha blanca en las tarjetas oscuras. Le agregué `dark:bg-gray-700` y `dark:border-gray-600`
- [ ] Las líneas debajo de los títulos (`border-b-2 border-gray-200`) brillaban mucho en modo oscuro. Les agregué `dark:border-gray-600`

**Clases o sintaxis inventadas que encontré:**
- Ninguna. No apareció `darkMode: 'class'` ni `tailwind.config.js`, que son de v3.

**Qué no entendí y cómo lo resolví:**
- Para probarlo sin cambiar Windows: DevTools → ⋮ → More tools → Rendering → "Emulate CSS media feature prefers-color-scheme" → dark.

**¿Puedo explicar cada línea?** Sí.

---

## 2026-11-02 · Proyecto listo para producción (semanas 9 y 10)

**Herramienta:** Claude

**Spec que usé:**

```
QUÉ: dejar mi Explorador PokeSearch listo para producción y para la sustentación,
con lo que falta de las semanas 9 y 10 y lo que aprendí en el Parcial 2.

ESTRUCTURA
- package.json con los scripts dev, build (con --minify) y validar, y html-validate en devDependencies.
- .gitignore sin node_modules ni css/tailwind.css.
- .htmlvalidate.json, .github/workflows/ci.yml, plantilla de PR y vercel.json.
- README con la URL, la API, cómo correrlo, la insignia del CI y capturas.

ESTILO
- No cambiar mis colores (#EF5350 y #C62828) ni el diseño.
- Código a mi manera, sin comentarios.

COMPORTAMIENTO
- npm run validar sin errores y npm run build funcionando.
- Lighthouse: favicon, loading="lazy" en las imágenes y CSS minificado.

RESTRICCIONES
- Solo lo que vimos en el curso.
```

**Auditoría contra la spec:**
- [x] `npm run validar` sin errores y `npm run build` con «Done»
- [x] CI, plantilla de PR, `vercel.json` y `.gitignore` como en la guía de la semana 9
- [x] Favicon, `loading="lazy"` con `width` y `height`, y CSS minificado
- [ ] El validador encontró que el botón «Cerrar» del modal no tenía `type`. Le puse `type="submit"` porque cierra el `<dialog>` enviando su `<form method="dialog">`
- [ ] El filtro solo miraba el primer tipo (`types[0]`): si filtraba «Veneno», Bulbasaur no salía aunque es Planta y Veneno. Lo cambié por `types.some(...)`
- [ ] Si la API trae un tipo que no está en `TIPOS`, la tarjeta se rompía. Agregué `infoTipo` con un valor por defecto
- [ ] `cargar()` no tenía `finally`: lo agregué para que `cargando` vuelva a `false` siempre, salga bien o mal
- [ ] Lighthouse marca contraste bajo en el rojo #EF5350 con texto blanco. Accesibilidad igual queda en 96, así que dejé mis colores como están

**Clases o sintaxis inventadas que encontré:**
- Ninguna.

**Qué no entendí y cómo lo resolví:**
- `npm ci` → instala exactamente lo que dice `package-lock.json`. Por eso el lock sí se sube a GitHub.
- `rel="noopener noreferrer"` → en los enlaces que abren otra pestaña, evita que esa página pueda tocar la mía.

**¿Puedo explicar cada línea?** Sí.
