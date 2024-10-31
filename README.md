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

# Diseño de Filtro Pasa Banda

## Diseñar un filtro pasa banda con:

- Atenuación de -3 dB en 👦\Omega_0 = 50 \pm 5👦 Hz, 👦100 \pm 4👦 Hz.
- 👦f_1 = 0.05👦 Hz
- 👦f_2 = 250👦 Hz
- 👦f_c = 5👦 Hz
- 👦f_u = 250👦 Hz

Con:
\[
-20 \, \text{dB en } \, 0.15 \, \Omega_0, 0.25 \, \Omega_0
\]

## Conversiones

\[
\Omega_1 = 2 \pi \cdot 0.5 \, \text{Hz} = 3.1415 \, \text{rad/s}
\]
\[
\Omega_2 = 2 \pi \cdot 250 \, \text{Hz} = 1570.79 \, \text{rad/s}
\]
\[
\Omega_c = 2 \pi \cdot 5 \, \text{Hz} = 31.41 \, \text{rad/s}
\]
\[
\Omega_u = 2 \pi \cdot 100 \, \text{Hz} = 628.318 \, \text{rad/s}
\]

## Cálculo de 👦Q👦 y 👦n👦

\[
n = \frac{\log_{10} \frac{1}{\sqrt{2}}}{\log_{10} \left(\frac{\Omega_1}{\Omega_2}\right)} = 1.91
\]
\[
\alpha = \frac{1}{Q} \quad \text{donde} \quad Q = \frac{\Omega_0}{\Delta \Omega}
\]
\[
\Delta \Omega = \Omega_2 - \Omega_1
\]
\[
\Omega_0 = \sqrt{\Omega_1 \cdot \Omega_2} = \sqrt{3.1415 \cdot 1570.79} = 70.35
\]
\[
\alpha = \frac{\Omega_0}{\Delta \Omega} = \frac{70.35}{1570.79 - 3.1415} = 0.045
\]

## Gráficos de Respuesta

| 👦\Omega👦 | Magnitud (dB) |
|------------|---------------|
| 👦\Omega_1👦 | -3 |
| 👦\Omega_0👦 | 0 |
| 👦\Omega_2👦 | -3 |

![Gráfico de Bode](bode_plot_example.png)

## Filtro Pasa Bajo Normalizado con 👦\alpha = 2.610 \, \text{rad/s}👦

\[
n = \frac{\log_{10} \left(\frac{1}{0.707}\right)}{\log_{10} \left(\frac{1}{2.610}\right)} = 1.861
\]
\[
\Omega_1 = 2.610, \quad \Omega_2 = 2.610
\]

| 👦\Omega👦 | Magnitud (dB) |
|------------|---------------|
| 👦\Omega_1👦 | -3 |
| 👦\Omega_0👦 | 0 |
| 👦\Omega_2👦 | -3 |

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

#### Aplicaciones y Beneficios del Diseño

El diseño de este filtro proporciona múltiples beneficios:

- **Preservación de Información Crítica**: Al centrarse en las frecuencias de interés, el filtro garantiza que la información crucial relacionada con la actividad cardíaca se conserve durante el procesamiento. Las componentes de frecuencia en el rango de 5 Hz a 100 Hz son particularmente relevantes para identificar patrones cardíacos y posibles anomalías.

- **Reducción de Ruido**: Este filtro es eficaz para eliminar ruidos de baja frecuencia (como interferencias electromagnéticas) y también atenuar componentes de alta frecuencia que podrían distorsionar la señal de ECG. Este proceso de limpieza es esencial para garantizar que el análisis posterior se base en datos fiables.

- **Mejora de la Calidad de la Señal**: Al aplicar un filtro de orden 3, se logra una mayor atenuación de las frecuencias no deseadas, lo que mejora la calidad general de la señal procesada. Esto es crucial para realizar análisis precisos y significativos, ya que una señal limpia facilita la identificación de características relevantes.

- **Flexibilidad en el Análisis**: La implementación de dos conjuntos de frecuencias de corte permite una mayor flexibilidad en el análisis. Dependiendo del enfoque del estudio, se puede optar por un análisis más detallado (5 Hz a 100 Hz) o uno más amplio (0.5 Hz a 250 Hz), adaptándose así a las necesidades específicas de cada análisis.


[^1^]:Guía de colocación de electrodos. (s. f.). Neotecnia. https://neotecnia.mx/blogs/noticias/guia-de-colocacion-de-electrodos?srsltid=AfmBOopEYZV3x6zO5EtnVZ28WQZA4e1kedPIHHK8izv-80wiKwPuaQQI
[^2^]:National Instruments. (s/f). Multifunction Input and Output Devices. https://www.ni.com/pdf/product-flyers/multifunction-io.pdf
[^3^]:ELECTROCARDIOGRAFO ECG AD8232. (s/f). MACTRONICA. https://www.mactronica.com.co/electrocardiografo-ecg-ad8232
[^4^]: Md, A. (s. f.). 5 Lead Electrode Placement Electrocardiogram - RA, LA, RL, LL, V -. . . iStock. https://www.istockphoto.com/es/vector/5-electrocardiogramas-de-colocaci%C3%B3n-de-electrodos-de-plomo-ra-la-rl-ll-v-posici%C3%B3n-gm1586070345-529063354
[^5^]: Neurosce. (2023, 16 junio). ▷ El sistema nervioso autónomo. Neuroscenter. https://neuroscenter.com/blog/sistema-nervioso-autonomo/
[^6^]: DASHBOARD IV. (2023, 7 septiembre). Genially. https://view.genially.com/64f8112ad70759001171057a/interactive-content-dashboard-iv
