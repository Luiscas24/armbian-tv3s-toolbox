# 🧰 Armbian-Openbox-TV3S-S905X

Una distribución basada en Armbian diseñada para optimizar, parchear y completar la instalación del sistema en dispositivos TV3s y TV Boxes con procesador **Amlogic S905X**.

El alcance actual del proyecto se centra en el SoC **Amlogic S905X** sobre la placa **P212** y la tarjeta de red **Realtek RTL8189ES**. Aunque este es el hardware inicial de desarrollo (y el disponible para pruebas), el proyecto está abierto a incorporar soporte para nuevos componentes en el futuro. Actualmente todas las pruebas se están haciendo con Debian Trixie, en particular en la versión de kernel 6.18.48 en el trunk 30. No puedo garantizar su funcionamiento pero sientase libre de probar en otras versiones si cuenta con los conocimientos necesarios, eso si ajustando la distribución en el script pre_instalacion.sh mencionado posteriormente.
Este proyecto nace como una solución comunitaria ante la falta de herramientas terminadas que permitan aprovechar de forma efectiva el potencial de estos dispositivos, facilitando el acceso a drivers y kernels actualizados de forma independiente.

---

### ⚠️ Requisito Previo (Paso 0)
Este proyecto **no reemplaza tu sistema actual ni elimina Android TV**. El ecosistema funciona en modo dual. Antes de usar esta caja de herramientas, debes:
1. Descargar e instalar una imagen base de Armbian para S905X en tu tarjeta MicroSD.
2. Tener un ordenador para preparar la instalación con un sistema operativo de base Debian con un usuario con permisos de administrador. 

Pasos de instalación
1. Ejecute el script hardware_enablement_s905x.sh en el ordenador que esté usando para grabar la imagen o en el que tenga la tarjeta si ya lo ha hecho previamente. Este script hace el proceso de configuración necesaria para que la imagen arranque en el hardware mencionado en el alcance, un TV Stick TV3S. 
2. Ingrese al directorio instalador_wifi y ejecute el script pre_instalacion.sh el cual descargará a su ordenador el software necesario para construir la compilación de controladores en su TV Box, entre ellos el controlador de red.
Nota: Debido al constante cambio y baja de los paquetes en el repositorio de Aurora deb se está trabajando en un repositprio espejo con los paquetes base para este punto, mientras tanto, si están dados de baja sugiero probar cada cierto tiempo razonable o si es entusiasta probar con los de su preferencia, eso si, siempre que sean compatibles con su imagen de instalación y sean para Debian Trixie.
4. Una vez inserte la tarjeta en equipo S905X proceda con la configuración inicial. Si tiene una tarjeta de red RTL8189ES se recomienda tener especial cuidado de indicar **No** en la pregunta donde se permite configurar la red del equipo, ya que posiblemente va a quedar atascado en un ciclo del que es muy dificil salir debido al defectuoso controlador de red incluido en la imagen grabada.
5. Ejecute el script post_instalacion_fase1.sh el cual le permitirá disponer del kernel y software necesario para compilar controladores como el de su tarjeta de red RTL8189ES.
6. Una vez se hayan instalado las herramientas de compilación adecuada y se haya reiniciado el equipo ejecuté el script post_instalacion_fase2.sh para construir e instalar el controlador de su tarjeta RTL8188ES.
7. Una vez instalada la tarjeta de red puede conectar su ordenador usando armbian-config o mediante su método de confianza. Puede dejarlo en este punto si su intención es tener un sistema operativo sin un entorno de escritorio.
8. Para instalar el entorno de escritorio de Openbox propuesto por la ditribución vaya a la carpeta instalar_openbox del proyecto y ejecute el script instalar_openbox.sh con el que tendrá usted acceso a un entorno de escritorio en su forma base. Nota: El actual script requiere conexión a internet.
9. Si desea instalar el software base propuesto por la distribución proceda a ejecutar el script post_instalacion_fase3.sh que provisionalmente se encuentra en el la carpeta instalador_wifi. Durante la ejecución se le irá preguntando sobre la instalación de los diferentes grupos de programas con un somero resúmen su funcionalidad con el fin de que usted pueda tomar una decisión informada sobre que paquetes de software considera de utilidad.
Importante: Si bien el script mencionado es seguro, aun se encuentra en fase de desrrollo y es posible que no instale todo el software para el que está diseñado o no tenga todas las optimizaciones previstas.

---

### 🚀 Hoja de Ruta del Proyecto (Iteración paso a paso)

*   [ ] **Fase 1: Motor del Sistema (Kernel & Conectividad):** Compilación automatizada en la nube de un Kernel moderno (6.x Edge) que incluye los drivers de red críticos (Realtek) actualmente inaccesibles. 
    * *Estado:* Pre-lanzamiento. Pendiente de pruebas finales y análisis de un posible DKMS.
*   [ ] **Fase 2: Entorno Base:** Generación de un entorno gráfico/consola dual ligero que permita sacar el máximo provecho al hardware ARM64. 
    * *Estado:* En curso.
    * *A resaltar: Se está analizando la integración plena de Apt-Fast a nivel del ssitema operativo.
*   []  **Fase 3: Instalación sin internet**: Con el fin de hacer de la distribución más accesible en zonas de dificil conectividad se plantea la generación de scripts totalmente offline en pares preparador/instalador.
*   [ ] **Fase 4: Almacenamiento Híbrido:** Script de post-instalación para montar de forma segura la memoria interna (eMMC) y compartir archivos con Android TV. 
    * *Estado:* En análisis con scripts plantilla iniciales.
*   [ ] **Fase 5: Inyección de Rendimiento:** Activación automatizada de zRAM (compresión de memoria) para optimizar los límites físicos de la RAM (1GB/2GB). 
    * *Estado:* En análisis.
*   [ ] **Fase 6: Estación de Trabajo Ligera:** Scripts de instalación optimizada para VS Codium y Chromium Educativo con bloqueador de anuncios integrado. 
    * *Estado:* Chromium funcional; desarrollo continuo en progreso.
    [] **Fase 7 Entorno de preparación**: Ampliación del soporte de sistemas operativos para la preparación de la distribución: Inicialmente otras distribuciones de núcleo GNU/Linux y posiblemente WSL, pero la idea es hacerlo compatible con Windows, Sistemas GNU/Linux en general y MAC OS 

---
_Creado para democratizar el acceso a hardware de ultra-bajo costo con fines educativos y sociales. Este proyecto se acoge a la licencia GPL-3.0. Todas las marcas, logos y aplicaciones de terceros instaladas opcionalmente a través de los scripts pertenecen a sus respectivos propietarios legales. Esta distribución solo automatiza y optimiza su despliegue en comunidades sin fines de lucro._

