

# Aplicación IoT: Ejemplo de Línea de Comandos IEEE 802.15.4

**Curso:** Desarrollo de Sistemas IoT  
**Universidad:** Universidad Nacional de Colombia  
**Autor:** Laura Daniela Alarcón Castaño  
**Plataforma:** ESP-IDF v5.5  
**Fecha:** 2025  
---

## 1. Introducción
Este repositorio demuestra el uso de la Línea de Comandos (CLI) para el protocolo **IEEE 802.15.4**. La CLI expone APIs de configuración y gestión a través de una interfaz de consola, permitiendo interactuar directamente con la capa física y MAC del microcontrolador.



Para este ejemplo, se utiliza como base el código oficial proporcionado por Espressif. El procedimiento para obtener e inicializar el proyecto es el siguiente:

1.  Presionar `Ctrl + Shift + P` para abrir la paleta de comandos en VS Code.
2.  Buscar y ejecutar `ESP-IDF: Show Examples` (seleccionando la versión de ESP-IDF instalada).
3.  Navegar y seleccionar `ieee802154/ieee802154_cli` (IEEE 802.15.4 Command Line Example).
4.  Seleccionar la carpeta donde se creará el proyecto.

## 2. Requisitos del Sistema
* **Hardware:** Placa de desarrollo ESP32-C6-DevKitC-1 v1.2 (conectada vía USB, puerto puente CH343).
* **Software:** Código base descargado y entorno ESP-IDF configurado.

## 3. Metodología y Configuración
El ejemplo incluye funciones predeterminadas optimizadas para IEEE 802.15.4, por lo que no es necesario realizar modificaciones en el código fuente original. A continuación, se procede a configurar el *target* (objetivo), compilar y flashear el proyecto utilizando la paleta de comandos (`Ctrl + Shift + P`):

1.  **Selección del Puerto:** `ESP-IDF: Select Port to Use (COM, tty, usbserial)`. Seleccionar el puerto correspondiente al ESP32-C6.
2.  **Selección del Target:** `ESP-IDF: Set Espressif Device target`. Elegir `ESP32C6`.
3.  **Compilación y Ejecución:** `ESP-IDF: Build, Flash and Start a Monitor on Your Device`.


## 4. Resultados y Análisis

### 4.1. Configuración de Transmisión (TX)
Utilizando los comandos CLI disponibles en el monitor serial, se configuró el ESP32-C6 como transmisor. Se definieron los siguientes parámetros clave:
* **PAN ID:** Identificador de la red de área personal.
* **Dirección (Address):** Dirección del dispositivo.
* **Canal:** Frecuencia de operación.

Posteriormente, se envió un mensaje corto para verificar el correcto funcionamiento de la transmisión de datos, tal como se evidencia en la siguiente captura:


### 4.2. Medición de Energía y CCA
Adicionalmente, se realizaron pruebas de medición de energía (Energy Detect - ED) durante una duración específica, variando parámetros como el umbral (threshold) y la potencia de transmisión (Tx power).

Aunque la varianza entre los datos obtenidos no fue significativa en este escenario de prueba controlado, el experimento valida la funcionalidad de **CCA (Clear Channel Assessment)**, crucial para evitar colisiones en redes inalámbricas.



## 5. Conclusiones
Esta aplicación fundamental permite comprender la operación práctica del estándar de comunicación 802.15.4. A través de la CLI, fue posible:
1.  Configurar dispositivos como transmisores o receptores de manera dinámica.
2.  Gestionar parámetros de red (PAN ID, Canales).
3.  Realizar diagnósticos de capa física mediante la medición de energía.

El ejercicio demuestra la versatilidad del ESP32-C6 para aplicaciones IoT de bajo consumo y redes malladas (Mesh).