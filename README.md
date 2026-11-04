# 📊 CA3 Scope — Osciloscopio digital y sistema de adquisición en tiempo real

[![Versión](https://img.shields.io/badge/Versi%C3%B3n-v1.0.0-0284C7.svg?style=flat-square)](https://github.com/)
[![Plataforma](https://img.shields.io/badge/Plataforma-Windows%2010%20%7C%2011%20(64--bit)-1E293B.svg?style=flat-square&logo=windows)](https://microsoft.com/windows)
[![Entorno](https://img.shields.io/badge/Distribuci%C3%B3n-Portable%20(Sin%20instalaci%C3%B3n)-16A34A.svg?style=flat-square)](https://github.com/)
[![Institución](https://img.shields.io/badge/UNLP-Facultad%20de%20Ingenier%C3%ADa-D97706.svg?style=flat-square)](https://www.ing.unlp.edu.ar/)

Repositorio oficial de distribución binaria y ejecutables portátiles de **CA3 Scope** para los estudiantes de la asignatura **Control Automático III (Código E1501)** — Departamento de Electrotecnia, Facultad de Ingeniería, Universidad Nacional de La Plata.

---

## ⚡ Descarga rápida

La aplicación no requiere instalación previa de Python, librerías adicionales ni permisos de administrador en el sistema operativo.

| Paquete | Versión | Archivo | Plataforma |
| :--- | :---: | :---: | :---: |
| **CA3 Scope** | `v1.0.0` | [`CA3Scope_v1.0.0.zip`](https://github.com/ca3-unlp/CA3Scope/releases/tag/CA3Scope_v1.0.0) | Windows 10 / 11 (64-bit) |

> 💡 **Nota:** También podés descargar el paquete directamente desde la sección lateral derecha de **[Releases](../../releases)** de este repositorio.

---

## 🚀 Guía de instalación y puesta en marcha

Seguí estos 3 sencillos pasos para comenzar a utilizar la aplicación:

### 1. Descomprimir el archivo ZIP (obligatorio)
Una vez descargado `CA3Scope_v1.0.0.zip`:
* Hacé clic derecho sobre el archivo descargado y seleccioná **"Extraer todo..."**.
* Elegí una carpeta de tu computadora (por ejemplo en tu `Escritorio`, `Documentos` o en un `Pendrive USB`).
* ⚠️ **ADVERTENCIA:** **No ejecutes la aplicación directamente dentro del explorador de archivos comprimidos sin extraer**. La aplicación requiere acceder a los binarios dinámicos ubicados en su carpeta `_internal/`. Si se ejecuta sin descomprimir, el sistema operativo impedirá la carga de librerías.

### 2. Abrir la aplicación
* Ingresá a la carpeta descomprimida `CA3Scope_v1.0.0`.
* Hacé doble clic en el archivo ejecutable principal:
  ```text
  CA3Scope.exe
  ```

### 3. Aviso de Windows SmartScreen (primera ejecución)
Al tratarse de un ejecutable académico compilado para la cursada y no contar con un certificado de firma comercial pago, es posible que Windows muestre la ventana azul de protección (*"Windows protegió su PC"*):
1. En dicha ventana flotante, hacé clic en el enlace **"Más información"**.
2. Aparecerá un nuevo botón inferior: hacé clic en **"Ejecutar de todos modos"**.
3. La aplicación se abrirá de inmediato y Windows recordará tu confirmación para las siguientes veces.

---

## 🛠️ Capacidades principales del instrumento

**CA3 Scope** ha sido diseñado específicamente para simplificar los ensayos de laboratorio de control, la sintonía de controladores y el análisis dinámico de procesos:

* 📡 **Adquisición multicanal en tiempo real:** Adquiere hasta 8 canales simultáneos mediante conexión serie USB-UART. Soporta transmisión de texto plano **ASCII (CSV)** y protocolo empacado de alta velocidad **Binario 16-bit** con cabecera de resincronización automática (`0xAA 0x55`) hasta $1000\text{ Hz}$.
* 🧪 **Simulador interno de señales:** Permite realizar prácticas experimentales, mediciones y sintonías desde casa sin necesidad de hardware físico conectado (seleccionando el puerto `SIMULADOR`). Genera señales en milivoltios enteras representativas de conversores ADC.
* 🎯 **Sistema de disparo (trigger) avanzado:**
  * Modos: **Normal** (redispado continuo sincronizado), **Single Shot** (captura única de transitorios ante escalón) y modo híbrido **Continuo + Trigger** (desplazamiento continuo con congelamiento temporal por *Holdoff*).
  * Posicionamiento de **pre-trigger** (del 0% al 100%) para observar la historia previa al evento ($t < 0$).
  * Flancos ascendente ($\uparrow$), descendente ($\downarrow$) o ambos ($\updownarrow$), e histéresis anti-ruido configurable.
* 🔍 **Navegación gráfica y zoom bidireccional:**
  * **Herramienta lupa (`[Lupa]`):** Selección por recuadro elástico con el botón izquierdo del mouse para ampliar zonas de interés.
  * **Zoom direccional:** `Ctrl + Rueda` para zoom exclusivo horizontal (tiempo) y `Shift + Rueda` para zoom exclusivo vertical (amplitud).
  * Botón **`[Restablecer]`** o doble clic sobre la gráfica para recuperar el encuadre automático global.
* 📐 **Escalas independientes de canales (`[Escalas]`):**
  * Factor multiplicador independiente por canal (preset predeterminado a `0.001` para convertir automáticamente lecturas en $\text{mV}$ de microcontroladores a $\text{Volts}$).
  * Botones rápidos `[Todos a 0.001 (mV)]` y `[Todos a 1.0 (V)]`.
* 📏 **Cursores interactivos y estadísticas automáticas:**
  * 4 cursores interactivos ($V_1, V_2, H_1, H_2$) con interpolación continua sobre la traza y lecturas instantáneas de $\Delta t$, frecuencia equivalente ($1/\Delta t$) y $\Delta V$.
  * Tabla de métricas estadísticas en tiempo real: $V_{\max}$, $V_{\min}$, $V_{p2p}$, valor medio $\bar{V}$ (DC), mediana $V_{med}$, desviación estándar $\sigma$ (equivalente al rizado AC $V_{rms,ac}$), frecuencia fundamental por cruce por cero y período.
  * Selector de origen de cálculo: *Ventana visible*, *Todos los datos* o *Entre cursores V1-V2*.
* 🧮 **Menú Herramientas:**
  * **Superposición de modelos teóricos $G(s)$:** Permite simular y superponer en tiempo real la respuesta analítica de funciones de transferencia continuas (Polinomiales o Ceros/Polos/Ganancia ZPK con retardo puro $L$) ante cualquier canal real de entrada, calculando coeficientes de ajuste ($R^2$, MAE).
  * **Canales matemáticos virtuales:** Genera trazas sintéticas en vivo ($Ch_A - Ch_B$ para errores de seguimiento $r - y$, derivadas numéricas con filtro suavizador e integrales acumuladas).
* 💾 **Exportación de datos:** Exportación flexible de rangos a archivos **CSV**, archivos binarios de **MATLAB (.mat)** (con script de importación automática provisto) y capturas de imagen **PNG** en alta resolución.

---

## 📖 Documentación oficial

El manual de usuario completo de la cátedra se encuentra disponible en formato PDF:

* 📄 **[Manual de usuario oficial (PDF en línea)](https://cdn.jsdelivr.net/gh/saavedramarcosdavid/ca3_scope_manual@main/Manual_Usuario_CA3Scope.pdf)**
* También podés acceder directamente desde la aplicación abriendo el menú **Ayuda $\to$ Acerca de CA3 Scope...** y haciendo clic en **"📖 Abrir Manual de Usuario (PDF)"**.

---

## 🔌 Compatibilidad de hardware

CA3 Scope es agnóstico a la placa de desarrollo utilizada siempre que transmita por puerto serie USB:
* **Microcontroladores:** Arduino UNO / Nano (ATmega328P), ESP32, STM32 (BluePill), Raspberry Pi Pico, PIC / dsPIC.
* **Conversores USB-UART:** CH340, FTDI FT232R, CP2102, PL2303.
* **Firmwares de referencia:** En el repositorio de desarrollo se incluyen firmwares de ejemplo optimizados tanto para modo ASCII como para modo Binario con interrupciones por Timer a 1 kHz.

---

## 🏛️ Información institucional y cátedra

* **Asignatura:** Control Automático III (Código E1501)
* **Departamento:** Departamento de Electrotecnia
* **Institución:** Facultad de Ingeniería — Universidad Nacional de La Plata (UNLP)
* **Año lectivo:** 2026

---

## 🔒 Propiedad intelectual y uso académico

Este software es de **uso exclusivo para las actividades académicas y de laboratorio** de la asignatura **Control Automático III (E1501)** de la Facultad de Ingeniería de la Universidad Nacional de La Plata.

**Todos los derechos reservados.** No se autoriza su redistribución pública, modificación ni uso con fines comerciales fuera del marco pedagógico oficial de la cátedra sin la previa autorización escrita de sus autores.
