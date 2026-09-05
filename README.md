# 🧰 Armbian-Openbox-TV3S-S905X

Una distribución basada en Armbian diseñada para optimizar, parchear y completar la instalación del sistema en dispositivos TV3s y TV Boxes con procesador **Amlogic S905X**.

### 📋 Alcance y Entorno de Desarrollo
El alcance actual del proyecto se centra en el SoC **Amlogic S905X** sobre la placa **P212** y la tarjeta de red **Realtek RTL8189ES**. Aunque este es el hardware inicial de desarrollo (y el disponible para pruebas), el proyecto está abierto a incorporar soporte para nuevos componentes en el futuro. 

Actualmente, todas las pruebas se realizan bajo **Debian Trixie**, específicamente con la versión de **kernel 6.18.48 (trunk 30)**. No se garantiza el funcionamiento en otras versiones, pero eres libre de probar si cuentas con los conocimientos necesarios, ajustando la distribución en el script `pre_instalacion.sh`.

Este proyecto nace como una solución comunitaria ante la falta de herramientas terminadas que permitan aprovechar de forma efectiva el potencial de estos dispositivos, facilitando el acceso a drivers y kernels actualizados de forma independiente.

---

### ⚠️ Advertencias Importantes

> ❗ **Scripts adicionales:** El repositorio puede contener scripts adicionales a los mencionados en este README. Úsalos con precaución y responsabilidad; algunos son remanentes de la fase de desarrollo y no son necesarios para el día a día.
> 
> 💀 **Peligro de Brick (Carpeta `gestion_mmc_plantilla`):** Estos scripts están actualmente **en desarrollo**. Son plantillas funcionales para mi hardware específico, pero no los ejecutes en el tuyo a menos que sepas exactamente qué hace cada comando, ya que podrías generar un brick irreparable en tu dispositivo.

---

### 🛠️ Requisito Previo (Paso 0)
Este proyecto **no reemplaza tu sistema actual ni elimina Android TV**. El sistema funciona en modo dual. Antes de comenzar, necesitas:
1. Descargar e instalar una imagen base de Armbian para S905X en tu tarjeta MicroSD.
2. Un ordenador de preparación con sistema operativo **base Debian** y un usuario con **permisos de administrador (sudo)**.

---

### 🚀 Pasos de Instalación

1. **Habilitar Hardware:** Ejecuta el script `hardware_enablement_s905x.sh` en el ordenador que uses para grabar la imagen (o donde tengas la tarjeta conectada). Este script realiza la configuración necesaria para que la imagen arranque en el TV Stick TV3S.
2. **Descarga de Controladores:** Entra al directorio `instalador_wifi` y ejecuta `pre_instalacion.sh`. Descargará el software necesario para construir los controladores en tu TV Box.
   * *Nota:* Debido a la inestabilidad y bajas de paquetes en los repositorios de *Aurora deb*, se trabaja en un espejo. Si fallan, se sugiere reintentar más tarde o usar paquetes compatibles con Debian Trixie bajo tu propio criterio.
3. **Primer Arranque (¡Cuidado con el Wi-Fi!):** Inserta la tarjeta en el equipo S905X e inicia la configuración inicial. Si usas la tarjeta **RTL8189ES**, **indica "NO" cuando te pregunte si deseas configurar la red**. De lo contrario, el controlador defectuoso de la imagen base congelará el sistema en un ciclo infinito difícil de recuperar.
4. **Post-Instalación Fase 1:** Ejecuta el script `post_instalacion_fase1.sh` para obtener el kernel y las herramientas de desarrollo necesarias para compilar. Reinicia el equipo al terminar.
5. **Post-Instalación Fase 2 (Activar Red):** Ejecuta `post_instalacion_fase2.sh` para compilar e instalar el controlador estable de la tarjeta **RTL8189ES**. Una vez instalado, ya puedes conectar el equipo a internet usando `armbian-config` o tu método preferido. *(Puedes detenerte aquí si buscas un sistema puramente de consola / Server)*.
6. **Instalar Entorno Gráfico:** Ve a la carpeta `instalar_openbox` y ejecuta `instalar_openbox.sh` para desplegar el entorno de escritorio Openbox en su forma base. *(Requiere conexión a internet)*.
7. **Instalar Software Base:** Ejecuta el script `post_instalacion_fase3.sh` (ubicado provisionalmente en `instalador_wifi`). El asistente te preguntará de forma guiada qué grupos de programas deseas instalar con un breve resumen de su función.
   * *Nota:* Este script sigue en desarrollo; es seguro, pero podría omitir software u optimizaciones previstas.

---

### 🗺️ Hoja de Ruta del Proyecto (Iteración paso a paso)

*   [ ] **Fase 1A: Conectividad y Red (Drivers Realtek):** Integración y empaquetado del controlador de red crítico (Realtek RTL8189ES) actualmente inaccesible en imágenes base.
    * *Estado:* Pre-lanzamiento. Pendiente de pruebas finales y análisis de un posible DKMS para asegurar la persistencia del controlador.
*   [ ] **Fase 1B: Motor del Sistema (Kernel en la Nube):** Compilación automatizada en la nube de un Kernel moderno (6.x Edge).
    * *Estado:* En pausa temporal. Actualmente el proyecto utiliza una imagen con kernel base estable mientras se consolida el entorno de desarrollo.
*   [ ] **Fase 2: Entorno Base:** Generación de un entorno gráfico/consola dual ligero.
    * *Estado:* En curso. *(A resaltar: Analizando la integración plena de `apt-fast` a nivel de sistema)*.
*   [ ] **Fase 3: Instalación sin Internet:** Creación de scripts totalmente offline (en pares preparador/instalador) para zonas de difícil conectividad.
    * *Estado:* Planeado.
*   [ ] **Fase 4: Almacenamiento Híbrido:** Script para montar de forma segura la memoria interna (eMMC) y compartir archivos con Android TV.
    * *Estado:* En desarrollo (Plantillas iniciales disponibles en la carpeta `gestion_mmc_plantilla`).
*   [ ] **Fase 5: Inyección de Rendimiento:** Activación automatizada de zRAM para optimizar equipos de 1GB/2GB de RAM.
    * *Estado:* En análisis.
*   [ ] **Fase 6: Estación de Trabajo Ligera:** Scripts de instalación optimizada para VS Codium y Chromium Educativo con adblocker.
    * *Estado:* Chromium funcional; desarrollo continuo en progreso.
*   [ ] **Fase 7: Entorno de Preparación Multiplataforma:** Ampliar el soporte del script del Paso 0 para permitir preparar la MicroSD desde cualquier Linux, WSL, Windows nativo y macOS.
    * *Estado:* Planeado.

---
_Creado para democratizar el acceso a hardware de ultra-bajo costo con fines educativos y sociales. Este proyecto se acoge a la licencia GPL-3.0. Todas las marcas, logos y aplicaciones de terceros instaladas opcionalmente a través de los scripts pertenecen a sus respectivos propietarios legales. Esta distribución solo automatiza y optimiza su despliegue en comunidades sin fines de lucro._

