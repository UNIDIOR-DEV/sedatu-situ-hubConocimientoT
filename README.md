# SEDATU · SITU — Repositorio de Noticias

Este repositorio alimenta el apartado **Noticias** del landing del SITU (Sistema de Información Territorial y Urbano).

El frontend del SITU lee el archivo `noticias.json` y las imágenes de la carpeta `imagenes/` directamente desde este repositorio a través del CDN de jsDelivr — no se requiere despliegue ni publicación manual: **basta con hacer commit en la rama `master`** para que el cambio se refleje en el sitio.

---

## Estructura del repositorio

```
sedatu-situ-noticias/
├── noticias.json                       Manifest con los datos de cada noticia
├── imagenes/                           Imágenes de las noticias (máx. 10)
├── README.md                           Este archivo
├── .gitignore
└── .github/
    └── PULL_REQUEST_TEMPLATE.md        Checklist para PRs
```

---

## URLs públicas (CDN)

El frontend consume el contenido a través de jsDelivr (CDN global con caché):

- **Manifest:** `https://cdn.jsdelivr.net/gh/UNIDIOR-DEV/sedatu-situ-noticias@master/noticias.json`
- **Imágenes:** `https://cdn.jsdelivr.net/gh/UNIDIOR-DEV/sedatu-situ-noticias@master/imagenes/<archivo>.webp`

> El CDN tiene caché de aproximadamente 12 horas. Para forzar refresco inmediato durante pruebas, se puede usar `https://purge.jsdelivr.net/gh/UNIDIOR-DEV/sedatu-situ-noticias@master/noticias.json`.

---

## Esquema de `noticias.json`

```json
{
  "version": 1,
  "actualizado": "YYYY-MM-DD",
  "noticias": [
    {
      "id": "YYYY-MM-DD-slug-corto",
      "titulo": "Título visible (máx. ~60 caracteres)",
      "descripcion": "Texto descriptivo (máx. 200 caracteres).",
      "imagen": "imagenes/nombre-archivo.webp",
      "fecha": "YYYY-MM-DD",
      "link": "https://opcional.gob.mx/..."
    }
  ]
}
```

### Reglas de los campos

| Campo         | Obligatorio | Reglas                                                                 |
|---------------|-------------|------------------------------------------------------------------------|
| `id`          | sí          | Único, formato `YYYY-MM-DD-slug-corto`                                 |
| `titulo`      | sí          | Máx. 60 caracteres recomendado                                         |
| `descripcion` | sí          | Máx. 200 caracteres                                                    |
| `imagen`      | sí          | Ruta relativa dentro del repo (`imagenes/...`)                         |
| `fecha`       | sí          | Formato ISO `YYYY-MM-DD`                                               |
| `link`        | no          | Cadena vacía `""` si no aplica                                         |

### Límite de noticias

El array `noticias` debe contener **un máximo de 10 entradas**. Si suben más, el frontend solo mostrará las primeras 10. Para publicar una noticia nueva cuando ya hay 10, **elimina la más antigua** antes de agregar la nueva.

---

## Cómo agregar una noticia (desde la UI de GitHub, sin git local)

1. **Sube la imagen** a la carpeta `imagenes/`:
   - Entra a la carpeta `imagenes/` en GitHub
   - Botón **Add file → Upload files**
   - Arrastra la imagen optimizada (ver reglas abajo)
   - En el cuadro de commit, deja la opción **Create a new branch and start a pull request**
   - Da un nombre descriptivo al branch, por ejemplo: `noticia/2026-06-15-foro-territorial`
2. **Edita `noticias.json`** en ese mismo branch:
   - Abre `noticias.json` → botón del lápiz (Edit this file)
   - Agrega tu nueva entrada **al inicio** del array `noticias`
   - Actualiza el campo `actualizado` con la fecha de hoy
   - Si ya hay 10 noticias, elimina la más antigua del final del array
   - Commit en el mismo branch
3. **Crea el Pull Request** y completa el checklist
4. Espera la revisión y el merge a `master`
5. El cambio se refleja en el sitio en máx. ~12 h (o se purga el caché de jsDelivr para verlo al instante)

## Cómo retirar una noticia

1. Edita `noticias.json` y elimina el bloque correspondiente del array
2. (Opcional) Borra el archivo de imagen de la carpeta `imagenes/` para mantener el repo limpio
3. Actualiza el campo `actualizado`
4. Commit en un branch y PR como arriba


---

## ¿A quién contactar?

- Problemas en el sitio: equipo de desarrollo SITU
- Aprobación editorial de noticias: jefatura de proyecto SITU
