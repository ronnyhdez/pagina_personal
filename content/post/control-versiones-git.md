+++
title = "Introducción al Control de versiones con git"

date = 2016-04-20
lastmod = 2018-01-13
draft = false

tags = ["git", "control versiones"]

summary = "¿Has escuchado recientemente de git? ¿Sobre control de versiones? Pues bueno, este tutorial trata de hacer una introducción al control de versiones y el
uso de git para nuestro flujo de trabajo. Está pensado para invetigadores, 
quienes inician en ciencia de datos o para quienes deseen tener un mayor orden
en su trabajo cotidiano"

[header]
image = "headers/files.jpg"
+++

## ¿Qué resuelve git? ¿Porqué usar git?

Si les ha sucecido que luego de trabajar en un documento, tienen una carpeta
llena con nombres como: "version_final", "version_final_final", "version_final_corregida", "version_final_revisada" pues git les será útil para
tener un control sobre los cambios que se introducen en el documento. 

En este tutorial haremos ejemplos con scripts de código en R y como los cambios
o bien cambios experimentales que vayamos trabajando los podamos registrar, usar
guardar y documentar con mayor eficiencia.

## Esquema de git
Aqui pretendo aclarar rapidamente que vamos a hacer con git, tener el big picture antes de entrar en detalles. Vamos a tener un repositorio remoto o en inglés upstream que será nuestro repositorio en github/gitlab/bitbucket. De este repositorio tendremos uno local que crearemos al hacer el clon. Siempre vamos a trabajar en repositorio local (en nuestra computadora) y esos cambios los vamos a subir al remoto con un push. De igual manera cambios que existan en el repositorio remoto (porque alguien hizo una contribucion, trabajamos desde otra computadora ys ubimos los cambios) lo vamos a hacer con un pull.

Vamos a tener una **rama** principal llamada **master**. El consejo aca es tener codigo limpio y funcional. Todo lo que sea trabajo en desarrollo, experimentos, pruebas, tareas especificas vamos a hacerlo en ramas. Las ramas van a tener el nombre que nosotros le pongamos. LUego los cambios realizadoss en estas ramas, una vez que comprobamos que funcionan y que el codigo es aceptable lo podemos fusionar a nuestra rama master.

Cada vez que hagamos cambios vamos a hacer un commit de los cambios que marcaran un punto en la historia del proyecto al cual podremos retornar en caso de que hagamos un desastre y dejemos nuestro código sin funcionar.

Cuando queremos trabajar con el repositorio de alguien más lo podemmos hacer con un fork del repositorio, que nos copiará el repositorio bajo el usuario de otra persona hacia nuestro usuario. De este podremos hacer cambios pero el flujo de trabajo es diferente. Lo explicaremos en otra sección.

## Iniciar con git
En este segmento vamos a seguir los pasos para tener un repositorio que tenga su cuenta remota con github/gitlab/bitbucket y local a través de nuestra terminal.

#### 1. Crear repositorio en github/gitlab/bitbucket
Si tenemos cuenta en github/gitlab/bitbucket podemos crear un repositorio. Le llamamos repositorio al sitio donde vamos a guardar nuestros archivos. Un repositorio lo podemos visualizar como una carpeta que contendrá nuestro trabajo.

Cuando se crea un nuevo repositorio lo recomendable es iniciarlo con un arhivo que se llama **.gitignore** y con un **readme**. La funcionalidad del .gitignore es que en este colocaremos los formatos de los archivos que no queremos que se integren en nuestro sistema de control de versiones. Generalmente no deseamos que archivos como imagenes (.png .jpeg) o bien archivos de datos muy grandes (.txt .csv .feather) sean compartidos entre repositorios remotos, locales o personas con las que colaboremos. 

En el caso del readme es un archivo que debe de dar una idea  de qué tenemos en el repositorio. Es una guía para nosotros mismos u otros usuarios que vayan a hacer uso del repositorio. 

Al crear un repositorio vamos a encontrarnos con una opción que dirá "clone or download". Vamos a hacer click en clone y la dirección que allí sale se va a copiar (tal como hacer un Ctrl + c). Esto nos lo vamos a llevar a nuestra terminal.


#### 2. Clonar repositorio en nuestra computadora
Una vez que tenemos creado el repositorio y la dirección copiada, vamos a abrir nuestra terminal. Si es usuario de windows puede usar el powershell.
Lo primero que vamos a ver es una dirección y allí tendremos que **dirigirnos
a la carpeta donde deseamos colocar el repositorio**.

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

Cuano tenemos un repositorio la rama principal está nombrada como **master**. A partir de esta podemos hacer ramas con los nombres que nosotros queramos. La idea de las ramas es trabajar de manera ordenada, en donde en mi rama master siempre vayamos a tener código limpio y funcional y lo que sean nuevas tareas y mejoras o experimentos lo hagamos en ramas que se bifurcan a partir de la rama master. 

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
Como estamos trabajando con un repositorio remoto y uno local, vamos a querer sincronizar los cambios. Estos cambios pasarán al estar en la historia del proyecto como **commits**. Un commit es un punto en la historia del proyecto que muestra el trabajo realizado en ese momento. En el flujo del trabajo que uno tenga es recomendable hacer commits regularmente y subirlos de manera regular para asegurar no perder el trabajo.

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
El mensaje sirve para darnos a nosotros o a colaboradores una idea del cambio que se trabajó. 

**4.4 Subir cambios al repositorio remoto**
```
git push
```

**4.5 Bajar cambios del repositorio remoto**
Si estamos trabajando con colaboradores y han integrado cambios en el repositorio remoto que nosotros no tenemos en nuestro repositorio local, los podemos traer de la siguiente manera:

```
git pull
```



