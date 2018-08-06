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

## Para pasar del Working Directory al Staying
```git add [archivos]```

#o este comando para agregar todo lo de la carpeta
```git add .```
#o
```git add -A```

## Ver el status de los archivos que han sido agregados
```git status```

## Quitar un archivo del staying
```git rm --cached [archivo]```

#Para borrar un archivo y ademas quitarlo del staying
```git rm -f [archivo]```

#Probar que un archivo existe o no en el staying
```git add -n [archivo]```

## Como hacer commits
```git commit -m "[comentario]"```

