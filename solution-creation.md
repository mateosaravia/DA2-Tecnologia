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

> ### 📄 El archivo generado es `.slnx`
>
> A partir de .NET 10, `dotnet new sln` genera un archivo **`.slnx`** (formato XML, mas simple y
> legible que el `.sln` clasico). Es decir, el comando de arriba crea `<Nombre>.slnx`.
>
> Ese nombre **con la extension incluida** es el que va en el parametro `solution-name` de los dos
> workflows (`build-test.yml` y `code-analysis.yml`). Por ejemplo: `solution-name: 'Test.slnx'`.
>
> Visual Studio abre soluciones `.slnx` de forma nativa desde la version 17.14.
>
> **El formato `.sln` clasico sigue siendo totalmente valido.** Si preferis usarlo, o si tu solucion
> ya existe en ese formato, no tenes que cambiar nada: los workflows funcionan igual con ambos.
> Para crear una solucion en el formato clasico:
>
> ```
> dotnet new sln -n <<Nombre del negocio, archivo de la solucion>> --format sln
> ```
>
> ⚠️ Lo que si conviene evitar es que queden **los dos archivos en la misma carpeta**: en ese caso
> los comandos `dotnet` que no reciben la solucion de forma explicita fallan con
> `MSBUILD : error MSB1011: Specify which project or solution file to use...`. Si migras de un
> formato al otro, borra el archivo viejo.

- Una vez creada la solucion crearemos dos directorios: `src` y `tests`. El directorio `src` servira para agrupar nuestro codigo fuente y el directorio `tests` servira para agrupar los proyectos de prueba. De esta forma tendremos una mejor organizacion en la solucion y en el repositorio. Para crear dichos directorios se puede hacer de manera tradicional (click derecho -> Nueva carpeta) o ejecutar los siguientes comandos independientemente:

```
mkdir src
mkdir tests
```
