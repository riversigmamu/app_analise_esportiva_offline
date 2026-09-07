ANÁLISIS DE MOVIMIENTO DEPORTIVO — GUÍA DE INSTALACIÓN (100% LOCAL)
========================================================================

CONTENIDO DE ESTA CARPETA
----------------------------
- index.html            -> la aplicación (en español)
- vision/                -> biblioteca MediaPipe Tasks Vision (JS + WASM), ya local
- models/                -> CARPETA VACÍA - falta 1 archivo (ver paso 1 abajo)
- LEEME.txt              -> este archivo
- documento-explicativo.docx -> explicación del proyecto para presentar en la feria


PASO 1 — DESCARGAR EL MODELO DE IA (1 archivo, ~5-10 MB)
--------------------------------------------------------------
El entorno donde se generó este paquete no tiene acceso a
storage.googleapis.com, así que el modelo no pudo incluirse de forma
automática. Hazlo una sola vez, en cualquier equipo CON internet:

1. Abre este enlace:
   https://storage.googleapis.com/mediapipe-models/pose_landmarker/pose_landmarker_lite/float16/1/pose_landmarker_lite.task

2. Guarda el archivo exactamente como:
   pose_landmarker_lite.task

3. Colócalo dentro de la carpeta "models/":
   models/pose_landmarker_lite.task

Con esto, toda la app (HTML + JS + WASM + modelo de IA) queda 100% en el
dispositivo. Nunca más necesita internet, ni para cargar ni para
funcionar durante la feria.


PASO 2 — POR QUÉ HACE FALTA UN SERVIDOR LOCAL
--------------------------------------------------
No se puede abrir "index.html" haciendo doble clic o abriéndolo
directamente en el navegador (file://). Los navegadores bloquean por
seguridad la carga de módulos JavaScript y del modelo .task en ese modo,
incluso sin usar internet. Hay que servir la carpeta con un servidor
local (localhost) — sigue siendo 100% offline, solo que no puede ser un
"archivo suelto". Elige la opción según el dispositivo que vayas a usar
en la feria.


OPCIÓN A — CELULAR ANDROID (Termux)
---------------------------------------
1. Instala Termux (descárgalo con internet, una sola vez, antes de la feria).
2. Copia toda esta carpeta al celular, por ejemplo en:
   /sdcard/analise-esportiva-offline
3. Abre Termux y ejecuta:
     pkg install python -y
     cd /sdcard/analise-esportiva-offline
     python -m http.server 8000
4. En Chrome del mismo celular, entra a:
     http://localhost:8000
5. Si aparece "Address already in use" (el puerto ya está ocupado):
     - Usa otro puerto:            python -m http.server 8080
     - O cierra el proceso previo: pkill -f http.server


OPCIÓN B — LINUX (terminal)
--------------------------------
1. Abre una terminal y entra a la carpeta del proyecto:
     cd /ruta/a/analise-esportiva-offline
2. Verifica que tienes Python 3 instalado:
     python3 --version
   (si no lo tienes: sudo apt install python3   — solo esta vez, con internet)
3. Levanta el servidor local:
     python3 -m http.server 8000
4. Abre el navegador (en el mismo equipo, o en un celular conectado a la
   misma red Wi-Fi/hotspot local) y entra a:
     http://localhost:8000
   o, desde otro dispositivo en la misma red:
     http://<IP-de-esta-computadora>:8000
   (para ver la IP: comando  hostname -I )
5. Para detener el servidor: Ctrl+C en la terminal.
6. Si el puerto 8000 ya está en uso:
     python3 -m http.server 8080     (y usa ese número en la URL)


OPCIÓN C — WINDOWS (terminal / PowerShell)
-----------------------------------------------
1. Instala Python desde https://python.org (una sola vez, con internet;
   durante la instalación marca la casilla "Add Python to PATH").
2. Abre el "Símbolo del sistema" (cmd) o "PowerShell".
3. Entra a la carpeta del proyecto, por ejemplo:
     cd C:\Users\TU_USUARIO\Downloads\analise-esportiva-offline
4. Levanta el servidor local:
     python -m http.server 8000
   (si "python" no se reconoce, prueba con:  py -m http.server 8000 )
5. Abre el navegador (Chrome/Edge) y entra a:
     http://localhost:8000
6. Para ver la app desde el celular de la feria conectado a la misma red:
     - Averigua la IP de la PC:   ipconfig   (busca "Dirección IPv4")
     - En el navegador del celular entra a:  http://<esa-IP>:8000
7. Para detener el servidor: Ctrl+C en la terminal.
8. Si el puerto 8000 ya está en uso, usa otro número, por ejemplo:
     python -m http.server 8080


USAR COMO APP (ícono en pantalla, sin barra de direcciones)
-----------------------------------------------------------------
Después de abrir http://localhost:8000 (o la IP correspondiente) en
Chrome del celular, usa el menú ⋮ → "Agregar a la pantalla de inicio".
El acceso directo abre en modo app, a pantalla completa.


CONSEJO DE PRUEBA
--------------------
Prueba todo esto ANTES del día de la feria, con el wi-fi/datos del
dispositivo apagados, para confirmar que realmente funciona sin
internet (después de tener el modelo descargado en "models/").


IMPORTANTE
------------
Esta aplicación es una demostración educativa para feria de ciencias.
No realiza diagnóstico médico. Ver "documento-explicativo.docx" para el
detalle completo de alcances y limitaciones.
