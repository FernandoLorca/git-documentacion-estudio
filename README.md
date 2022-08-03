# GIT

Es un software de control de versiones, su propósito es llevar registro de los cambios en archivos de computadora y coordinar el trabajo que varias personas realizan sobre archivos compartidos. Existe la posibilidad de trabajar de forma remota y una opción es GitHub

- Permite regresar a versiones anteriores de forma sencilla y muy rápida.
- Facilita el trabajo colaborativo.
- Permite respaldar tus proyectos en la nube (ej con github).
- Reduce considerablemente los tiempos de deploy.
- Las "branches" o ramas, permiten trabajar con una base de código paralela al proyecto en sí.

## Comandos

### git config --global user.name "mi nombre"

Para agregar un nombre de usuario a la cuenta global de git

- No colocar como nombre de usuario el correo de su cuenta de Github, podría traer problemas a futuro.

### git --global user.email "florcapinto@gmail.com"

Agregar correo de cuenta a utilizar. (Recomendable usar cuenta asociada a Github)

- Omitir "correo" para ver cuenta.

### git init

Inicia un repositorio en el directorio estoy trabajando.

### git status -s

Nos da toda la información necesaria sobre la rama actual.

### git add . (Meter en la caja)

Agregar todos los archivos para que esté pendiente de los cambios.

### git commit -m "inicié mi repo" (Etiquetar la caja)

Establece un punto de control en el proceso de desarrollo al cual puedes volver más tarde si es necesario.
Es neceasrio escribir un mensaje corto para explicar qué hemos desarrollado o modificado en el código fuente.

- Antes de realizar commit es necesario traer todo lo que tenga el repositorio en la nube si es necesario.

## git log --oneline

Muestra la lista de commit del mas reciente al más antiguo

- En resumidas cuentas nosotros realizamos cambios en nuestros archivos, el comando _status_ verificará que archivos han sidos modificados. Cuando deseemos registrar esos cambios tendremos que agregarlos con _add ._ así ya estará listo para poder hacer un _commit_. El commit realiza la copia de ese instante para poder volver en el tiempo si es que es necesario.

- En ocasiones al colocar _git commit_ es posible que se abra el editor por defecto de git que es VIM. Para salir de este se hace con _:q!_

## Github pages

Acepta sólo html css y js (Proyectos estáticos)

- settings => Pages => Source (se selecciona rama master (puede ser _'main'_))
- Se selecciona carpeta (root)

## Clonar repositorio

git clone 'url'

## Ignorar archivos .gitignore

En ocasiones vamos a trabajar con archivos en los que queremos que se respalden en la nube pero que no aparezcan de manera pública (Archivos que guardan información privilegiada)
Para esto es necesario crear un archivo _.gitignore_ y en este archivo colocar los archivos que queremos que git esconda. Mirar ejemplo.

- arhivo.js // Ignora el archivo en cuestion
- \*.js // Ignora todos los arhivos con extensión .js
- node_modules/ //Ignora toda la carpeta

## git log --oneline

Nos muestra un historial de los commit realizados.

## git checkout (id del commit)

Con este comando podremos 'viajar en el tiempo' y ver como estaba el código en cierto momento.

- No es para hacer cambios, sólo para revisar!

Durante el curso normal del desarrollo, HEAD apunta por lo general a la rama main u otra rama local _(HEAD -> master)_, pero, cuando extraes una confirmación anterior, HEAD ya no apunta a una rama, sino que apunta directamente a una confirmación. Este estado recibe el nombre de "HEAD desasociado" (detached HEAD)

- Para volver a la rama principal es posible volver con _git checkout (id commit main)_ o con _git checkout main_

En el caso de que visitemos un historial de un commit con checkout y comencemos a realizar cambios a partir de ese momento en el tiempo, nuestro nuevo commit quedará huerfano

## git reset (Id commit)

Vamos a conocer como podemos movernos entre los diferentes commit que tengamos registrados. _Esto es útil si aún no has subido tu commit a GitHub o a otro repositorio remoto._
Al realizar este comando viajaremos en el tiempo a la id señalada pero todos los commit que estaban de ese momento elegido en adelante se eliminan. Los archivos siguen estando agí pero git no les sigue dando seguimiento.
Si realizamos un cambio después de haber usado git reset los commit del futuro terminarán de desaparecer permanentemente, pero si realizamos el reset, no hacemos commit y usamos el mismo git reset con una id de un commit del futuro volveremos a ese commit sin problemas.

- Para poder realizar git reset de manera agresiva usaremos _git reset --hard (Id commit)_ (desaparecen archivos también).
- Si nos equivocamos y queremos volver a un commit futuro después de haber echo un hard reset podemos usar el comando _git reflog_ y nos aparecerá un historial de todo los commit realizados en el pasado con sus IDs, por lo que podremos volver a esos momentos usando el _git reset --hard (Id commit)_

### Cuidado con el reset

Ambos comandos _git revert_ y _git reset_, deshacen commits anteriores. Pero si ya has subido tu commit a un repositorio remoto, se recomienda que no uses git reset, ya que reescribe el historial de commits. Esto puede hacer que trabajar en un repositorio con otros desarrolladores y mantener un historial consistente de commits sea muy difícil.

### git pull origin (nombre de rama (main))

Este comando nos traerá los commit que estaban antes de dejar la embarrada usando reset y creando commit. No es la mejor solución.

### git revert (Id commit a eliminar)

Elimina los cambios realizados y hace otro commit informando que se eliminaron los cambios. De igual manera queda el commit anterior como respaldo.

## Ramas o branch. git branch

Para crear una rama se realiza con _git branch nombre-de-la-rama_. Para viajar a a lguna rama usamos _git checkout nombre-de-la-rama_.

- Para mostrar visualmente las ramas podemos usar _git log --oneline --graph_
- Al realizar un push (para subir a repo online), git me notificará que no estamos en la rama main y me recomienda usar el sgte comando _git push --set-upstream origin nombre-de-rama_
- Para poder viajar a main con chekout debemos primeramente realizar un commit guardando los cambios realizados en la rama.

### git merge seleccionar-rama

Este comando lo usaremos para poder actualizar el main o la rama en la que estemos posicionados (?) con los cambios que se estuvieron realizando en dicha rama seleccionada.

- La notificación de 'Fast-forward' Es el 'mejor mensaje que nos puede tirar git' xd

- Caso hipotetico: Si yo creo una nueva rama, por ej: 02-rama, en esa rama creo un archivo llamado service.html, todo bien. Pero entro al index.html, creo un h1 con un titulo 'Este es un titulo' y después yo (o otra persona, caso mas real) crea nuevamente un h1 o otro cambio en el mismo archivo index.html EN LA RAMA MAIN, al momento de realizar merge se generará un conflicto. <br>
  Visual studio code reconoce el conflicto y me muestra las lineas específicas en donde existe el conflito. ¿Que hacer?: Borrar directamente las lineas que no queremos que vallan específicamente, usar la interfaz que ofrece vscode ('Accept Current Change', 'Accept incoming Change', Accept Both Changes' y 'Compare Changes') <br>
  Vscode seguirá indicandome que el archivo tiene conflicto y SIEMPRE se debe realizar un commit indicando la solución al conflicto.

### git branch -d nombre-de-la-rama

Comando para eliminar ramas

## git tag nombre-de-la-version -m '0.0.1'

Sirven para hacer versiones de nuestro proyecto. Se realizan en rama main.

- Los tag no se suben al repo online (github) y es necesario agregar bandera _--tags_: _git push --tags_
- Ej: _git tag versionAlpha -m '0.0.1'_
- Listar tag: _git tag_
- Borrar tags: _git tag -d nombre-del-tag_
- Hacer una versión en uin commit anterior: _git tag -a nombre-del-tag (Id del commit) -m 'version alpha'_
- Mostrar información del tag _git show nombre-del-tag_
