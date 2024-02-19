# Minando los datos de las Elecciones Locales de Colombia - 2023

Este proyecto buscó la forma de automatizar y facilitar la obtención de los datos publicados en el Preconteo de la Registraduría de manera que cualquier persona interesada pudiera, en unos pocos pasos, obtener una base de datos completa sin necesidad de hacer la digitación manual.

Naturalmente esto es minería de datos y se acoge a la disponibilidad que permita la Registraduría. La lógica del código es la siguiente:

- **Obtención de los puestos de votación**  
  En el backend de cada puesto de votación que se puede explorar en la página del preconteo, existe un archivo vinculado llamado nomeclator.json que contiene los códigos de todos los puestos de votación. Este código único permite reconocer el departamento, el municipio y otras variables de identificación del puesto de votación. Veamos por ejemplo el código del Colegio Santa Isabel de Hungria que es el Puesto 1 de la Zona 1 de Cali: https://resultadosprec2023.registraduria.gov.co/asamblea/6802/colombia/valle/cali/zona01/col-santa-isabel-de-hungria-aguacatal  
  El código de este puesto es 31001010107 que sea lee así: 310 = Valle del Cauca, 01 = Cali, 010107 = Información adicional del puesto. Como se puede ver, existen prefijos para circunscripciones departamentales y municipales de manera que identificando estos prefijos se puede minar los datos de todo un grupo de poblaciones.  
  En el tutorial de la sección siguiente se explica cómo conseguir este código.
  El código ya está conectado a la url del nomenclator.json pero de cualquier manera se añadió a este repositorio una copia por si hay problemas posteriores de acceso.

- **Obtención de los resultados electorales**  
  Luego de la obtención del prefijo deseado (ejemplo: deseo obtener todos los datos del Valle entonces voy a trabajar con el prefijo 310) la segunda parte del código itera múltiples veces sobre una estructura de url donde solo se irá cambiando, automáticamente, el código siguiente al prefijo. El usuario acá no debe hacer nada diferente a ejectuar el código.
  Por otro lado, el usuario sí puede modificar la corporación de la que desea obtener votos. En el código hay más detalles pero cambiando solo dos letras de la url base de la iteración puede descargar los datos de asamblea, concejo, alcaldía, gobernación o jal.  
  Los archivos .CSV que están en el repositorio son ejemplos de resultados con algo de procesamiento adicional.

**_Recomendaciones_**: Leer el paso a paso para obtener los prefijos y usar el código `VotacionColombia2023_VersionJupyter.ipynb` en Google Colab (este es más fácil de entender para quienes no están familiarizados con Python). Dentro del código están las indicaciones específicas a cada lógica, leerlas también.

**Disclaimer**: Este código está cubierto por una licencia GPL 3.0. Es un código relativamente sencillo, el valor de este proyecto está realmente en la identificación de la lógica de conexión de datos en el backend y su aprovechamiento. Cada uno es libre de usar y modificar el código a su necesidad y se sugiere otorgarme los créditos correspondientes. Para mayor información ver `LICENSE.txt`.

## Contacto

Nicolás Cardona - [@cardonanl](https://twitter.com/CardonaNL) - [nicolascardona.com](https://www.nicolascardona.com/)

Cualquier inquietud no dude en contactarme.

# ¿Cómo obtener los códigos bases para la iteración?

## Paso 1

- En la página https://resultadosprec2023.registraduria.gov.co/ entre a la corporación deseada, escoja un depratamento, un municipio, una zona y directamente un puesto de votación. No se recomiendo elegir comuna.
- Usando Google Chrome (ie), presione click derecho en una zona vacia y selecciones `Inspeccionar`.

![Paso1](https://github.com/cardonanl/EleccionesLocalesColombia2023/assets/85651740/5efb733f-097c-488e-875b-6c7b83099a25)

## Paso 2

- Esto abrirá una nueva visualización en su misma pantalla. En la barra superior seleccione la opción `Network`.
- Esto le deberá mostrar una serie de archivos. Si no cargan, presione CTRL + R.
- Dentro de la lista de archivos, busque alguno que contenga un número y sea formato .json; en el ejemplo es 31001010107.json

![Paso2](https://github.com/cardonanl/EleccionesLocalesColombia2023/assets/85651740/7b1b678d-5369-4349-b07e-4a2f9982b6b7)

## Paso 3
- Los tres primeros números son el prefijo del departamento y los cinco primeros números son el prefijo del municipio.
- Con el número identificado, dirijase al código `VotacionColombia2023_VersionJupyter.ipynb` y siga las demás instrucciones.
- Si esta teniendo problemas para copiar el número o desea explorar ese archivo (31001010107.json contiene en un formato especial los datos electorales del puesto en cuestión y puede ser explorado por otros medios) presione doble click y se le abrirá una nueva ventana.
- En el código podrá encontrar un algoritmo de prueba para obtener solo los datos electorales de un solo puesto de votación elegido si así se desea.

![Paso3](https://github.com/cardonanl/EleccionesLocalesColombia2023/assets/85651740/b634ece9-32d2-4f4a-b586-340e5042da63)
