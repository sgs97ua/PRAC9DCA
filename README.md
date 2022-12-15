# Práctica 9
# Sistemas de Control de Versiones de Última generación

## Santiago Galiano Segura 74017583H

## Pregunta 1

### **Crea (si no tienes ya) una cuenta en github, gitlab, codeberg, sourcehut o bitbucket. Una vez hecho da de alta un proyecto/repositorio y configura git localmente para que puedas hacer push/pull a él.**

A continuación se muestran los comandos:

``` bash
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/sgs97ua/PRAC9DCA.git
git push -u origin main
AQUÍ ME DA ERROR POR NO HABER AGREGADO EL FICHERO
git add apuntes.txt
git commit -m "First commit"
git branch -a
git remote add origin https://github.com/sgs97ua/PRAC9DCA.git
git push -u origin main
git config --global user.name "sgs97ua"
git config --global user.email "sgs97@alu.ua.es"
git pull origin main
git pull
git push
```

## Pregunta 2
### **Créate algunos alias locales y globales en git.**

En mi caso lo he modificado de forma local y global.


``` bash
git config local alias.st status //Lo configuramos de forma local
git st // Ejecuta el comando gitstatus
git config --global alias.st status //Configuración global
```

## Pregunta 3
### **Provoca un fallo en el software en un commit de manera que después de crear varios commits más puedas encontrarlo con git bisect.**


Con el git bisect lo que hacemos es iniciar un proceso de búsqueda desde el primer commit al último commit.
En ese proceso se van acotando los commits hasta que se encuentra el commit erróneo.

``` bash
git bisect start
git log
git bisect good 956dd77fd5d498fe09a3f2d95e1625a87ab09260
git log
git bisect bad d0e09faeb043e31227244f68b12ce56ddb4fbbde
git bisect good 490052fc143fd652d0543f6e9ccfc851339a4fac
git bisect bad b2337acfaec2492d6c225157c9db93436582e45f
git bisect good 1c3ba2bbd54a6d3f9c67a3f6107a665f21ddc504
git revert b2337acfaec2492d6c225157c9db93436582e45
git bisect reset --Hemos encontrado el ERROR
```
El error se encontraba en el commit
b2337acfaec2492d6c225157c9db93436582e45

Para soluicionarlo hemos utilizado el comando git revert.
```
git revert d0e09faeb043e31227244f68b12ce56ddb4fbbde
git log
git revert d0e09faeb043e31227244f68b12ce56ddb4fbbde
git push
```


## Pregunta 4
### **Haz uso de algún hook de git.**

Un hook es un script que se ejcuta autmáticamente cada ve que se realiza una
acción específica en un repositorio Git.

Para hacer uso de algún hook de git hemos tenido que ir a .git/hooks y
en mi caso he utilizado el pre-commit. Lo que hace es comprobar
si los cambios nuevo documento creado tenga carácteres ASCII o si hay un espacio en blanco antes de un salto de línea.

Lo que hemos hecho ha sido quitar la extensión .sample.

Al crear un documento con nombre sin carácteres ASCII no hace el commit.
``` bash
Error: Attempt to add a non-ASCII file name.

This can cause problems if you want to work with people on other platforms.

To be portable it is advisable to rename the file.

If you know what you are doing you can disable this check using:

  git config hooks.allownonascii true
```
Lo mismo ocurre si en un fichero hay un espacio delante de un espacio en blanco.

``` bash
README.md:20: trailing whitespace.
+git add apuntes.txt
README.md:49: trailing whitespace.
+En ese proceso se van acotando los commits hasta que se encuentra el commit erróneo.
README.md:81: trailing whitespace.
+Para hacer uso de algún hook de git hemos tenido que ir a .git/hooks y
README.md:82: trailing whitespace.
+en mi caso he utilizado el pre-commit. Lo que hace es comprobar
README.md:83: trailing whitespace.
+el nuevo documento creado tenga carácteres ASCII.
apuntes.txt:67: trailing whitespace.
+en mi caso he utilizado el pre-commit. Lo que hace es comprobar
apuntes.txt:68: trailing whitespace.
+el nuevo documento creado tenga carácteres ASCII.
```