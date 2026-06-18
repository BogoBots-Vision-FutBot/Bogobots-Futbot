# Bogobots-Futbot



## Enfoque
Nuestro enfoque en nuestra solucion para este reto, consiste en analizar por medio de computer vision los partidos de la **Copa Futbot 2026**, es poder identificar la informacion y acontecimientos mas importantes para un facil seguimiento y analisis del partido, tales como los mencionados en [Outputs](#Outputs).


## Arquitectura del proyecto

Nuestro proyecto procesa un video frame por frame para poder identificar todos los inputs que necesitamos para poder regresar todos los outpus mencionados en [Outputs](#Outputs), a continuacion se presenta el pipeline que realiza nuestro proyecto frame por frame.


### Pipeline




## Outputs
- Contador de goles de ambos equipos
- Cronometro de un robot fuera de la cancha debido a un penalti por equipo
- Segmentacion y identificacion de robots
- Identificador de robots del mismo equipo y de diferente equipo
- Identificacion de la pelota con las que se hace puntaje
- Homografia del partido incluyendo a los robots y la pelota
- Contador de colisiones
- Heatmap de la posicion y movimiento de los robots atraves del partido


## Requisitos de Hardware y Software
- Windows 10 o 11
- MacOS 13 en adelante
- Linux (recomendado)
- Acceso a Internet
- Google Collab

## Instalaciones y Reproduccion

Debido al gran gasto computacional que el modelo SAM3 genera dentro de nuestro proyecto, lo desarollamos y probamos en la plataforma **Google Collab**, con esto nos aseguramos que cualquier persona sin importar su dispositivo de computo probar nuestro Proyecto.

1. Entra en tu navegador de preferencia
   
2. En el buscador busca <pre> ``` Google Collab ``` </pre>

3.Entra y crea un nuevo notebook

4. Cambiar el entorno de ejecución a GPU
Es obligatorio usar GPU para que SAM3 funcione en un tiempo razonable.
En la barra superior de Colab:
Entorno de ejecución -- Cambiar tipo de entorno de ejecución -- T4 GPU -- Guardar

5.En la primera celda ejecuta:
```python
from google.colab import drive
drive.mount('/content/drive')
```
Se abrirá una ventana pidiendo permisos — acéptalos con tu cuenta de Google.****

6.En una nueva celda ejecuta:
```python
%cd /content/drive/MyDrive
!git clone https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot.git
%cd Bogobots-Futbot

```
Esto descargará todos los archivos del proyecto directamente en tu Google Drive.

7.En una nueva celda ejecuta:
```python
!pip install supervision ultralytics trackers
```

8. Descarga del modelo
Solicita acceso en: https://huggingface.co/facebook/sam3
Descarga el archivo llamado sam3.pt
Mete este archivo en la seccion "Mi Unidad" de tu Drive

9. Abrir y configurar el notebook
En el panel izquierdo de Colab ve a:
Archivos -- /content/drive/MyDrive/tu-repo/main.ipynb
Haz doble clic para abrirlo.

Localiza la siguiente variable y cámbiala al nombre de tu archivo de video:
```python
video_path_relative = 'tu_video.mp4'
```
El video que ejecutes debe de estar en "Mi unidad"







