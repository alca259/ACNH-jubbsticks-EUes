# ACNH EUes Translations

Este repositorio contiene los textos de localización (formato MSBT exportado a `.msbt.txt`) de *Animal Crossing: New Horizons* para el idioma español (Europa, `EUes`). Sirve como espacio de trabajo para traducir, revisar y volver a empaquetar los archivos de diálogo y cadenas del juego.

## Estructura de carpetas

Descripción general (alto nivel) de qué hay en cada carpeta principal. No es un listado exhaustivo de cada archivo, sino la función de cada bloque lógico.

### Raíz
- `Gyroid_list.txt`: Tabla interna de correspondencia / nombres canon de giroide usados para asegurar coherencia en las traducciones.
- `List of new labels by file.txt`: Registro manual de etiquetas nuevas añadidas o detectadas para facilitar control de progreso.

### `EUes/`
Carpeta editable principal con las traducciones en español. Mantiene el mismo arbolado que la variante de referencia inglesa (`USen/`). Cada subcarpeta agrupa un conjunto temático de mensajes:

- `LayoutMsg/`: Mensajes de maquetación / versión (metadatos breves tipo versión del paquete).
- `Mail/`: Plantillas de cartas y correos internos (madre, PNJ especiales, etc.).
- `String/`: Nombres de objetos, peces, insectos, plantas, materiales, opciones de personalización (colores, telas, partes). Incluye lógica de prefijos (`C#`, `F#`, `X`) para variantes.
- `System/`: Textos de interfaz de usuario, logros Nook Miles, descriptores de pasaporte y otros mensajes de sistema.
- `TalkFtr/`: Diálogos asociados a muebles / features interactivos (p.ej. mesa de trabajo).
- `TalkNNpc/`: Diálogos de vecinos normales (personalidades varias), selección de regalos, etc.
- `TalkObj/`: Diálogos de objetos especiales interactuables que no son PNJ estándar.
- `TalkSNpc/`: Diálogos de PNJ especiales (Sócrates, Fígaro, Tota, etc.).
- `TalkSys/`: Mensajes y diálogos de sistema dirigidos al jugador (notificaciones internas, tablón, etc.).

### `USen/`
Estructura paralela a `EUes/` con los mismos archivos en inglés (referencia original). No se edita: se usa para entender contexto, matices y etiquetas. Las etiquetas (`label`) deben coincidir uno a uno con `EUes/`.

### `romfs/`
Salida binaria preparada para inyección en la ROM/mod. Contiene archivos comprimidos `.sarc.zs` agrupando las familias de mensajes ya empaquetadas:

- `Message/`: Archivos por categoría (`*_EUes.sarc.zs`) generados a partir de los textos traducidos (LayoutMsg, Mail, String, System, TalkFtr, TalkNNpc, TalkObj, TalkSNpc, TalkSys).
- `System/Resource/`: Recursos auxiliares del sistema (no se editan aquí normalmente). 

### Flujo general
1. Editar únicamente en `EUes/` manteniendo etiquetas y marcas (`{{ ... }}`) intactas.
2. Sincronizar estructura con `USen/` (si aparece un archivo nuevo en inglés, crear su par en español).
3. Regenerar los `.sarc.zs` dentro de `romfs/Message/` mediante la herramienta de empaquetado utilizada en el proyecto (paso externo a este repo).
4. Actualizar `List of new labels by file.txt` cuando se introduzcan nuevas etiquetas.

### Reglas clave de traducción (resumen)
- No modificar valores de `label` ni bloques de atributos.
- Conservar exactamente las etiquetas de control `{{wordInfo ...}}`, `{{anim:...}}`, `{{color ...}}`, `{{pageBreak}}`, etc.
- Mantener longitud de línea ≤ 90 caracteres (sin contar etiquetas) salvo fragmentos separados por `{{pageBreak}}`.
- Usar variantes peninsulares del español y coherencia de género / artículos según `{{wordInfo}}`.
- Nombres especiales establecidos (ej.: Brewster → Fígaro, Blathers → Sócrates) y nombres de giroide según `Gyroid_list.txt`.

### Notas
- Cualquier cambio que rompa etiquetas o estructura impedirá la correcta compilación de los paquetes `.sarc.zs`.
- Verificar consistencia terminológica entre categorías (p.ej. un mismo objeto no cambia de nombre entre `String/` y referencias en diálogos).

### Compatibilidad con DLC Happy Home Paradise (`resourcetablesize`)
El mod/base que añade soporte de carga para el DLC Happy Home Paradise suele incluir un fichero `resourcetablesize` (u homólogo dentro de `romfs/System/Resource/`) ajustado para idiomas soportados oficialmente. Ese fichero concreto NO es compatible con el paquete de idioma español personalizado (`EUes`) aquí incluido. Por este motivo se proporciona (o se debe proporcionar) un fichero vacío como sustitución, permitiendo que el juego cargue los textos en español fan-traducido pero sacrificando la compatibilidad con el contenido del DLC.

Resumen del compromiso:
- Fichero DLC original: activa Happy Home Paradise pero rompe / impide el uso correcto del idioma `EUes` personalizado.
- Fichero vacío: habilita el idioma `EUes` traducido, desactiva la integración del DLC.

Si se quisiera compatibilidad total (DLC + español personalizado) sería necesario reconstruir un `resourcetablesize` que incorpore el nuevo índice de recursos para `EUes` y el del DLC, tarea que no está cubierta aún en este repositorio.

---
Para dudas o ampliaciones de este README se recomienda extender la sección de flujo o añadir ejemplos concretos de empaquetado.

