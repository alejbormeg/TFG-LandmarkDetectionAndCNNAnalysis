# Pasos para el entrenamiento del 3FabRec

- Tenemos que construir una clase Dataset para leer bien los datos de la base de datos Forense. 
- Al realiza la detección de caras con la red Facenet se detectan problemas en la identificación de perfiles en tres imágenes: 72_2.jpg 75_2.jpg y 157_3.jpg . Además las imgágenes en blanco y nego dan problemas porque no tienen 3 canales. 
- En primer lugar, las imágenes en Blanco y negro las pasamos a 3 canales triplicando la matriz 2d original.
- Ante esto procedemos a realizar un estudio de lo bien que detecta caras en todas las imágenes clasificando por caras de perfil, 3/4 o frontales.
- Identificamos una imagen repetida (21.jpg y 163.jpg) pero decidimos mantener ambas porque tienen distintos landmarks marcados. 
- Las imagenes que usemos van a utilizar un id asociado a la posición que ocupan dentro del Dataset (los ids van de 0 a 163).
- La imagen con id 122 tiene los landmarks puestos únicamente en la imagen frontal, por lo que la contamos como frontal y tomamos el bb de esta que nos da facenet.
- La imagen con id 55 identifica una cara errónea, por lo que debemos seleccionar el segundo BB, que es el que se corresponde con la cara del sujeto.
- La imagen con id 57 identifica cara errónea, por lo que seleccionamos tercer BB que es el que se corresponde con la cara del sujeto.
- El porcentaje de acierto en las imágenes frontales es del 100% al igual que las de 3/4. La precisión baja al 87% en las de perfil, y tenemos que descartar las tres imágenes anteriores.
- En conclusión, las BB se detectan muy bien en general, por lo que únicamente vamos a descartar las 3 imágenes.
- Creamos el fichero annotations.csv para que sea más sencillo de leer luego
