# Sistema de Detección de Personas en Escenarios de Desastre

## Objetivo del trabajo

El objetivo del presente proyecto es diseñar un sistema de detección automática de personas en situaciones de desastre, utilizando imágenes aéreas capturadas por UAVs. Este sistema busca identificar personas en condiciones complejas, especialmente objetos pequeños que pueden estar ocultos parcial o totalmente por escombros, agua, humo u otros elementos, para apoyar tareas de búsqueda y rescate. El enfoque se centra en técnicas de detección de objetos mediante modelos de visión por computador, entrenados con el C2A Dataset.

## Integrantes

- **u202218044** - Mayhua Hinostroza, José Antonio
- **u202216120** - Manchay Paredes, Lucero Salome
- **u202212675** - Rodriguez Valencia, Rosa Maria
- **u202216661** - Medina Agnini, Bruno Alessandro

## Descripción del dataset

**Nombre del conjunto de datos**: *Dataset de Detección Humana en Escenarios de Desastre*\
**Fuente**: Dataset personalizado para entrenamiento de modelos YOLO.

Este conjunto de datos fue diseñado específicamente para entrenar modelos de detección de objetos capaces de identificar personas en situaciones de emergencia y desastre mediante imágenes aéreas capturadas por UAVs (drones).

### Características principales

- **Objetivo**: Detección de personas (`human`) en escenarios de desastre
- **Tipo de imágenes**: Cuatro categorías principales de desastres:
  - **Inundaciones** (`flood_image`) - Personas en zonas inundadas
  - **Incendios** (`fire_image`) - Personas en zonas de incendio y humo
  - **Edificios colapsados** (`collapsed_building_image`) - Personas en escombros y estructuras dañadas
  - **Incidentes de tráfico** (`traffic_incident_image`) - Personas en accidentes vehiculares
- **Formato de anotación**: YOLO estándar (sin información de pose)
- **Resolución**: Variable según la fuente de la imagen
- **Clases**: Una sola clase - `human` (class_id = 0)

### Formato de anotación YOLO

Las anotaciones siguen el formato YOLO estándar:

```
<clase> <x_centro> <y_centro> <ancho> <alto>
```

- **Coordenadas normalizadas**: Valores entre 0 y 1 respecto al tamaño de la imagen
- **Clase**: Siempre 0 (human)
- **Bounding boxes**: Definen la ubicación y tamaño de cada persona detectada

**Ejemplo de anotación:**

```
0 0.597857 0.402284 0.004286 0.007614
0 0.763571 0.892132 0.035714 0.048223
0 0.630000 0.881980 0.028571 0.032995
```

Cada línea representa una persona detectada en la imagen con sus coordenadas de bounding box normalizadas.

### Estructura del dataset

```
data/
├── analisis_pose_completo.xlsx
└── Dataset/
    ├── Imagenes_prueba/          # Imágenes para testing adicional
    │   ├── testeo1.jpg
    │   ├── testeo2.jpg
    │   ├── testeo3.jpg
    │   ├── testeo4.webp
    │   ├── testeo5.png
    │   ├── testeo6.jpg
    │   ├── testeo7.jpg
    │   ├── testeo8.jpg
    │   ├── waldo1.jpg
    │   ├── waldo2.jpg
    │   └── waldo5.png
    ├── train/
    │   ├── images/               # Imágenes de entrenamiento (6,129 imágenes)
    │   │   ├── flood_image*.png
    │   │   ├── fire_image*.png
    │   │   ├── collapsed_building_image*.png
    │   │   └── traffic_incident_image*.png
    │   ├── labels/               # Anotaciones YOLO (.txt)
    │   ├── labels.cache
    │   └── train_annotations.json
    ├── val/
    │   ├── images/               # Imágenes de validación
    │   ├── labels/               # Anotaciones YOLO (.txt)
    │   ├── labels.cache
    │   └── val_annotations.json
    └── test/
        ├── images/               # Imágenes de prueba
        ├── labels/               # Anotaciones YOLO (.txt)
        ├── labels.cache
        └── test_annotations.json
```

### Estadísticas del dataset

- **Total de imágenes de entrenamiento**: 6,129
- **Distribución por categoría de desastre**:
  - Imágenes de inundaciones
  - Imágenes de incendios
  - Imágenes de edificios colapsados
  - Imágenes de incidentes de tráfico
- **Clase única**: `human` (ID: 0)
- **Formato de archivo**: PNG para imágenes, TXT para etiquetas YOLO
- **Anotaciones adicionales**: Archivos JSON con metadatos complementarios

## Conclusiones

- El proyecto implementa un sistema robusto de detección de personas en escenarios de desastre, utilizando la arquitectura YOLOv9e y un dataset especializado. La estructura del código y la documentación reflejan buenas prácticas en la organización de datos, configuración del entorno y pipeline de entrenamiento, lo que facilita la reproducibilidad y escalabilidad del sistema.

- El dataset está correctamente adaptado para la tarea, con una única clase (human) y anotaciones en formato YOLO, lo que simplifica el problema y mejora la velocidad de inferencia. La estructura de carpetas y la documentación detallada aseguran la integridad y facilidad de uso del conjunto de datos, aunque se identifica que la detección en escenarios acuáticos sigue siendo un reto.

- El modelo alcanza métricas sólidas: precisión del 87.7%, recall del 75.7% y mAP@0.5 superior al umbral mínimo propuesto (0.60), lo que valida su aplicabilidad en contextos reales de rescate. Sin embargo, el recall indica que aún existe margen de mejora para reducir los falsos negativos, especialmente en condiciones visuales adversas.

- El sistema es apto para ser integrado en plataformas de rescate (como drones), gracias a su velocidad de inferencia y precisión. No obstante, el análisis cualitativo muestra que el rendimiento varía según el tipo de desastre, siendo menor en inundaciones por los reflejos y distorsiones del agua. Se recomienda profundizar en técnicas de augmentación específicas para estos escenarios.

- La documentación del proyecto y el informe son claros, detallados y alineados, lo que facilita la comprensión y futura extensión del trabajo. La transparencia en la publicación de resultados y métricas, así como la referencia a fuentes y datasets, refuerza la confiabilidad y utilidad del sistema para la comunidad académica y profesional.

## Licencia

Este proyecto está bajo la Licencia MIT. Para más detalles, revisar el archivo [LICENSE](./LICENSE).

