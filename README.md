# Bogobots-Futbot

## Escuela: Tecnologico de Monterrey - Campus Estado de Mexico

### Miembros del equipo:
1. Nancy Lesly García Jimenez
2. Erick Nicolás Lugo Gonzalez
3. Miguel Bandian Reyes Serrato
4. Leonardo Gracida Munoz

## Proyecto: Deteccion y narractiva de TrutleBots en un partido de futbol en vivo.

Video presentacion en YouTube
[Video presentacion en YouTube](https://www.youtube.com/watch?v=JWTw7fdQiGw)


## Enfoque
Nuestro enfoque en nuestra solucion para este reto, consiste en analizar por medio de computer vision los partidos de la **Copa Futbot 2026**, es poder identificar la informacion y acontecimientos mas importantes para un facil seguimiento y analisis del partido, tales como los mencionados en [Outputs](#Outputs).


## Arquitectura del proyecto

Nuestro proyecto procesa un video frame por frame para poder identificar todos los inputs que necesitamos para poder regresar todos los outpus mencionados en [Outputs](#Outputs), a continuacion se presenta el pipeline que realiza nuestro proyecto frame por frame.


### Pipeline

#### Pipeline general del proyecto:
<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/Pipeline%20Principal%20de%20Procesamiento.png?raw=true" width="200">

A continuacion se presentan las subdivisiones del pipeline para mayor entendimiento y explicacion.

### 1. Transposición de frame

<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/prepocesado_grande.png?raw=true" width="500%">
<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/ejemplo_1.png?raw=true" width=100% >

### 2. Detecciones (Robots)
<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/Etapa%20de%20Detecci%C3%B3n%20e%20Identificaci%C3%B3n%20de%20Equipos.png?raw=true" width=60% >

Para las porterias simplemente usamos el prompt "yellow rectangle" y "blue rectangle", y las detecciones las indexamos a Bytetracker

#### 3. Detecciones (Pelota)
<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/ball_grand_1.png?raw=true" >

<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/robot_%20and_%20ball.gif?raw=true">

### 4. Goles
<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/goles_grande.png?raw=true" width=100% >

<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/ejemplo%20goles.gif?raw=true" width="300">

### 5. Penaltis
<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/penaltis_logica.png?raw=true">
<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/penaltis_ejemplos.gif?raw=true">

### 6. Generacion de mapa tactico
<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/Generaci%C3%B3n%20de%20Mapa%20T%C3%A1ctico.png?raw=true" width="300">
<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/homografia.gif?raw=true">

### 7. Mapa de Calor y Coliciónes
<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/Detecci%C3%B3n%20de%20Colisiones%20y%20Mapa%20de%20Calor.png?raw=true" width="70%">

Para las colisiones se guarda un registro cuando un contato entre mascaras cumple ciertas condiciones, estos se dividieron entre overlap y border touch

<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/Contact.png?raw=true" width="600">

Para detectar overlaps se toman las mascaras y se vuelven arreglos booleanos donde un 1 indica una mascara mientras que el 0 no, se hace una operación para verificar que pixeles se invaden, esto se queda en el registro de colisiones.

<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/Overlap.png?raw=true" width="600">

Si no hubo overlap se revisa el contacto de bordes, se consigue el borde de cada mascara erosionando las mascara y restandosela a la original, despues se dilatan los bordes con un kernel de 5x5, se agregn pixeles de tolerancia para detectar mascaras que anque no se toquen directamente si estan muy cerca una d ela otra, esto queta en el registro de colisones

<img src="https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot/blob/main/images/Border.png?raw=true" width="600">

### 8. Generción de graficas

La ultima celda del colab toma el registro de colisiones generado anteriormente y proyecta los graficos en tres graficas distintas: Una dispersión general de colisiones y dos mapas de calor, uno de overlap y otro de border touch.

## Outputs
- Contador de goles de ambos equipos
- Cronometro de un robot fuera de la cancha debido a un penalti por equipo
- Segmentacion y identificacion de robots
- Identificador de robots del mismo equipo y de diferente equipo
- Identificacion de la pelota con las que se hace puntaje
- Homografia del partido incluyendo a los robots y la pelota
- Contador y registro de colisiones
- Heatmap de la posicion y movimiento de los robots atraves del partido


## Requisitos de Hardware y Software
- Windows 10 o 11
- MacOS 13 en adelante
- Linux (recomendado)
- Acceso a Internet
- Google Collab

## Instalaciones y Reproduccion

Debido al gran gasto computacional que el modelo SAM3 genera dentro de nuestro proyecto, lo desarollamos y probamos en la plataforma **Google Collab**, con esto nos aseguramos que cualquier persona sin importar su dispositivo de computo pueda probar nuestro Proyecto, ya que esta plataforma tiene acceso a GPUs en el plan gratis.

Antes que nada recuerda crear una cuenta en la plataforma de HuggingFace, pedir acceso al repositorio de SAM3. Ya que tengas acceso, genera tu token individual para acceder a tu perfil de HugginFace, copialo y guardalo en las variables de entorno o secrets de Google Colab.

#### Recuerda darle acceso a tu notebook

#### Ejemplo:

<img src="images/secret_example.png?raw=true" width="500">

1.Entra en tu navegador de preferencia
   
2.En el navegador busca <pre> ``` Google Collab ``` </pre>

3.Entra y crea un nuevo notebook

4.Cambiar el entorno de ejecución a GPU

Es obligatorio usar GPU para que SAM3 funcione en un tiempo razonable.
En la barra superior de Colab:
Entorno de ejecución -- Cambiar tipo de entorno de ejecución -- T4 GPU -- Guardar

O puedes usar la GPU G4 si usas google Pro.

5.En la primera celda ejecuta:

```python
from google.colab import drive
drive.mount('/content/drive')
```
Esta seccion es para acceder a tu Drive desde tu colab para mantener todo el flujo dentro de la nube de manera comoda.

Se abrirá una ventana pidiendo permisos — acéptalos con tu cuenta de Google.****

6.En una nueva celda ejecuta:
```python
%cd /content/drive/MyDrive
!git clone https://github.com/BogoBots-Vision-FutBot/Bogobots-Futbot.git
%cd Bogobots-Futbot

```
Esto descargará todos los archivos del proyecto directamente en tu Google Drive folder base.
Si deseas guardar el colab en otro folder  recuerda modificar
```
%cd /content/drive/MyDrive
```
7.En una nueva celda ejecuta:
```python
!pip install supervision ultralytics trackers
```

8.Descarga del modelo

Solicita acceso en: https://huggingface.co/facebook/sam3

Descarga el archivo llamado sam3.pt

Mete este archivo en la seccion "Mi Unidad" de tu Drive

Importante: este archivo debe estar en el mismo folder que to archivo de colab

9.Abrir y configurar el notebook
En el panel izquierdo de Colab ve a:
Archivos -- /content/drive/MyDrive/BOGOBOTS_v3.ipynb
Haz doble clic para abrirlo.

### El repositorio contiene el archivo de colab usado (BOGOBOTS_v3).
Aunquesea aqui esta el link al colab:
[BOGOBOTS_V3](https://colab.research.google.com/drive/1T-l5v0uGgNeDXuKNAFVvsSOoccASOFLg?usp=sharing)

Para el analisis y trackeo lo que debes modificar son las siguientes variables:

Antes que nada en la carpeta vid_img_analisis vamos a agregar imagenes y videos que se pueden usar para el analisis en colab.

Esta variable contiene la imagen del primer frame en el se ajustan los 4 puntos iniciales para la transposicion de la homografia:
```python
image_bgr = cv2.imread("/content/drive/MyDrive/futbot/frame.jpg")
```
Esta variable contiene el path del video final generado por el colab
```python
OUTPUT_VIDEO = "/content/drive/MyDrive/futbot/IMG_9933_sam_v3.mp4"
```
Esta variable contiene el path del video que se va a ingresar para el analisis y procesamiento.
```python
SOURCE_VIDEO = "/content/drive/MyDrive/futbot/source_video.mp4"
```
Esta variable contiene el path del archivo .pet del modelo SAM3

```python
SAM_MODEL = "/content/drive/MyDrive/futbot/sam3.pt"
```

En la parte final del archivo colab se hace la parte del analisis para las colisiones, mapas de calor graficas, etc.

Se deben moficiar estas dos variables:

Este es el path del video aparte para el calculo de las colisiones y mapas de calor
```python
OUTPUT_VIDEO_COLLISIONS = "/content/drive/MyDrive/futbot/BOGOBOTS_v3_with_collisions.mp4"
```

Este es el path del archivo de texto que contiene la informacion necesaria para la creacion de gaficas mostradas anteriormente
```python
OUTPUT_TXT_COLLISIONS = "/content/drive/MyDrive/futbot/all_collision_coordinates.txt
```

Al ya tener estos paths listos dale click a la funcion de Run All

<img src="images/run_all.png?raw=true" width="500">


Esto generara todos los outputs mostrados en el README

### Importante: Todos estos paths son de nuestro entorno si deseas correrlo te recomendamos usar Google Colab pro y cambiar a los folders que tu desees en tu Google Drive. También es importante mencionar que el video usado fue editado eliminando tiempos muertos y acelerando algunas partes para usar menos recursos de GPU durante la ejecución.

## Licencia

Este proyecto está bajo la licencia MIT.  
Consulta el archivo `LICENSE` para más información.

## Créditos

Este proyecto contó con apoyo de herramientas de inteligencia artificial para asistencia en desarrollo y documentación:

- Gemini
- Claude
