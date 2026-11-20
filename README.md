# SEDATU · SITU — Hub de Conocimiento Territorial

Este repositorio contiene los datos e imágenes del Hub de Conocimiento Territorial del landing del SITU. El frontend consume `hubConocimientoT.json` mediante jsDelivr.

La sección contiene un bloque superior independiente, con imagen y texto, seguido del carrusel de noticias. El título «Hub de Conocimiento Territorial» ya está definido en el landing.

## Qué cambia en el frontend

El componente actual solo lee el array `noticias`. Para mostrar el bloque superior hay que actualizar, una sola vez, `Front/components/HubConocimientoT/CarruselHubConocimientoT.js` en el repositorio [SITU](https://github.com/UNIDIOR-DEV/SITU) y publicar esa versión del frontend.

Una vez instalado ese componente, los cambios de texto, imagen y enlace se realizan desde este repositorio. Un cambio en el JSON por sí solo no instala el nuevo diseño.

El [parche del frontend](integracion/SITU_hub_seccion_superior.patch) contiene el cambio del componente y su documentación. Está preparado sobre la versión `6d45f57f8f32ddc9a204603057df532af40bc2be` del repositorio SITU, rama `feature/inicio-visualizacion`. Desde un clon de ese repositorio, comprueba y aplica el archivo con `git apply --check ruta/al/SITU_hub_seccion_superior.patch` y después `git apply ruta/al/SITU_hub_seccion_superior.patch`. El build y la publicación corresponden al frontend.

## Estructura

```text
sedatu-situ-hubConocimientoT/
├── hubConocimientoT.json
├── imagenes/
└── README.md
```

## URLs públicas

- Manifest: https://cdn.jsdelivr.net/gh/UNIDIOR-DEV/sedatu-situ-hubConocimientoT@master/hubConocimientoT.json
- Imágenes: https://cdn.jsdelivr.net/gh/UNIDIOR-DEV/sedatu-situ-hubConocimientoT@master/imagenes/
- Refresco del manifest: https://purge.jsdelivr.net/gh/UNIDIOR-DEV/sedatu-situ-hubConocimientoT@master/hubConocimientoT.json

La propagación depende de la caché del CDN. El componente también conserva una copia del contenido en el navegador durante una hora y consulta el manifest al cargar la página. El bloque superior y las noticias se guardan juntos en esa copia.

## Esquema del manifest

```json
{
  "version": 1,
  "actualizado": "YYYY-MM-DD",
  "seccion_superior": {
    "titulo": "Título del contenido destacado",
    "descripcion": "Texto del bloque superior.",
    "imagen": "imagenes/destacado.webp",
    "link": ""
  },
  "noticias": [
    {
      "id": "YYYY-MM-DD-slug-corto",
      "titulo": "Título de la noticia",
      "descripcion": "Descripción de la noticia.",
      "imagen": "imagenes/noticia.webp",
      "fecha": "YYYY-MM-DD",
      "link": ""
    }
  ]
}
```

## Bloque superior

| Campo | Uso |
| --- | --- |
| `titulo` | Título del bloque. Debe contener texto para mostrarlo. |
| `descripcion` | Descripción; admite saltos de línea. Se recomienda un máximo de 200 caracteres. |
| `imagen` | Ruta relativa dentro de `imagenes/`. Si está vacía, se muestra un paisaje ilustrado, como referencia visual. |
| `link` | Destino del botón «Más información». Si está vacío, el botón no aparece. |

El bloque es independiente del carrusel: se muestra aunque `noticias` esté vacío y no cuenta dentro del límite de diez noticias. Para retirarlo, elimina `seccion_superior` o asigna `null`.

El título y la descripción incluidos en esta propuesta son provisionales. Sustitúyelos por el contenido editorial definitivo y agrega la imagen y el enlace cuando estén disponibles.

## Noticias

Las noticias conservan los campos `id`, `titulo`, `descripcion`, `imagen`, `fecha` y `link`. Los identificadores deben ser únicos y la fecha debe utilizar el formato ISO `YYYY-MM-DD`. Se recomienda un título de hasta 60 caracteres y la descripción debe tener como máximo 200 caracteres.

El componente muestra las primeras diez entradas del array. En escritorio se agrupan de tres en tres; en celular se muestra una noticia por vista. Para agregar una noticia cuando ya hay diez, retira la más antigua.

## Edición y revisión

1. Crea una rama desde `master`.
2. Sube la imagen a `imagenes/` cuando corresponda.
3. Edita `hubConocimientoT.json` y actualiza `actualizado`.
4. Comprueba que el JSON sea válido, que las rutas de imágenes existan y que los enlaces sean correctos.
5. Crea un Pull Request para revisión editorial y técnica.
6. Después de la revisión, integra el cambio a `master`.

Los nombres actuales son `sedatu-situ-hubConocimientoT` y `hubConocimientoT.json`; el componente ya utiliza estas rutas.

## Contacto

- Problemas en el sitio: equipo de desarrollo SITU.
- Aprobación editorial: jefatura de proyecto SITU.
