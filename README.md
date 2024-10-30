# Analisis de señal ECG
## Descripción 
Este proyecto realiza un análisis detallado de una señal fisiológica (ECG) obtenida del corazón durante una serie de latidos. Incluye la visualización de la señal, filtrado para eliminar el ruido fuera del rango útil, segmentación de la señal en ventanas alrededor de los intervalos R-R detectados, y un análisis de la señal mediante la transformada wavelet. Además, se calcula la variabilidad de frecuencia cardíaca (HVR) basada en los intervalos R-R de cada segmento para evaluar la variabilidad entre latidos, especialmente cuando el ritmo cardíaco se encuentra cerca de la inestabilidad.

<img src="https://github.com/estebandide/AnalisisECG/blob/main/Gr%C3%A1fico%20Diagrama%20de%20Flujo%20Din%C3%A1mico%20Celeste.png"  width="600" height="500">
*Figura 1: Diagrama de flujo. Tomado de : Autoria propia *

## Sistema Nervioso Autónomo (SNA)

El Sistema Nervioso Autónomo (SNA) es una parte fundamental del sistema nervioso periférico responsable de controlar funciones involuntarias y automáticas del cuerpo, como el ritmo cardíaco, la presión arterial, la digestión y la respiración. Su principal función es regular estas actividades sin intervención consciente, asegurando que el cuerpo mantenga un equilibrio adecuado frente a diferentes estímulos y condiciones internas o externas.

<img src="https://github.com/estebandide/AnalisisECG/blob/main/Sistema-Nervioso-autonomo-Neuroscenter.png"  width="400" height="300">
*Figura 1: Sistema nervioso autonomo. Tomado de : [^5^] *

El SNA se divide en dos ramas principales que trabajan de manera complementaria para asegurar que el organismo responda y se adapte correctamente a sus necesidades:

### Sistema Nervioso Simpático

Esta rama del SNA se activa en situaciones de estrés, peligro o alta demanda energética. Popularmente conocido como el sistema de "lucha o huida", prepara al cuerpo para reaccionar ante situaciones de emergencia aumentando la frecuencia cardíaca, dilatando las vías respiratorias y redirigiendo el flujo sanguíneo hacia los músculos. Estos cambios ayudan a preparar al cuerpo para una respuesta rápida y efectiva.

### Sistema Nervioso Parasimpático

Es responsable del estado de "descanso y digestión". Contrario al simpático, el sistema parasimpático reduce la frecuencia cardíaca, facilita la digestión y promueve procesos de recuperación y conservación de energía en el cuerpo. Esta actividad es crucial para restaurar el equilibrio después de que el organismo ha respondido a una situación de estrés o alta actividad.

### Homeostasis

Es una de las funciones esenciales del SNA. Este proceso permite que el cuerpo mantenga un estado de equilibrio interno, ajustando aspectos como la frecuencia cardíaca y la presión arterial para adaptarse a las demandas tanto internas como externas. La actividad coordinada entre el sistema simpático y el parasimpático es clave para la homeostasis, ya que permite que el organismo responda al estrés mientras conserva energía y se recupera en momentos de calma.

<img src="https://github.com/estebandide/AnalisisECG/blob/main/Homeos.jpeg"  width="400" height="300">
*Figura 3: Homeostasis en el SNA. Tomado de : [^6^]*

En el contexto del SNA, se habla de actividad tónica y actividad fásica. La actividad tónica es la acción basal constante que el SNA mantiene para regular funciones esenciales del cuerpo, como el tono muscular y la frecuencia cardíaca en reposo. La actividad fásica, en cambio, son las respuestas temporales y rápidas que ocurren en el SNA ante estímulos específicos, como un aumento de la frecuencia cardíaca en una situación de peligro.

### Variabilidad de la Frecuencia Cardíaca (HVR)
Que refleja la variabilidad en el tiempo entre los latidos del corazón (intervalo R-R). La HVR es un indicador de la capacidad de respuesta y adaptación del SNA: una HVR adecuada significa que el cuerpo tiene una buena capacidad de adaptación ante diferentes condiciones fisiológicas, ya que refleja un equilibrio dinámico entre la actividad simpática y parasimpática.

### Neurotransmisores del SNA

El SNA regula sus funciones a través de neurotransmisores específicos, principalmente norepinefrina (noradrenalina) y acetilcolina. La norepinefrina es el principal neurotransmisor del sistema simpático y su liberación resulta en un aumento de la frecuencia cardíaca y la presión arterial, preparando al cuerpo para una respuesta activa. La acetilcolina, liberada por el sistema parasimpático, tiene el efecto opuesto: disminuye la frecuencia cardíaca y promueve la relajación, ayudando al organismo a conservar energía.

Esta coordinación entre las diferentes partes del SNA es esencial para mantener la funcionalidad óptima del organismo, permitiendo que se adapte de manera efectiva tanto a situaciones de estrés como a estados de reposo y recuperación.



## Adquisición de la señal ECG
Para la captura de la señal ECG, se seleccionó un sujeto de manera anónima, quien autorizó el uso de su señal bajo condiciones de confidencialidad. La adquisición de la señal se realizó mediante una tarjeta DAQ que es un dispositivo utilizado para medir señales físicas y convertirlas en datos digitales que puedan ser procesado, siguiendo una guía específica para la colocación de los electrodos. La ubicación de los electrodos se basó en las recomendaciones establecidas en [^1^], asegurando una correcta captación de la actividad eléctrica cardíaca. Se incluyó una explicación detallada en cada sección para clarificar los procedimientos técnicos y metodológicos empleados en cada etapa del proceso de adquisición.

<img src="https://github.com/lavaltt/Analisis_de_senales_EMG/blob/main/daq.jpg?raw=true"  width="400" height="300">

*Figura 2: Data Acquisition System. Tomado de : [^2^]*

Adicionalmente, se utilizó un módulo AD8232, un sensor diseñado para medir la actividad cardíaca. Este módulo se destaca por su precisión en la captura de señales cardíacas, ya que su proceso de amplificación y filtrado resulta óptimo para este tipo de señal. Además, permite una fácil lectura de la señal por parte de la tarjeta DAQ, facilitando la adquisición y procesamiento de la actividad eléctrica del corazón.

<img src="https://github.com/lavaltt/Analisis_de_senales_EMG/blob/main/modulo.jpg?raw=true"  width="400" height="300">

*Figura 3: Modulo de adquisición y amplificación AD8832. Tomado de : [^3^]*

Inicialmente, se conectaron los electrodos en la posición indicada en la Figura 3 a un sujeto de prueba y se procedió a registrar la señal ECG en reposo y durante una actividad física controlada. Los electrodos, conectados al módulo AD8232, enviaban la señal cardíaca para su amplificación. Una vez amplificada, la señal se transmitía a la tarjeta DAQ, que realizó el muestreo a una frecuencia de 250 Hz y entregó los valores digitalizados para su almacenamiento y análisis posterior en Python. Para el monitoreo en tiempo real, se utilizó LabVIEW, permitiendo observar la señal sin necesidad de un osciloscopio, garantizando así que no hubiera cambios significativos en la señal registrada frente a la visualizada en el software.

<img src="https://github.com/estebandide/AnalisisECG/blob/main/ELECTRODOS.jpg"  width="400" height="300">

*Figura 4: Ubicacion de los electrodos para adquirir la señal. Tomado de : Tomado de : [^4^]*

<img src="https://github.com/lavaltt/Analisis_de_senales_EMG/blob/main/circuito.jpg?raw=true"  width="400" height="300">

*Figura 5: Circuito realizado para la adquisicón de la señal. Tomado de : Autoría propia*

* Vídeo de la adquisición de la señal:


https://github.com/user-attachments/assets/a102acf0-6d91-4223-a113-5afae681d795

### DAQ y Python 
La DAQ fue enlazada por medio de código a python, de manera que pudiera visualizarse la captura de la señal en tiempo real y los datos fueran guardados en cualquier formato deseado. El código configura los parametros y la tarea de adquisicion, a su vez que estructura la graficación en vivo de la señal adquirida. (Código adjunto en el proyecto).

Muestra del código para la gráfica:
```python
# Graficar la señal
plt.figure(figsize=(50, 10))
plt.plot(tiempo, data, color='red')
plt.title("Señal ECG")
plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud (V)")
plt.grid()
plt.show()
```
## Carga de datos
Los datos adquiridos gracias a la DAQ y python, fueron guardados en un archivo tipo .csv para su correcto análisis y desarrollo. Inicialmente, para cargar los datos en este formato se utilizó la libreria pandas y se graficaron los adtos para observar la señal EMG obtenida. 

```python
#Lectura y carga de datos 
with open(r'C:\Users\valen\OneDrive\Desktop\Ingenieria Biomedica\VI semestre\Procesamiento digital de señales\Laboratorio de señales\Lab4a\Lab4\datosECG4.csv', 'r', encoding='utf-8') as file:
    lines = file.readlines()
#reemplazando comas por puntos
data = []
for line in lines:
    line = line.strip().replace(',', '.')  # Elimina espacios y reemplaza comas
    try:
        value = float(line)
        data.append(value)
    except ValueError:
        continue
data = np.array(data)
fs = 250  
print(data[:5]) # verificar los datos
tiempo = np.arange(len(data)) / fs # Generar el eje de tiempo
```




[^1^]:Guía de colocación de electrodos. (s. f.). Neotecnia. https://neotecnia.mx/blogs/noticias/guia-de-colocacion-de-electrodos?srsltid=AfmBOopEYZV3x6zO5EtnVZ28WQZA4e1kedPIHHK8izv-80wiKwPuaQQI
[^2^]:National Instruments. (s/f). Multifunction Input and Output Devices. https://www.ni.com/pdf/product-flyers/multifunction-io.pdf
[^3^]:ELECTROCARDIOGRAFO ECG AD8232. (s/f). MACTRONICA. https://www.mactronica.com.co/electrocardiografo-ecg-ad8232
[^4^]: Md, A. (s. f.). 5 Lead Electrode Placement Electrocardiogram - RA, LA, RL, LL, V -. . . iStock. https://www.istockphoto.com/es/vector/5-electrocardiogramas-de-colocaci%C3%B3n-de-electrodos-de-plomo-ra-la-rl-ll-v-posici%C3%B3n-gm1586070345-529063354
[^5^]: Neurosce. (2023, 16 junio). ▷ El sistema nervioso autónomo. Neuroscenter. https://neuroscenter.com/blog/sistema-nervioso-autonomo/
[^6^]: DASHBOARD IV. (2023, 7 septiembre). Genially. https://view.genially.com/64f8112ad70759001171057a/interactive-content-dashboard-iv
