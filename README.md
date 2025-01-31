# Introducción al sistema operativo Linux 3

## Reglas de Sintaxis

En Linux, la línea de comandos (o terminal) es una herramienta poderosa que permite interactuar directamente con el sistema operativo. Para utilizar eficientemente la terminal, es fundamental entender las reglas de sintaxis que rigen cómo se escriben y ejecutan los comandos. A continuación, se detallan las reglas básicas de sintaxis en Linux.

### **Regla 1: Capitalización (Sensible a Mayúsculas y Minúsculas)**

En Linux, la distinción entre mayúsculas y minúsculas es **crucial**. Esto se aplica tanto a los nombres de los comandos como a los archivos, directorios y parámetros.

- **Comandos**: Los nombres de los comandos siempre se escriben en minúsculas. Por ejemplo, el comando `ls` (para listar archivos) no funcionará si se escribe como `LS` o `Ls`.
  
  Ejemplo:
  ```bash
  ls   # Correcto
  LS   # Incorrecto
  ```

- **Archivos y directorios**: Si tienes un archivo llamado `Documento.txt`, no podrás acceder a él escribiendo `documento.txt` o `DOCUMENTO.TXT`. Linux los tratará como archivos diferentes.

  Ejemplo:
  ```bash
  cat Documento.txt   # Correcto
  cat documento.txt   # Error (si el archivo no existe en minúsculas)
  ```

### **Regla 2: Parámetros**

Los parámetros (también llamados argumentos) son información adicional que se pasa a un comando para modificar su comportamiento. Estos parámetros deben estar separados por espacios.

- **Estructura básica**:
  ```bash
  comando [parámetro1] [parámetro2] ...
  ```

- **Ejemplo**:
  ```bash
  cp archivo.txt copia_archivo.txt
  ```
  En este caso, `cp` es el comando, `archivo.txt` es el primer parámetro (el archivo original) y `copia_archivo.txt` es el segundo parámetro (el nombre de la copia).

- **Importante**: El intérprete de comandos (shell) siempre interpreta la primera palabra como el nombre del comando y las siguientes como parámetros.

### **Regla 3: Opciones**

Las opciones (también llamadas flags) son un tipo especial de parámetro que modifica el comportamiento de un comando. Estas opciones suelen comenzar con un guion (`-`) o dos guiones (`--`), dependiendo de su formato.

1. **Opciones de una sola letra**:
   - Se escriben con un solo guion (`-`) seguido de una letra.
   - Ejemplo:
     ```bash
     ls -a -l
     ```
     Aquí, `-a` muestra todos los archivos (incluidos los ocultos) y `-l` muestra los detalles en formato de lista.

2. **Opciones de varias letras o palabras**:
   - Se escriben con dos guiones (`--`) seguidos de una palabra o frase.
   - Ejemplo:
     ```bash
     ls --help
     ```
     Esto muestra la ayuda del comando `ls`.

3. **Contraer opciones de una sola letra**:
   - Si un comando tiene varias opciones de una sola letra, estas se pueden combinar después de un solo guion.
   - Ejemplo:
     ```bash
     ls -alR
     ```
     Esto es equivalente a `ls -a -l -R`.

4. **Opciones con parámetros**:
   - Algunas opciones requieren un valor adicional (parámetro). En este caso, el parámetro debe colocarse inmediatamente después de la opción.
   - Ejemplo:
     ```bash
     tar -cvf archivo.tar directorio/
     ```
     Aquí, `-f` es la opción que indica el nombre del archivo, y `archivo.tar` es el parámetro que se le pasa.

---

### **Resumen de Reglas de Sintaxis**

| Regla                  | Descripción                                                                 | Ejemplo                     |
|------------------------|-----------------------------------------------------------------------------|-----------------------------|
| **Capitalización**      | Linux distingue entre mayúsculas y minúsculas.                              | `ls` ≠ `LS`                 |
| **Parámetros**          | Separados por espacios. La primera palabra es el comando.                   | `cp archivo.txt copia.txt`  |
| **Opciones**            | Usan `-` para una letra o `--` para varias letras/palabras.                 | `ls -a`, `ls --help`        |
| **Contraer opciones**   | Varias opciones de una letra pueden combinarse.                             | `ls -alR`                   |
| **Opciones con parámetros** | El parámetro se coloca después de la opción.                          | `tar -cvf archivo.tar dir/` |

## Sistema de Archivos en Linux**

### **1. Estructura de Directorios en Linux**

En Linux, el sistema de archivos está organizado en una estructura jerárquica en forma de árbol, donde el directorio principal es el **directorio raíz**, representado por una barra `/`. Todos los demás directorios y archivos están bajo este directorio raíz.

#### **Directorios Principales**

| Directorio | Descripción |
|------------|-------------|
| **/**       | Directorio raíz. |
| **/bin**    | Contiene comandos ejecutables esenciales para todos los usuarios. |
| **/boot**   | Archivos necesarios para el arranque del sistema. |
| **/dev**    | Archivos especiales asociados a dispositivos de hardware. |
| **/etc**    | Archivos de configuración del sistema. |
| **/home**   | Directorios personales de los usuarios. |
| **/lib**    | Bibliotecas compartidas necesarias para los programas en `/bin` y `/sbin`. |
| **/media**  | Puntos de montaje para dispositivos extraíbles (USB, CD-ROM, etc.). |
| **/mnt**    | Puntos de montaje temporales para sistemas de archivos. |
| **/opt**    | Software adicional o de terceros. |
| **/root**   | Directorio personal del superusuario (root). |
| **/sbin**   | Comandos esenciales para el administrador del sistema. |
| **/tmp**    | Archivos temporales. |
| **/usr**    | Utilidades y aplicaciones de usuario. |
| **/var**    | Archivos variables, como logs y bases de datos. |

---

### **2. Rutas Absolutas y Relativas**

En Linux, las rutas (o paths) son la forma en que se accede a los archivos y directorios. Existen dos tipos de rutas:

#### **Ruta Absoluta**

- Comienza desde el directorio raíz `/`.
- Especifica la ruta completa desde la raíz hasta el archivo o directorio.
- Ejemplo: `/home/usuario/Documentos/archivo.txt`

#### **Ruta Relativa**

- Depende del directorio actual en el que se encuentra el usuario.
- Utiliza `.` (directorio actual) y `..` (directorio padre) para navegar.
- Ejemplo: Si estás en `/home/usuario/`, la ruta relativa a `Documentos/archivo.txt` sería `./Documentos/archivo.txt`.

---

### **3. Tipos de Archivos y Códigos de Colores**

En Linux, todo es tratado como un archivo. Existen varios tipos de archivos, y cada uno tiene un código de color para facilitar su identificación.

#### **Tipos de Archivos**

1. **Archivos Ordinarios**: Contienen datos (texto, imágenes, etc.).
2. **Directorios**: Contienen referencias a otros archivos o directorios.
3. **Enlaces Simbólicos (Soft Links)**: Apuntan a otro archivo o directorio.
4. **Enlaces Físicos (Hard Links)**: Son una copia directa de un archivo, compartiendo el mismo inodo.
5. **Archivos Especiales**: Representan dispositivos físicos (discos, impresoras, etc.).

#### **Códigos de Colores**

| Color           | Tipo de Archivo               |
|-----------------|-------------------------------|
| **Blanco**       | Archivo normal.               |
| **Azul**         | Directorio.                   |
| **Verde brillante** | Archivo ejecutable.           |
| **Rojo brillante**  | Archivo comprimido.           |
| **Magenta**      | Archivo de imagen.            |
| **Cyan**         | Archivo de audio.             |
| **Azul cielo**   | Enlace simbólico.             |

---

### **4. Comandos Básicos para la Gestión de Archivos y Directorios**

#### **Comandos Esenciales**

| Comando | Descripción | Ejemplo |
|---------|-------------|---------|
| **`pwd`** | Muestra la ruta del directorio actual. | `pwd` |
| **`ls`**  | Lista los archivos y directorios. | `ls -l` (lista detallada) |
| **`cd`**  | Cambia de directorio. | `cd /home/usuario` |
| **`mkdir`** | Crea un nuevo directorio. | `mkdir nuevo_directorio` |
| **`touch`** | Crea un archivo vacío. | `touch archivo.txt` |
| **`cp`**   | Copia archivos o directorios. | `cp archivo.txt /backup/` |
| **`mv`**   | Mueve o renombra archivos o directorios. | `mv archivo.txt nuevo_nombre.txt` |
| **`rm`**   | Elimina archivos o directorios. | `rm archivo.txt` |
| **`ln`**   | Crea enlaces (simbólicos o físicos). | `ln -s archivo.txt enlace.txt` |
