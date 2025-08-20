# SAP-ABAP-GUI
Gestor de concesionarios y coches desarrollado en ABAP con interfaz GUI utilizando programación orientada a objetos, ALV, botones con funcionalidades de popup, envío de información por email, expotación de datos de ALV a .csv y creación de Logs.

# Programa ABAP ZPROG_FINAL_XX

Desarrollar un programa ABAP a través de la interfaz GUI que se llame **ZPROG_FINAL_XX**, donde `XX` es vuestro identificador, que permita gestionar los coches de un concesionario, implementando funcionalidades CRUD completas para concesionarios y coches, así como opciones de visualización y comunicación.

## 1. Modelo de Datos

Se crea lo siguiente en el Diccionario ABAP (SE11):

### Dominios
- `ZDOM_COD_CONC_XX` – Código de concesionario (CHAR5)  
- `ZDOM_NOMBRE_CONC_XX` – Nombre del concesionario (CHAR40)  
- `ZDOM_RESP_CONC_XX` – Responsable (Nombre y apellido) del concesionario (CHAR40)  
- `ZDOM_TELF_CONC_XX` – Teléfono del concesionario (CHAR10)  
- `ZDOM_URL_CONC_XX` – URL del concesionario (CHAR50)  
- `ZDOM_COD_COCHE_XX` – Código de coche (CHAR8)  
- `ZDOM_MARCA_XX` – Marca del coche (CHAR20)  
- `ZDOM_MODELO_XX` – Modelo del coche (CHAR30)  
- `ZDOM_COLOR_XX` – Color (CHAR15)  
- `ZDOM_EMAIL_XX` – Email (CHAR50)  

### Elementos de datos
Se crean los elementos de datos basados en los dominios anteriores, por ejemplo:  
- `ZED_COD_CONC_XX`, `ZED_NOMBRE_CONC_XX`, ...

### Tablas de BD
- **ZCONC_XX**
  - `COD_CONC` (clave primaria)  
  - `NOMBRE_CONC`  
  - `RESP_CONC`  
  - `TELEFONO_CONC`  
  - `URL_CONC`  

- **ZCOC_XX**
  - `COD_COCHE` (clave primaria)  
  - `COD_CONC`  
  - `MARCA`  
  - `MODELO`  
  - `COLOR`  


## 2. Programa Principal (SE38) ZPROG_FINAL_XX

### Pantalla de selección (SELECTION-SCREEN)
Contiene los siguientes parámetros de entrada para filtrar los datos que se muestran en el ALV:
- `so_cod_conc`  
- `so_marca`  
- `so_modelo`  
- `so_color`  

## 4. Funcionalidades del Programa

### A. CRUD de Concesionarios y Coches
El programa debe permitir, a través de los botones del ALV:
- Crear concesionario / coche (MF que llame a una screen **POPUP**)  
- Modificar concesionario / coche (MF que llame a una screen **POPUP**)  
- Eliminar concesionario / coche (MF que llame a una screen **POPUP**)  
    > Solo se podrá eliminar un concesionario si no tiene coches asociados.

### B. Visualización en ALV
- Mostrar en un **ALV** los coches filtrados por los parámetros de selección.  
- Los datos del ALV deben mostrar:
  - Código y nombre del concesionario  
  - Código del coche  
  - Marca, modelo y color  

> El resto de campos deben estar ocultos (RESPONSABLE_CONC, TELEFONO_CONC, URL_CONC).

### C. Envío de información del coche por email (popup)
- Al seleccionar un coche del ALV, un botón de la toolbar personalizada permitirá:
  - Abrir un **popup modal** con:
    - Campo para introducir un EMAIL  
    - Botón **ENVIAR**  
- Al pulsar **ENVIAR**, el programa simulará el envío de la información del coche seleccionado al email ingresado.   
- La simulación de envío se revisará en la transacción `/nSOST`.

### D. SMARTFORMS
- Crear un botón **Imprimir** que muestre el contenido del ALV en **SmartForms**.  
- El diseño y estilos del SmartForms se dejan a vuestro criterio (se recomienda sencillo).  
- Crear el **tipo tabla** y estructura donde aplique.  

### E. Exportación a CSV 
- Añadir un botón en la toolbar del ALV para exportar el contenido actual a un fichero `.CSV`. 
- Se puede usar `GUI_DOWNLOAD` para esta funcionalidad.  

#### F. Logs
Al final, crear un log que almacene todos los pasos (correctos o fallidos) del funcionamiento del programa.  
Ejemplos:
- *Se ha insertado un concesionario nuevo con X datos.*  
- *No se ha podido insertar un concesionario con X datos.*  
