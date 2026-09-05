# 🧰 Armbian-Openbox-TV3S-S905X

Una distribución basada en Armbian diseñada para optimizar, parchear y completar la instalación del sistema en dispositivos TV3s y TV Boxes con procesador **Amlogic S905X**.

El alcance actual del proyecto se centra en el SoC **Amlogic S905X** sobre la placa **P212** y la tarjeta de red **Realtek RTL8189ES**. Aunque este es el hardware inicial de desarrollo (y el disponible para pruebas), el proyecto está abierto a incorporar soporte para nuevos componentes en el futuro.

Este proyecto nace como una solución comunitaria ante la falta de herramientas terminadas que permitan aprovechar de forma efectiva el potencial de estos dispositivos, facilitando el acceso a drivers y kernels actualizados de forma independiente.

---

### ⚠️ Requisito Previo (Paso 0)
Este proyecto **no reemplaza tu sistema actual ni elimina Android TV**. El ecosistema funciona en modo dual. Antes de usar esta caja de herramientas, debes:
1. Descargar e instalar una imagen base de Armbian para S905X en tu tarjeta MicroSD.
2. Configurar e iniciar el TV Stick desde la MicroSD por primera vez.

---

### 🚀 Hoja de Ruta del Proyecto (Iteración paso a paso)

*   [ ] **Fase 1: Motor del Sistema (Kernel & Conectividad):** Compilación automatizada en la nube de un Kernel moderno (6.x Edge) que incluye los drivers de red críticos (Realtek) actualmente inaccesibles. 
    * *Estado:* Pre-lanzamiento. Pendiente de pruebas finales y análisis de un posible DKMS.
*   [ ] **Fase 2: Entorno Base:** Generación de un entorno gráfico/consola dual ligero que permita sacar el máximo provecho al hardware ARM64. 
    * *Estado:* En curso.
*   [ ] **Fase 3: Almacenamiento Híbrido:** Script de post-instalación para montar de forma segura la memoria interna (eMMC) y compartir archivos con Android TV. 
    * *Estado:* En análisis con scripts plantilla iniciales.
*   [ ] **Fase 4: Inyección de Rendimiento:** Activación automatizada de zRAM (compresión de memoria) para optimizar los límites físicos de la RAM (1GB/2GB). 
    * *Estado:* En análisis.
*   [ ] **Fase 5: Estación de Trabajo Ligera:** Scripts de instalación optimizada para VS Codium y Chromium Educativo con bloqueador de anuncios integrado. 
    * *Estado:* Chromium funcional; desarrollo continuo en progreso.

---
_Creado para democratizar el acceso a hardware de ultra-bajo costo con fines educativos y sociales. Este proyecto se acoge a la licencia GPL-3.0. Todas las marcas, logos y aplicaciones de terceros instaladas opcionalmente a través de los scripts pertenecen a sus respectivos propietarios legales. Esta distribución solo automatiza y optimiza su despliegue en comunidades sin fines de lucro._

