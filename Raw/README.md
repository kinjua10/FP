# Raw/ — insumos originales

> Todo lo que llega de afuera, tal como llegó. **Solo lectura:** no se edita, no se renombra
> y no se borra. Si hay que corregir o transformar algo, el resultado va a `Output/`.

## Subcarpetas

| Carpeta | Qué va |
| :--- | :--- |
| `capturas/` | Capturas de pantalla, fotos de pizarras, imágenes de errores. |
| `scripts_originales/` | Código tal como lo pasaron (SQL, scripts, configs de terceros). |
| `notas_rapidas/` | Notas sueltas, transcripciones, mails pegados, minutas sin procesar. |

Si un tipo de insumo se repite seguido (ej. PDFs, exports), creá una subcarpeta nueva y
agregala a esta tabla.

## Cómo nombrar los archivos

`AAAA-MM-DD_origen_descripcion-corta.ext`

- `2026-10-23_soporte_error-carga-facturas.png`
- `2026-10-23_proveedor-x_script-stock.sql`

La fecha es la de **llegada** del insumo, no la de procesamiento. Así se ordenan solos y se
sabe de cuándo es cada versión.

## Archivos pesados

- **Hasta 10 MB:** se commitean normalmente.
- **Más de 10 MB** (PDFs largos, videos, exports grandes): usar Git LFS
  (`git lfs track "Raw/**/*.pdf"`) o guardarlos fuera del repo y dejar acá un `.md` con el
  link y una descripción.
- GitHub rechaza archivos de más de 100 MB aunque se intente.

## Lo que nunca va en Raw/ (ni en el repo)

- Credenciales, tokens, archivos `.env`.
- Datos personales o de clientes sin anonimizar.
