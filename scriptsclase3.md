1. Cree dos archivos de texto similares (con una o dos líneas diferentes). Compárelos empleando diff.
R/ diff  -ReferenceObject (get-content cheni1.txt) -DifferenceObject (get-content cheni2.txt)

2. Qué ocurre si se ejecuta:
get-service | export-csv servicios.csv | out-file
Por qué?
R/ NO SE PUEDE EJECUTAR EL PROCESO PUESTO QUE EL OUT-FILE NECESITA DE LA ESPECIFICACION DEL NOMBRE DEL ARCHIVO (-PATH),
ADEMAS IDENTIFIQUÉ QUE SIN LA BARRITA Y EL OUT-FILE SE PUEDE GENERAR EL ARCHIVO SIN INCONVENIENTES EN FORMATO .CSV EL CUAL ES 
UN ARCHIVO EN FORMATO DE PALABRAS Y COMAS.

3. Cómo haría para crear un archivo delimitado por puntos y comas (;)? PISTA: Se emplea export-csv, pero con un parámetro adicional.
R/ get-service | Export-csv servicios.csv -Delimiter ';'

4. Export-cliXML y Export-CSV modifican el sistema, porque pueden crear y sobreescribir archivos. 
Existe algún parámetro que evite la sobreescritura de un archivo existente? Existe algún parámetro que permita que el comando pregunte antes de sobresscribir un archivo?
R/ El parámetro -NoClobber no permite la sobreescritura, y -Confirm lanza el diálogo de pregunta acerca de sobrescribir o no.

5.Windows emplea configuraciones regionales, lo que incluye el separador de listas. En Windows en inglés, el separador de listas es la coma (,). Cómo se le dice a Export-CSV que emplee el separador del sistema en lugar de la coma?
R/ Get-Process | Export-Csv procesos.csv -Delimiter (Get-Culture).TextInfo.ListSeparator

6. Identifique un cmdlet que permita generar un número aleatorio.
R/ get-random

7. Identifique un cmdlet que despliegue la fecha y hora actuales.
R/ get-date

8. Qué tipo de objeto produce el cmdlet de la pregunta 7?
R/ Objeto tipo "Datetime2, casteado a String

9. Usando el cmdlet de la pregunta 7 y select-object, despliegue solamente el día de la semana, así:
   DayOfWeek
   ---------
    Thursday
R/(get-date).DayOfWeek

10. Identifique un cmdlet que muestre información acerca de parches (hotfixes) instalados en el sistema.
R/get-hotfix

11. Empleando el cmdlet de la pregunta 10, muestre una lista de parches instalados. 
Luego extienda la expresión para ordenar la lista por fecha de instalación, y muestre en pantalla únicamente la fecha de instalación, 
el usuario que instaló el parche, y el ID del parche. Recuerde examinar los nombres de las propiedades.
R/Get-HotFix | Sort-Object -Property InstalledOn | Format-custom -Property InstalledOn,installedby , hotfixid

12. Complemente la solución a la pregunta 11, para que el sistema ordene los resultados por la descripción del parche, 
e incluya en el listado la descripción, el ID del parche, y la fecha de instalación. Escriba los resultados a un archivo HTML.
R/Get-HotFix | Export-Clixml |Sort-Object -Property description | Format-Table -Property description, hotfixid, installedon

13. Muestre una lista de las 50 entradas más nuevas del log de eventos System. 
Ordene la lista de modo que las entradas más antiguas aparezcan primero; 
las entradas producidas al mismo tiempo deben ordenarse por número índice. Muestre el número índice, 
la hora y la fuente para cada entrada. Escriba esta información en un archivo de texto plano.
R/ Get-EventLog -LogName System -newest 50 | Sort-Object -Property TimeGenerated | Sort-Object -Property id -Descending | Select-Object -Property index, TimeGenerated, source | Out-File -filepath .\logsSistema.txt
