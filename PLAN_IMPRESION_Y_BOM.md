# Plan de Impresión 3D y Lista de Componentes (BOM) · Microduck

> Documento de referencia técnica para la fabricación física y compra de componentes del robot **Microduck** (Versión Comunitaria v2.2 optimizada para servos **Feetech HD-1910-C001**).

---

## 1. Plan de Impresión 3D

Todos los modelos se encuentran disponibles en formato STL listos para laminar en la carpeta [`stl-files/`](file:///home/nacho/projects/microduck/stl-files/) y como proyecto preconfigurado en [`cad-repo/打印/microduck-飞特版-BambuStudio2026-10-20.3mf`](file:///home/nacho/projects/microduck/cad-repo/打印/microduck-飞特版-BambuStudio2026-10-20.3mf).

### A. Parámetros Globales de Laminación (Slicer)

| Parámetro | Valor Recomendado | Justificación Técnica |
| :--- | :--- | :--- |
| **Boquilla (Nozzle)** | **0.4 mm** | Balance ideal entre detalle en ranuras de montaje y velocidad. |
| **Altura de capa** | **0.20 mm** (0.16 mm en carcasas de cabeza) | 0.20 mm para piezas estructurales; 0.16 mm suaviza las curvas del cráneo. |
| **Paredes / Perímetros** | **4 a 5 paredes** | **Crítico:** Las paredes absorben la tensión de los tornillos e insertos de latón. |
| **Capas sup. / inf.** | 5 superiores, 4 inferiores | Garantiza rigidez frente a torsión en los anclajes de servos. |
| **Relleno (Infill)** | **25% – 30% Giroidal** | Distribución isotrópica de tensiones mecánicas. Evitar rejilla (*grid*). |
| **Compensación de holgura** | `X-Y Hole Compensation: +0.05 a +0.10 mm` | Ayuda a que los rodamientos y tornillos ajusten sin forzar. |

---

### B. Distribución por Bandejas de Impresión

Se han agrupado las 33 piezas en **5 bandejas de trabajo** según material y tipo de pieza:

#### 🟢 Bandeja 1: Extremidades y Estructura de Marcha
* **Material:** PLA+ / PETG rígido
* **Color sugerido:** Amarillo pato o negro
* **Piezas:**
  1. `05_foot_left_pie_izquierdo.stl` (1 ud)
  2. `06_foot_right_pie_derecho.stl` (1 ud)
  3. `21_ankle_right_tobillo_derecho.stl` (1 ud)
  4. `22_ankle_left_tobillo_izquierdo.stl` (1 ud)
  5. `25_leg_pierna_espinilla.stl` (2 uds)
  6. `31_left_upper_leg_muslo_izquierdo.stl` (1 ud)
  7. `32_right_upper_leg_muslo_derecho.stl` (1 ud)
  8. `23_upper_leg_rigidity_plate_refuerzo_muslo.stl` (2 uds)
* **Soportes:** Soportes tipo árbol (*tree supports*) en voladizos de más de 55°.

#### 🟢 Bandeja 2: Chasis del Torso y Caderas
* **Material:** PLA+ / PETG rígido
* **Color sugerido:** Amarillo pato o negro
* **Piezas:**
  1. `29_trunk_base_chasis_torso.stl` (1 ud - Chasis base)
  2. `07_hip_l_cadera.stl` (2 uds)
  3. `26_yaw2roll_articulacion_cadera.stl` (1 ud)
  4. `28_bearing_roll_soporte_rodamiento.stl` (2 uds)
  5. `10_motor_support_soporte_servo.stl` (1 ud)
  6. `14_power_support_soporte_bateria.stl` (1 ud)
  7. `03_banana_pcb_locker_cierre_pcb.stl` (1 ud)

#### 🟢 Bandeja 3: Cabeza, Cuello y Carcasas Externas
* **Material:** PLA+ (capa 0.16 mm recomendada)
* **Color sugerido:** Amarillo pato
* **Piezas:**
  1. `30_top_head_shell_cabeza_superior.stl` (1 ud - Con rejillas de ventilación v2.2)
  2. `04_bottom_head_shell_cabeza_inferior.stl` (1 ud)
  3. `33_left_shell_carcasa_izquierda.stl` (1 ud)
  4. `15_right_shell_carcasa_derecha.stl` (1 ud)
  5. `20_face_part_frontal_camara.stl` (1 ud - Ajustado a cámara Radxa/RPi)
  6. `09_jaw_mandibula_rigida.stl` (1 ud)
  7. `11_neck_pitch_cuello_inclinacion.stl` (1 ud)
  8. `12_neck_cuello.stl` (2 uds)
  9. `24_yaw_roll_motion_movimiento_cuello.stl` (1 ud)

#### ⚪ Bandeja 4: Detalles Pequeños y Ojos
* **Material:** PLA Blanco / Negro
* **Piezas:**
  1. `13_eyes_noenoeil_ojos.stl` (1 ud - Ojos)
  2. `18_sole_left_suela_izquierda.stl` (1 ud)
  3. `19_sole_right_suela_derecha.stl` (1 ud)

#### 🟠 Bandeja 5: Piezas Flexibles (TPU)
* **Material:** **TPU Flexible (95A u 85A)** *(Imprescindible para amortiguación y seguridad del mecanismo del pico)*
* **Color sugerido:** Naranja pato
* **Piezas:**
  1. `08_jaw_soft_pico_inferior_TPU.stl` (1 ud)
  2. `17_soft_mouth_top_pico_superior_TPU.stl` (1 ud)
  3. *(Opcional)* `27_wheel_tire_rueda_patin_TPU.stl` (4 uds - Sólo si se monta la variante de patines)

---

## 2. Lista Completa de Componentes (BOM)

A continuación se detalla todo el material no impreso necesario para que el robot funcione:

### A. Actuadores y Motores (Eje de Tracción)
| # | Componente | Cantidad | Especificaciones / Modelo | Función en el Robot |
| :-: | :--- | :-: | :--- | :--- |
| 1 | **Servos serie bus** | **15** | **Feetech HD-1910-C001** (Protocolo STS, 7.4V, 1.47 N·m) | 10 en piernas, 4 en cuello/cabeza, 1 en el pico |
| 2 | **Depurador USB-Serie** | 1 | **Feetech URT2** o conversor USB-TTL a 1 Mbps | Asignar IDs (10-14, 20-24, 30-34) y calibrar el cero |

### B. Electrónica de Procesamiento y Alimentación
| # | Componente | Cantidad | Especificaciones / Modelo | Función en el Robot |
| :-: | :--- | :-: | :--- | :--- |
| 3 | **Ordenador Central (SBC)** | 1 | **Radxa Zero 3W** (1GB o 2GB RAM, **sin eMMC**) | Ejecuta Linux Armbian, Rust runtime y la red ONNX de RL |
| 4 | **Tarjeta de Almacenamiento** | 1 | MicroSD de **32 GB o 64 GB** (Clase A1 o A2) | Sistema operativo y modelos de marcha |
| 5 | **Placa RPI Robot HAT** | 1 | Proyecto abierto [`pollen-robotics/elec_RPI_Robot_HAT`](https://github.com/pollen-robotics/elec_RPI_Robot_HAT) | Gestión de energía, conectores de bus y sensores |
| 6 | **Placa IMU de Bus** | 1 | Placa `imu_to_dxl` con sensor **LSM6DSV16X** | Lectura de aceleración/giro en el bus de los motores |
| 7 | **Batería** | 1 | Formato **Sony NP-F550** (Li-ion 2S, 7.4 V, ~2200–2600 mAh) | Alimentación general del robot (~40–60 min de autonomía) |
| 8 | **Conectores de Batería** | 2 | Clavijas banana PCB de 2.5 mm bañadas en oro | Conexión firme entre batería y chasis |

### C. Sensores y Periféricos
| # | Componente | Cantidad | Especificaciones / Modelo | Función en el Robot |
| :-: | :--- | :-: | :--- | :--- |
| 9 | **Cámara frontal** | 1 | Módulo **IMX219** (estilo Raspberry Pi Camera v2) | Visión por computador y seguimiento de objetos |
| 10 | **Sensor de Distancia (ToF)**| 1 | Módulo **VL53L5CX** (conexión I2C/Qwiic) | Detección de obstáculos y escalones |
| 11 | **Altavoz** | 1 | Mini altavoz de 8Ω / 1W | Sonidos y graznidos (conectado a la etapa HAT) |

### D. Mecánica, Rodamientos y Tornillería
| # | Componente | Cantidad | Dimensiones / Tipo | Dónde se monta |
| :-: | :--- | :-: | :--- | :--- |
| 12 | **Rodamientos pequeños** | **3** | **10 × 15 × 3 mm** (Diámetro int × ext × grosor) | Articulaciones de cadera y cuello |
| 13 | **Rodamientos grandes** | **11** | **16 × 22 × 4 mm** | Articulaciones de carga en muslos, rodillas y tobillos |
| 14 | **Tornillos M2** | 1 kit | M2×5 mm, M2×6 mm y M2×8 mm (cabeza cilíndrica/plana) | Fijación de servos a los soportes impresos |
| 15 | **Tornillos M2.5** | 1 kit | M2.5×6 mm y M2.5×8 mm | Estructura del chasis, torso y fijación de placas |
| 16 | **Insertos roscados de latón**| 1 kit | M2 y M2.5 de longitud corta (3–4 mm) | Se insertan con soldador caliente en los agujeros guía |
| 17 | **Fijador de roscas** | 1 bote | **Loctite 243** (fuerza media azul) | Impide que las vibraciones de la marcha aflojen tornillos |
| 18 | **Almohadillas de goma** | 2 | Goma EVA antideslizante o silicona autoadhesiva | Pegadas bajo la suela para tracción sobre suelos lisos |

---

## 3. Diagrama de Conexiones del Robot

```
                     [Batería NP-F550 (7.4V 2S)]
                                  │
                                  ▼
                     [RPI Robot HAT (Placa Base)]
                      ├── Regula 5V ──> [Radxa Zero 3W (CPU)]
                      │                       │  (MIPI CSI)
                      │                       ├──> [Cámara IMX219]
                      │                       │  (I2C)
                      │                       └──> [Sensor ToF VL53L5CX]
                      │
                      └── Bus Serie TTL (1 Mbps, 7.4V directo)
                                  │
          ┌───────────────────────┴───────────────────────┐
          ▼                                               ▼
  [Placa IMU Bus]                                [15x Servos Feetech]
 (LSM6DSV16X @ ID 200)                    ├── Cuello/Cabeza: IDs 30, 31, 32, 33
                                          ├── Pico: ID 34
                                          ├── Pata Izq: IDs 20, 21, 22, 23, 24
                                          └── Pata Dcha: IDs 10, 11, 12, 13, 14
```
