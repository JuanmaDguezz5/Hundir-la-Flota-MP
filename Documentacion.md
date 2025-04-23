---
bibliography: ../Referencias.bib
biblio-style: "apalike"
link-citations: true


---
# <span style='color:blue'> **Hundir la Flota** </span> 
### Grado en Ingeniería Informática

**Curso 2024/2025**

**Autores:**
- Salmoun Vargas, Ibrahim  
- Duarte Guillén, Alejandro  
- Domínguez Panal, Juan Manuel  
- Sánchez Millán, Víctor  
***

[comment]:<> "Los tres asteriscos añaden una línea horizontal"

## Índice 
1. [Introducción](#introducción)

2. [Documentación de usuario](#usuario)
   - [Descripción funcional](#funcional)
   - [Tecnologías](#tecnología)
   - [Instalación](#instalación)
   - [Acceso al sistema](#acceso)
   - [Manual de referencia](#referencia)
   - [Guía del operador](#operador)
   
3. [Documentación del sistema](#sistema)
   - [Especificación del sistema](#requisitos)
   - [Módulos](#módulos)
   - [Plan de pruebas](#pruebas)  

***

<div id='introducción' />
## Introducción

## Introducción

En el presente trabajo se presenta una implementación modular del juego clásico “Hundir la Flota” usando el lenguaje C. El objetivo es aplicar los conceptos de programación modular, estructuras de datos dinámicas y gestión de memoria, practicados en la asignatura de Metodología de la Programación, para desarrollar un sistema completo y mantenible.

El trabajo aborda los siguientes objetivos específicos:

- Demostrar la capacidad de separar el código en módulos cohesivos (datos, configuración, tableros, lógica y presentación) facilitando su comprensión y extensión.
- Utilizar memoria dinámica para crear y liberar tableros de dimensiones variables y flotas definidas por el usuario.
- Ofrecer una interfaz en consola intuitiva que permita configurar partidas, colocar barcos manual o automáticamente, y realizar disparos con feedback inmediato.
- Desarrollar una inteligencia artificial básica que alterna disparos aleatorios con una estrategia de búsqueda y persecución tras el primer impacto.
- Implementar funciones de persistencia para guardar y recuperar el estado de la partida en archivos de texto.
- Realizar un plan de pruebas que incluya casos de prueba unitarios, de integración y de aceptación por parte de usuarios finales.

La estructura de este documento sigue un flujo descendente: primero se explica la visión del usuario (manual de uso, tecnologías y requisitos), luego la perspectiva del desarrollador (especificación de módulos y plan de pruebas), y finalmente la documentación interna generada para cada componente del código.




<div id='usuario' />
# Documentación de usuario
# Documentación de usuario
Esta sección está orientada a los usuarios del sistema, describiendo su funcionalidad, tecnología empleada, proceso de instalación y uso general.

## Descripción funcional
El programa “Hundir la Flota” simula en consola el juego de estrategia naval clásico, ofreciendo una experiencia completa de partida con las siguientes fases y características:

### Inicialización de la configuración
Al iniciar la aplicación, el sistema solicita al usuario:

- **Dimensión del tablero:** Un valor entero `n` que define un tablero cuadrado de tamaño `n × n`. Permite adaptar la complejidad del juego.
- **Tipos de barcos:** Carga desde `Barcos.txt` una lista de barcos disponibles, cada uno con nombre, identificador y tamaño (número de casillas que ocupa).
- **Flota por jugador:** Para cada tipo de barco, el usuario establece cuántas unidades desea en su flota; el total de barcos por jugador se calcula automáticamente.

### Colocación de la flota
Se ofrecen dos modos:

- **Manual:** El jugador introduce coordenadas `(fila, columna)` y orientación `(horizontal, vertical o diagonal)` para cada barco. El sistema valida que no existan colisiones o contactos inapropiados.
- **Automático:** Empleando un algoritmo de búsqueda aleatoria, el sistema ubica cada barco de manera válida, comprobando límites y separación mínima entre barcos.

### Mecánica de juego
Durante la partida:

1. Los jugadores alternan turnos para disparar a una posición enemiga especificada por coordenadas.
2. Para disparo manual, el usuario introduce la fila y columna; para disparo automático (IA), el sistema selecciona casillas según una estrategia de tres fases: aleatoria, búsqueda de dirección tras un impacto y persecución en línea hasta hundir el barco.
3. Tras cada disparo, se muestra un mensaje indicando el resultado: “Agua” (ningún barco), “Tocado” (parte de barco impactada) o “Hundido” (todas las partes de un barco han sido alcanzadas).
4. Los tableros se actualizan en memoria, mostrando en el tablero propio las marcas de disparos y en el del oponente el avance.

### Gestión de sesiones y persistencia

- **Guardar partida:** El estado completo (configuración, flotas, tableros y estadísticas) se escribe en `Juego.txt` para su posterior reanudación.
- **Cargar partida:** Se recupera una sesión previa, restaurando todos los datos y permitiendo continuar la partida donde se dejó.

### Finalización y resumen
Cuando una flota queda completamente hundida, el sistema identifica al ganador y:

- Muestra un resumen con estadísticas: disparos realizados por cada jugador, tiempo transcurrido (opcional) y estado final de ambos tableros.
- Ofrece la opción de reiniciar la partida con la misma configuración o volver al menú principal para modificar parámetros.

## Tecnología
El desarrollo de “Hundir la Flota” se ha apoyado en las siguientes tecnologías y herramientas:

### Lenguaje y compilación

- **C (ISO C99):** Lenguaje estructurado que permite control detallado de la memoria y el rendimiento.
- **GCC (GNU Compiler Collection):** Compilador utilizado en entornos Linux, macOS y Windows, con soporte para optimización y detección de errores en tiempo de compilación.

### Librerías y estándares

- `stdio.h` / `stdlib.h`: Entrada/salida de consola y manejo de memoria dinámica.
- `string.h`: Operaciones con cadenas de caracteres para identificar barcos y procesar entradas del usuario.
- `time.h`: Generación de números aleatorios para IA y colocación automática.

### Entorno de desarrollo

- **Editor de texto/IDE:** Visual Studio Code o cualquier editor compatible con C.
- **Control de versiones:** Git para seguimiento de cambios, ramificación de funcionalidades y colaboración.
- **Plataforma de integración continua (CI):** Opcional, se puede configurar GitHub Actions o GitLab CI para ejecutar compilaciones y pruebas automáticas.

### Tecnología

- **Lenguaje de programación:** C  
- **Compilador:** gcc (GNU Compiler Collection)  
- **Sistema operativo:** Windows  
- **Editor de código:** Visual Studio Code / CodeBlocks  
- **Página oficial de gcc:** [https://gcc.gnu.org/](https://gcc.gnu.org/)

## Manual de instalación
Para instalar el sistema:

1. Clonar el repositorio o copiar los archivos fuente en una carpeta local.
2. Abrir una terminal y navegar hasta la carpeta del proyecto.
3. Ejecutar: `gcc main.c -o tareas`
4. Ejecutar el programa con: `./tareas`

## Acceso al sistema
Para acceder al sistema:

1. Abrir una terminal
2. Ejecutar: `./tareas`

**Salir del sistema:** Presionar la opción correspondiente del menú principal.

**Problemas comunes:**

- Si aparece un error de compilación, verificar que gcc esté instalado.
- Si el programa no ejecuta, verificar permisos de ejecución con `chmod +x tareas`

## Manual de referencia
Este sistema ofrece:

- Gestión de tareas en lista.
- Interfaz en consola sencilla.
- Almacenamiento de tareas en memoria.

**Errores comunes:**

- Entrada inválida: el sistema solicita nueva entrada.
- Selección de opción no existente: muestra un mensaje de advertencia.

## Guía del operador
No se requiere un operador especializado. Sin embargo, en caso de mal funcionamiento:

- Reiniciar el sistema.
- Verificar entrada de usuario.
- Consultar los mensajes de error.
  



<div id='sistema' />
# Documentación del sistema
Documentación referida a los aspectos del análisis, diseño, implementación y prueba del _software_, así como la implantación del mismo. En general debe hacer referencia al sistema, ya que está orientada a los programadores que van a realizar el mantenimiento. Debe estar muy bien estructurada, desde lo más general a los más interno.   


<div id='requisitos' />
## Especificación del sistema

## Especificación del sistema

### Objetivo General
Desarrollar un programa interactivo para el juego *Hundir la Flota*, donde dos jugadores colocan barcos en un tablero y se turnan para intentar hundir los barcos del oponente mediante disparos. El programa debe permitir la configuración inicial, gestionar los turnos, comprobar los tiros y declarar un ganador.

### Requisitos Funcionales

- Permitir la configuración inicial del juego (tamaño del tablero, número de barcos, modo de juego).
- Permitir la colocación de barcos en el tablero.
- Gestionar los turnos de los jugadores.
- Comprobar si un disparo es acierto o fallo.
- Mostrar los tableros actualizados tras cada jugada.
- Detectar cuándo todos los barcos de un jugador han sido hundidos y finalizar la partida.



<div id='módulos' />
## Módulos

### 1. `config.c` / `config.h`

**Funcionalidad:**  
Este módulo se encarga de manejar la configuración inicial del juego. Puede incluir la lectura de parámetros desde el usuario, la consola o archivos, así como la inicialización de constantes o estructuras necesarias para el funcionamiento del juego.

**Interfaz:**

- Funciones para cargar la configuración inicial.
- Inicialización de constantes o estructuras globales.

---

### 2. `datos.c` / `datos.h`

**Funcionalidad:**  
Este módulo maneja los datos esenciales del juego, como la información de los jugadores, estadísticas y el estado actual de la partida. Puede incluir la definición de estructuras y funciones para manipular dichos datos.

**Interfaz:**

- Funciones para inicializar, leer o modificar los datos de los jugadores.
- Estructuras de datos como `Jugador`, `Flota`, etc.

---

### 3. `juego.c` / `juego.h`

**Funcionalidad:**  
Este módulo contiene la lógica principal del juego. Controla los turnos, ataques, comprobación de impactos, y verificación de condiciones de victoria.

**Interfaz:**

- Función principal para ejecutar el juego (por ejemplo, `jugar()`).
- Funciones auxiliares para comprobar impactos, gestionar turnos, determinar el ganador, etc.

---

### 4. `principal.c`

**Funcionalidad:**  
Es el módulo principal que contiene la función `main()`. Se encarga de iniciar el juego y coordinar la ejecución de los demás módulos.

**Interfaz:**

- No expone funciones hacia otros módulos; se limita a organizar la ejecución del programa.

---

### 5. `tableros.c` / `tableros.h`

**Funcionalidad:**  
Este módulo gestiona la representación y actualización visual de los tableros de juego. Incluye funciones para imprimir, modificar y visualizar los tableros del jugador y del enemigo.

**Interfaz:**

- Funciones para imprimir los tableros.
- Funciones para actualizar el estado visual tras cada jugada.
  

# Plan de prueba

Este plan describe el conjunto de pruebas aplicadas al sistema **Hundirse**, un juego de batalla naval por consola. Se detallan pruebas individuales por módulo (unidad), pruebas de integración y pruebas de aceptación para evaluar la funcionalidad desde la perspectiva del usuario final.

---

## Prueba de los módulos

### Módulo `juego.c`

**Funciones probadas:**
- `int disparoManual(...)`

**Caja blanca**  
Se construyó el grafo de control de flujo para la función `disparoManual`. Se identificaron 3 rutas independientes, y se probaron los siguientes casos:

- Fila y columna válidas, casilla VACÍA (flujo directo).
- Fila o columna fuera de rango (`fila = -1, col = 10`), repite lectura.
- Casilla no VACÍA (`estado != VACIO`), repite lectura.

**Caja negra**  
Se diseñaron casos con entradas en límites, fuera de rango y casillas previamente disparadas:

- Fila/col: `0`, `DIM-1`, `-1`, `DIM`.
- Casilla previamente disparada: `propio->casillas[2][2].estado = 1`.
- Verificación de salidas: mensajes `Agua`, `Tocado`, `Hundido`.

---

### Módulo `tableros.c`

**Funciones probadas:**
- `void inicializarTablero(TTablero *t);`
- `void mostrarTablero(const TTablero *t);`

**Caja blanca**  
Se verificó que `inicializarTablero` recorra completamente la matriz y asigne el estado `VACIO`. Se inspeccionó visualmente el tablero impreso por `mostrarTablero()` para confirmar consistencia de los símbolos en pantalla.

**Caja negra**  
- Tablero vacío: todos los valores = VACIO, sin barcos visibles.
- Tablero con estados modificados: se muestran correctamente los símbolos esperados.

---

### Módulo `datos.c`

**Funciones probadas:**
- `int cargarBarcos(FILE *f, TBarco barcos[]);`
- `int guardarPartida(...)`

**Caja blanca**  
Prueba con archivo `Barcos.txt`. Se cubrieron caminos de control incluyendo:

- Archivo no encontrado.
- Error de formato (línea sin número esperado).
- Lectura correcta de 5 barcos.

**Caja negra**  
- Archivo vacío: retorno negativo.
- Archivo con datos válidos: posiciones cargadas correctamente.
- Archivo con líneas mal formateadas: se detectan errores.

---

### Módulo `config.c`

**Funciones probadas:**
- `int leerConfiguracion(FILE *f, int *dim);`

**Caja blanca**  
Se recorrieron condiciones del archivo de configuración:

- Lectura correcta de dimensión (valor positivo).
- Valor fuera de rango o inválido: detección de error.

**Caja negra**  
- Archivo con valor correcto: dimensión aceptada.
- Archivo con texto en lugar de número: error controlado.
- Valor nulo o negativo: rechazo.

---

## Pruebas individuales (alumno)

**Alumno:** _[Juan Manuel Domínguez Panal]_

**Función analizada:** `IntroducirDatos(...)`  
**Tipo de prueba:** Ruta básica (caja blanca) y caja negra.

**Pruebas realizadas:**

- **Caja blanca – rutas independientes:**
  ## Pruebas de Caja Blanca – `IntroducirDatos(...)`
  
```c
  void introducirDatos(TConfiguracion *config, TJugador jugadores[], int num_jugadores)
{
    int j;

    inicializarConfiguracion(config);

    printf("\n=== CONFIGURACIÓN INICIAL ===\n");

    printf("Introduce la dimensión del tablero (n x n): ");
    scanf("%d", &config->dimension_tablero);

    if (!leerTiposBarcosDesdeFichero(config, "Barcos.txt")) {
        printf("Error al cargar tipos de barcos. No se puede continuar.\n");
        return;
    }
}
````

### Diagrama de Flujo Lógico
  
flowchart TD
    A[Inicio] --> B[Inicializar Config]
    B --> C[Solicitar dimensión]
    C --> D[leerTiposBarcosDesdeFichero]
    D -->|falso| E[Mensaje de error]
    E --> F[Fin]
    D -->|verdadero| F


### Complejidad Ciclomática

- NN = 6 nodos 
- NA= 7 aristas: 1 → 2, 2 → 3, 3 → 4, 4 → 5 (si es falso), 4 → 6 (si es verdadero), 5 → fin, 6 → fin
- V(G) = NA - NN + 2 = 3
Complejidad ciclomática = 3

### Determinar el conjunto básico de rutas linealmente independientes
Ruta 1: Ejecución exitosa

Se inicializa configuración

Usuario introduce dimensión

Archivo "Barcos.txt" se carga correctamente

Ruta 2: Error al cargar archivo

Se inicializa configuración

Usuario introduce dimensión

Falla la carga de "Barcos.txt"

Se muestra mensaje de error y se termina la función

### Tabla de Casos de Prueba 

| Ruta | Descripción                  | Entrada esperada                         | Resultado                        |
|------|------------------------------|------------------------------------------|----------------------------------|
| 1    | Fichero cargado correctamente | Tamaño válido (ej. 10), archivo válido   | Función finaliza sin error       |
| 2    | Fichero ausente o ilegible   | Tamaño válido, archivo no existe         | Se imprime error y termina       |


- **Caja negra – entradas/salidas:**
  Función probada: introducirDatos
  
Criterio: Verificar entradas válidas e inválidas sin considerar el código fuente.
### Tabla de Casos de Prueba 

| Prueba | Descripción                             | Entrada simulada                       | Resultado esperado                          |
|--------|-----------------------------------------|----------------------------------------|---------------------------------------------|
| 1      | Dimensión válida, archivo correcto      | 10, archivo "Barcos.txt" válido        | Finaliza sin error                          |
| 2      | Dimensión 0                             | 0, archivo válido                      | Acepta pero puede provocar errores          |
| 3      | Entrada no numérica                     | abc, archivo válido                    | scanf falla o se queda en bucle             |
| 4      | Archivo no existente                    | 10, archivo no existe                  | Muestra error y finaliza                    |
| 5      | Archivo vacío o corrupto                | 10, archivo sin datos válidos          | Error al cargar y finaliza                  |
| 6      | Dimensión negativa                      | -5, archivo válido                     | Aceptado o malformado, posible fallo        |


---

## Prueba de integración

Se realizaron pruebas para verificar la correcta interacción entre los distintos módulos del sistema. Las pruebas incluyeron la ejecución de funciones que dependen de la colaboración entre componentes, simulando el flujo completo del juego desde la carga de datos hasta el disparo.

### Módulos integrados

- `datos.c` con `config.c`: lectura de parámetros de configuración y de barcos desde archivos.
- `tableros.c` con `juego.c`: manejo del estado del tablero en función de los disparos.
- `main.c`: punto de entrada que coordina el flujo general.

**Caja blanca**  
Se inspeccionaron las llamadas cruzadas entre módulos:

- Verificación de que `leerConfiguracion()` devuelve correctamente la dimensión del tablero y es usada por `inicializarTablero()`.
- Validación de que `disparoManual()` invoca `actualizarDisparo()` con las coordenadas ingresadas y que este modifica correctamente el estado de `TTablero`.
- Inspección del flujo entre lectura de barcos (`cargarBarcos()`) y su ubicación en el tablero al iniciar el juego.

**Caja negra**  
Pruebas ejecutadas desde `main.c` como si fuera un usuario real:

- Configuración correcta → Carga de barcos → Inicialización de tableros → Disparos manuales → Resultados correctos impresos en consola.
- Casos de error:
  - Archivo de configuración ausente o corrupto.
  - Archivo de barcos con errores de sintaxis.
  - Flujo con disparos fuera de rango o a casillas ya usadas.

---

## Plan de pruebas de aceptación

Estas pruebas están orientadas a validar el sistema desde la perspectiva del usuario final. Se elaboraron en base al criterio de que el jugador debe poder jugar una partida completa sin errores visibles, con una experiencia fluida y comprensible.

### Escenarios de aceptación definidos

1. El usuario ejecuta el programa sin argumentos. Se carga la configuración por defecto y el sistema solicita la entrada.
2. El usuario realiza disparos válidos, observando resultados en consola (Agua, Tocado, Hundido).
3. El sistema no se cae ante entradas inválidas (e.g., letras en lugar de números, coordenadas fuera de rango).
4. El usuario puede continuar jugando hasta hundir todos los barcos.
5. Al finalizar, el sistema muestra un mensaje de victoria y termina la ejecución correctamente.

### Criterios de aceptación

- No deben producirse errores de segmentación ni bloqueos inesperados.
- El sistema debe interpretar correctamente los archivos de configuración y barcos.
- Las reglas del juego deben respetarse (no repetir disparos, solo se hunde un barco si todas sus partes fueron alcanzadas).
- La interacción debe mantenerse en todo momento clara y fluida desde la consola.



<div id='referencias' />
# Referencias {-}

---
nocite: |
  @*
...
