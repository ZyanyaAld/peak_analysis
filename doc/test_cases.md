### Casos de Prueba para el Módulo 1: Extractor y Creador de Secuencias FASTA


### 1.  **Caso: Archivo del genoma no se encuentra.**
    
    -   **Entradas:**
        -   Ruta incorrecta o inexistente para el archivo FASTA del genoma.
        -   Archivo de picos válido.
        -   Directorio de salida.
    -   **Esperado:** `"Error: Genome file not found"`
    
    ```python
    mk_fasta_from_peaks.py -i peak_file.txt -g Ecoli.fna -o fasta_peaks/ 
    ```
    ```
    Error: "Ecoli.fna" genome file not found
    ```

### 2.  **Caso: Archivo de picos vacío.**
    
    -   **Entradas:**
        -   Archivo de picos vacío.
        -   Archivo FASTA del genoma.
        -   Directorio de salida.
    -   **Esperado:** `"Error: the peak file is empty."`

 ```python
    mk_fasta_from_peaks.py -i peak_file.txt -g Ecoli.fna -o fasta_peaks/ 
```
  
```
Error: the peak file is empty
```

### 3.  **Caso: Posiciones `Peak_start` y `Peak_end` fuera del rango del genoma.**
    
    -   **Entradas:**
        -   Archivo de picos con algunas posiciones `Peak_start` y `Peak_end` fuera del tamaño del genoma.
        -   Archivo FASTA del genoma válido.
        -   Directorio de salida.
    -   **Esperado:**
        -   El sistema debe imprimir un mensaje de advertencia: `"Warning: Some peaks are bigger than the genome". Check the log.out file`
        
        -   Generar un archivo de log indicando los picos fuera de rango. El archivo debe contener las líneas del archivo de picos que tienen problemas.

```python
    mk_fasta_from_peaks.py -i peak_file.txt -g Ecoli.fna -o fasta_peaks/ 
```

```bash
ls
```

```bash
log.out
fasta_peaks/
```

###  4. **Caso: Formato incorrecto del archivo de picos.**

   - **Entradas:**
     - Archivo de picos con formato incorrecto (por ejemplo, columnas mal ordenadas o faltantes).
     - Archivo FASTA del genoma válido.
     - Directorio de salida.

   - **Esperado:**
     - El sistema debe mostrar el mensaje:  
       `"Error: Invalid peak file format. Check the column order and contents."`
     - No debe generar archivos FASTA ni un `log.out`.

   ```python
   mk_fasta_from_peaks.py -i malformed_peaks.txt -g Ecoli.fna -o fasta_peaks/
   ```

   ```bash
   Error: Invalid peak file format. Check the column order and contents.
   ```

### 5. **Caso: `TF_name` duplicados en el archivo de picos.**

   - **Entradas:**
     - Archivo de picos con múltiples entradas para el mismo `TF_name`.
     - Archivo FASTA del genoma válido.
     - Directorio de salida.

   - **Esperado:**
     - Las secuencias deben agruparse correctamente bajo el mismo `TF_name`.
     - El archivo FASTA generado debe contener todas las secuencias correspondientes.

   ```python
   mk_fasta_from_peaks.py -i duplicate_peaks.txt -g Ecoli.fna -o fasta_peaks/
   ```

   ```bash
   ls fasta_peaks/
   TF1.fa TF2.fa
   ```



###  6. **Caso: Archivo FASTA del genoma vacío o con formato incorrecto.**

   - **Entradas:**
     - Archivo FASTA del genoma vacío o con un formato incorrecto (falta del símbolo `>` en los encabezados).
     - Archivo de picos válido.
     - Directorio de salida.

   - **Esperado:**
     - El sistema debe mostrar el mensaje:  
       `"Error: Invalid or empty genome FASTA file."`
     - No debe generar archivos FASTA.

   ```python
   mk_fasta_from_peaks.py -i peak_file.txt -g empty_genome.fna -o fasta_peaks/
   ```

   ```bash
   Error: Invalid or empty genome FASTA file.
   ```


### 7. **Caso: Sin coincidencias entre picos y el genoma.**

   - **Entradas:**
     - Archivo de picos con coordenadas que no coinciden con ninguna región del genoma.
     - Archivo FASTA del genoma válido.
     - Directorio de salida.

   - **Esperado:**
     - El sistema debe mostrar el mensaje:  
       `"Warning: No matching sequences were found."`
     - No se debe crear ningún archivo FASTA, pero sí un `log.out` con el detalle.

   ```python
   mk_fasta_from_peaks.py -i unmatched_peaks.txt -g Ecoli.fna -o fasta_peaks/
   ```

   ```bash
   Warning: No matching sequences were found.
   ls fasta_peaks/
   log.out
   ```
