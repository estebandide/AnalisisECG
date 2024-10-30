# Analisis de señal ECG
## Descripción 
Este proyecto realiza un análisis detallado de una señal fisiológica (ECG) obtenida del corazón durante una serie de latidos. Incluye la visualización de la señal, filtrado para eliminar el ruido fuera del rango útil, segmentación de la señal en ventanas alrededor de los intervalos R-R detectados, y un análisis de la señal mediante la transformada wavelet. Además, se calcula la variabilidad de frecuencia cardíaca (HVR) basada en los intervalos R-R de cada segmento para evaluar la variabilidad entre latidos, especialmente cuando el ritmo cardíaco se encuentra cerca de la inestabilidad.

<img src="https://github.com/estebandide/AnalisisECG/blob/main/Gr%C3%A1fico%20Diagrama%20de%20Flujo%20Din%C3%A1mico%20Celeste.png"  width="400" height="300">
*Figura 1: Diagrama de flujo. Tomado de : Autoria propia 

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
https://github.com/user-attachments/assets/f08dcb8f-0673-4767-bba3-483fa98fad7b





[^1^]:Guía de colocación de electrodos. (s. f.). Neotecnia. https://neotecnia.mx/blogs/noticias/guia-de-colocacion-de-electrodos?srsltid=AfmBOopEYZV3x6zO5EtnVZ28WQZA4e1kedPIHHK8izv-80wiKwPuaQQI
[^2^]:National Instruments. (s/f). Multifunction Input and Output Devices. https://www.ni.com/pdf/product-flyers/multifunction-io.pdf
[^3^]:ELECTROCARDIOGRAFO ECG AD8232. (s/f). MACTRONICA. https://www.mactronica.com.co/electrocardiografo-ecg-ad8232
[^4^]: Md, A. (s. f.). 5 Lead Electrode Placement Electrocardiogram - RA, LA, RL, LL, V -. . . iStock. https://www.istockphoto.com/es/vector/5-electrocardiogramas-de-colocaci%C3%B3n-de-electrodos-de-plomo-ra-la-rl-ll-v-posici%C3%B3n-gm1586070345-529063354
