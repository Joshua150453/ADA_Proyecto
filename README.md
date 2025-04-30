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
        <tr><td colspan="3"><span style="font-weight:bold;">Formato</span>: Avance 1</td></tr>
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
                        <tr><td>TÍTULO DEL TRABAJO:</td><td>Rúbrica de Evaluación – Carga Masiva + EDA en Python</td></tr>
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


## ÍNDICE

- [Descripción general](#tablero-de-commits)
- [Procesamiento de datos](#Procesamiento-de-datos) 
  - [10 millones location_data](#10-millones-location_data)
  - - [10 millones users](#10-millones-users)
## 1. Descripción
Este proyecto analiza y visualiza el grafo de la red social 'X' a partir de un conjunto de datos de 10 millones de usuarios con sus conexiones y ubicaciones. El objetivo es descubrir patrones de conectividad y estructuras comunitarias mediante la construcción del grafo (usuarios como nodos, conexiones como aristas) y el análisis exploratorio de datos, incluyendo estadísticas básicas y visualizaciones. Se utilizarán los archivos de ubicación y usuarios proporcionados para este análisis en un entorno de programación.

## Materiales usados
- Google Collab: Entorno de ejecución
- sqlite3: Permite interactuar con bases de datos SQLite directamente en Python. Facilita la creación, conexión y manipulación de bases de datos SQL sin un servidor externo. Ideal para almacenamiento local y estructurado de datos.
- pickle: Serializa y deserializa objetos Python a un flujo de bytes. Permite guardar y cargar estructuras de datos complejas fácilmente. Útil para persistencia y transferencia de objetos Python.
- os: Proporciona funciones para interactuar con el sistema operativo. Permite manipular archivos, directorios y ejecutar comandos del sistema. Esencial para la interacción con el entorno del sistema.
- networkx: Crea, manipula y analiza grafos y redes complejas en Python. Ofrece herramientas para modelar relaciones y estudiar sus propiedades. Fundamental para el análisis de redes de diversos tipos.
- matplotlib.pyplot: Módulo para crear visualizaciones estáticas, interactivas y animadas en Python. Genera gráficos de líneas, barras, dispersión y más. Herramienta clave para la exploración y presentación visual de datos.
## 2. Procesamiento de datos
### 2.1. 10 millones location_data
#### import os:
- Propósito: Importa la librería os de Python.
- Función: Esta librería proporciona funciones para interactuar con el sistema operativo, como trabajar con rutas de archivos y verificar si un archivo existe.

#### def load_location_data(filename='10_million_location.txt', data_folder='/content/drive/MyDrive/data-ada', limit=None)::
Definición de función: Define una función llamada load_location_data.
Parámetros:
- filename='10_million_location.txt': Define un parámetro llamado filename con un valor predeterminado de '10_million_location.txt'. Este parámetro espera el nombre del archivo que contiene los datos de ubicación.
- data_folder='/content/drive/MyDrive/data-ada': Define un parámetro llamado data_folder con una ruta predeterminada. Este parámetro indica la carpeta donde se espera encontrar el archivo.
- limit=None: Define un parámetro opcional llamado limit. Si se proporciona un número entero, la función dejará de leer el archivo después de procesar esa cantidad de líneas.

#### filepath = os.path.join(data_folder, filename):
Construcción de la ruta: Utiliza la función os.path.join() para combinar la data_folder y el filename en una ruta de archivo completa. Esto asegura que la ruta sea válida independientemente del sistema operativo.

#### if not os.path.exists(filepath)::
- Verificación de existencia: Utiliza la función os.path.exists() para verificar si el archivo especificado en filepath realmente existe.
- Condición: Si el archivo no existe, la condición es verdadera.

#### raise FileNotFoundError(f"El archivo {filename} no se encuentra en {os.path.abspath(filepath)}"):
- Manejo de error: Si el archivo no existe, se lanza una excepción FileNotFoundError.
- Mensaje de error: El mensaje de error incluye el nombre del archivo y la ruta absoluta donde se esperaba encontrarlo, lo que ayuda al usuario a identificar el problema.

#### locations_dict = {}:
- Inicialización de diccionario: Se crea un diccionario vacío llamado locations_dict. Este diccionario se utilizará para almacenar los datos de ubicación, donde las claves serán los IDs de usuario (basados en el número de línea) y los valores serán tuplas de (latitud, longitud).

#### with open(filepath, 'r') as file::
- Apertura de archivo: Se abre el archivo especificado en filepath en modo lectura ('r').
- with statement: El uso de with open(...) asegura que el archivo se cierre automáticamente después de que se termine de trabajar con él, incluso si ocurren errores. La variable file representa el objeto del archivo abierto.

#### for idx, line in enumerate(file)::
- Iteración sobre líneas: Se inicia un bucle for para iterar sobre cada línea del archivo.
- enumerate(): La función enumerate() devuelve tanto el índice (idx) de la línea (comenzando desde 0) como el contenido de la línea (line).

#### if limit and idx >= limit::
- Verificación de límite: Se verifica si se proporcionó un valor para limit (es decir, limit no es None) y si el índice actual de la línea (idx) es mayor o igual al límite.
- Condición de parada: Si ambas condiciones son verdaderas, significa que se ha leído la cantidad de líneas especificada por el limit.

#### break:
Salida del bucle: Si se alcanza el límite, la instrucción break sale del bucle for, deteniendo la lectura del archivo.

#### lat, lon = map(float, line.strip().split(',')):
Procesamiento de la línea:
- line.strip(): Elimina cualquier espacio en blanco al principio y al final de la línea.
- .split(','): Divide la línea en una lista de cadenas utilizando la coma (,) como separador. Se espera que cada línea contenga dos valores separados por una coma (latitud y longitud).
- map(float, ...): Aplica la función float() a cada elemento de la lista resultante, convirtiendo las cadenas a números de punto flotante.
- lat, lon = ...: Asigna los dos valores flotantes resultantes a las variables lat (latitud) y lon (longitud).

#### locations_dict[idx + 1] = (lat, lon):
- Almacenamiento en el diccionario: Se agrega una nueva entrada al diccionario locations_dict. La clave es idx + 1 (se usa idx + 1 porque los IDs de usuario en la descripción del archivo comienzan en 1, mientras que los índices de enumerate comienzan en 0), y el valor es una tupla (lat, lon) que contiene las coordenadas de ubicación.
#### print(f"Datos de ubicaciones cargados exitosamente desde {filepath}"):
- Mensaje de éxito: Después de leer el archivo (o alcanzar el límite), se imprime un mensaje indicando que los datos de ubicación se cargaron correctamente y desde qué archivo.

#### print(f"Cargadas {len(locations_dict)} ubicaciones."):
- Cantidad cargada: Se imprime la cantidad total de ubicaciones que se cargaron en el diccionario locations_dict.

#### return locations_dict:
- Retorno del diccionario: La función devuelve el diccionario locations_dict que contiene los datos de ubicación cargados.

#### Descripción del Flujo:
- La función load_location_data se llama con el nombre del archivo de ubicación y la carpeta donde se encuentra (y opcionalmente un límite de líneas a leer).
- Se construye la ruta completa al archivo.
- Se verifica si el archivo existe en la ruta especificada. Si no existe, se detiene la función y se informa del error.
- Si el archivo existe, se crea un diccionario vacío para almacenar los datos de ubicación.
- Se abre el archivo para lectura.
- Se lee el archivo línea por línea, manteniendo un registro del número de línea.
Para cada línea (hasta alcanzar el límite, si se proporcionó):
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
-  Verificar: Finalmente se realiza una verificación de los datos.
   for user_id in range(1, 21):  # De 1 a 10 ususarios
    print(f"{user_id}: {locations_dict[user_id][0]}, {locations_dict[user_id][1]}")

### 2.2. 10 millones users
La función load_user_data_with_chunks_and_save_manual procesa un archivo de texto que contiene información sobre las conexiones entre usuarios de una red social, y guarda esta información en múltiples archivos "chunk" en formato pickle. El objetivo es manejar eficientemente grandes archivos de datos, dividiéndolos en partes más pequeñas para facilitar su procesamiento y almacenamiento. La función realiza las siguientes operaciones:
- Lee el archivo de entrada: Lee el archivo de texto especificado, donde cada línea representa un usuario y sus conexiones.
- Procesa cada línea: Convierte las conexiones de cada usuario a una lista de enteros, filtra conexiones inválidas (IDs no positivos, mayores al máximo ID, o iguales al propio ID del usuario) y limita el número de conexiones por usuario.
- Crea chunks de datos: Agrupa los datos de los usuarios en "chunks" de un tamaño específico.
- Guarda los chunks: Guarda cada chunk como un archivo pickle separado.
- Maneja errores: Maneja errores de archivo y de procesamiento de líneas.

#### Flujo de Ejecución:
##### Importar módulos:
- Importa el módulo os para operaciones con el sistema de archivos (verificar existencia de archivos, crear directorios).
- Importa el módulo pickle para serializar (convertir a bytes) los datos de los chunks y guardarlos en archivos.

##### Definir la función load_user_data_with_chunks_and_save_manual:
La función toma los siguientes parámetros:
- filename: Nombre del archivo de entrada (por defecto: '10_million_user.txt').
- data_folder: Carpeta donde se encuentra el archivo de entrada (por defecto: '/content/drive/MyDrive/data-ada').
- output_folder: Carpeta donde se guardarán los archivos chunk (por defecto: '/content/drive/MyDrive/user_dict_chunks').
- chunksize: Número de usuarios por chunk (por defecto: 100,000).

##### Construir la ruta del archivo de entrada:
Usa os.path.join para combinar la carpeta y el nombre del archivo para obtener la ruta completa al archivo de entrada.

##### Verificar la existencia del archivo de entrada:
- Usa os.path.exists para comprobar si el archivo de entrada existe.
- Si el archivo no existe, se lanza una excepción FileNotFoundError con un mensaje descriptivo.

##### Crear el directorio de salida (si no existe):
- Usa os.path.exists para comprobar si el directorio de salida existe.
- Si el directorio no existe, se crea usando os.makedirs.

##### Inicializar variables:
- max_id: Se establece el máximo ID de usuario permitido (10,000,000).
- total_users: Contador para el número total de usuarios procesados (inicializado en 0).
- chunk_count: Contador para el número de chunks guardados (inicializado en 0).
- user_dict: Diccionario para almacenar los datos de los usuarios del chunk actual (inicializado como un diccionario vacío).

##### Procesar el archivo de entrada línea por línea:
- Se abre el archivo de entrada en modo lectura con codificación UTF-8.
- Se itera sobre cada línea del archivo.
Para cada línea:
- Se intenta procesar la línea (dentro de un bloque try...except para manejar errores de formato):
- Se eliminan los espacios en blanco de la línea y se divide en una lista de cadenas, asumiendo que las conexiones están separadas por comas.
- Se convierte cada cadena a un entero usando map y int
- Se calcula el ID del usuario actual (idx) como total_users + 1.
- Se filtran las conexiones:
- Se eliminan las conexiones que no son positivas, que son mayores que max_id, o que son iguales al propio ID del usuario.
- Se convierte el resultado a un conjunto (para eliminar duplicados) y luego a una lista.
- Se trunca la lista de conexiones a max_connections_per_user conexiones.
- Si el usuario tiene conexiones filtradas, se agrega una entrada al diccionario user_dict con el ID del usuario como clave y la lista de conexiones como valor.
- Si ocurre un error al procesar la línea (por ejemplo, si la línea no contiene números válidos), se captura la excepción ValueError y se continúa con la siguiente línea (usando continue).

##### Guardar chunks de usuarios:
Dentro del bucle que procesa las líneas, se verifica si el número de usuarios procesados (total_users) es un múltiplo del tamaño del chunk (chunksize).
Si es un múltiplo de chunksize:
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

### Análisis Exploratorio de Datos (EDA)
Se lleva acabo la construcción del grafo, su visualización básica y datos de análisis extra.

#### Importar Librerías:
- sqlite3: Para interactuar con la base de datos SQLite.
- pickle: Para serializar y deserializar objetos de Python (usado para guardar y cargar los "chunks" de datos de usuarios).
- os: Para operaciones del sistema operativo, como trabajar con rutas de archivos y directorios.
- networkx: Para crear, manipular y visualizar grafos.
- matplotlib.pyplot: Para crear visualizaciones de grafos.

#### Construir_grafo_desde_chunks_con_disco:
- Propósito: Construye un grafo desde archivos de "chunk" que contienen datos de usuarios y los guarda en una base de datos SQLite.
Cómo funciona:
- Crea una conexión a una base de datos SQLite.
- Crea tablas para almacenar nodos (usuarios) y aristas (conexiones).
- Obtiene una lista de archivos "chunk".
- Itera a través de cada archivo "chunk":
- Carga el "chunk" usando pickle.load().
- Itera a través de los usuarios y sus conexiones en el "chunk":
Si el usuario tiene información de ubicación:
- Inserta el usuario en la tabla de nodos (si no existe).
- Itera a través de las conexiones del usuario:
- Si el amigo también tiene ubicación, inserta la conexión como una arista en la tabla de aristas.
- Confirma los cambios en la base de datos después de procesar cada "chunk".
- Cierra la conexión a la base de datos.

#### Dibujar_muestra_grafo_desde_db:
- Propósito: Dibuja una muestra del grafo desde la base de datos SQLite.
Cómo funciona:
- Establece una conexión a la base de datos SQLite.
- Obtiene una muestra de nodos (usuarios) de la tabla de nodos.
- Crea un grafo dirigido usando networkx.
- Añade nodos al grafo, utilizando la latitud y longitud como atributos de posición.
- Obtiene las aristas (conexiones) de la tabla de aristas que conectan los nodos de la muestra.
- Añade aristas al grafo.
- Dibuja el grafo usando networkx y matplotlib.
- Muestra el grafo dibujado.

#### Mostrar_grafo_desde_sqlite:
- Propósito: Muestra los primeros 100 nodos y las primeras 1000 aristas de la base de datos SQLite.
Cómo funciona:
- Se conecta a la base de datos SQLite.
- Ejecuta consultas para seleccionar los primeros 100 nodos y las primeras 1000 aristas.
- Imprime los resultados en un formato legible.
- Cierra la conexión a la base de datos.

#### Estadisticas_basicas:
- Propósito: Calcula y muestra estadísticas básicas del grafo almacenado en la base de datos SQLite.
Cómo funciona:
- Se conecta a la base de datos SQLite.
- Calcula el número de nodos y aristas usando consultas SQL.
- Calcula el grado promedio y la densidad del grafo.
- Imprime las estadísticas calculadas.
- Cierra la conexión a la base de datos.
