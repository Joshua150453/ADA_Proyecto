<table align="center">
    <thead>
        <tr>
            <td><img src="https://1.bp.blogspot.com/-3wALNMake70/XK-07VtIngI/AAAAAAABOrY/n3X_ZJV5fGEpTs8ppMQvKk_yic7BfyBYQCLcBGAs/s1600/universidad-la-salle-logo.jpg?raw=true" alt="EPIS" style="width:50%; height:auto"/></td>
            <th>
                <span style="font-weight:bold;">UNIVERSIDAD LA SALLE</span><br />
                <span style="font-weight:bold;">FACULTAD DE INGENIERÍA DE SOFTWARE</span><br />
            </th>
        </tr>
    </thead>
    <tbody>
        <tr><td colspan="3"><span style="font-weight:bold;">Formato</span>: Avance Final</td></tr>
    </tbody>
</table>

<div align="center">
    <span style="font-weight:bold;">GUÍA DEL AVANCE</span><br />
</div>

<div>
    <table border="1" align="center">
        <thead>
            <tr><th colspan="3">INFORMACIÓN BÁSICA</th></tr>
        </thead>
        <tbody>
            <tr>
                <td colspan="2">
                    <table>
                        <tr><td>ASIGNATURA:</td><td>Analisis y diseño de algoritmos</td></tr>
                        <tr><td>TÍTULO DEL TRABAJO:</td><td>Rúbrica de Evaluación – Todo</td></tr>
                        <tr>
                            <td>NÚMERO DEL TRABAJO:</td><td>01</td>
                            <td>AÑO:</td><td>2025</td>
                            <td>NRO. SEMESTRE:</td><td>V</td>
                        </tr>
                        <tr>
                            <td colspan="6">DOCENTE:
                                <ul>
                                    <li>Edson Francisco Luque Mamani - rescobedoq@unsa.edu.pe</li>
                                </ul>
                            </td>
                        </tr>
                        <tr>
                            <td colspan="6">INTEGRANTE:
                                <ul>
                                    <li>Ortiz Rosas Joshua David</li>
                                </ul>
                            </td>
                        </tr>
                    </table>
                </td>
                <td>
                    </table>
                    <table>
                </td>
            </tr>
        </tbody>
    </table>
</div>


## [Código en Google Collab] (https://colab.research.google.com/drive/1Rswz9g68C3gEKg9S5NWhXwrH-PLghS5Z#scrollTo=ojE1YADC86rd)
## ÍNDICE

- [Descripción general](#tablero-de-commits)
- [Procesamiento de datos](#Procesamiento-de-datos) 
  - [10 millones location_data](#10-millones-location_data) 
  - [10 millones users](#10-millones-users) 
  - [Análisis Exploratorio de Datos (EDA)](#Análisis-Exploratorio-de-Datos-(EDA))
  - [Propiedades y Métricas de la Red](#Propiedades-y-Métricas-de-la-Red)
  - [Propiedades y Métricas de la Red](#Propiedades-y-Métricas-de-la-Red) 
  - [Análisis Avanzado](#Análisis-Avanzado)
  - [Visualización](#Visualización)
  - [Conclusión](#Conclusión)
  - [Referencias](#Referencias) 
## 1. Descripción
Este proyecto analiza y visualiza el grafo de la red social 'X' a partir de un conjunto de datos de 10 millones de usuarios con sus conexiones y ubicaciones. El objetivo es descubrir patrones de conectividad y estructuras comunitarias mediante la construcción del grafo (usuarios como nodos, conexiones como aristas) y el análisis exploratorio de datos, incluyendo estadísticas básicas y visualizaciones. Se utilizarán los archivos de ubicación y usuarios proporcionados para este análisis en un entorno de programación.

## Materiales usados
- **Google Collab:** Entorno de ejecución
- **sqlite3:** Permite interactuar con bases de datos SQLite directamente en Python. Facilita la creación, conexión y manipulación de bases de datos SQL sin un servidor externo. Ideal para almacenamiento local y estructurado de datos.
- **pickle:** Serializa y deserializa objetos Python a un flujo de bytes. Permite guardar y cargar estructuras de datos complejas fácilmente. Útil para persistencia y transferencia de objetos Python.
- **os:** Proporciona funciones para interactuar con el sistema operativo. Permite manipular archivos, directorios y ejecutar comandos del sistema. Esencial para la interacción con el entorno del sistema.
- **networkx:** Crea, manipula y analiza grafos y redes complejas en Python. Ofrece herramientas para modelar relaciones y estudiar sus propiedades. Fundamental para el análisis de redes de diversos tipos.
- **matplotlib.pyplot:** Módulo para crear visualizaciones estáticas, interactivas y animadas en Python. Genera gráficos de líneas, barras, dispersión y más. Herramienta clave para la exploración y presentación visual de datos.
- **IPython.display (importando display y HTML):** Para mostrar contenido HTML (las visualizaciones de Plotly) directamente en entornos como Jupyter Notebooks o Google Colab.
- **community (específicamente community.community_louvain importado como co):** Una librería para la detección de comunidades en grafos, implementando el algoritmo de Louvain.
## 2. Procesamiento de datos
### 2.1. 10 millones location_data
#### import os:
- **Propósito:** Importa la librería os de Python.
- **Función:** Esta librería proporciona funciones para interactuar con el sistema operativo, como trabajar con rutas de archivos y verificar si un archivo existe.

#### def load_location_data(filename='10_million_location.txt', data_folder='/content/drive/MyDrive/data-ada', limit=None)::
**Definición de función:** Define una función llamada load_location_data.
**Parámetros:**
- **filename='10_million_location.txt':** Define un parámetro llamado filename con un valor predeterminado de '10_million_location.txt'. Este parámetro espera el nombre del archivo que contiene los datos de ubicación.
- **data_folder='/content/drive/MyDrive/data-ada':** Define un parámetro llamado data_folder con una ruta predeterminada. Este parámetro indica la carpeta donde se espera encontrar el archivo.
- **limit=None:** Define un parámetro opcional llamado limit. Si se proporciona un número entero, la función dejará de leer el archivo después de procesar esa cantidad de líneas.

#### filepath = os.path.join(data_folder, filename):
**Construcción de la ruta:** Utiliza la función os.path.join() para combinar la data_folder y el filename en una ruta de archivo completa. Esto asegura que la ruta sea válida independientemente del sistema operativo.

#### if not os.path.exists(filepath)::
- **Verificación de existencia:** Utiliza la función os.path.exists() para verificar si el archivo especificado en filepath realmente existe.
- **Condición:** Si el archivo no existe, la condición es verdadera.

#### raise FileNotFoundError(f"El archivo {filename} no se encuentra en {os.path.abspath(filepath)}"):
- **Manejo de error:** Si el archivo no existe, se lanza una excepción FileNotFoundError.
- **Mensaje de error:** El mensaje de error incluye el nombre del archivo y la ruta absoluta donde se esperaba encontrarlo, lo que ayuda al usuario a identificar el problema.

#### locations_dict = {}:
- **Inicialización de diccionario:** Se crea un diccionario vacío llamado locations_dict. Este diccionario se utilizará para almacenar los datos de ubicación, donde las claves serán los IDs de usuario (basados en el número de línea) y los valores serán tuplas de (latitud, longitud).

#### with open(filepath, 'r') as file::
- **Apertura de archivo:** Se abre el archivo especificado en filepath en modo lectura ('r').
- **with statement:** El uso de with open(...) asegura que el archivo se cierre automáticamente después de que se termine de trabajar con él, incluso si ocurren errores. La variable file representa el objeto del archivo abierto.

#### for idx, line in enumerate(file)::
- **Iteración sobre líneas:** Se inicia un bucle for para iterar sobre cada línea del archivo.
- **enumerate():** La función enumerate() devuelve tanto el índice (idx) de la línea (comenzando desde 0) como el contenido de la línea (line).

#### if limit and idx >= limit::
- **Verificación de límite:** Se verifica si se proporcionó un valor para limit (es decir, limit no es None) y si el índice actual de la línea (idx) es mayor o igual al límite.
- **Condición de parada:** Si ambas condiciones son verdaderas, significa que se ha leído la cantidad de líneas especificada por el limit.

#### break:
**Salida del bucle:** Si se alcanza el límite, la instrucción break sale del bucle for, deteniendo la lectura del archivo.

#### lat, lon = map(float, line.strip().split(',')):
#### **Procesamiento de la línea:**
- **line.strip():** Elimina cualquier espacio en blanco al principio y al final de la línea.
- **.split(','):** Divide la línea en una lista de cadenas utilizando la coma (,) como separador. Se espera que cada línea contenga dos valores separados por una coma (latitud y longitud).
- **map(float, ...):** Aplica la función float() a cada elemento de la lista resultante, convirtiendo las cadenas a números de punto flotante.
- **lat, lon = ...:** Asigna los dos valores flotantes resultantes a las variables lat (latitud) y lon (longitud).

#### locations_dict[idx + 1] = (lat, lon):
- **Almacenamiento en el diccionario:** Se agrega una nueva entrada al diccionario locations_dict. La clave es idx + 1 (se usa idx + 1 porque los IDs de usuario en la descripción del archivo comienzan en 1, mientras que los índices de enumerate comienzan en 0), y el valor es una tupla (lat, lon) que contiene las coordenadas de ubicación.
#### print(f"Datos de ubicaciones cargados exitosamente desde {filepath}"):
- **Mensaje de éxito:** Después de leer el archivo (o alcanzar el límite), se imprime un mensaje indicando que los datos de ubicación se cargaron correctamente y desde qué archivo.

#### print(f"Cargadas {len(locations_dict)} ubicaciones."):
- **Cantidad cargada:** Se imprime la cantidad total de ubicaciones que se cargaron en el diccionario locations_dict.

#### return locations_dict:
- **Retorno del diccionario:** La función devuelve el diccionario locations_dict que contiene los datos de ubicación cargados.

#### Descripción del Flujo:
- La función load_location_data se llama con el nombre del archivo de ubicación y la carpeta donde se encuentra (y opcionalmente un límite de líneas a leer).
- Se construye la ruta completa al archivo.
- Se verifica si el archivo existe en la ruta especificada. Si no existe, se detiene la función y se informa del error.
- Si el archivo existe, se crea un diccionario vacío para almacenar los datos de ubicación.
- Se abre el archivo para lectura.
- Se lee el archivo línea por línea, manteniendo un registro del número de línea.
#### **Para cada línea (hasta alcanzar el límite, si se proporcionó):**
- Se eliminan los espacios en blanco de la línea.
- Se divide la línea en dos partes usando la coma como separador (esperando latitud y longitud).
- Se convierten estas dos partes a números de punto flotante.
- Se almacenan estos números en el diccionario locations_dict, utilizando el número de línea (más uno) como clave y una tupla de (latitud, longitud) como valor.
- Una vez que se han leído todas las líneas (o se ha alcanzado el límite), se imprime un mensaje de éxito y la cantidad de ubicaciones cargadas.
- Finalmente, la función devuelve el diccionario locations_dict que contiene los datos de ubicación.
En resumen, esta función toma un archivo de texto con datos de latitud y longitud, los lee, los procesa y los guarda en un diccionario de Python, donde cada ID de usuario (basado en el orden de aparición en el archivo) se asocia con su ubicación. También incluye manejo de errores si el archivo no se encuentra y una opción para limitar la cantidad de datos leídos.

#### Limite
limite = 10_000_000, se usa esta linea para determinar el limite de datos a leer.

#### Carga y verificación
- locations_dict = load_location_data(limit = limite) # 22 segundos, se usa esta linea para realizar la carga de los datos, en total tarada 22 segundos a 30
-  **Verificar:** Finalmente se realiza una verificación de los datos.
    for user_id in range(1, 21):  # De 1 a 10 ususarios
    print(f"{user_id}: {locations_dict[user_id][0]}, {locations_dict[user_id][1]}")

### 2.2. 10 millones users
La función load_user_data_with_chunks_and_save_manual procesa un archivo de texto que contiene información sobre las conexiones entre usuarios de una red social, y guarda esta información en múltiples archivos "chunk" en formato pickle. El objetivo es manejar eficientemente grandes archivos de datos, dividiéndolos en partes más pequeñas para facilitar su procesamiento y almacenamiento. La función realiza las siguientes operaciones:
- **Lee el archivo de entrada:** Lee el archivo de texto especificado, donde cada línea representa un usuario y sus conexiones.
- **Procesa cada línea:** Convierte las conexiones de cada usuario a una lista de enteros, filtra conexiones inválidas (IDs no positivos, mayores al máximo ID, o iguales al propio ID del usuario) y limita el número de conexiones por usuario.
- **Crea chunks de datos:** Agrupa los datos de los usuarios en "chunks" de un tamaño específico.
- **Guarda los chunks:** Guarda cada chunk como un archivo pickle separado.
- **Maneja errores:** Maneja errores de archivo y de procesamiento de líneas.

#### Flujo de Ejecución:
##### Importar módulos:
- Importa el módulo os para operaciones con el sistema de archivos (verificar existencia de archivos, crear directorios).
- Importa el módulo pickle para serializar (convertir a bytes) los datos de los chunks y guardarlos en archivos.

##### Definir la función load_user_data_with_chunks_and_save_manual:
La función toma los siguientes parámetros:
- **filename:** Nombre del archivo de entrada (por defecto: '10_million_user.txt').
- **data_folder:** Carpeta donde se encuentra el archivo de entrada (por defecto: '/content/drive/MyDrive/data-ada').
- **output_folder:** Carpeta donde se guardarán los archivos chunk (por defecto: '/content/drive/MyDrive/user_dict_chunks').
- **chunksize:** Número de usuarios por chunk (por defecto: 100,000).

##### Construir la ruta del archivo de entrada:
Usa os.path.join para combinar la carpeta y el nombre del archivo para obtener la ruta completa al archivo de entrada.

##### Verificar la existencia del archivo de entrada:
- Usa os.path.exists para comprobar si el archivo de entrada existe.
- Si el archivo no existe, se lanza una excepción FileNotFoundError con un mensaje descriptivo.

##### Crear el directorio de salida (si no existe):
- Usa os.path.exists para comprobar si el directorio de salida existe.
- Si el directorio no existe, se crea usando os.makedirs.

##### Inicializar variables:
- **max_id:** Se establece el máximo ID de usuario permitido (10,000,000).
- **total_users:** Contador para el número total de usuarios procesados (inicializado en 0).
- **chunk_count:** Contador para el número de chunks guardados (inicializado en 0).
- **user_dict:** Diccionario para almacenar los datos de los usuarios del chunk actual (inicializado como un diccionario vacío).

##### Procesar el archivo de entrada línea por línea:
- Se abre el archivo de entrada en modo lectura con codificación UTF-8.
- Se itera sobre cada línea del archivo.
- **Para cada línea:**
- Se intenta procesar la línea (dentro de un bloque try...except para manejar errores de formato):
- Se eliminan los espacios en blanco de la línea y se divide en una lista de cadenas, asumiendo que las conexiones están separadas por comas.
- Se convierte cada cadena a un entero usando map y int
- Se calcula el ID del usuario actual (idx) como total_users + 1.
- **Se filtran las conexiones:**
- Se eliminan las conexiones que no son positivas, que son mayores que max_id, o que son iguales al propio ID del usuario.
- Se convierte el resultado a un conjunto (para eliminar duplicados) y luego a una lista.
- Se trunca la lista de conexiones a max_connections_per_user conexiones.
- Si el usuario tiene conexiones filtradas, se agrega una entrada al diccionario user_dict con el ID del usuario como clave y la lista de conexiones como valor.
- Si ocurre un error al procesar la línea (por ejemplo, si la línea no contiene números válidos), se captura la excepción ValueError y se continúa con la siguiente línea (usando continue).

##### Guardar chunks de usuarios:
Dentro del bucle que procesa las líneas, se verifica si el número de usuarios procesados (total_users) es un múltiplo del tamaño del chunk (chunksize).
- **Si es un múltiplo de chunksize:**
- Se construye la ruta del archivo de salida para el chunk actual.
- Se abre un archivo en modo escritura binaria ('wb').
- Se serializa el diccionario user_dict usando pickle.dump y se guarda en el archivo.
- Se imprime un mensaje indicando que el chunk se ha guardado.
- Se vacía el diccionario user_dict usando user_dict.clear().
- Se incrementa el contador de chunks (chunk_count).

##### Guardar el último chunk:
Después de procesar todas las líneas del archivo, puede haber datos restantes en user_dict que no forman un chunk completo.
- Se verifica si user_dict no está vacío.
- Si no está vacío, se guarda el chunk restante de la misma manera que los chunks completos.
- Se imprime un mensaje indicando que el chunk final se ha guardado.
- Se incrementa el contador de chunks (chunk_count).

##### Imprimir mensaje de finalización:
Se imprime un mensaje indicando que el procesamiento se ha completado, el número total de usuarios procesados y el número de archivos chunk guardados.

##### Manejar errores generales:
- Se incluye un bloque try...except que rodea todo el procesamiento del archivo para capturar cualquier excepción que pueda ocurrir durante la lectura o el procesamiento del archivo.
- Si ocurre una excepción, se lanza una excepción RuntimeError con un mensaje de error descriptivo.
##### Funcion de carga;
La función procesa el archivo de conexiones de usuarios, filtrando y limitando las conexiones de cada usuario. Guarda los datos en archivos chunk pickle para manejar grandes conjuntos de datos eficientemente.

##### Cargar usuarios:
La función get_user_connections recupera las conexiones de usuarios desde archivos "chunk" pickle, cargando los user_ids dados y optimizando la lectura de grandes conjuntos de datos.

##### Verificación:
Se verifican los datos cargados.

### 2.3. Análisis Exploratorio de Datos (EDA)
Se lleva acabo la construcción del grafo, su visualización básica y datos de análisis extra.

#### Importar Librerías:
- **sqlite3:** Para interactuar con la base de datos SQLite.
- **pickle:** Para serializar y deserializar objetos de Python (usado para guardar y cargar los "chunks" de datos de usuarios).
- **os:** Para operaciones del sistema operativo, como trabajar con rutas de archivos y directorios.
- **networkx:** Para crear, manipular y visualizar grafos.
- **matplotlib.pyplot:** Para crear visualizaciones de grafos.

#### Construir_grafo_desde_chunks_con_disco:
- **Propósito:** Construye un grafo desde archivos de "chunk" que contienen datos de usuarios y los guarda en una base de datos SQLite.
- **Cómo funciona:**
- Crea una conexión a una base de datos SQLite.
- Crea tablas para almacenar nodos (usuarios) y aristas (conexiones).
- Obtiene una lista de archivos "chunk".
- Itera a través de cada archivo "chunk":
- Carga el "chunk" usando pickle.load().
- Itera a través de los usuarios y sus conexiones en el "chunk":
- **Si el usuario tiene información de ubicación:**
- Inserta el usuario en la tabla de nodos (si no existe).
- Itera a través de las conexiones del usuario:
- Si el amigo también tiene ubicación, inserta la conexión como una arista en la tabla de aristas.
- Confirma los cambios en la base de datos después de procesar cada "chunk".
- Cierra la conexión a la base de datos.

#### Dibujar_muestra_grafo_desde_db:
- **Propósito:** Dibuja una muestra del grafo desde la base de datos SQLite.
- **Cómo funciona:**
- Establece una conexión a la base de datos SQLite.
- Obtiene una muestra de nodos (usuarios) de la tabla de nodos.
- Crea un grafo dirigido usando networkx.
- Añade nodos al grafo, utilizando la latitud y longitud como atributos de posición.
- Obtiene las aristas (conexiones) de la tabla de aristas que conectan los nodos de la muestra.
- Añade aristas al grafo.
- Dibuja el grafo usando networkx y matplotlib.
- Muestra el grafo dibujado.

#### Mostrar_grafo_desde_sqlite:
- **Propósito:** Muestra los primeros 100 nodos y las primeras 1000 aristas de la base de datos SQLite.
- **Cómo funciona:**
- Se conecta a la base de datos SQLite.
- Ejecuta consultas para seleccionar los primeros 100 nodos y las primeras 1000 aristas.
- Imprime los resultados en un formato legible.
- Cierra la conexión a la base de datos.

#### Estadisticas_basicas:
- **Propósito:** Calcula y muestra estadísticas básicas del grafo almacenado en la base de datos SQLite.
- **Cómo funciona:**
- Se conecta a la base de datos SQLite.
- Calcula el número de nodos y aristas usando consultas SQL.
- Calcula el grado promedio y la densidad del grafo.
- Imprime las estadísticas calculadas.
- Cierra la conexión a la base de datos.

### 2.4. Propiedades y Métricas de la Red
#### 2.4.1. Detección de Comunidades
La detección de comunidades constituye un pilar fundamental en el análisis de redes, facilitando la identificación de grupos de nodos (en este contexto, usuarios) que exhiben una densidad de conexiones intra-grupo superior a la observada con el resto de la red. Estos agregados cohesivos, denominados comunidades, son intrínsecos a la estructura de la red y suelen revelar patrones subyacentes de interacción, afinidad o proximidad, ya sean de naturaleza social, geográfica o temática. Su comprensión es esencial para dilucidar la organización interna y la dinámica funcional de la red.

En el marco del presente proyecto, se han explorado y aplicado dos enfoques algorítmicos distintos para la identificación de estas estructuras comunitarias, los cuales se describen a continuación:

- **Cómo se hace en el código:**
- **Algoritmo de Girvan-Newman (Implementación Manual):** Se empleó una implementación manual del algoritmo de Girvan-Newman, un método iterativo que descompone progresivamente la red basándose en la métrica de centralidad de intermediación, con el fin de revelar las comunidades inherentes.
- **Cálculo Iterativo de Centralidad de Intermediación:** En cada iteración del algoritmo, se procede a la determinación de la centralidad de intermediación para todas las aristas del grafo. Esta métrica cuantifica la trascendencia de una arista como un punto de paso crucial en los caminos más cortos que conectan pares de nodos dentro de la red. Para la correcta aplicación de este cálculo, es imperativo que el grafo sea no dirigido, dado que la centralidad de intermediación se conceptualiza bajo la premisa de una "importancia de puente" bidireccional de las conexiones, facilitando el flujo de información o interacción en ambas direcciones.
- **Remoción de Aristas Clave:** La arista que ostenta el valor más elevado de centralidad de intermediación es sistemáticamente identificada y subsiguientemente eliminada del grafo. Esta acción se fundamenta en que dicha arista representa un enlace crítico que une potenciales comunidades. La disrupción de estos enlaces "puente" es el mecanismo que induce la segregación de los grupos.
- **Fragmentación y Re-cálculo:** Tras la remoción de una arista, se realiza un recálculo de todas las centralidades para el grafo modificado. Este proceso iterativo conduce a una fragmentación gradual del grafo en componentes conectados, cada uno de los cuales se consolida como una comunidad. El algoritmo persiste en su ejecución hasta que se satisface un número predefinido de comunidades objetivo o hasta la disolución completa de la estructura de la red en componentes individuales. Es pertinente señalar que, en escenarios donde la topología inicial del grafo ya presenta componentes débilmente conectados, el algoritmo podría finalizar en su primera iteración si el número de componentes conectados ya existentes coincide o excede el umbral de comunidades objetivo.
- Consideraciones Computacionales: Dada la inherente complejidad computacional del algoritmo de Girvan-Newman (O(M^2 N) para grafos dispersos), su aplicación en este proyecto se circunscribió a una muestra controlada de nodos (e.g., 500 a 1000 nodos) del grafo total. Esta estrategia fue indispensable para mantener la viabilidad computacional y los tiempos de procesamiento dentro de límites aceptables.

### 2.5. Análisis Avanzado
#### 2.5.1. Análisis de Camino Más Corto
El análisis de camino más corto constituye una métrica fundamental para evaluar la eficiencia y la fluidez con la que la información o cualquier tipo de interacción se propaga a través de una red. Esta propiedad es central para comprender el fenómeno de "mundo pequeño", donde los nodos están conectados por distancias relativas cortas.

- **Proceso de Implementación en el Código:**
- **Carga de una Muestra del Grafo:**  Para gestionar la escala del conjunto de datos completo y garantizar la viabilidad computacional, el código inicia el proceso cargando una muestra representativa del grafo no ponderado desde la base de datos SQLite. Esta estrategia es esencial para permitir la ejecución eficiente de los algoritmos de búsqueda de caminos en un tiempo computacionalmente viable.
- **Selección de Nodos Origen:** Se selecciona una sub-muestra aleatoria de nodos que servirán como puntos de partida para los cálculos de caminos más cortos. Esta técnica de muestreo es crucial para evitar la prohibitiva complejidad de procesar todos los posibles pares de nodos en un grafo de gran tamaño, proporcionando una estimación robusta de la conectividad promedio.
- **Ejecución de BFS (Implementación Manual):** Por cada nodo origen seleccionado en la sub-muestra, se ejecuta una implementación manual del algoritmo de Búsqueda en Amplitud (BFS). BFS es el algoritmo óptimo para encontrar caminos más cortos en grafos no ponderados, explorando la red capa por capa desde el nodo origen. Este método garantiza que la primera ruta descubierta hacia cualquier nodo sea la más corta en términos del número de aristas (saltos). Durante esta exploración, se registran las distancias discretas desde el nodo origen hasta todos los nodos alcanzables dentro de la muestra del grafo.
- **Cálculo de la Longitud Promedio:** Una vez obtenidas las distancias más cortas desde cada nodo origen de la muestra hacia sus respectivos nodos alcanzables, estas distancias se agregan y se promedian. El resultado es la longitud promedio del camino más corto de la red (basada en la muestra), una métrica clave que cuantifica la cohesión general y la eficiencia en la conectabilidad estructural del grafo. Un valor bajo indica una red densamente conectada y con una comunicación eficiente.

#### 2.5.2. Árboles de Expansión Mínima (MST)
Los Árboles de Expansión Mínima (MST) proporcionan una perspectiva única sobre la conectividad más eficiente dentro de una red ponderada. Un MST es un subgrafo que interconecta todos los nodos de la red utilizando el menor peso total posible de aristas, sin generar ningún ciclo. En el contexto de esta red social, los "pesos" de las aristas corresponden a la distancia geográfica Haversine entre los usuarios, lo que permite transformar un problema de conectividad social en uno de eficiencia espacial.
- **Proceso de Implementación en el Código:**
- **Carga del Grafo Ponderado:** El proceso se inicia con la carga de una muestra del grafo desde la base de datos SQLite. Es de vital importancia que este grafo esté ponderado, lo que significa que cada arista entre dos usuarios debe poseer un valor numérico asociado (su peso). En esta aplicación, el peso se define por la distancia Haversine entre las coordenadas geográficas de los usuarios conectados por dicha arista, lo que dota al grafo de una dimensión espacial cuantitativa.
- **Inicialización del Algoritmo de Prim:** La implementación manual del algoritmo de Prim se inicia seleccionando un nodo arbitrario de la muestra del grafo. Este nodo es inmediatamente agregado al conjunto de nodos que comenzarán a formar el MST. El resto de los nodos en la muestra se marcan inicialmente como "no visitados" o "no incluidos" en el árbol en construcción.
- **Expansión Iterativa del Árbol (Implementación Manual de Prim):** El algoritmo de Prim sigue un enfoque voraz (greedy) para la construcción del MST. En cada paso iterativo, el algoritmo identifica y selecciona la arista de menor peso que conecta un nodo que ya ha sido incluido en el MST con un nodo que aún no ha sido visitado. Esta arista, junto con el nodo no visitado que conecta, se incorpora al MST en crecimiento. Este procedimiento se repite, expandiendo el árbol, asegurando que en cada adición se mantenga la propiedad de mínima conectividad. Una cola de prioridad (min-heap) se utiliza eficientemente para gestionar y seleccionar rápidamente la aristas de menor peso disponibles, optimizando el rendimiento del algoritmo.
- **Finalización del Proceso:** Este procedimiento iterativo continúa hasta que todos los nodos de la muestra inicial han sido exitosamente incluidos en el MST. El resultado final es un subgrafo que representa la conexión de todos los usuarios de la muestra con la distancia geográfica total mínima posible. Este MST ilustra la "columna vertebral" más eficiente de la conectividad geográficamente determinada de la red, revelando las interconexiones esenciales con el menor coste espacial.

### 2.6. Visualización
#### 2.6.1. Visualizaciones Interactivas
Las visualizaciones interactivas son un componente crucial para transformar la complejidad de los datos y los resultados del análisis de grafos en representaciones comprensibles y explorables. Esta capacidad permite una comprensión intuitiva y dinámica de la estructura de la red, superando las limitaciones de los datos tabulares o los gráficos estáticos.

- **Proceso de Implementación en el Código:**
- Carga de Datos de Ubicación y Conexiones:** El código inicia la fase de visualización recuperando las coordenadas de latitud y longitud de una muestra de nodos, junto con la información de sus aristas conectadas, directamente desde la base de datos SQLite. La utilización de una muestra es fundamental para asegurar un rendimiento adecuado en la visualización interactiva.
- **Construcción de la Estructura para Plotly:** Aunque la visualización final se realiza con Plotly, se emplea la librería networkx de manera auxiliar para construir un objeto networkx.Graph temporal. Este objeto se popula con los nodos y aristas de la muestra, y se enriquece al adjuntar las coordenadas geográficas (lat y lon) como atributos a cada nodo, lo que simplifica la preparación de los datos para Plotly.
- **Generación de Trazos Geoespaciales (Plotly):** Utilizando las capacidades geoespaciales de Plotly, se generan dos tipos principales de "trazos" (go.Scattergeo):
  - **Un trazo para las aristas:** representadas como líneas finas (mode='lines') que unen las coordenadas geográficas de los nodos conectados.
  - **Un trazo para los nodos:** visualizados como marcadores (mode='markers') posicionados en sus respectivas ubicaciones geográficas.
- **Configuración y Renderización Interactiva:** Se configura el diseño del mapa base (incluyendo el alcance global, y los colores de la tierra y los países) para proporcionar un contexto geográfico claro. Finalmente, se construye un objeto go.Figure que integra ambos trazos. Este objeto se convierte a formato HTML interactivo (fig.to_html) y se despliega directamente en el entorno de desarrollo (Google Colab, por ejemplo, mediante IPython.display.HTML). La interactividad inherente de Plotly permite a los usuarios realizar acciones como zoom, desplazamiento y, al posicionar el cursor sobre un nodo o arista, acceder a información detallada (como el ID del usuario), lo que enriquece significativamente la exploración de la densidad de conexiones y la distribución espacial de la red.

#### 2.6.2. Visualización de Comunidades
La visualización de comunidades representa una extensión del análisis interactivo, al integrar directamente los resultados de la detección de comunidades sobre el mapa geográfico. Esta integración permite una comprensión visual y espacial de cómo los grupos cohesivos se distribuyen dentro de la red, facilitando la interpretación de las estructuras sociales inherentes.
- **Proceso de Implementación en el Código:**
- **Carga del Grafo de Muestra:** Similar al proceso de visualización general, el código comienza cargando una muestra representativa del grafo desde la base de datos SQLite. Esta muestra debe incluir tanto la información de las conexiones entre nodos como sus coordenadas geográficas.
- **Detección de Comunidades (Louvain para Eficiencia):** Para esta fase de visualización, se opta por la función community.community_louvain.best_partition de la librería python-louvain. Esta elección se justifica por la alta eficiencia del algoritmo de Louvain en la detección rápida de comunidades en muestras de grafos grandes, lo cual es fundamental para una visualización fluida y responsiva. Este paso asigna una identificación de comunidad a cada nodo dentro de la muestra.
- **Asignación Dinámica de Colores:** Una vez que cada nodo tiene asignada una comunidad, el código procede a utilizar una paleta de colores (por ejemplo, 'viridis' de matplotlib.cm) para generar un color único y distintivo para cada ID de comunidad. Este mapeo de colores asegura que las diferentes comunidades sean fácilmente distinguibles visualmente en el mapa interactivo.
- **Actualización y Renderización del Trazo de Nodos:** El trazo de los nodos en Plotly (go.Scattergeo) se actualiza de manera crucial. El atributo marker=dict(color=...) de cada nodo se asigna dinámicamente al color correspondiente a su comunidad. Adicionalmente, se mejora la información emergente (hoverinfo='text') para que, al pasar el cursor sobre un nodo, se visualice no solo el ID del usuario, sino también el ID de la comunidad a la que pertenece. La figura de Plotly, ahora enriquecida con los nodos coloreados por comunidad, se renderiza como un archivo HTML interactivo y se despliega en el entorno. Esta representación visualmente potente permite a los usuarios no solo explorar la red geográficamente, sino también observar de manera inmediata cómo se agrupan los usuarios en distintas comunidades y cómo estas se distribuyen espacialmente, proporcionando una herramienta analítica y comunicativa de gran valor.

### 2.7. Conclusión
#### Resumen de hallazgos:
- **Gestión Eficiente de Datos a Gran Escala:** La adopción de una estrategia de procesamiento por chunks y la persistencia del grafo en una base de datos SQLite fueron cruciales. Estas decisiones técnicas permitieron superar las limitaciones de memoria, procesar eficazmente los vastos volúmenes de nodos y aristas, y facilitar la consulta del grafo sin necesidad de gastar la totalidad de la memoria RAM.
- **Identificación de Estructuras Comunitarias:** La implementación manual del algoritmo de Girvan-Newman, aplicado a una muestra representativa del grafo, posibilitó la identificación de comunidades o grupos cohesivos. Este hallazgo es fundamental para comprender la organización interna y la formación de clústeres sociales. La integración complementaria del algoritmo de Louvain para la visualización destacó la practicidad de emplear diversas herramientas según la fase del análisis.
- **Evaluación de la Eficiencia de la Red:** El cálculo de la longitud promedio del camino más corto, utilizando el algoritmo BFS en una muestra, ofreció una perspectiva sobre la eficiencia de la comunicación o la propagación de información dentro de la red. Este resultado es vital para determinar si la red exhibe características de un "mundo pequeño".
- **Optimización de la Conectividad Geográfica:** La construcción de un Árbol de Expansión Mínima (MST), ponderado por la distancia Haversine entre usuarios y calculado mediante la implementación del algoritmo de Prim, reveló la estructura de conectividad social más eficiente en términos de proximidad geográfica. Esto proporciona una visión única sobre cómo las conexiones pueden fortalecerse en función de la cercanía espacial.
- **Visualización Interactiva:** Las representaciones visuales desarrolladas con Plotly, que superponen la estructura del grafo y las comunidades sobre un mapa geográfico interactivo, constituyen herramientas poderosas para explorar y comunicar los hallazgos de manera intuitiva y atractiva, facilitando la comprensión espacial de la red.

#### Trabajo Futuro:
- **Detección de Nodos Influyentes:** Ampliar el análisis mediante la implementación de métricas de centralidad adicionales (e.g., centralidad de grado, cercanía, PageRank) con el fin de identificar a los usuarios más influyentes o estratégicamente centrales dentro de la red.
- **Mejora de la Escalabilidad de Algoritmos:** Para datasets de magnitud aún mayor, explorar la implementación de algoritmos de grafos en entornos distribuidos (e.g., Apache Spark GraphX, Dask-Graph) o la adopción de bases de datos de grafos especializadas (e.g., Neo4j, ArangoDB).
- **Optimización de Visualizaciones**: Investigar técnicas de agregación de nodos o el uso de herramientas de visualización de grafos de alto rendimiento (e.g., Gephi) para manejar muestras de mayor tamaño y explorar diferentes aspectos visuales del grafo.
- **Análisis de la Robustez de la Red:** Evaluar la resiliencia de la red frente a la eliminación aleatoria de nodos o aristas, así como ante ataques dirigidos, lo que es crucial para comprender su estabilidad y vulnerabilidad.

### 2.8. Referencias
*   SQLite.org. "SQLite Home Page." https://www.sqlite.org/
*   NetworkX Developers. "NetworkX: Network analysis in Python." https://networkx.org/
*   The Pandas Development Team. "Pandas: powerful Python data analysis toolkit." https://pandas.pydata.org/
*   Harris, C.R., Millman, K.J., van der Walt, S.J. et al. "Array programming with NumPy." Nature 585, 357–362 (2020). https://numpy.org/
*   Algoritmo de Brandes GeeksforGeeks: "Betweenness Centrality in Graph" https://www.geeksforgeeks.org/betweenness-centrality-centrality-measure/
*   Algoritmo de Girvan-Newman (Detección de Comunidades) Towards Data Science (Medium) https://towardsdatascience.com/tag/community-detection/
*   Algoritmo de Prim (Árbol de Expansión Mínima) Programiz: "Prim's Algorithm" https://www.programiz.com/dsa/prim-algorithm
*   Algoritmo BFS (Búsqueda en Amplitud) GeeksforGeeks: "Breadth First Search (BFS) for a Graph" https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/
*   Fórmula de Haversine GISGeography: "Haversine Formula" - https://community.esri.com/t5/coordinate-reference-systems-blog/distance-on-a-sphere-the-haversine-formula/ba-p/902128
