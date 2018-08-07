## Para inicializar un repositorio se utiliza:
```git init```
#o si no puedes crear una carpeta
```git init [carpeta]```

#para remover carpetas se utiliza
```rm -rf [nombre de la carpeta]```

#borrar un archivo
```rm [archivo]```

#para crear archivos en cmd
```type nul > archivo.extension```
#ejemplo
```type nul > index.js```

## Para pasar del Working Directory al staging
```git add [archivos]```

#o este comando para agregar todo lo de la carpeta
```git add .```
#o
```git add -A```

## Ver el status de los archivos que han sido agregados
```git status```

## Quitar un archivo del staging
```git rm --cached [archivo]```

#Para borrar un archivo y ademas quitarlo del staging
```git rm -f [archivo]```

#Probar que un archivo existe o no en el staging
```git add -n [archivo]```

## Como hacer commits
```git commit -m "[comentario]"```

# commit --amend (Si te falto agregar algo a ese commmit)
```git commit --amend```
#Esto provocaria que este commit fuera anexado al ultimo commit hecho anteriormente, se abrira la confirmacion y si todo es correcto escribimos...
```:wq```

# ver los commits
```git log```

## Versionar el proyecto
# Si se requiere etiquetar commits con versiones del proyecto se utiliza:
```git tag -a [version] -m "[mensaje]"```

# Si se necesita darle version a un commit anterior...
```git tag [version] [HASHKEY]```

# Para obtener Hashkey se necesita usar:
```git tag -l```

# Para borrar una version
```git tag -d [version]```

o para renombrarlo
```git tag -f -a 0.1 -m '[mensaje]' HASHKEY```
y luego
```git tag -d [version equivocada]```

##LOGS
```git log```
# Ver todo en una linea
```git log --oneline```

# Ver todo en una linea y ademas ver un grafico
```git log --oneline --graph```

# Ver commits (restringir cuantos)
```git log -[numero]```

## Ver cambios en lineas de código
```git diff [HASHKEY]```
Esto provocara que puedas ver los cambios en lineas de codigo de uno a otra version

# Para comparar las versiones en especifico
```git diff [version1] [version2]```

## GIT RESET
# SOFT
Este reset permite quitar los cambios a partir de un commit
```git reset --soft [HASHKEY]```
#Ejemplo:
```
$ git log --oneline
[1b8e29f] (HEAD -> master, tag: 0.5) agregando nuevo hero
[3c66d3d] (tag: 0.3) agregando el header
[0c873d4] (tag: 0.1) Inicializar nuestro landing
```
Si se quiere eliminar los cambios de la version 0.5 debera elegir el HASKEY anterior en este caso la 0.3.
```git reset --soft 3c66d3d```

Lo que provocaría eso seria que los cambios se revierten y los archivos de ese commit vuelven al staging listos para volver a ser agregados con un commit

# MIXED
Quita los commits y tambien quita los archivos del staging.
Funciona exactamente igual al SOFT excepto que SI quita los archivos del staging
Tomando de ejemplo el git log del SOFT...
```git reset --soft 3c66d3d```
De esta manera se quitan los cambios a partir de esa hashkey y los archivos se quitan del staging directory

# HARD (Mucho cuidado, se recomienda saber los hashkey o tenerlos guardados en algun lado para si al utilizar este comando de manera erronea, se pueda revertir)
Este comando es muy poderoso a la hora de borrar cosas ya que puedes llegar a borrar no solo los commit, y los archivos de staging sino los archivos del proyecto completo lo que quiere decir que esos archivos no existiran más en tu carpeta.

# Ejemplo en un add
Supongamos que agregamos todo con git add .
Luego queremos quitarlos pero utilizamos hard:
```git reset --hard```

Lo que pasaria es que perderiamos todo lo que se fue al staging area.

# Borrar el universo y revertirlo
Usando 
```git reset --hard [hashkey]```
Podemos borrar todos los cambios hasta cierto punto dado, por ejemplo:
Usamos
```
$ git log --oneline
304aea8 (HEAD -> master) agregando guitarra acustica
e6c6d7d sumando nuevo hero
3c66d3d (tag: 0.3) agregando el header
0c873d4 (tag: 0.1) Inicializar nuestro landing
```
Usamos el reset hard en el punto de inicio
```git reset --hard 0c873d4```

```
$ git log
commit 0c873d45dfd8fdab9483af1a1fabd5d1730da658 (HEAD -> master, tag: 0.1)
Author: BrayanSalas <brayansalasch@hotmail.com>
Date:   Mon Aug 6 10:51:14 2018 -0500

    Inicializar nuestro landing
```
Y de esta manera todos los commits, y las partes del staging directory han sido eliminados y de esta manera estariamos al inicio del proyecto, pero existe una manera de revertirlo.


La manera es guardar los hashkey que tenemos y poner hasta cual queremos, en este caso hasta el ultimo que fue el de "agregando guitarra acustica"
```git reset --hard 304aea8```

```
$ git log
commit 304aea81a1ba65d3798543fa1a9544980ede6a8f (HEAD -> master)
Author: BrayanSalas <brayansalasch@hotmail.com>
Date:   Mon Aug 6 12:23:26 2018 -0500

    agregando guitarra acustica

commit e6c6d7d93c77f224cc920a1f8d8db8c386f8cb0c
Author: BrayanSalas <brayansalasch@hotmail.com>
Date:   Mon Aug 6 12:17:35 2018 -0500

    sumando nuevo hero

commit 3c66d3dd910c22e4dc24c6dde9152fe77aa98cd1 (tag: 0.3)
Author: BrayanSalas <brayansalasch@hotmail.com>
Date:   Mon Aug 6 11:00:08 2018 -0500

    agregando el header

commit 0c873d45dfd8fdab9483af1a1fabd5d1730da658 (tag: 0.1)
Author: BrayanSalas <brayansalasch@hotmail.com>
Date:   Mon Aug 6 10:51:14 2018 -0500
```
## RAMAS Git Branch
La rama master es la rama default de git.

# Ver ramas
```git branch -l```

# Crear una rama
```git branch [nombre]```

# Borrar una rama
```git branch -d [nombre]```

# Borrar forzadamente una rama (Cuando tienen commits y no te dejan usar -d)
```git branch -D [nombre]```

# Renombrar una rama
```git branch -m [nombreActual] [nombreNuevo]```

# Moverte entre ramas
```git checkout [nombreDeLaRama]```

tambien puedes moverte entre commits para crear ramas virtuales y así poder ver cambios en tiempo real de un momento en especifico por ejemplo:
```
commit 3aad5f3436c56cf3e4c5efba09c63f5febbaaabb (HEAD -> master, RD)
Author: BrayanSalas <brayansalasch@hotmail.com>
Date:   Mon Aug 6 13:18:15 2018 -0500

    agregando clasica y footer

commit 304aea81a1ba65d3798543fa1a9544980ede6a8f
Author: BrayanSalas <brayansalasch@hotmail.com>
Date:   Mon Aug 6 12:23:26 2018 -0500

    agregando guitarra acustica

commit e6c6d7d93c77f224cc920a1f8d8db8c386f8cb0c
Author: BrayanSalas <brayansalasch@hotmail.com>
Date:   Mon Aug 6 12:17:35 2018 -0500

    sumando nuevo hero

commit 3c66d3dd910c22e4dc24c6dde9152fe77aa98cd1 (tag: 0.3)
Author: BrayanSalas <brayansalasch@hotmail.com>
Date:   Mon Aug 6 11:00:08 2018 -0500

    agregando el header

commit 0c873d45dfd8fdab9483af1a1fabd5d1730da658 (tag: 0.1)
Author: BrayanSalas <brayansalasch@hotmail.com>
Date:   Mon Aug 6 10:51:14 2018 -0500

    Inicializar nuestro landing
```
# Creando rama virtual
```git checkout 304aea81a1ba65d3798543fa1a9544980ede6a8f```

# Creando rama y a la vez accediendo
```git branch -b [nombreDeLaRama]```

## Ejemplo para usar Ramas
Digamos que tenemos un proyecto donde se esta realizando Responsive Design (rama RD) donde se esta creando todo el CSS y los media queries, y entonces te das cuenta que hay un bug, entonces te vas a la rama principal y creas otra rama con el nombre del error (opcional)
Recuerda estar en la rama master...
```git branch hotfix```
*Se agrego un borde*

Ahora se debe de cambiar a la rama RD para resolver el problema de diseño
*Se hacen media queries y cosas sobre CSS*

Ya solo falta tener la version nueva
*Se hace la version verde*

## Mezclar cambios (MERGE)
Se realiza un merge del hotfix (se agrego un marco) con la rama master
```git merge hotfix```
En este caso la salida nos presenta que fue un Fast-forward lo que quiere decir que son cambios directos.

Luego se hace el segundo merge que es el Responsive
```git merge RD```

Como en este entonces es diferente al primer merge ahora nos pedira un commit de confirmacion de cambios y nos notifica que se cambio la manera con la que se hizo que fue de manera recursiva.

Para este entonces el git log se ve así:
```
$ git log --oneline
249c93c (HEAD -> master) Merge branch 'RD'
77d1307 (RD) invie responsive
51107be (hotfix) hotfix 1
3aad5f3 agregando clasica y footer
304aea8 agregando guitarra acustica
e6c6d7d sumando nuevo hero
3c66d3d (tag: 0.3) agregando el header
0c873d4 (tag: 0.1) Inicializar nuestro landing
```

# Ultimo merge (merge con conflictos)
Al realizar el ultimo merge que fue el de nueva-imagen al hacer:
```git merge nueva-imagen```

Aparece el siguiente conflicto:
```
$ git merge nueva-imagen
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```
Lo que nos dice es que se ha hecho la combinacion automática pero que tu decidas que lineas deseas conservar y se visualizan los cambios (Screenshot gitMerge.jpg)
Una vez que te pongas de acuerdo que es lo que quieres conservar o combinar (con tu equipo de trabajo) de ambos. En este caso combinamos ambos y eliminamos manualmente.

Una vez teniendo esto se guarda el archivo, y en la terminal se hace un 
```git status```

y aparece lo siguiente:
```
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Changes to be committed:

        new file:   nueva-version.jpg

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   index.html
```
Lo más importante a resaltar es:
Si quieres hacer tus cambios usa *git commit*

Si no quieres realizar tus cambios escribes:
```git merge --abort```

Primero hay que agregar los cambios entonces se utiliza:
```git add -A```
o
```git add .```

despues se hace un git status para verificar y despues lo que deciamos sobre un git commit.
```git status```

```git commit```
Posteriormente ponle un mensaje, luego escribes :wq para salir. (En caso de que estes desde vim)

Una vez hecho esto la rama principal tendra todos los merge.

##Git rebase
Es algo parecido a merge pero sin crear bifurcaciones de la historia del proyecto. Se puede usar uno u otro pero se recomienda que solo para uso local el rebase.

##Git STASH
Suponiendo una situacion donde estabamos añadiendo un nuevo feature a RD y derrepente sale un bug del lado del hotfix, podemos guardar el estado temporalmente con: 
```git stash```
Despues de hacer esto ya puedes moverte entre ramas para corregir el error en hotfix.

Al volver a la rama RD para volver al punto guardado debemos observar la lista para ver el ID stash@{numero}
```git stash list```

# Para eliminarlos se utiliza:
```git stash drop stash@{numero}```

# Aplicar cambios con (se aplica el {0}:
```git stash apply```
uno en especifico seria:
```git stash apply stash@{numero}```

SE UTILIZA CUANDO NO SE ESTA MUY SEGURO DE QUE CAMBIOS HACERLES COMMIT

## Cherry-pick Escogiendo commits
# *Ejemplo*
Se hicieron 2 archivos "nuevos" y se encuentra un problema (hotfix) y sin cambiar de rama arreglamos el problema alli mismo como hotfix2 y hacemos un commit aun en la rama RD pero este deberia estar en una rama hotfix2 por lo cual debio hacer...
Salir a la rama principal
```git checkout master```

#crear una nueva rama y acceder
```git checkout hotfix2```

#una vez accediendo se trae el commit (para esto debio tener el hash) de la lista
```git cherry-pick [hash]```

#luego de hacer esto cambiamos a la rama master denuevo
```git checkout master```

#y hacemos un merge
```git merge hotfix2```

luego hipoteticamente continuamos trabajando en la rama RD y se creo un archivo cambio4
```touch cambio4```
se añadio y se hizo commit...
cambiamos a la rama master...
hicimos un merge...

Y se puede ver el grafico de la siguiente manera:
 ```git log --oneline --graph```
| * e47362d (RD) cambio 4 rd
| * 3eab347 cambio 3 rd
| * 2edd3d6 arreglando el hotfix2
| * 9bd7178 cambio2 rd
| * 316211e cambio1 rd
* | 67c1dd5 (hotfix2) arreglando el hotfix2
* |   ca85a51 Merge branch 'nueva-imagen'
|\ \
| * | 4272b30 (nueva-imagen) nueva version de invie - verde
* | |   249c93c Merge branch 'RD'
|\ \ \
| | |/
| |/|
| * | 77d1307 invie responsive
| |/
* | 51107be (hotfix) hotfix 1
|/
* 3aad5f3 agregando clasica y footer
* 304aea8 agregando guitarra acustica
* e6c6d7d sumando nuevo hero


## GITHUB

# Crear una SSH key
``` ssh-keygen -t rsa -b 4096 -C "email@email.com"```

# Obtener clave (copiar manual en Windows)
```cat ~/.ssh/id_rsa.pub```

# Subir un repositorio remoto de uno local
```git remote add origin [.git]```
origin es el nombre que le damos al repositorio remoto

# Poder revisar que todo este enlazado
```git remote -v```

# Poder revisar que todo este enlazado
```git remote remove [name]```
el nombre por defecto que ponemos es origin

