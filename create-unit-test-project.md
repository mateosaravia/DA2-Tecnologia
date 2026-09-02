[⬅️ Volver a Pruebas Unitarias](https://github.com/IngSoft-DA2/DA2-Tecnologia/blob/unit-testing/README.md)

# 🚀 Creación de una Solución y Proyecto de Pruebas MSTest

El siguiente tutorial describe paso a paso cómo crear una solución en .NET, organizar los proyectos fuente y de pruebas, y configurar un proyecto MSTest para comenzar a escribir pruebas unitarias sobre tu lógica de negocio.

---

## 🟦 1. Creación de la Solución

> **¿Qué es una solución?**  
> Una solución es un contenedor que agrupa múltiples proyectos de .NET (aplicaciones, bibliotecas, pruebas, etc.), facilitando la gestión y el desarrollo colaborativo.

### 📝 Pasos

1. **Abre una terminal** en el directorio donde quieras crear la solución.  
   Asegúrate de estar en el directorio raíz del repositorio clonado.

   ```bash
   ls
   ```

2. **Crea la solución:**  
   Reemplaza `<NombreNegocio>` por el nombre de tu negocio o proyecto.

   ```bash
   dotnet new sln -n <NombreNegocio>
   ```

   - `dotnet`: CLI de .NET
   - `new`: Crear un nuevo recurso
   - `sln`: Indica que quieres una solución
   - `-n`: Especifica el nombre

   > 📄 **El archivo generado es `<NombreNegocio>.slnx`.**
   > A partir de .NET 10 `dotnet new sln` genera el formato `.slnx` (XML, más simple y legible).
   > Ese nombre **con la extensión incluida** es el que va en el parámetro `solution-name` de los
   > workflows `build-test.yml` y `code-analysis.yml`.
   >
   > El formato `.sln` clásico sigue siendo válido: si lo preferís, usá
   > `dotnet new sln -n <NombreNegocio> --format sln`. Los workflows funcionan igual con ambos.
   > Lo que sí conviene evitar es que queden los dos archivos en la misma carpeta, porque ahí los
   > comandos `dotnet` sin solución explícita fallan con `error MSB1011`.

3. **Crea los directorios principales:**

   ```bash
   mkdir src
   mkdir tests
   ```

   - `src`: Contendrá el código fuente
   - `tests`: Contendrá los proyectos de pruebas

---

## 🧪 2. Creación del Proyecto de Pruebas MSTest

### 📂 Pasos

1. **Ubícate en la carpeta de pruebas:**

   ```bash
   cd tests
   ```

2. **Crea el proyecto MSTest:**  
   Reemplaza el nombre según tu contexto.

   ```bash
   dotnet new mstest -n Vidly.BusinessLogic.Test
   ```

   - `mstest`: Tipo de proyecto (pruebas unitarias)
   - `-n`: Nombre.  
     Ejemplo:  
     - `Vidly`: Contexto del negocio  
     - `BusinessLogic`: El proyecto a probar  
     - `Test`: Indica que es para pruebas

   ![Creación del proyecto MSTest](./images/image-2.png)

   > 📊 **¿Y la cobertura de código?**
   > El workflow `build-test.yml` exige que los proyectos de prueba tengan `coverlet.collector`,
   > pero **no tenés que agregarlo a mano**: el archivo `Directory.Build.targets` que copiaste en la
   > [configuración inicial del repositorio](https://github.com/IngSoft-DA2/DA2-Tecnologia/blob/repo-configuration/README.md)
   > lo agrega automáticamente a todo proyecto de prueba de la solución.
   > Esto vale tanto si creás el proyecto por CLI como desde Visual Studio.

3. **Verifica la creación:**

   ```bash
   ls
   ```

   ![Chequeo proyecto MSTest](./images/image-3.png)

---

## ⚙️ 3. Agregar Proyecto de Pruebas a la Solución

1. **Ve al directorio raíz de la solución:**

   ```bash
   cd ..
   ```

2. **Agrega el proyecto de pruebas a la solución:**

   ```bash
   dotnet sln add tests/Vidly.BusinessLogic.Test
   ```

   ![Agregar proyecto a solución](./images/image-4.png)

3. **Verifica que fue agregado:**

   ```bash
   dotnet sln list
   ```

   ![Chequeo en solución](./images/image-5.png)

---

## 📦 4. Creación del Proyecto de Lógica de Negocio

1. **Ubícate en la carpeta de código fuente:**

   ```bash
   cd src
   ```

2. **Crea el proyecto Class Library:**

   ```bash
   dotnet new classlib -n Vidly.BusinessLogic
   ```

   ![Creación proyecto ClassLib](./images/image-7.png)

3. **Verifica la creación:**

   ```bash
   ls
   ```

   ![Verificación ClassLib](./images/image-8.png)

   El archivo `Vidly.BusinessLogic.csproj` debe verse similar a:

   ![Archivo configuración BusinessLogic](./images/image-9.png)

---

## ➕ 5. Agregar Proyecto de Lógica a la Solución

1. **Vuelve a la raíz y agrega el proyecto a la solución:**

   ```bash
   cd ..
   dotnet sln add src/Vidly.BusinessLogic
   ```

2. **Verifica la adición:**

   ```bash
   dotnet sln list
   ```

   ![Verificación agregado a solución](./images/image-10.png)

---

## 🔗 6. Referenciar la Lógica de Negocio en el Proyecto de Pruebas

1. **Ubícate en el directorio del proyecto de pruebas:**

   ```bash
   cd tests
   cd Vidly.BusinessLogic.Test
   ```

2. **Agrega la referencia del proyecto de lógica de negocio:**

   ```bash
   dotnet add reference ../../src/Vidly.BusinessLogic/Vidly.BusinessLogic.csproj
   ```

   ![Agregar referencia](./images/image-11.png)

3. **Verifica la referencia:**  
   Abre el archivo `Vidly.BusinessLogic.Test.csproj` y revisa que la referencia esté correctamente agregada.

   ![Verificación referencia en csproj](./images/image-12.png)

---

## 🏁 ¡Listo!

Ahora tienes una solución organizada, con un proyecto de lógica de negocio y un proyecto de pruebas MSTest correctamente configurados y referenciados.  
Puedes comenzar a escribir tus pruebas unitarias para garantizar la calidad de tu código. 🧑‍💻✅

---

## 📚 Recursos útiles

- [Documentación oficial de MSTest](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-with-mstest)
- [Buenas prácticas para pruebas unitarias - Microsoft Docs](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)
- [Pirámide de Testing](./unit-testing.md)
- [Como usar la extension testing en DevKit - VSC](https://code.visualstudio.com/docs/csharp/testing)
