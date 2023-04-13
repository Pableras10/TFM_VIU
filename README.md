# TFM_VIU
TFM Detección automática de vehículos aéreos no tripulados (drones) mediante el uso de redes para la detección de objetos 

La parte práctica del proyecto consiste en entrenar un modelo de red tipo YOLOv5 y otra de tipo Retinanet con Resnet que sea capaz de detectar drones en tiempo real. 
Para el ejemplo se ha dedicido utilizar YOLO y Retinanet de entre todas las redes previamente descritas en el apartado anterior,
ya que proporcionan un modelo con un alto rendimiento y máxima velocidad y un alto porcentaje de precisión en la detección de objetos, aún no siendo el mejor. 

 

Conjunto de datos 
-----------------
Los dataset empleados para el trabajo han sido:  

Amateur Unmanned Air Vehicle Detection: Aksoy, Mehmet Çağrı; Orak, Alp Sezer; Özkan, Hasan Mertcan; Selimoğlu, Bilgin (2019), “Drone Dataset: Amateur Unmanned Air Vehicle Detection”, Mendeley Data, V4, doi: 10.17632/zcsj2g2m4c.4 
Drone-dataset-uav: Mehdi Özel - Istanbul (Turkey), https://www.kaggle.com/datasets/dasmehdixtr/drone-dataset-uav  



Entrenamiento 
-------------
Para llevar a cabo el entrenamiento de la red, se han utilizado dos dataset con imágenes de drones y con su correspondiente etiquetado de coordenadas bounding box. 
Cada imagen en formato jpg lleva asociado un fichero: 

-Para YOLO: es de tipo txt dónde se indican la clase del objeto, en nuestro caso 0 (DRON), seguido por las 4 coordenadas que delimitan el objeto. 
-Retinanet: es de tipo csv con la ruta de cada imagen, y las 4 coordenadas del bbox seguida de la clase. 

El entrenamiento del modelo se ha realizado juntando los dos dataset en uno final para tener más imágenes y mejorar el proceso, 
consiguiendo un total de 4228 imágenes de drones con sus respectivas etiquetas. 

Se ha hecho una limpieza previa de imágenes erróneas o que no fueran muy correctas en su identificación antes de su uso final. 
Para el proceso de entrenamiento, se han dividido los datos en entrenamiento (80%) y validación (20%) 


Para conseguir que nuestra red se capaz de detectar correctamente drones en una imagen o video, necesitamos realizar un entrenamiento mediante YOLOv5 
y otro con Retinanet y Resnet50 (backbone). El primer paso es descargar dos modelos h5 con pesos ya preentrenados en otros dataset de datos (Coco y Pascal Voc) 
para mediante transfer learning entrenar las últimas capas de nuestro modelo con el dataset de drones que hemos configurado y tratar de conseguir un rendimiento 
elevado en la detección de los mismos. 
 
Los datos previamente se han dividido en dos partes: entrenamiento y validación. Se ajustan los parámetros configurables de la red con distintos valores 
que se han ido realizando en diferentes pruebas. Entre dichos valores tenemos: la función de pérdida, learning rate, momentum, épocas, batch size, etc. 
Para YOLOv5 estos parámetros se pueden configurar en el archivo hyp-data.yaml  mientras que para RetinaNet se configuran en el archivo train.py. 
