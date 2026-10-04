# AureaTech · Zona residencial inteligente

Maqueta a escala de un barrio que se monitoriza solo: farolas, casas, un lago y una calle con sensores reales conectados a un **ESP32**. Los datos viajan por WiFi a una aplicación de escritorio en **Python (Flet)** y se guardan en **MariaDB**.

Proyecto en equipo del Grado en Ingeniería Informática de la **Universidad Europea de Madrid**.

<p align="center">
  <img src="img/maqueta.jpg" alt="Maqueta de AureaTech terminada" width="640">
</p>

---

## Qué hace

| Sensor / actuador | Función en la maqueta |
|---|---|
| **HC-SR04** (ultrasonidos) | Detecta a una persona caminando y enciende las farolas por tramos: según la distancia se encienden la primera, la segunda o la tercera |
| **LDR** (luz) | Distingue día y noche: de día las farolas se quedan apagadas y al anochecer se encienden |
| **DHT22** | Temperatura y humedad ambiente |
| **MQ-2** | Detección de gas o humo |
| **LEDs** | Las farolas |
| **Servo** | Barrera que da acceso a los vehículos |
| **Buzzer** | Alarmas |
| **ESP32-CAM** | Cámara del acceso para el reconocimiento de matrículas |

El ESP32 envía las lecturas por WiFi a la aplicación, que las guarda, las muestra en tiempo real y aplica las reglas de automatización.

```text
 sensores ──► ESP32 ──WiFi──► app Python (Flet) ──► MariaDB
 ESP32-CAM ──────────────────►   │  visión: YOLO
                ▲                │
                └── farolas, servo, buzzer ◄── reglas de automatización
```

---

## Reconocimiento de matrículas (mi parte)

Dentro del equipo me encargué del módulo de visión del acceso de vehículos:

- **Modelo YOLO (Ultralytics) entrenado para detectar matrículas** en las imágenes de la ESP32-CAM, exportado también a **ONNX** para poder desplegarlo fuera de PyTorch.
- Extracción y normalización del texto de la matrícula.
- Comprobación contra la lista de **matrículas autorizadas** de la comunidad: si está permitida, el servo abre la barrera.

---

## Hardware

<p align="center">
  <img src="img/esquema-electrico.jpg" alt="Esquema eléctrico" width="640">
</p>

Toda la electrónica va escondida bajo la base: una protoboard con el ESP32 y el cableado, sobre una estructura de DM cortada a láser.

<p align="center">
  <img src="img/sensores.jpg" alt="Detalle de sensores en la maqueta" width="420">
  <img src="img/cableado.jpg" alt="Cableado bajo la base" width="420">
</p>

<p align="center">
  <img src="img/montaje.jpg" alt="Maqueta durante el montaje" width="640">
</p>

---

## Stack

`ESP32` · `ESP32-CAM` · `Arduino IDE` · `Python` · `Flet` · `YOLO (Ultralytics)` · `ONNX` · `MariaDB` · `PlantUML` · impresión 3D · corte láser

---

## Equipo

Trabajo en grupo de cuatro personas; todos participamos en el diseño, la electrónica, el software y la maqueta.

- **Daniel de Abajo** · [@danieldeab](https://github.com/danieldeab)
- **Paula Gómez Lucas** · [@paula-gomezlucas](https://github.com/paula-gomezlucas)
- **Pablo Serrano** · [@Pablster](https://github.com/Pablster)
- **Franco Zimmermann** · [@FrancoZimm](https://github.com/FrancoZimm)

> El código fuente vive en el repositorio privado del equipo. Este repo es una presentación del proyecto.
