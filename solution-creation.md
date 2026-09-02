# Creacion de una solucion

- Para crear una solucion debemos situarnos con la terminal en el directorio donde queremos crear dicho archivo de solucion. Dicho directorio debera de ser el del repositorio clonado.
- Una vez situados en dicho directorio con la terminal se debera de ejecutar el siguiente comando:

```
dotnet new sln -n <<Nombre del negocio, archivo de la solucion>>
```
Comandos y parametros:
- `dotnet`: terminal CLI para realizar acciones de .NET
- `new`: parametro para indicar la creacion de algo
- `sln`: se desea crear un archivo de solucion
- `-n`: se indica el nombre que el archivo debe tomar, en caso de no indicar toma el nombre del directorio en donde es creado

> ### 📄 El archivo generado es `<Nombre>.slnx`
>
> Ese nombre, **con la extension incluida**, es el que va en el parametro `solution-name` de los dos
> workflows (`build-test.yml` y `code-analysis.yml`). Por ejemplo: `solution-name: 'Test.slnx'`.
>
> Tambien podes usar el formato `.sln` agregando `--format sln` al comando; los workflows aceptan
> los dos. ⚠️ Lo que si hay que evitar es tener un `.sln` y un `.slnx` en la misma carpeta: ahi los
> comandos `dotnet` que no reciben la solucion de forma explicita fallan con
> `MSBUILD : error MSB1011: Specify which project or solution file to use...`.

- Una vez creada la solucion crearemos dos directorios: `src` y `tests`. El directorio `src` servira para agrupar nuestro codigo fuente y el directorio `tests` servira para agrupar los proyectos de prueba. De esta forma tendremos una mejor organizacion en la solucion y en el repositorio. Para crear dichos directorios se puede hacer de manera tradicional (click derecho -> Nueva carpeta) o ejecutar los siguientes comandos independientemente:

```
mkdir src
mkdir tests
```
