# Desarrollo:

## 1- Instalar Git
Los pasos y referencias asumen el uso del sistema operativo Windows, en caso otros SO seguir recomendaciones específicas.

  - Bajar e instalar el cliente git. Por ejemplo, https://git-for-windows.github.io/
  - Bajar e instalar un cliente visual.
 Por ejemplo, TortoiseGit para Windows o SourceTree para Windows/MAC:
    - https://tortoisegit.org/
    - https://www.sourcetreeapp.com/
    - Lista completa: https://git-scm.com/downloads/guis/

![captura](imagenes/1.png)

## 2- Crear un repositorio local y agregar archivos
  - Crear un repositorio local en un nuevo directorio.
  - Agregar un archivo Readme.md, agregar algunas líneas con texto a dicho archivo.
  - Crear un commit y proveer un mensaje descriptivo.
  
![captura](imagenes/2.png)
![captura](imagenes/3.png)
![captura](imagenes/4.png)

## 3- Configuración del Editor Predeterminado
 - Instalar Notepad ++ para Windows o TextMate para Mac OS, colocarle un alias y configurarlo como editor predeterminado
   
   Yo utilizo Visual Studio Code como editor predeterminado, para configurarlo utilizo
   git config --global core.editor "code --wait"
  
![captura](imagenes/5.png)

## 4- Creación de Repos 01 -> Crearlo en GitHub, clonarlo localmente y subir cambios
  - Crear una cuenta en https://github.com
  - Crear un nuevo repositorio en dicha página con el Readme.md por defecto
  
![captura](imagenes/6.png)
![captura](imagenes/7.png)
  
  - Clonar el repo remoto en un nuevo directorio local
  
![captura](imagenes/8.png)
  
  - Editar archivo Readme.md agregando algunas lineas de texto
  - Editar (o crear si no existe) el archivo .gitignore agregando los archivos *.bak
  
![captura](imagenes/9.png)
  
  - Crear un commit y porveer un mensaje descriptivo
  
![captura](imagenes/10.png)
  
  - Intentar un push al repo remoto
  
![captura](imagenes/11.png)
  
  - En caso de ser necesario configurar las claves SSH requeridas y reintentar el push.

## 5- Creación de Repos 02-> Crearlo localmente y subirlo a GitHub
  - Crear un repo local
  - Agregar archivo Readme.md con algunas lineas de texto
  - Crear repo remoto en GitHub
  - Asociar repo local con remoto
  - Crear archivo .gitignore
  - Crear un commit y proveer un mensaje descriptivo
  - Subir cambios.
  
![captura](imagenes/2.png)
![captura](imagenes/3.png)
![captura](imagenes/4.png)

## 6- Ramas
  - Crear una nueva rama
  
![captura](imagenes/12.png)
  
  - Cambiarse a esa rama
  
![captura](imagenes/13.png)
  
  - Hacer un cambio en el archivo Readme.md y hacer commit
  
![captura](imagenes/14.png)
  
  - Revisar la diferencia entre ramas

![captura](imagenes/15.png)

## 7- Merges
  - Hacer un merge FF
  
![captura](imagenes/16.png)
  
  - Borrar la rama creada
  - Ver el log de commits
  
![captura](imagenes/17.png)
  
  - Repetir el ejercicio 6 para poder hacer un merge con No-FF
  
![captura](imagenes/18.png)
![captura](imagenes/19.png)

## 8- Resolución de Conflictos
  - Instalar alguna herramienta de comparación. Idealmente una 3-Way:
    
    Yo utilizo VSCode con la herramienta de comparacion predeterminada que trae incluida

  - Crear una nueva rama conflictBranch
  
![captura](imagenes/20.png)
  
  - Realizar una modificación en la linea 1 del Readme.md desde main y commitear
  
![captura](imagenes/21.png)
  
  - En la conflictBranch modificar la misma línea del Readme.md y commitear
  
![captura](imagenes/22.png)
  
  - Ver las diferencias con git difftool main conflictBranch
  
![captura](imagenes/23.png)
  
  - Cambiarse a la rama main e intentar mergear con la rama conflictBranch
  
![captura](imagenes/24.png)
  
  - Resolver el conflicto con git mergetool
  
![captura](imagenes/25.png)
  
  - Agregar .orig al .gitignore
  
![captura](imagenes/26.png)
  
  - Hacer commit y push
  
![captura](imagenes/27.png)

## 9- Familiarizarse con el concepto de Pull Request
  - Explicar que es un pull request.
    Un Pull Request (PR) es una petición para que los cambios realizados en una rama (branch) de tu repositorio sean revisados y, si se aprueban, fusionados (mergeados) en otra rama, generalmente la rama principal (main).

  - Crear un branch local y agregar cambios a dicho branch. 
  
![captura](imagenes/28.png)
  
  - Subir el cambio a dicho branch y crear un pull request.
  
![captura](imagenes/29.png)
  
  - Completar el proceso de revisión en github y mergear el PR al branch master.
  
![captura](imagenes/30.png)
![captura](imagenes/31.png)

## 10- Algunos ejercicios online
  - Entrar a la página https://learngitbranching.js.org/
  - Completar los ejercicios **Introduction Sequence**
  
![captura](imagenes/32.png)
  
  - Opcional - Completar el resto de los ejercicios para ser un experto en Git!!!