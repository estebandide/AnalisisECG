# Analisis de señal ECG
## Descripción 
Este proyecto realiza un análisis detallado de una señal fisiológica (ECG) obtenida del corazón durante una serie de latidos. Incluye la visualización de la señal, filtrado para eliminar el ruido fuera del rango útil, segmentación de la señal en ventanas alrededor de los intervalos R-R detectados, y un análisis de la señal mediante la transformada wavelet. Además, se calcula la variabilidad de frecuencia cardíaca (HVR) basada en los intervalos R-R de cada segmento para evaluar la variabilidad entre latidos, especialmente cuando el ritmo cardíaco se encuentra cerca de la inestabilidad.


<img src="https://github.com/estebandide/AnalisisECG/blob/main/Gr%C3%A1fico%20Diagrama%20de%20Flujo%20Din%C3%A1mico%20Celeste.png"  width="600" height="500">

*Figura 1: Data Acquisition System. Tomado de autoria propia*



## Sistema Nervioso Autónomo (SNA)

El Sistema Nervioso Autónomo (SNA) es una parte fundamental del sistema nervioso periférico responsable de controlar funciones involuntarias y automáticas del cuerpo, como el ritmo cardíaco, la presión arterial, la digestión y la respiración. Su principal función es regular estas actividades sin intervención consciente, asegurando que el cuerpo mantenga un equilibrio adecuado frente a diferentes estímulos y condiciones internas o externas.

<img src="https://github.com/estebandide/AnalisisECG/blob/main/Sistema-Nervioso-autonomo-Neuroscenter.png"  width="400" height="300">
*Figura 2: Sistema nervioso autonomo. Tomado de : [^5^]*

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

### Neurotransmisores del SNA

El SNA regula sus funciones a través de neurotransmisores específicos, principalmente norepinefrina (noradrenalina) y acetilcolina. La norepinefrina es el principal neurotransmisor del sistema simpático y su liberación resulta en un aumento de la frecuencia cardíaca y la presión arterial, preparando al cuerpo para una respuesta activa. La acetilcolina, liberada por el sistema parasimpático, tiene el efecto opuesto: disminuye la frecuencia cardíaca y promueve la relajación, ayudando al organismo a conservar energía.

Esta coordinación entre las diferentes partes del SNA es esencial para mantener la funcionalidad óptima del organismo, permitiendo que se adapte de manera efectiva tanto a situaciones de estrés como a estados de reposo y recuperación.

## Variabilidad de la Frecuencia Cardíaca (HRV)

La **Variabilidad de la Frecuencia Cardíaca (HRV)** es una medida de la fluctuación en los intervalos de tiempo entre latidos consecutivos del corazón (intervalos R-R) y se considera un indicador clave de la salud y el equilibrio del **Sistema Nervioso Autónomo (SNA)**. A diferencia de la frecuencia cardíaca promedio, que solo mide el número de latidos por minuto, la HRV examina cómo varía el tiempo entre latidos individuales, proporcionando información valiosa sobre la capacidad de adaptación del cuerpo frente a diferentes condiciones internas y externas.

La HVR refleja la influencia del sistema nervioso simpático y parasimpático sobre el corazón. En un organismo sano, el SNA es dinámico y responde de forma continua a cambios tanto internos como ambientales. Esta respuesta se manifiesta en el ajuste de los intervalos R-R en tiempo real, lo que se traduce en una mayor HRV, la cual está generalmente asociada a una buena salud y capacidad de recuperación.

### Importancia de la HRV en la Salud Cardiovascular

Una alta variabilidad de la frecuencia cardíaca se considera un signo positivo de la capacidad adaptativa del SNA. Un mayor HVR implica que el sistema nervioso parasimpático está activo y que el organismo puede manejar el estrés adecuadamente, además de adaptarse con facilidad a situaciones de reposo o esfuerzo. En cambio, una baja HRV se asocia frecuentemente con una actividad simpática excesiva o una baja actividad parasimpática, lo cual puede ser indicativo de un estado de estrés crónico, fatiga, o problemas cardiovasculares, entre otros.

Una baja HRV se ha relacionado con diversas condiciones patológicas, como hipertensión, enfermedades cardíacas, estrés crónico y trastornos de ansiedad. Además, estudios muestran que una baja HRV puede ser un indicador temprano de riesgos cardiovasculares y mortalidad, ya que el corazón pierde flexibilidad para adaptarse a los cambios en el entorno y las demandas del organismo.

### Componentes de la HRV

El análisis de la HRV a menudo se realiza descomponiendo la señal de los intervalos R-R en diferentes componentes de frecuencia, ya que cada uno refleja diferentes aspectos de la regulación autónoma:
- **Frecuencia Baja (LF)**: Este componente refleja tanto la actividad simpática como una influencia del sistema renina-angiotensina, e indica el control vascular general.
- **Frecuencia Alta (HF)**: Representa principalmente la actividad parasimpática y se asocia con el tono vagal, que regula la relajación y recuperación del corazón en momentos de reposo.
- **Relación LF/HF**: La relación entre estos dos componentes se utiliza como un índice de balance autonómico. Un valor alto en la relación LF/HF sugiere predominio simpático, mientras que un valor bajo sugiere predominio parasimpático.

### Métodos de Análisis de la HRV

Existen varias técnicas para analizar la HRV, que permiten obtener información detallada de cómo responde el SNA en distintas condiciones:
- **Análisis en el dominio del tiempo**: Este método examina la variabilidad en los intervalos de tiempo entre los latidos, utilizando métricas como la desviación estándar de los intervalos R-R (SDNN) y el índice RMSSD, que mide la variabilidad a corto plazo y está altamente influenciado por la actividad parasimpática.
- **Análisis en el dominio de la frecuencia**: Utiliza técnicas como la transformada de Fourier o la transformada wavelet para descomponer la señal en sus componentes de frecuencia, permitiendo observar los patrones LF y HF, que ofrecen una comprensión más profunda del balance autónomo.

### Factores que Afectan la HRV

La HVR es sensible a múltiples factores externos e internos, como la edad, el nivel de condición física, el estado emocional, y el ciclo circadiano. En personas jóvenes y en buen estado físico, la HRV tiende a ser mayor debido a la flexibilidad autonómica. En cambio, en personas mayores o bajo estrés crónico, la HVR suele disminuir debido a un predominio simpático o a una reducción de la actividad parasimpática.

Además, los estilos de vida y hábitos, como la alimentación, el sueño y el ejercicio, pueden influir en la HRV. El ejercicio regular, la meditación y el sueño de calidad tienden a mejorar la HVR, mientras que el estrés, el consumo excesivo de alcohol, y el insomnio tienden a reducirla, lo que afecta negativamente la regulación autónoma del corazón.

## Transformada Wavelet

La Transformada Wavelet es una técnica para descomponer una señal en el tiempo y la frecuencia, permitiendo analizar detalles a distintas escalas. A diferencia de la Transformada de Fourier, que solo ofrece información de la frecuencia, la Transformada Wavelet proporciona información sobre cuándo ocurren ciertos cambios en la frecuencia, siendo útil para señales no estacionarias como el ECG.

La transformada wavelet utiliza funciones llamadas wavelets (ondículas) que se ajustan en escala (para analizar detalles finos o generales) y en tiempo (para analizar diferentes momentos de la señal). Este enfoque permite captar tanto eventos puntuales como tendencias.

### Tipos de Wavelets

Existen diferentes wavelets que se eligen según el tipo de señal y el análisis requerido:
- **Haar**: Simple y detecta cambios bruscos.
- **Daubechies**: Útil para señales complejas, como ECG.
- **Morlet**: Ideal para señales oscilatorias.

### Análisis Multi-Resolución

La Transformada Wavelet permite descomponer una señal en distintos niveles de detalle:
- **Frecuencia baja**: Refleja las tendencias generales.
- **Frecuencia alta**: Muestra detalles finos o picos, útiles para detectar eventos específicos.

### Aplicaciones

La Transformada Wavelet se usa en:
- **Procesamiento de señales fisiológicas**: Para detectar eventos en ECG, EEG, etc.
- **Compresión de datos**: Reduce el tamaño de archivos manteniendo calidad.
- **Análisis de series temporales**: Identificación de eventos en datos financieros o de monitoreo.


## Adquisición de la señal ECG
Para la captura de la señal ECG, se seleccionó un sujeto de manera anónima, quien autorizó el uso de su señal bajo condiciones de confidencialidad. La adquisición de la señal se realizó mediante una tarjeta DAQ que es un dispositivo utilizado para medir señales físicas y convertirlas en datos digitales que puedan ser procesado, siguiendo una guía específica para la colocación de los electrodos. La ubicación de los electrodos se basó en las recomendaciones establecidas en [^1^], asegurando una correcta captación de la actividad eléctrica cardíaca. Se incluyó una explicación detallada en cada sección para clarificar los procedimientos técnicos y metodológicos empleados en cada etapa del proceso de adquisición.


<img src="https://github.com/estebandide/AnalisisECG/blob/main/LABVIEW.jpg"  width="600" height="500">

*Figura 1: Esquema LabVIEW. Tomado de autoria propia*


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
Este código grafica la señal ECG previamente cargada en función del tiempo. Se configura una figura de tamaño amplio (50x10), y se usa `plt.plot` para trazar los datos de `data` en el eje vertical (amplitud) contra el eje de tiempo `tiempo` (en segundos), en color rojo. La gráfica se titula "Señal ECG" y se etiquetan los ejes para claridad. Finalmente, se agrega una cuadrícula (`plt.grid()`) para facilitar la lectura visual y se muestra la gráfica (`plt.show()`).

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
Este código abre y carga datos de un archivo CSV (datosECG4.csv) que contiene valores de una señal ECG, reemplazando comas por puntos para convertir las lecturas a formato numérico. Tras leer las líneas y limpiar los valores, se almacenan en la lista data, omitiendo cualquier línea que no sea numérica. Luego, data se convierte a un arreglo de NumPy y se define la frecuencia de muestreo (fs = 250 Hz). Finalmente, se crea un eje de tiempo tiempo para la señal, que permitirá representar la señal ECG en función del tiempo.

<img src="https://github.com/estebandide/AnalisisECG/blob/main/crudo.jpg"  width="900" height="300">
*Figura 5: Señal en crudo. Tomado de : Autoría propia*

## Análisis de la Señal Cruda

La señal cruda registrada presenta todas las características fundamentales que definen su naturaleza en bruto, sin aplicar ningún tipo de filtrado o procesamiento. Estos detalles permiten evaluar las propiedades básicas y comportamiento de la señal, lo que es esencial para entender su composición y preparar los pasos posteriores de análisis y procesamiento.

### Características de la Señal Original

#### Frecuencia de Muestreo
- **Frecuencia de muestreo**: 250 Hz
- La frecuencia de muestreo de 250 Hz indica que la señal fue capturada 250 veces por segundo. Este valor es adecuado para capturar variaciones rápidas en la señal, permitiendo representar con precisión los eventos de alta frecuencia y evitando problemas de aliasing, siempre que el contenido de la señal esté dentro del rango permitido.

#### Tiempo de Muestreo
- **Duración total del muestreo**: 300 segundos
- Este tiempo total de registro permite analizar la señal en períodos prolongados, detectando posibles patrones cíclicos o cambios de amplitud que podrían aparecer en intervalos largos.

#### Niveles de Cuantificación
- La señal fue digitalizada y cuantificada en niveles específicos. Los niveles de cuantificación afectan la precisión con la que se representan las amplitudes, ya que cada nivel representa un rango de valores de la señal original. Una mayor cantidad de niveles ofrece una representación más fiel de la señal análoga original.

### Estadísticas de la Señal Original

Para comprender la señal en su estado bruto, es fundamental evaluar sus estadísticas básicas. A continuación, se presentan las métricas más representativas:

- **Media**: 1.9075, la media de la señal, o valor promedio, indica la tendencia central de la amplitud. Un valor cercano a cero en ciertas señales puede indicar simetría alrededor del eje horizontal, mientras que en esta señal, una media de 1.9075 sugiere un desplazamiento en la amplitud.

- **Mediana**: 1.8740, la mediana representa el valor central de la señal y proporciona información sobre la distribución de los datos. Si la mediana y la media son muy similares, como en este caso, la señal probablemente presenta una distribución aproximadamente simétrica.

- **Desviación Estándar**: 0.3535, la desviación estándar mide la dispersión de los valores de la señal respecto a la media. Un valor bajo sugiere que la señal no presenta grandes fluctuaciones alrededor de la media, mientras que un valor más alto indicaría variabilidad significativa. En este caso, una desviación estándar de 0.3535 implica una dispersión moderada, indicando cierta variabilidad en la señal sin ser extremadamente volátil.

```python
#ESTADÍSTICAS DE LA SENAL CRUDA
# Calcular estadísticas 
media = np.mean(data)
mediana = np.median(data)
desviacion= np.std(data)
```
Este código calcula estadísticas básicas de la señal cruda data, obteniendo su media, mediana y desviación estándar. La media y mediana indican el valor promedio y central de la señal, respectivamente, mientras que la desviación estándar mide la variabilidad o dispersión de los valores de la señal alrededor de la media. Estos cálculos permiten entender las características generales de la señal sin procesar.

## Pre-procesamineto de la señal

### Filtro pasa-banda 
#### Diseño de Filtros Utilizados

Para el análisis de la señal, se emplearon filtros específicos que permiten mejorar la calidad de la señal y resaltar las características relevantes. En este caso, se utilizó un **filtro pasa banda de orden 3** con dos conjuntos de frecuencias de corte: uno que va de **5 Hz a 100 Hz** y otro que abarca de **0.5 Hz a 250 Hz**. A continuación, se describen en detalle los parámetros del filtro y la lógica detrás de su elección.

#### Parámetros del Filtro

##### Tipo de Filtro
- **Filtro**: Pasa Banda
- **Orden**: 3

##### Frecuencias de Corte
- **Primer conjunto de frecuencias de corte**:
  - **-3 dB**: 5 Hz a 100 Hz
  - **-20 dB**: 0.5 Hz a 250 Hz

#### Diseño del Filtro

##### Pasa Banda
Este tipo de filtro se diseñó para permitir el paso de frecuencias en un rango específico (5 Hz a 100 Hz en este caso) y atenuar las frecuencias que quedan fuera de este rango. La elección de un filtro pasa banda es crucial en el análisis de señales biológicas, como el ECG, ya que se busca eliminar ruidos y artefactos fuera del rango de interés. Esto es especialmente relevante en el contexto de la actividad cardíaca, donde las frecuencias de interés se encuentran generalmente en un rango específico.

##### Orden del Filtro
El orden del filtro determina la pendiente de atenuación de la respuesta en frecuencia. Un filtro de orden 3 ofrece una transición más pronunciada entre las frecuencias permitidas y las no permitidas en comparación con filtros de menor orden. Esto significa que las frecuencias fuera del rango de paso se atenuarán de manera más efectiva, lo que ayuda a mantener la integridad de la señal de interés.

##### Frecuencias de Corte
   - **-3 dB (5 Hz a 100 Hz)**: Este rango es esencial para el análisis de señales cardíacas, ya que abarca la mayoría de las componentes de la frecuencia cardíaca normal. En este rango, se conservan las características importantes del ECG, incluidas las oscilaciones asociadas con los ciclos cardíacos.
   - **-20 dB (0.5 Hz a 250 Hz)**: Este rango permite incluir oscilaciones de baja frecuencia que pueden ser relevantes para ciertas patologías o fenómenos fisiológicos. La elección de 0.5 Hz asegura que se capturen eventos de interés que pueden estar relacionados con ritmos cardíacos anormales o variaciones fisiológicas.

```python
# Parámetros del filtro pasa banda
lc = 5.0    # Frecuencia de corte baja para el pasa banda
hc = 100.0   # Frecuencia de corte alta para el pasa banda
order_bandpass = 3  # Orden del filtro pasa banda

# Normalización para el filtro pasa banda
nyquist = 0.5 * fs
low = lc / nyquist
high = hc / nyquist

# Filtro pasa banda Butterworth
b_bandpass, a_bandpass = signal.butter(order_bandpass, [low, high], btype='band')
filtered_data = signal.filtfilt(b_bandpass, a_bandpass, data)
```

Este código configura y aplica un filtro pasa banda Butterworth para permitir el paso de frecuencias entre 5 y 100 Hz, filtrando otras frecuencias de una señal. Se definen las frecuencias de corte bajas (lc) y altas (hc), ajustadas al rango de Nyquist. Con un filtro de orden 3 (order_bandpass), se calculan los coeficientes del filtro y se aplica sobre la señal data usando signal.filtfilt, lo cual elimina desfasajes al filtrar en ambas direcciones, resultando en una señal contenida en el rango de frecuencias deseado.

#### Aplicaciones y Beneficios del Diseño

El diseño de este filtro proporciona múltiples beneficios:

- **Preservación de Información Crítica**: Al centrarse en las frecuencias de interés, el filtro garantiza que la información crucial relacionada con la actividad cardíaca se conserve durante el procesamiento. Las componentes de frecuencia en el rango de 5 Hz a 100 Hz son particularmente relevantes para identificar patrones cardíacos y posibles anomalías.

- **Reducción de Ruido**: Este filtro es eficaz para eliminar ruidos de baja frecuencia (como interferencias electromagnéticas) y también atenuar componentes de alta frecuencia que podrían distorsionar la señal de ECG. Este proceso de limpieza es esencial para garantizar que el análisis posterior se base en datos fiables.

- **Mejora de la Calidad de la Señal**: Al aplicar un filtro de orden 3, se logra una mayor atenuación de las frecuencias no deseadas, lo que mejora la calidad general de la señal procesada. Esto es crucial para realizar análisis precisos y significativos, ya que una señal limpia facilita la identificación de características relevantes.

- **Flexibilidad en el Análisis**: La implementación de dos conjuntos de frecuencias de corte permite una mayor flexibilidad en el análisis. Dependiendo del enfoque del estudio, se puede optar por un análisis más detallado (5 Hz a 100 Hz) o uno más amplio (0.5 Hz a 250 Hz), adaptándose así a las necesidades específicas de cada análisis.

### Diseño de Filtros Utilizado

En el análisis de señales, se utilizó un **filtro rechaza banda de orden 3** con frecuencias de corte específicas para eliminar interferencias en un rango particular. Este tipo de filtro es esencial para asegurar la calidad de la señal de interés, minimizando la influencia de ruidos y artefactos. A continuación, se describen en detalle los parámetros del filtro y la razón detrás de su elección.

#### Parámetros del Filtro

##### Tipo de Filtro
- **Filtro**: Rechaza Banda
- **Orden**: 3

##### Frecuencias de Corte
- **Primer conjunto de frecuencias de corte**:
  - **-3 dB**: 50 Hz a 60 Hz
  - **-20 dB**: 52 Hz a 58 Hz

##### Diseño del Filtro

1. **Rechaza Banda**: Este tipo de filtro se diseñó para atenuar las frecuencias en un rango específico (50 Hz a 60 Hz) mientras permite el paso de las frecuencias que se encuentran por debajo y por encima de este rango. Este enfoque es crítico en el análisis de señales biológicas, donde ciertas frecuencias pueden introducir ruido significativo.

2. **Orden del Filtro**: Un filtro de orden 3 ofrece una transición más pronunciada en la respuesta en frecuencia, lo que significa que las frecuencias cercanas al rango de rechazo se atenuarán de manera efectiva. Esto es fundamental para minimizar el impacto de las interferencias en las frecuencias que se desean conservar.

3. **Frecuencias de Corte**:
   - **-3 dB (50 Hz a 60 Hz)**: Este rango está diseñado para eliminar componentes no deseadas que pueden interferir con la señal de interés. Muchas veces, las interferencias pueden provenir de fuentes eléctricas o equipos cercanos que operan en este rango, por lo que su eliminación es esencial para obtener una señal limpia.
   - **-20 dB (52 Hz a 58 Hz)**: Esta subbanda más estrecha permite un rechazo aún más fuerte en las frecuencias cercanas al rango de interés. El objetivo es eliminar ruidos que podrían ser críticos y que pueden distorsionar la interpretación de los datos, particularmente en aplicaciones donde la precisión es fundamental.
     
```python
# Parámetros para el filtro de rechaza banda 
stop_low = 50.0
stop_high = 60.0
order_bandstop = 5  # Orden del filtro rechaza banda
low_stop = stop_low / nyquist
high_stop = stop_high / nyquist

# Filtro rechaza banda Butterworth
b_bandstop, a_bandstop = signal.butter(order_bandstop, [low_stop, high_stop], btype='bandstop')
filtered_bandstop_data = signal.filtfilt(b_bandstop, a_bandstop, filtered_data)
```
Este código define y aplica un filtro rechaza banda Butterworth para eliminar frecuencias no deseadas entre 50 y 60 Hz de una señal, como las que puede introducir el ruido eléctrico. Se establecen los límites de frecuencia (stop_low y stop_high) y se ajustan al rango de Nyquist. Luego, se configura el filtro de orden 5 (order_bandstop), y se aplica usando signal.filtfilt, que filtra la señal filtered_data hacia adelante y hacia atrás para evitar desfasajes, obteniendo una señal sin componentes en el rango especificado.

##### Aplicaciones y Beneficios del Diseño

La implementación de este filtro rechaza banda aporta múltiples beneficios:

- **Eliminación de Interferencias**: Al enfocarse en un rango específico de frecuencias, este filtro es eficaz para eliminar ruidos que pueden ser introducidos por dispositivos electrónicos, como la red eléctrica, que a menudo generan componentes en el rango de 50 Hz a 60 Hz. Esto es particularmente relevante en entornos donde se realizan estudios biomédicos.

- **Preservación de Señales de Interés**: Al rechazar únicamente las frecuencias no deseadas, el filtro permite que las componentes relevantes de la señal pasen sin alteraciones significativas. Esto es esencial para el análisis de datos donde se requiere claridad y precisión.

- **Mejora de la Calidad de la Señal**: Con un filtro de orden 3, la atenuación de las frecuencias en el rango de rechazo es más efectiva. Esto significa que la calidad general de la señal se mejora, facilitando análisis posteriores más precisos y significativos.

- **Flexibilidad en el Análisis**: La elección de frecuencias de corte específicas permite que el filtro se adapte a diferentes contextos y condiciones de ruido, brindando la flexibilidad necesaria para realizar análisis bajo diversas condiciones experimentales.

<img src="https://github.com/estebandide/AnalisisECG/blob/main/FILTRO.jpg"  width="900" height="300">
*Figura 5: Señal filtrada verde (Pasa banda), señal filtrada azul (rechaza banda). Tomado de : Autoría propia*

## Analsiis de HRV

La variabilidad de la frecuencia cardíaca (HRV) es una medida de las variaciones en el intervalo de tiempo entre latidos consecutivos del corazón (intervalos R-R). Es un indicador importante de la actividad del sistema nervioso autónomo (SNA), que regula funciones automáticas del cuerpo, y se utiliza comúnmente en el análisis de la salud cardíaca y el estrés. Una mayor HRV generalmente indica una buena adaptación del sistema cardiovascular y una alta resiliencia, mientras que una HRV baja puede estar asociada con estrés.

<img src="https://github.com/estebandide/AnalisisECG/blob/main/HRV.jpg"  width="900" height="300">
*Figura 5: Señal medicion de los R-R. Tomado de : Autoría propia*

### Gráfica del ECG Filtrado con Picos R Detectados

#### Identificación de los Picos R

En esta gráfica, la señal azul representa el ECG filtrado, y las marcas rojas indican los picos R identificados. Estos picos son puntos clave en la señal de ECG que corresponden a los momentos de contracción ventricular en cada latido, es decir, cuando el corazón se contrae para bombear sangre. Detectar con precisión los picos R es fundamental para calcular los intervalos R-R, que son los tiempos entre latidos consecutivos y sirven como base para medir la HRV.

La consistencia de los picos R en la gráfica indica un ritmo cardíaco regular, lo cual es un buen signo en términos de estabilidad. Sin embargo, es normal observar pequeñas variaciones en la altura y en la posición de cada pico R, lo que puede reflejar la influencia de factores como la respiración, el estrés o el estado de reposo o actividad física de la persona. Estas variaciones contribuyen a la HRV y son importantes para comprender cómo el sistema nervioso autónomo regula el ritmo cardíaco.

#### Análisis Temporal

- **Eje Horizontal:** Representa el tiempo en segundos, permitiendo observar cómo varía la señal ECG a lo largo del tiempo.
- **Eje Vertical:** Muestra la amplitud de la señal ECG en milivoltios (mV), que indica la fuerza de los impulsos eléctricos durante cada latido.

Al observar el trazado de ECG, los picos R deben estar bastante regulares en el tiempo para reflejar un ritmo cardíaco normal. En este análisis, la separación entre picos R es consistente, aunque existen algunas variaciones en la altura y en el intervalo entre ellos. Esto refleja una HRV positiva, que es un indicador de que el corazón responde a las demandas del cuerpo.

#### Observación de Variaciones en los Picos R

Se ha identificado una variación más grande en el intervalo entre picos R alrededor de los 150-160 segundos. Esta variación podría deberse a un cambio en la actividad del sistema nervioso autónomo, una respuesta al entorno, o incluso a una ligera arritmia. Identificar estas variaciones ayuda a diferenciar entre fluctuaciones normales y posibles anomalías que podrían requerir un análisis adicional, especialmente si se observan en otras partes del ECG o si se acompañan de síntomas clínicos.

#### Importancia para la HRV

La HRV mide la variabilidad en el tiempo entre latidos consecutivos (intervalos R-R) y es un reflejo del equilibrio entre los sistemas nerviosos simpático y parasimpático, que regulan el ritmo cardíaco. Un patrón de picos R con una variabilidad adecuada (sin ser excesiva) sugiere que el sistema nervioso autónomo es flexible y responde bien a las demandas del cuerpo. 

Este equilibrio es favorable para la salud cardiovascular y permite que el organismo reaccione de manera óptima a situaciones de estrés, cambios en el entorno y otras demandas fisiológicas. Por lo tanto, un monitoreo adecuado de los picos R y de los intervalos R-R es esencial para evaluar el estado del sistema nervioso autónomo y de la salud cardiovascular en general.

#DETECCION DE INTERVALOS R-R

distance = int(0.6 * fs)  #Distancia mínima entre picos (600 ms aprox.)
peaks, _ = find_peaks(filtered_bandstop_data, distance=distance, height=0.5)  # heigh: amplitud


```python
# Calcular los intervalos R-R
intervalos_RR = np.diff(peaks) / fs  
num_picos = len(peaks)
num_intervalos = len(intervalos_RR)


tiempo_RR = np.cumsum(intervalos_RR)  # Tiempo acumulado de cada intervalo R-R
```

Este fragmento de código calcula los intervalos R-R de una señal ECG al medir el tiempo entre picos consecutivos detectados. Para ello, usa np.diff en el arreglo peaks y divide por la frecuencia de muestreo fs, obteniendo así los intervalos en segundos. También cuenta el número de picos y de intervalos R-R para referencias adicionales, y utiliza np.cumsum para calcular el tiempo acumulado de cada intervalo, permitiendo analizar la evolución temporal de la frecuencia cardíaca.

<img src="https://github.com/estebandide/AnalisisECG/blob/main/ESTA.jpg"  width="900" height="300">
*Figura 5: Señal estadisticos de los R-R. Tomado de : Autoría propia*

### Gráfica de Duración de los Intervalos R-R

La segunda gráfica analiza la duración de los intervalos R-R, es decir, los tiempos entre latidos sucesivos. Esta gráfica es crucial para entender la variabilidad de la frecuencia cardíaca (HRV), ya que permite observar cómo fluctúa el tiempo entre cada latido.

#### Significado de la Media y Desviación Estándar

- **Media de los Intervalos R-R:** La media calculada es de 0.9767 segundos, lo que representa la duración promedio entre latidos en un estado de reposo. Este valor equivale a una frecuencia cardíaca promedio de aproximadamente 61 latidos por minuto, calculada como \( 60 / \text{media} \), es decir, \( 60 / 0.9767 \approx 61 \). Esta frecuencia cardíaca es típica en un estado de reposo y puede considerarse un indicio de una buena salud cardíaca, ya que sugiere que el corazón está funcionando a un ritmo controlado.

- **Desviación Estándar de los Intervalos R-R:** La desviación estándar obtenida es de 0.1452 segundos, lo cual refleja la variabilidad en los intervalos R-R. Una desviación estándar mayor indica una mayor HRV, lo que es positivo en términos de salud. Una HRV elevada muestra que el sistema nervioso autónomo es flexible y puede adaptarse a las necesidades cambiantes del cuerpo. Por el contrario, una HRV baja puede indicar un sistema autónomo menos adaptable, lo cual podría relacionarse con un mayor riesgo de problemas cardíacos y con una salud general comprometida.

#### Interpretación de la Gráfica

La gráfica de los intervalos R-R muestra las variaciones en la duración de los intervalos R-R. 

- **Puntos Morados:** Representan los valores individuales de los intervalos R-R suavizados, lo cual permite observar las variaciones sin el ruido de la señal original.
- **Líneas de Color:** Las líneas de color en la gráfica indican la media (en rojo) y las bandas de una desviación estándar (en verde y naranja). Las bandas ayudan a establecer un rango normal dentro del cual suelen caer los intervalos R-R en condiciones de reposo.

Los intervalos que se encuentran fuera de estas bandas pueden considerarse desviaciones significativas del ritmo promedio. Estas desviaciones no necesariamente indican un problema, ya que el corazón responde a diversos factores fisiológicos y ambientales, como el estrés, el ejercicio o incluso el estado emocional. Sin embargo, intervalos que frecuentemente caen fuera de estas bandas podrían requerir un análisis adicional, especialmente si están acompañados de síntomas o se observan en patrones repetidos.

#### Observación de Picos en los Intervalos R-R

En la gráfica, se observan picos significativos en la duración de los intervalos R-R alrededor del índice 50 y después del índice 250. Estos picos podrían ser causados por artefactos en la señal, errores en la detección de los picos R, o cambios en la actividad del sistema nervioso autónomo. Identificar y analizar estos picos es útil para distinguir entre variaciones fisiológicas normales y posibles irregularidades en el ritmo cardíaco.

#### HRV y Salud Cardiovascular

La HRV, medida a través de la variabilidad en los intervalos R-R, es un indicador clave de la salud del sistema cardiovascular. Un corazón con buena HRV muestra una mayor flexibilidad y adaptabilidad del sistema nervioso autónomo, lo cual es importante para afrontar las demandas del organismo en diferentes situaciones, desde la relajación hasta el ejercicio intenso. 

Un descenso en la HRV puede asociarse con un mayor riesgo de enfermedades cardíacas, problemas en el equilibrio entre los sistemas simpático y parasimpático, y una menor capacidad de adaptación a factores de estrés. Por tanto, monitorear la HRV ayuda en la prevención de enfermedades cardíacas y permite realizar un seguimiento de la salud cardiovascular de manera integral.

Luego podemos apreciar como  se realizo la obtencion de esta grafica mediante el uso de python, 

```python
#ESTADÍSTICAS DE LOS INTERVALOS R-R

# Calcular estadísticas de los intervalos R-R
media_RR = np.mean(intervalos_RR)
mediana_RR = np.median(intervalos_RR)
desviacion_std_RR = np.std(intervalos_RR)

# Gráfica de los intervalos R-R 
plt.figure(figsize=(20, 5))

window_size = 5  
smoothed_intervals = np.convolve(intervalos_RR, np.ones(window_size) / window_size, mode='valid')


```

Este código calcula estadísticas básicas (media, mediana y desviación estándar) de los intervalos R-R de una señal ECG, que representan el tiempo entre dos picos cardíacos consecutivos y reflejan la variabilidad del ritmo. Además, aplica un suavizado con una ventana móvil de tamaño 5 para resaltar la tendencia general de los intervalos, eliminando fluctuaciones rápidas. Finalmente, grafica los datos usando un tamaño de figura amplio para visualizar la evolución de estos intervalos de forma clara.

[^1^]:Guía de colocación de electrodos. (s. f.). Neotecnia. https://neotecnia.mx/blogs/noticias/guia-de-colocacion-de-electrodos?srsltid=AfmBOopEYZV3x6zO5EtnVZ28WQZA4e1kedPIHHK8izv-80wiKwPuaQQI
[^2^]:National Instruments. (s/f). Multifunction Input and Output Devices. https://www.ni.com/pdf/product-flyers/multifunction-io.pdf
[^3^]:ELECTROCARDIOGRAFO ECG AD8232. (s/f). MACTRONICA. https://www.mactronica.com.co/electrocardiografo-ecg-ad8232
[^4^]: Md, A. (s. f.). 5 Lead Electrode Placement Electrocardiogram - RA, LA, RL, LL, V -. . . iStock. https://www.istockphoto.com/es/vector/5-electrocardiogramas-de-colocaci%C3%B3n-de-electrodos-de-plomo-ra-la-rl-ll-v-posici%C3%B3n-gm1586070345-529063354
[^5^]: Neurosce. (2023, 16 junio). ▷ El sistema nervioso autónomo. Neuroscenter. https://neuroscenter.com/blog/sistema-nervioso-autonomo/
[^6^]: DASHBOARD IV. (2023, 7 septiembre). Genially. https://view.genially.com/64f8112ad70759001171057a/interactive-content-dashboard-iv
