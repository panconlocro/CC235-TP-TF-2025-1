# Sistema de Detección de Personas en Escenarios de Desastre

## Objetivo del trabajo

El objetivo del presente proyecto es diseñar un sistema de detección automática de personas en situaciones de desastre, utilizando imágenes aéreas capturadas por UAVs. Este sistema busca identificar personas en condiciones complejas, especialmente objetos pequeños que pueden estar ocultos parcial o totalmente por escombros, agua, humo u otros elementos, para apoyar tareas de búsqueda y rescate. El enfoque se centra en técnicas de detección de objetos mediante modelos de visión por computador, entrenados con el C2A Dataset.

## Integrantes

- **u202218044** - Mayhua Hinostroza, José Antonio  
- **u202216120** - Manchay Paredes, Lucero Salome  
- **u202212675** - Rodriguez Valencia, Rosa Maria  
- **u202216661** - Medina Agnini, Bruno Alessandro  

## Descripción del dataset

**Nombre del conjunto de datos**: *C2A Dataset: Human Detection in Disaster Scenarios*  
**Autor**: Ragib Nihal  
**Fuente**: Publicado en [Kaggle](https://www.kaggle.com) en marzo de 2024.  

Este conjunto de datos fue creado con el propósito de entrenar modelos de visión por computador para la detección de personas en escenarios de desastre mediante imágenes aéreas capturadas por UAVs (drones).

### Características principales

- **Cantidad de objetos anotados**: más de 360,000
- **Tipo de imágenes**: Escenarios reales y simulados de desastres, como:
  - Incendios y humo
  - Inundaciones
  - Edificios colapsados y escombros
  - Accidentes de tráfico
- **Resolución**: Variable, desde 123×152 hasta 5184×3456 píxeles
- **Clases**: Solo personas (class_id = 0), clasificadas según postura

### Clasificación por postura (`pose_id`)

| Pose ID | Postura     | Descripción     |
|---------|-------------|-----------------|
| 0       | Bent        | Inclinado       |
| 1       | Kneeling    | Arrodillado     |
| 2       | Lying       | Acostado        |
| 3       | Sitting     | Sentado         |
| 4       | Upright     | De pie          |

### Formatos de anotación

**1. YOLO (You Only Look Once)**  
Formato por línea:  
