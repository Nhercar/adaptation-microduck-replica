# Microduck · Réplica, Guía de Fabricación 3D y Control por RL

Este repositorio contiene la reconstrucción, modelos 3D listos para imprimir, documentación en español, planos CAD y guías de ensamblaje para construir el robot bípedo **Microduck** (el pato robotizado presentado por Jensen Huang, CEO de NVIDIA, durante su keynote en GTC).

---

## 🙏 Fuentes, Créditos y Agradecimientos

Este proyecto recopila, traduce, organiza y adapta el enorme trabajo de ingeniería inversa y desarrollo realizado por la comunidad open-source. **Todo el crédito del diseño mecánico y la ingeniería inversa pertenece a los siguientes proyectos originales:**

1. **[fanhao375/microduck-replica](https://github.com/fanhao375/microduck-replica)** (por `@fanhao375` y colaboradores):
   * Reconstrucción completa del stack de hardware, arquitectura eléctrica (HAT y placas de bus IMU), ingeniería inversa del bus serie y adaptación del runtime en Rust para actuadores alternativos.
2. **[fanhao375/microduck-replica-cad](https://github.com/fanhao375/microduck-replica-cad)** (por el diseñador mecánico **机械行者Robo**):
   * Modelado 3D desde cero en SolidWorks a partir de los datos cinemáticos de MuJoCo, archivos STEP, optimización de tolerancias v2.2 (con ranuras de disipación térmica y holguras para servos Feetech), manual de ensamblaje de 21 páginas y perfiles `.3mf` para Bambu Studio.
   * Redes del autor: [Canal de Bilibili (Tutoriales en vídeo)](https://space.bilibili.com/312747174) · Xiaohongshu / Douyin: 机械行者Robo.
3. **Proyecto Original de Pollen Robotics y Hugging Face**:
   * Desarrolladores originales del robot comercial y del entorno de simulación por Reinforcement Learning:
     * [`pollen-robotics/microduck`](https://github.com/pollen-robotics/microduck): Software de control embebido en Rust a 50 Hz.
     * [`pollen-robotics/microduck_rl`](https://github.com/pollen-robotics/microduck_rl): Entorno de entrenamiento PPO en MuJoCo / NVIDIA Warp / mjlab.
     * [`pollen-robotics/elec_RPI_Robot_HAT`](https://github.com/pollen-robotics/elec_RPI_Robot_HAT): Diseño de la placa base de control (KiCad).

---

## 📌 Estado del Proyecto: ¿Qué es abierto y qué no?

* **Software de Control y RL:** 100% de código abierto (Apache-2.0).
* **Electrónica:** La placa superior **RPI Robot HAT** está liberada de forma oficial con esquemas, Gerber y lista de componentes.
* **Mecánica (CAD):** Los archivos oficiales no fueron publicados por Pollen. Este repositorio proporciona la **reconstrucción comunitaria v2.2** lista para imprimir en cualquier impresora 3D FDM.

---

## 🦆 Dos Rutas de Construcción: ¿Dynamixel o Feetech?

El robot se puede construir bajo dos variantes de actuadores. **Es fundamental elegir una antes de imprimir**, ya que las piezas del chasis varían según el plato del motor:

| Parámetro | Opción 1: Original (Dynamixel XL330) | Opción 2: Comunitaria (Feetech HD-1910) ⭐ *Recomendada* |
| :--- | :--- | :--- |
| **Servomotores** | 15× Dynamixel XL330-M288-T | 15× Feetech HD-1910-C001 |
| **Coste estimado de servos** | ~450 € – 600 € | **~160 € – 210 €** |
| **Voltaje de trabajo** | Nominal 5V (corre forzado a 7.4–8.2V en el robot) | **Nominal 4.0–8.4V** (nativo para baterías 2S) |
| **Par motor (Torque)** | 0.52 N·m | **1.47 N·m** (2.5 veces más potente) |
| **Plato del servo** | Cóncavo | Convexo (sobresale) |
| **Archivos 3D** | Versión CAD v1.1 | **Versión CAD v2.2** (incluida en este repo) |
| **Simulación y RL** | Compatible directo con pesos pre-entrenados | Requiere el driver adaptado (`RobotIo` STS) y pesos re-entrenados |

---

## 📁 Estructura del Repositorio

* [`stl-files/`](stl-files/): **33 modelos STL individuales** exportados en formato binario, listos para cualquier laminador (Bambu Studio, PrusaSlicer, OrcaSlicer, Cura) con nombres ordenados en español e inglés.
* [`step-files/`](step-files/): Archivos CAD neutros `.STEP` de las piezas modificadas para la versión Feetech (v2.2 con ranuras de ventilación y mayor holgura en muslos).
* [`PLAN_IMPRESION_Y_BOM.md`](PLAN_IMPRESION_Y_BOM.md): Guía de impresión por bandejas (PLA vs TPU) y lista de la compra completa de materiales (rodamientos, tornillos, electrónica, batería).
* [`cad-repo/`](cad-repo/): Repositorio mecánico completo:
  * `打印/microduck-飞特版-BambuStudio2026-10-20.3mf`: Proyecto de Bambu Studio con 5 bandejas pre-orientadas.
  * `安装说明书/microduck装配安装说明书.pdf`: Manual de ensamblaje en PDF con 21 páginas ilustradas.
  * `组件图/`: 23 planos de despiece y vistas explosionadas de cada subconjunto.
* [`replica-repo/`](replica-repo/): Repositorio con toda la ingeniería inversa eléctrica y de software:
  * `docs/`: Guías de adquisición, tablas de inercia y análisis de actuadores.
  * `hardware/`: Diseños PCB alternativos (IMU de bus serie, Hub de distribución).
  * `software/`: Adaptación del driver en Rust para protocolo Feetech STS.

---

## 🖨️ Resumen de Impresión 3D

* **Materiales necesarios:**
  * **PLA+ o PETG** (~400 g): Para las piezas estructurales rígidas (chasis, patas, carcasa de cabeza, torso).
  * **TPU Flexible 95A / 85A** (~50 g): **Obligatorio** para las piezas suaves del pico (`08_jaw_soft` y `17_soft_mouth_top`). Si se construye la variante con patines, los 4 neumáticos también se imprimen en TPU.
* **Ajustes de laminación recomendados:**
  * Boquilla: 0.4 mm.
  * Altura de capa: 0.20 mm (0.16 mm para carcasas de la cabeza).
  * Paredes: **4 a 5 perímetros** (vital para soportar los tornillos y los rodamientos).
  * Relleno: 25% – 30% giroidal.

---

## 🛠️ Resumen de Componentes Externos (BOM)

Para que el robot cobre vida se necesitan:
1. **Actuadores:** 15 servomotores serie Feetech HD-1910-C001 (o Dynamixel XL330-M288-T) + 1 programador USB-Serie.
2. **Cerebro (SBC):** Radxa Zero 3W (1GB o 2GB de RAM, sin eMMC) + MicroSD de 32GB/64GB (Clase A1/A2).
3. **Placas base:** 1 placa RPI Robot HAT + 1 placa IMU de bus (LSM6DSV16X).
4. **Alimentación:** Batería tipo Sony NP-F550 (2S 7.4V) con terminales banana PCB de 2.5 mm.
5. **Sensores:** Cámara IMX219 (tipo Raspberry Pi v2) + Sensor ToF VL53L5CX.
6. **Mecánica:** 3 rodamientos 10×15×3 mm, 11 rodamientos 16×22×4 mm, tornillos M2 y M2.5, insertos de latón para calor y fijador Loctite 243.

Consulta todos los detalles y especificaciones en [`PLAN_IMPRESION_Y_BOM.md`](PLAN_IMPRESION_Y_BOM.md).
