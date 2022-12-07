# Localización de landmarks cefalométricos por medio de técnicas de few-shot learning y análisis de redes convolucionales


## Abstract 

**KEYWORDS**: Fourier Analysis, Wavelet Transform, Fourier Transform,
Wavelets, Machine Learning, Computer Vision, Deep Learning,
Cephalometric Landmarks prediction, Convolutional Neural Networks,
Forensic Anthropology.

The main purpose of the work detailed below is to show a possible
mathematic modelization of a Convolutional Neural Network (CNN) and
demonstrate one of the main properties of this kind of network,
Translation Invariance. On the other side, we will adapt the
architecture of an existing network in order to solve a real problem
about cephalometric landmark detection from a Machine Learning
perspective using few-shot learning.

CNN are recent tools which have demonstrated a great capacity for
image-processing tasks. Their good performance on this kind of tasks can
be checked empirically. However, their mathematical modelization and the
theoretical justification of why they are good for this kind of tasks
still is an open case study. For this reason, the main purpose of this
part of the work is to present a possible modelization for CNN based on
the theoretical approximation presented by Mallat in his work **Group
Invariant Scattering**. Once the modelization is shown, we try to prove
one of the most important properties of this network, Translation
Invariance.

To do so, we present an operator called scattering propagator. Using
this operator in a cascade of convolutions we reach the windowed
scattering transform, presented as the mathematical modelization of CNN.
We present a set of properties that this operator must satisfy, like
Lipschitz-continuity, non-expansivity and translation invariant
coefficients. The operator that satisfies all these properties is the
Littlewood-Paley wavelet transform. Once we have the operator we define
the modelization of the windowed scattering and we study the
similarities with the Convolutional Neural Networks. To prove the
translation invariance we use that the windowed operator is
non-expansive.

In the second part of this work, we adapt an existing CNN specialized in
facial landmarks detection called 3FabRec (which is an Adversarial
Autoencoder with interleaved layers that predict landmarks). The
objective is to predict cephalometric facial landmarks using this
framework. Cephalometric landmarks have biological inspiration. The main
problem is the small dataset provided with only a few images in-the-wild
to train the model. We will change the loss function to be able to train
the framework with unmarked landmarks.

To do so, the dataset provided had 167 images of people in the wild. We
wanted to train the framework to predict a maximum of $30$ landmarks in
each image. After a previous analysis of the dataset, we discovered that
not all the landmarks are marked in all images, and we needed to use an
auxiliary network called Facenet to identify bounding boxes on the
images and be able to train the model. Due to the few amount of data we
have, this is contained in the field of few-shot learning.

We studied the state-of-art discovering that only a few articles in the
search we did were related to this specific problem. In these articles,
a set of images in the same position and illumination conditions were
used, instead of the in-the-wild dataset we use. Our model solves the
problem using a Network pretrained on the AFLW dataset and making
fine-tuning with the forensic dataset. We apply data augmentation
techniques to do so and we obtain competitive results. The mean RMSE of
our model is $2.7$. We improve the global RMSE error and also compare
the performance on each landmark, we improve the results in most of
them.


## Resumen

**PALABRAS CLAVE**: Análisis de Fourier, Transformada de Ondeletas, Transformada de Fourier, Bases de Ondeletas, Aprendizaje Automático, Visión por Computador, Aprendizaje Profundo, Localización de Landmarks Cefalométricos, Redes Neuronales Convolucionales, Antropología Forense.


El trabajo fin de grado (TFG) que a continuación se detalla tiene como objetivo presentar una posible modelización, desde el punto de vista matemático, de lo que es una **Red Neuronal Convolucional** (CNN), junto con la demostración de una de sus principales propiedades: la invarianza frente a traslaciones. Por otro lado, se pretende adaptar una arquitectura de red neuronal convolucional ya existente a un problema real que resulte apropiado con *few-shot* learning, que se abordará desde el punto de vista informático.

Las CNN pese a haber surgido recientemente, han demostrado tener un gran potencial para el procesamiento de imágenes, convirtiéndose rápidamente en una de las principales herramientas para estos fines. Su buen rendimiento en este tipo de tareas es comprobable empíricamente. Sin embargo, siguen siendo una vía de estudio abierta en lo que se refiere a la modelización matemática y la justificación teórica de estos resultados. Así, en la primera parte del TFG se pretende desarrollar **la modelización matemática** propuesta por Mallat, en su trabajo **Group Invariant Scattering**, junto con la demostración de una de sus principales propiedades: **la invarianza por traslaciones**.

En lo que respecta a la modelización, comenzamos con la búsqueda de un operador denominado *propagador de dispersión*, el cual,  aplicando la operación de convolución de forma recursiva, construye el denominado *operador de ventana*, presentado como la modelización matemática de una CNN, y actuará sobre caminos de frecuencias finitos (pues, como demostraremos, se puede conseguir retener tanta información como se quiera). Algunas propiedades importantes que debe verificar nuestro operador son la *Lipschitz-continuidad*, que sea no expansivo o que produzca coeficientes invariantes a traslaciones. Dichas propiedades nos impedirá usar herramientas clásicas como la transformada de Fourier, y tendremos que recurrir a la transformada de ondeletas de *Littlewood-Paley*. A continuación, se realiza un estudio de las diferencias y similitudes que guarda con las CNN tal y como las conocemos.

En lo que respecta a la invarianza por traslaciones, haciendo uso de las propiedades del *operador de ventana*, se consigue demostrar, en primer lugar, que dicho operador es no expansivo al aplicarse en conjuntos de caminos de frecuencias, y con dicha propiedad se demuestra su invarianza por traslaciones.

En la segunda parte del trabajo, se pretende adaptar un framework, ya existente, especializado en el reconocimiento de landmarks faciales, denominado **3FabRec** (un *Adversarial Autoencoder* con capas auxiliares encargadas del reconocimiento de landmarks en imágenes) para que sea capaz de marcar landmarks cefalométricos, puntos antropométricos situados en la cabeza, empleando un conjunto de datos reducido de imágenes en diversas posiciones y condiciones de calidad e iluminación. Además, se modificará su función de coste para poder ser entrenado con landmarks faltantes.

Para llevar a cabo esta tarea se parte de un conjunto de 167 imágenes de distintos sujetos en una gran variedad de posturas, condiciones de iluminación y de calidad de imagen con los landmarks etiquetados por un experto. Este conjunto de datos se dividirá en entrenamiento y test. Entrenaremos la red neuronal mencionada anteriormente para lograr predecir hasta un máximo de **30 landmarks** distribuidos por toda la cara. Tras un análisis previo de los datos, detectamos la presencia de landmarks faltantes en la mayoría de imágenes, así como la necesidad de emplear un identificador de caras para marcar *bounding boxes* en las imágenes y poder recortarlas en un paso previo al entrenamiento de la red. Debido a los pocos ejemplos de entrenamiento que poseemos, consideramos el problema dentro del ámbito del *few-shot learning*.

Los trabajos encontrados que guardan relación sobre el tema son muy escasos, y los que aplican técnicas de deep learning, no emplean conjuntos de datos *in-the-wild*. Nuestra propuesta plantea aprovechar el conocimineto adquirido por una red en un amplio dataset, como es *AFLW*, en el reconocimiento de landmarks no antropométricos y ajustarla mediante *fine-tuning* y técnicas *data augmentation* para el reconocimiento de landmarks cefalométricos. Vamos a resolver, por tanto, un problema de **regresión** y, como veremos, los resultados obtenidos son competitivos con el estado del arte. La media del RMSE cometido por nuestro modelo es de $2.7$ píxeles de error, frente a los $3.41$ del mejor modelo. Esta mejora a nivel global en el marcado también se estudia a nivel de landmark.


