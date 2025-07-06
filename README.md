# Sistema de Detección de Personas en Escenarios de Desastre

## Objetivo del trabajo

El objetivo del presente proyecto es diseñar un sistema de detección automática de personas en situaciones de desastre, utilizando imágenes aéreas capturadas por UAVs. Este sistema busca identificar personas en condiciones complejas, especialmente objetos pequeños que pueden estar ocultos parcial o totalmente por escombros, agua, humo u otros elementos, para apoyar tareas de búsqueda y rescate. El enfoque se centra en técnicas de detección de objetos mediante modelos de visión por computador, entrenados con el C2A Dataset.

## Integrantes

- **u202218044** - Mayhua Hinostroza, José Antonio
- **u202216120** - Manchay Paredes, Lucero Salome
- **u202212675** - Rodriguez Valencia, Rosa Maria
- **u202216661** - Medina Agnini, Bruno Alessandro

## Descripción del dataset

**Nombre del conjunto de datos**: *C2A Dataset: Human Detection in Disaster Scenarios*\
**Autor**: Ragib Nihal\
**Fuente**: Publicado en Kaggle en marzo de 2024.

Este conjunto de datos fue creado con el propósito de entrenar modelos de visión por computador para la detección de personas en escenarios de desastre mediante imágenes aéreas capturadas por UAVs (drones).

### Características principales

- Cantidad de objetos anotados: más de 360,000
- Tipo de imágenes: Escenarios reales y simulados de desastres:
  - Incendios y humo
  - Inundaciones
  - Edificios colapsados y escombros
  - Accidentes de tráfico
- Resolución: Variable, desde 123×152 hasta 5184×3456 píxeles
- Clases: Solo personas (class\_id = 0), clasificadas según postura

### Clasificación por postura (pose\_id)

| Pose ID | Postura  | Descripción |
| ------- | -------- | ----------- |
| 0       | Bent     | Inclinado   |
| 1       | Kneeling | Arrodillado |
| 2       | Lying    | Acostado    |
| 3       | Sitting  | Sentado     |
| 4       | Upright  | De pie      |

### Formatos de anotación

**YOLO (You Only Look Once)**

Formato por línea:

```
<clase> <x_centro> <y_centro> <ancho> <alto> <pose>
```

- Coordenadas normalizadas respecto al tamaño de la imagen
- Clase es siempre 0 (persona)
- El valor "pose" va de 0 a 4

**Ejemplo:**

```
0 0.051601 0.861111 0.096085 0.069444 4
```

Esto representa una persona de pie (pose\_id = 4) en una imagen de 281×288 píxeles.

**COCO (Common Objects in Context)**

Formato JSON estructurado:

```json
{
  "images": [
    {
      "id": 1,
      "width": 264,
      "height": 247,
      "file_name": "flood_image0363_4.png",
      "license": 1,
      "date_captured": "2023-07-31"
    }
  ],
  "annotations": [
    {
      "id": 1,
      "image_id": 1,
      "category_id": 0,
      "bbox": [247, 32, 8, 8],
      "pose": 0
    }
  ],
  "categories": [
    {
      "id": 0,
      "name": "0",
      "supercategory": "char"
    }
  ]
}
```

### Estructura del dataset

```
archive/
└── C2A_Dataset/
    └── new_dataset3/
        ├── train/
        │   ├── images/               # 6,129 imágenes
        │   ├── labels/               # 6,129 archivos .txt (YOLO)
        │   └── train_annotations.json
        ├── val/
        │   ├── images/               # 2,043 imágenes
        │   ├── labels/               # 2,043 archivos .txt
        │   └── val_annotations.json
        ├── test/
        │   ├── images/               # 2,043 imágenes
        │   ├── labels/               # 2,043 archivos .txt
        │   └── test_annotations.json
        └── All labels with Pose information/
└── Coco_annotation_pose/
    ├── train_annotations_with_pose_information.json
    ├── val_annotations_with_pose_information.json
    └── test_annotations_with_pose_information.json
```

**Link del dataset completo**
https://drive.google.com/drive/folders/1jzsKvhByIuPlkn8udVCh8RbjQsjMI-80?usp=sharing

no se puedo subir el dataset completo al repo por el tamaño

### Metadatos clave

- Número de imágenes:
  - Entrenamiento: 6,129
  - Validación: 2,043
  - Test: 2,043
- Clases: Persona (class\_id = 0)
- Posturas: 5 clases (pose\_id de 0 a 4)
- Formatos:
  - YOLO básico (.txt)
  - YOLO + Pose
  - COCO (.json)
  - COCO con pose explícita

## Conclusiones

- El proyecto implementa un sistema robusto de detección de personas en escenarios de desastre, utilizando la arquitectura YOLOv9e y un dataset especializado. La estructura del código y la documentación reflejan buenas prácticas en la organización de datos, configuración del entorno y pipeline de entrenamiento, lo que facilita la reproducibilidad y escalabilidad del sistema.

- El dataset está correctamente adaptado para la tarea, con una única clase (human) y anotaciones en formato YOLO, lo que simplifica el problema y mejora la velocidad de inferencia. La estructura de carpetas y la documentación detallada aseguran la integridad y facilidad de uso del conjunto de datos, aunque se identifica que la detección en escenarios acuáticos sigue siendo un reto.

- El modelo alcanza métricas sólidas: precisión del 87.7%, recall del 75.7% y mAP@0.5 superior al umbral mínimo propuesto (0.60), lo que valida su aplicabilidad en contextos reales de rescate. Sin embargo, el recall indica que aún existe margen de mejora para reducir los falsos negativos, especialmente en condiciones visuales adversas.

- El sistema es apto para ser integrado en plataformas de rescate (como drones), gracias a su velocidad de inferencia y precisión. No obstante, el análisis cualitativo muestra que el rendimiento varía según el tipo de desastre, siendo menor en inundaciones por los reflejos y distorsiones del agua. Se recomienda profundizar en técnicas de augmentación específicas para estos escenarios.

- La documentación del proyecto y el informe son claros, detallados y alineados, lo que facilita la comprensión y futura extensión del trabajo. La transparencia en la publicación de resultados y métricas, así como la referencia a fuentes y datasets, refuerza la confiabilidad y utilidad del sistema para la comunidad académica y profesional.

## Licencia

Este proyecto está bajo la Licencia MIT. Para más detalles, revisar el archivo [LICENSE](./LICENSE).

