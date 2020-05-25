# Clasificación de imágenes para Lenguaje de señas mexicano

### Receta:

Clone el repositorio y ejecute los siguientes comandos:

´´´
cd clasificacion_de_imagenes
´´´

Configure las siguientes variables:
´´´
IMAGE_SIZE=224
ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}"
´´´

Ejecute tensorboard para monitorear el progreso del entrenamiento
´´´
tensorboard --logdir tf_files/training_summaries &
´´´

Entrene el modelo:
´´´
python -m scripts.retrain \
  --bottleneck_dir=tf_files/bottlenecks \
  --how_many_training_steps=500 \
  --model_dir=tf_files/models/ \
  --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
  --output_graph=tf_files/retrained_graph.pb \
  --output_labels=tf_files/retrained_labels.txt \
  --architecture="${ARCHITECTURE}" \
  --image_dir=tf_files/imagenes

#### Pruebe el modelo: 
(para este ejemplo se utiliza una imagen correspondiente a la letra "A")
´´´
python -m scripts.label_image \
    --graph=tf_files/retrained_graph.pb  \
    --image=tf_files/imagenes/LetraA/Class 1-!-19.jpg
   
 ´´´
