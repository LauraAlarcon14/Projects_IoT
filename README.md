# 📚 Repositorio: Desarrollo de Sistemas IoT (ESP32-C6)

**Curso:** Desarrollo de Sistemas IoT  
**Universidad:** Universidad Nacional de Colombia  
**Autor:** Laura Daniela Alarcón Castaño  
**Plataforma Base:** ESP-IDF v5.5.0 (Target: ESP32-C6)  


---

## 1. Introducción y Proyectos Incluidos

Este repositorio contiene dos proyectos de firmware desarrollados para el microcontrolador **ESP32-C6**, demostrando tanto la conectividad de alto nivel (IoT en la nube) como la interacción de bajo nivel con el protocolo de radio IEEE 802.15.4.

| Carpeta | Funcionalidad Principal | Protocolo Clave | Archivo Principal |
| :--- | :--- | :--- | :--- |
| `mqtt-led-control` | Control de LED RGB WS2812 y sincronización de estado con Broker MQTT (AWS EC2). | Wi-Fi / MQTT | `station_example_main.c` |
| `ieee802154-cli` | Interfaz de Línea de Comandos (CLI) para diagnóstico y configuración de la radio 802.15.4. | IEEE 802.15.4 | `esp_ieee802154_cli.c` |

---

## 2. Proyecto 1: Control de LED RGB con MQTT y AWS

Este es un sistema IoT completo que simula una aplicación de monitoreo y control en tiempo real.

### 2.1 Arquitectura del Sistema

El sistema utiliza Mosquitto y AWS EC2 como intermediarios en la nube para sincronizar el estado del dispositivo físico con una interfaz web.

1.  **Dispositivo (ESP32-C6):** Conecta a WiFi, usa el driver RMT para controlar el LED RGB (GPIO 8) y publica el color actual en MQTT (QoS 0).
2.  **Nube (AWS EC2):** Aloja el **Broker Mosquitto** central.
3.  **Visualización:** El cliente web (via WebSockets) se suscribe al tópico para reflejar el color.



### 2.2 Componentes de Firmware

El firmware utiliza el componente de LED Strip de Espressif (`v2.5.5`) para gestionar el protocolo WS2812.

| Componente | Detalle |
| :--- | :--- |
| **Driver LED** | `espressif/led_strip: 2.5.5` |
| **GPIO LED** | `GPIO 8` |
| **Tópico Publicación** | `esp32/led` |

---

## 3. Proyecto 2: CLI IEEE 802.15.4 (Diagnóstico)

Este proyecto valida las capacidades de radio del ESP32-C6 para el estándar 802.15.4, proporcionando una herramienta de diagnóstico de bajo nivel accesible a través del Monitor Serial (UART).

### 3.1 Interfaz de Comandos (`ieee802154>`)

La CLI permite la manipulación directa de las capas PHY y MAC para pruebas de red.

| Comando (Ejemplo) | Propósito | Capa |
| :--- | :--- | :--- |
| `ieee802154 set_channel 26` | Configurar Frecuencia | PHY |
| `ieee802154 set_pan_id 0x1234` | Configurar ID de Red | MAC |
| `ieee802154 tx 0x0001 "Test"` | Enviar un paquete de prueba | MAC/PHY |
| `ieee802154 ed 5 1` | **Energy Detect (ED)**: Medir ruido del canal | PHY |

### 3.2 Componentes de Software

El proyecto se basa en componentes del ESP-IDF registrados a través de `CMakeLists.txt`: `ieee802154`, `console`, `cmd_ieee802154` y `cmd_system`.

---

## 4. Entorno de Desarrollo y Flasheo

### 4.1 Configuración de la Plataforma

| Parámetro | Valor |
| :--- | :--- |
| **Target** | `esp32c6` |
| **IDF Version** | `5.5.0` |
| **Flash Mode** | `dio` (Dual I/O) |
| **Frecuencia Flash** | `80m` (80 MHz) |
| **Tamaño Flash** | `2MB` |

### 4.2 Mapa de Memoria (Argumentos de Flasheo)

| Offset | Archivo Binario | Propósito |
| :--- | :--- | :--- |
| `0x0` | `bootloader/bootloader.bin` | Código de arranque |
| `0x8000` | `partition_table/partition-table.bin` | Tabla de particiones (NVS, app) |
| `0x10000` | `mqtt-server.bin` | Binario de la aplicación principal |

---

## 5. Instrucciones de Compilación

Para compilar y flashear cualquiera de los proyectos, asegúrese de que el entorno `ESP-IDF v5.5` esté activo y navegue al directorio del proyecto:

```bash
# 1. (Opcional) Configurar parámetros de WiFi, MQTT, etc.
idf.py menuconfig

# 2. Compilar, Flashear y Abrir el Monitor Serial
idf.py build flash monitor