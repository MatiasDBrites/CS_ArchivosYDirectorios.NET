# CS_ArchivosYDirectorios.NET
Trabajo con archivos y directorios en una aplicación .NET 

Clonar

```bash
git clone https://github.com/MicrosoftDocs/mslearn-dotnet-files && cd mslearn-dotnet-files
```

Ejecute el comando siguiente para crear un proyecto de consola de .NET:

```bash
dotnet new console -f net6.0 -n mslearn-dotnet-files -o .
```

Ejecute el comando siguiente para abrir el nuevo proyecto de .NET en la misma instancia de Visual Studio Code:

```bash
code -a .
```

En la ventana EXPLORADOR, en **mslearn-dotnet-files**
, expanda la carpeta **stores**
 y cada una de las carpetas numeradas que contiene.

****Búsqueda de los archivos sales.json****

Las tareas siguientes crearán un programa para buscar todos los archivos sales.json en todas las carpetas del proyecto `mslearn-dotnet-files`
.

### **Inclusión del espacio de nombres System.IO**

1. En la ventana EXPLORADOR, seleccione el archivo `Program.cs` para abrirlo en el editor.

Pegue el código siguiente en la primera línea del archivo `Program.cs`
 para importar los espacios de nombres `System.IO`
 y `System.Collections.Generic`
:

```csharp
using System.IO;
using System.Collections.Generic;
```

### **Escritura de una función para buscar los archivos sales.json**

Cree una función denominada `FindFiles` que tome un parámetro `folderName`.

1. Reemplace la línea **Console.WriteLine("Hello, World!");** por el código siguiente:

```csharp
IEnumerable<string> FindFiles(string folderName)
{
    List<string> salesFiles = new List<string>();

    var foundFiles = Directory.EnumerateFiles(folderName, "*", SearchOption.AllDirectories);

    foreach (var file in foundFiles)
    {
        // The file name will contain the full path, so only check the end of it
        if (file.EndsWith("sales.json"))
        {
            salesFiles.Add(file);
        }
    }

    return salesFiles;
}
```

Inserte el código siguiente debajo de las instrucciones `using`
 para llamar a la función `FindFiles`
. Este código pasa el nombre de la carpeta *stores*
 como la ubicación en la que buscar los archivos.

```csharp
var salesFiles = FindFiles("stores");

foreach (var file in salesFiles)
{
    Console.WriteLine(file);
}
```

## **Ejecución del programa**

1. Escriba el comando siguiente en la ventana de terminal para ejecutar el programa:

```bash
dotnet run
```

El programa debe mostrar la salida siguiente:

Resultado

```
stores/sales.json
stores/201/sales.json
stores/202/sales.json
stores/203/sales.json
stores/204/sales.json
```

Excelente. Ha escrito correctamente un programa de línea de comandos que recorre todas las carpetas del directorio `stores` y enumera todos los archivos *sales.json* que encuentre.

En este ejemplo, la ruta al directorio *stores* era bastante sencilla y se encontraba dentro del directorio de trabajo del programa. En la unidad siguiente, aprenderá a crear rutas complejas que funcionan en varios sistemas operativos mediante la clase `Path`.

### **¿Se ha bloqueado?**

Si ha tenido problemas para ejecutar el programa, este es el código completo del archivo `Program.cs`. Reemplace el contenido del archivo `Program.cs` por este código:

```csharp
var salesFiles = FindFiles("stores");
    
foreach (var file in salesFiles)
{
    Console.WriteLine(file);
}

IEnumerable<string> FindFiles(string folderName)
{
    List<string> salesFiles = new List<string>();

    var foundFiles = Directory.EnumerateFiles(folderName, "*", SearchOption.AllDirectories);

    foreach (var file in foundFiles)
    {
        // The file name will contain the full path, so only check the end of it
        if (file.EndsWith("sales.json"))
        {
            salesFiles.Add(file);
        }
    }

    return salesFiles;
}
```

[![Acceso-De-Archivos.png](https://i.postimg.cc/mrXQRF8g/Acceso-De-Archivos.png)](https://postimg.cc/xkmk38ww)
