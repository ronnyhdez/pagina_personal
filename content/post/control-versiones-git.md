+++
title = "Introducción al Control de versiones con git"

date = 2016-04-20
lastmod = 2018-01-13
draft = false

tags = ["git", "control versiones"]

summary = "Introduccion al control de versiones con git"

[header]
image = "headers/files.jpg"
+++

## ¿Qué resuelve git? ¿Porqué usar git?

Si les ha sucecido que luego de trabajar en un documento, tienen una carpeta
llena con nombres como: "version_final", "version_final_final", "version_final_corregida", "version_final_revisada" pues git les será útil para
tener un control sobre los cambios que se introducen en el documento. 

En este tutorial haremos ejemplos con scripts de código en R y cómo los cambios que vayamos trabajando, los podemos registrar, usar, guardar y documentar con mayor eficiencia tanto para trabajar individualemente como grupalmente. 

![](/img/git.png)

## Esquema de git
Aqui pretendo aclarar rapidamente que vamos a hacer con git, tener el big picture antes de entrar en detalles. Vamos a tener un repositorio remoto o en inglés upstream que será nuestro repositorio en github/gitlab/bitbucket. De este repositorio tendremos uno local que crearemos al hacer el clon. Siempre vamos a trabajar en repositorio local (en nuestra computadora) y esos cambios los vamos a subir al remoto con un push. De igual manera cambios que existan en el repositorio remoto (porque alguien hizo una contribucion, trabajamos desde otra computadora ys ubimos los cambios) lo vamos a hacer con un pull.

Vamos a tener una **rama** principal llamada **master**. El consejo aca es tener código limpio y funcional. Todo lo que sea trabajo en desarrollo, experimentos, pruebas o tareas específicas, vamos a hacerlo en ramas. Las ramas van a tener el nombre que nosotros decidamos. Los cambios que se encuentran en estas ramas, una vez que se encuentran finalizados, revisados y funcionales los podremos integrar a nuestra rama master en un proceso conocido como **merge**

Cada vez que hagamos cambios en el código, vamos a hacer un **commit**. Esto lo podemos interpretar como marcar un punto en la historia del proyecto. Git nos mostrará información sobre cada uno de nuestros commits tal como la fecha, hora, usuario, archivos cambiados y las líneas de los archivos que se cambiaron. La idea de los commits es que siempre podamos retornar a un punto específico en la historia del proyecto.

En el caso de trabajar con el repositorio de alguien más, lo podemos realizar a través de un proceso que se conoce como **fork**, que no es más que una bifurcación del repositorio de esa persona. Al realizar un "fork" del repositorio de otra persona estamos creando una copia de dicho repositorio bajo nuestro usuario. Ahora bien, la manera de ofrecer los cambios que hemos trabajado a la persona dueña del repositorio tiene un proceso algo diferente que veremos en otro tutorial.

## Iniciar con git
En este segmento vamos a seguir los pasos para tener un repositorio que tenga su cuenta remota con github/gitlab/bitbucket y local a través de nuestra terminal.

#### 1. Crear repositorio en github/gitlab/bitbucket
Si tenemos cuenta en github/gitlab/bitbucket podemos crear un repositorio. Le llamamos repositorio al sitio donde vamos a guardar nuestros archivos. Un repositorio lo podemos visualizar como una carpeta que contendrá nuestro trabajo.

Cuando se crea un nuevo repositorio lo recomendable es iniciarlo con un arhivo que se llama **.gitignore** y con un **readme**. La funcionalidad del .gitignore es que este archivo (es como un archvio de texto) contiene especificaciones sobre los formatos de los archivos que no queremos que se integren en nuestro sistema de control de versiones. Generalmente no deseamos que archivos como imagenes (.png .jpeg) o bien archivos de datos muy grandes (.txt .csv .feather) sean compartidos entre repositorios remotos, locales o personas con las que colaboremos. Un ejemplo de un archivo .gitignore es el siguiente:
        
![](/img/ejemplo_gitignore.png)

Si no identifican algunos de los elementos de ahí no hay de qué preocuparse, mejor nos enfocámos en los tipos de archivos que nosotros necesitamos que sean tomados en cuenta por git, es decir, que no queremos que se suban a nuestro repositorio de github por ejemplo. Si es el caso que tenemos que hacer el knit de un Rmarkdown y necesitamos un archivo .csv para renderizarlo, pero solamente queremos el archivo Rmakrdown en el sistema de git, pues en nuestro archivo .gitignore escribimos .csv, guardamos el archivo y listo. 

En el caso del **readme** es un archivo que debe de dar una idea  de qué tenemos en el repositorio. Es una guía para nosotros mismos u otros usuarios que vayan a hacer uso del repositorio y nuestro código. En github los readme se ven así:

![](/img/readme.png)

Una vez que el repositorio haya sido creado, vamos a encontrarnos con una opción que dirá **"clone or download"**. Vamos a hacer click en clone y la dirección que allí sale la tenemos que copiar (ctrl + c). La imagen muestra lo que sucede al hacer clone en el botón verde que ofrece github:

![](/img/clone.png)

Ya con la información de la dirección del repositorio copiada, vamos a llevarla a nuestra terminal:

#### 2. Clonar repositorio en nuestra computadora
Una vez que tenemos creado el repositorio y la dirección copiada, vamos a abrir nuestra terminal. Si es usuario de windows puede usar el powershell.
Lo primero que vamos a ver es una dirección y allí tendremos que **dirigirnos a la carpeta donde deseamos colocar el repositorio**.

```
cd ~ #Esto me va a llevar al home
```

```
cd Desktop/ #Me lleva al escritorio
```

```
ls #Me da lista de los elementos que existen en la dirección que estoy
```

```
cd primeras_letras_nombre <TAB> #Con TAB autocompleta el nombre
```

 - Este procedimiento lo vamos realizando hasta llegar a la carpeta en la cual queremos clonar el repositorio.

El segundo paso es **clonar el repositorio**:

```
git clone <dirección del repositorio que copiamos>
```

Por último nos dirigimos a la carpeta del repositorio

```
cd <nombre_repositorio>
```
¡Listo! Ya tenemos el repositorio remoto tal cual en nuestra computadora local. A partir de aquí podemos trabajar en nuestros archivos.

#### 3. Crear una rama en el repositorio
¿Qué pasa si queremos hacer una variación en el código sin miedo a dañar lo que ya tenemos? Pues bien, git nos permite hacer ramas que son una bifurcación del trabajo que llevamos realizado hasta ese momento y que si luego queremos, podemos volver a integrar a la rama principal.

Cuano tenemos un repositorio la rama principal está nombrada como **master**. A partir de esta rama master podemos hacer ramas con los nombres que nosotros queramos. La idea de las ramas es trabajar de manera ordenada, en donde en mi rama master siempre debemos de tener código limpio y funcional y lo que sean nuevas tareas, mejoras o experimentos lo hagamos en ramas que se bifurcan a partir de la rama master. 

Cuando el trabajo realizado en la rama sea funcional y limpio, lo podemos integrar a la rama master. Caso contrario podemos olvidarnos de la rama y volver a nuestra rama master.

**Crear rama**
```
git checkout -b <NOMBRE_RAMA> #Nos crea y dirige a la nueva rama
```

**Verificar rama en la que estamos**
```
git status
```

**cambiar entre ramas**
Para cambiar entre ramas que ya existen NO hay que usar "-b"
```
git checkout <NOMBRE_RAMA>
```

#### 4. Subir/bajar cambios
Como estamos trabajando con un repositorio remoto y uno local, vamos a querer sincronizar los cambios. Estos cambios pasarán a estar en la historia del proyecto como **commits**. Un commit es un punto en la historia del proyecto que muestra el trabajo realizado en ese momento. En el flujo del trabajo que uno tenga es recomendable hacer commits regularmente y hacer el push de manera regular para asegurarnos de no perder el trabajo.

**4.1 Revisar estado de los cambios **
Cuando tengamos cambios en nuestros archivos, podemos revisar cuáles han cambiado y si los tenemos incluidos o no en nuestro registro de cambios
```
git status
```

**4.2 Agregar cambios**
Los archivos que queramos agregar a la historia del proyecto lo podemos hacer de dos maneras, una donde indicamos explícitamente el archivo específico:
```
git add <NOMBRE_ARCHIVO>
```

O de tal manera en que agreguemos todos los archivos con cambios de una vez
```
git add .
```

**4.3 Someter cambios a la historia de git**
```
git commit -m "MENSAJE_CORTO"
```
El mensaje sirve para darnos a nosotros mismos o a colaboradores, una idea del cambio que se trabajó. 

**4.4 Subir cambios al repositorio remoto**
```
git push
```

**4.5 Bajar cambios del repositorio remoto**
Si estamos trabajando con colaboradores y han integrado cambios en el repositorio remoto que nosotros no tenemos en nuestro repositorio local, los podemos traer de la siguiente manera:

```
git pull
```

### Referencias

https://git-scm.com/book/en/v2
https://git-scm.com/book/es/v1/Ramificaciones-en-Git-Procedimientos-b%C3%A1sicos-para-ramificar-y-fusionar

