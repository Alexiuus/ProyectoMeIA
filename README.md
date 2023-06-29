# Proyecto MeIA - Segmentación semántica de vehículos en imágenes aéreas de drones usando Aprendizaje profundo

## Integrantes

- `Iván Mandujano González Moreno`
- `Fátima Fonseca Rodríguez`
- `Alexis Centeno`
- `José Antonio Valadez Ortega`
- `Sergio Mauricio Nuñez`

## Introducción
El propósito de este proyecto es mejorar la calidad de la red neuronal provista utilizando técnicas de aumentación de datos y modificando los parámetros de la red.
 
## Data Augmentation

### Primera forma

Decidimos expandir todo el dataset modificando sus imágenes, aplicándo las siguientes transformaciones:

* Rotación (150º).
* Espejado (vertical).
* Contraste (0.2). 

Todo esto cons los métodos de tensorflow para el manejo de imágenes.

En principio optamos por crear una imagen por cada transformación. Esta idea fue rechazada porque el dataset crecía demasiado, ocupando demasiada RAM cuando se cargaban para el entrenamiento. 

Por ello, decidimos crear una sola imagen por cada imagen en el dataset a la cual se le aplicaran las 3 transformaciones. Estas imágenes eran guardadas en una carpeta llamada `modify`.

Esto mejoró la red original apróximando bastante bien la mayoría de veces. 

* loss: 0.0502 - accuracy: 0.9823 - val_loss: 0.0986 - val_accuracy: 0.9706

!["img1.png"](/imgs/img1.png)

Esto lo puede ver en detalle en el archivo: `primera-forma-sin-cambios-en-red-neuronal.ipynb`

Aún así, no logramos mejorar sus valores con ningún cambio en la red. Aparentemente, se ocasionaba un sobreajuste en el entrenamiento, esto porque los valores en entrenamiento nos daban mucho mejor:

* loss: 0.0099 - accuracy: 0.9874 - val_loss: 0.0454 - val_accuracy: 0.9518

Pero en la parte de testeo os valores obtenidos al predecir ni se acercaban al original.

!["img2.png"](/imgs/img2.png)

Esto lo puede ver en detalle en el archivo: `primera-forma-con-cambios-en-red-neuronal.ipynb`

### Segunda forma

Aplicamos data aumentation al conjunto de datos de entrenamiento utilizando los metodos de tensorflow para manejo de estructuras de tensores:

- normalizacion
- ruido gaussiano
- espejo/volteo horizontal
- espejo/volteo vertical
- rotacion 90 grados
- rotacion 180 grados
- rotacion 270 grados
- ajuste de contraste
- ajuste de brillo
- ajuste de saturacion
