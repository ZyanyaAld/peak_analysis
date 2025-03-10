# Proyecto de Automatizaci�n para la Identificaci�n de Sitios de Uni�n de Factores de Transcripci�n en E. coli en experimentos de ChIP-Seq

Fecha: [10/03/2025]

Participantes: 

*Zyanya Valentina Velazquez Aldrete*
Correo: [zyanyava@lcg.unam.mx](mailto:zyanyava@lcg.unam.mx)

�Claro, Zyanya! He corregido el texto manteniendo el formato Markdown. Aqu� est�:

## Descripci�n del Problema
<!-- Puedes empezar con una introducci�n, luego la justificaci�n y plantear el problema. -->

El proyecto busca automatizar la extracci�n y el an�lisis de secuencias gen�micas donde los factores de transcripci�n se unen en _Escherichia coli_. Se cuenta con un archivo que contiene informaci�n sobre los picos de uni�n, y con otro archivo que posee la secuencia completa del genoma. El objetivo es generar archivos FASTA espec�ficos para cada factor de transcripci�n (TF), agrupando las secuencias de los picos de uni�n correspondientes. Posteriormente, estas secuencias ser�n analizadas mediante el software `meme` para identificar motivos. Para eso, se tiene que generar un script shell con todas las instrucciones `meme` usando las secuencias FASTA de los picos de cada TF.

## Especificaci�n de Requisitos

### Requisitos Funcionales

#### A. Extracci�n de Secuencias FASTA
    
1.  **Entrada de Datos:**
    
    -   El m�dulo debe aceptar como argumentos de l�nea de comandos los siguientes archivos:
        -   Archivo de picos que contiene la informaci�n de las regiones de uni�n de cada factor de transcripci�n (ver secci�n "Archivo de Picos" al final de la secci�n de requisitos).
        -   Archivo de la secuencia del genoma de _E. coli_ en formato FASTA.
    -   A�adir un argumento para especificar el directorio de salida donde se almacenar�n los archivos generados.
  
2.  **Extracci�n y Procesamiento de Secuencias:**
    
    -   Leer el archivo de picos para obtener las posiciones de inicio y fin de los picos asociados a cada `TF_name`.
    -   Extraer las secuencias desde el archivo FASTA del genoma utilizando las coordenadas `Peak_start` y `Peak_end`, asegur�ndose de considerar solamente la cadena forward y la cadena reverse (esto puede evitar que perdamos informaci�n de la cadena reverse).
   
3.  **Generaci�n de Archivos FASTA:**
    
    -   Crear archivos FASTA individuales para cada `TF_name`. Los nombres de los archivos deben coincidir con el `TF_name` y usar la extensi�n `.fa`.
    -   Almacenar estos archivos en el directorio de salida especificado.

#### B. Automatizaci�n del An�lisis de Motivos

1.  **Entrada de Directorio:**
    - Archivos con las secuencias de DNA de los picos de cada TF.
    
2.  **Generaci�n de Script de Automatizaci�n:**
    
    -   Iterar sobre cada archivo FASTA en el directorio proporcionado.
    -   Para cada archivo, debe generar una l�nea de comando para el software `meme`, ajustada para ejecutar el an�lisis de motivos con los par�metros predefinidos.
    
3.  **Salida del Script:**
    
    -   El m�dulo debe generar un script de shell que contiene todas las l�neas de comandos necesarias para ejecutar `meme` en cada archivo FASTA.
    -   Este script debe grabarse en el directorio de trabajo actual con un nombre predefinido, como `run_meme.sh`.

### Requisitos No Funcionales

-   **Portabilidad y Usabilidad:**
    
    -   Compatible con sistemas Unix/Linux.
    -   El sistema debe ser ejecutable desde la l�nea de comandos.
    -   Todos los datos de entrada a los programas deben pasarse via argumentos.
    -   Si se implementa c�digo debe usarse Python o scripts shell.
    
-   **Calidad y Mantenimiento:**
    
    -   Utilizaci�n de Git para el seguimiento y revisi�n del c�digo.
    -   Documentaci�n clara y comentarios efectivos deben acompa�ar todo el proyecto.
    -   Deben realizarse pruebas necesarias para la validaci�n correcta del software.
   
   
   **Establecer Criterios de Calidad**

Criterios que determinar�n si una prueba es efectiva. 

-   **Cobertura de Pruebas:**  Porcentaje del c�digo cubierto por pruebas unitarias, de integraci�n y de sistema.
    
-   **Tasa de Detecci�n de Errores:**  Proporci�n de errores detectados en fases tempranas frente a fases posteriores.
    
-   **Tiempos de Respuesta:**  Tiempo promedio para solucionar los errores detectados.
    
-   **Satisfacci�n del Usuario:**  Medici�n de la satisfacci�n del usuario final con el producto.

### 1.  Responde:
    
    -   �Falt� alg�n requisito importante?
    
    Se agregaron Criterios de Calidad para hacer pruebas que verifiquen si una prueba es efectiva.
      
    -   �Alg�n requisito necesita ser modificado o aclarado?
    
	    - Se podria a�adir en la seccion de "Archivo de Picos" el formato de entrada esperado del archivo
	    - Se a�adio que paraa no perder la informacion se analise la cadena reverse, si las especificaciones de los archivos lo pide.


### Descripci�n de Datos de Entrada y Salida 

#### Formato del Archivo de Picos

Este archivo contiene informaci�n crucial sobre las regiones de uni�n de los 144 factores de transcripci�n (TFs) en _Escherichia coli_. Los datos est�n organizados en columnas que permiten identificar detalles espec�ficos sobre la uni�n de los TFs a lo largo del genoma. El formato del archivo y la descripci�n de cada columna se detallan a continuaci�n:

-   **Dataset_Ids:**
    
    -   _Descripci�n:_ Identificadores �nicos para cada conjunto de datos. Estas IDs indican diferentes experimentos o condiciones bajo las cuales se determinaron los sitios de uni�n para los TFs.
    -   _Ejemplo:_ "DS001","DS002", etc.
-   **TF_name:**
    
    -   _Descripci�n:_ El nombre del factor de transcripci�n que se une al genoma en la regi�n especificada.
    -   _Ejemplo:_ "AraC", "LacI", etc.
-   **Peak_start:**
    
    -   _Descripci�n:_ La posici�n inicial en el genoma donde comienza el pico de uni�n. Se refiere a la ubicaci�n del primer nucle�tido del pico.
    -   _Ejemplo:_ 345676, 123456, etc.
-   **Peak_end:**
    
    -   _Descripci�n:_ La posici�n final en el genoma donde termina el pico de uni�n. Se refiere a la ubicaci�n del �ltimo nucle�tido del pico.
    -   _Ejemplo:_ 345786, 123556, etc.
-   **Peak_center:**
    
    -   _Descripci�n:_ Posici�n central del pico de uni�n, calculada como el promedio o posici�n entre el `Peak_start` y `Peak_end`.
    -   _Ejemplo:_ 345731, 123501, etc.
-   **Peak_number:**
    
    -   _Descripci�n:_ N�mero secuencial utilizado para identificar picos dentro de un conjunto de datos. Esto es �til para referencias internas.
    -   _Ejemplo:_ 1, 2, 3, etc.
-   **Max_Fold_Enrichment:**
    
    -   _Descripci�n:_ Valor que representa el m�ximo enriquecimiento observado en el sitio de uni�n del pico.
    -   _Ejemplo:_ 15.4, 22.3, etc.
-   **Max_Norm_Fold_Enrichment:**
    
    -   _Descripci�n:_ Valor de m�ximo enriquecimiento normalizado, ajustado por un factor de control para comparaciones equitativas entre experimentos.
    -   _Ejemplo:_ 12.0, 20.1, etc.
-   **Proximal_genes:**
    
    -   _Descripci�n:_ Lista de genes cercanos al pico de uni�n, proporcionando contexto para el an�lisis funcional.
    -   _Ejemplo:_ "geneA, geneB", "geneX, geneY", etc.
-   **Center_position_type:**
    
    -   _Descripci�n:_ Denota la ubicaci�n gen�mica del pico central, como interg�nica, intr�nica, etc.
    -   _Ejemplo:_ "interg�nica", "intr�nica", etc.

## An�lisis y Dise�o

<!-- Incluir el algoritmo o pseudoc�digo. Tambi�n puedes usar casos de uso, u otros diagramas UML. Como sugerencia dar soluci�n requisito por requisito. Describir formatos de datos de entrada y salida. -->

#### M�dulo 1: Extractor y Creador de Secuencias FASTA

**Objetivo:** Extraer las secuencias gen�micas correspondientes a los picos de uni�n de los factores de transcripci�n y generar archivos FASTA individuales para cada `TF_name`.

**Flujo de Trabajo:**

1.  **Lectura de Entradas:**
    
    -   Cargar el archivo de picos y el archivo FASTA del genoma.
    -   Obtener el directorio de salida desde la l�nea de comandos.
2.  **Procesamiento de Datos:**
    
    -   Leer cada fila del archivo de picos.
    -   Extraer los campos `TF_name`, `Peak_start`, `Peak_end` para cada entrada.
    -   Para cada `TF_name`, usar las posiciones `Peak_start` y `Peak_end` para extraer la secuencia correspondiente del archivo FASTA del genoma.
    -   Validar que las coordenadas (Peak_start, Peak_end) esten dentro de los limites del FASTA.
    -   Permitir aplicar filtros opcionales (por ejemplo, longitud m�nima de secuencia).
    -   Se podr�a optimizar si se trata de archivos grandes.
    
3.  **Generaci�n de FASTA:**
    
    -   Agrupar las secuencias extra�das por `TF_name`.
    -   Crear un archivo FASTA por cada `TF_name` en el directorio de salida con la misma estructura `<TF_name>.fa`.

**Algoritmo**

```plaintext
1. Inicio
2. Leer archivo de picos
3. Para cada registro:
   a. Obtener TF_name, Peak_start, Peak_end
   b.Validar que Peak_start y Peak_end estan dentro de los l�mites del genoma.
   c. Extraer secuencia del genoma usando Peak_start y Peak_end
   d. Agrupar secuencias por TF_name (usando diccionarios)
4. Por cada TF_name:
   a. Crear archivo FASTA
   b. Escribir secuencias en archivo
5. Fin
```

#### M�dulo 2: Automatizador del An�lisis con `meme`

**Objetivo:** Generar un script de shell que contenga todos los comandos necesarios para ejecutar `meme` en los archivos FASTA generados para cada factor de transcripci�n.

**Flujo de Trabajo:**

1.  **Lectura de Entradas:**
    
    - Directorio con archivos FASTA.
    
2.  **Generaci�n de Comandos:**
    
    -   Iterar sobre cada archivo `.fa` en el directorio.
    -   Generar una l�nea de comando para ejecutar `meme` usando cada archivo FASTA.
    -   Incluir opciones necesarias (por ejemplo, `-oc <output_directory>`, `-mod oops`, etc.) y asegurar nombrar el directorio de salida para cada ejecuci�n de `meme`.
    -   Permitir personalizar los parametros de `meme`
    
3.  **Salida del Script:**
    
    -   Salida a pantalla


**Algoritmo:**

```plaintext
1. Inicio
2. Leer todos los archivos FASTA en el directorio
3. Para cada archivo FASTA:
   a. Formar comando: meme <archivo_fasta> -oc <nombre_directorio> ...
   b. Personalizar par�metros
   b. Imprimir comando
4. Redireccionar salida a un archivo script: run_meme.sh
5. Fin
```

### Diagrama de Caso de Uso (PlantUML) para Visualizar el Proceso

Usar un editor para visualizar el diagrama <https://sujoyu.github.io/plantuml-previewer/>

```plantuml
@startuml
actor "Usuario" as usuario

rectangle "Sistema de Extracci�n y Creaci�n de FASTA (Python)" {
    usecase "Leer archivo de picos y genoma FASTA" as UC1
    usecase "Extraer y agrupar secuencias por TF_name" as UC2
    usecase "Generar archivos FASTA" as UC3
}

rectangle "Script de Automatizaci�n de meme (Shell)" {
    usecase "Leer directorio de archivos FASTA" as UC4
    usecase "Generar script de comandos meme (con parametros personalizables)" as UC5
}

usuario --> UC1 : Ejecuta script Python
UC1 --> UC2
UC2 --> UC3 : Guarda archivos FASTA
usuario --> UC4 : Ejecuta script Shell
UC4 --> UC5 : Crea script de ejecuci�n de meme

@enduml
```


```mermaid
%% Diagrama de Casos de Uso en Mermaid
%% Representa la interacci�n del usuario con el sistema de extracci�n y creaci�n de FASTA

graph TD
  usuario["?? Usuario"] -->|Ejecuta script Python| UC1["?? Leer archivo de picos y genoma FASTA"]
  UC1 --> UC2["?? Extraer y agrupar secuencias por TF_name"]
  UC2 -->|Guarda archivos FASTA| UC3["?? Generar archivos FASTA"]
  
  usuario -->|Ejecuta script Shell| UC4["?? Leer directorio de archivos FASTA"]
  UC4 -->|Crea script de ejecuci�n de meme| UC5["?? Generar script de comandos meme(con parametros personalizables)"]
```


