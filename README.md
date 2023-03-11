# Comandos HDFS

## Notas
Para ejecutar los comandos hdfs en un server remoto es necesario usar `hdfs://<host>:<port_namenode>/<path_en_hdfs>` cuando nos referimos al server remoto de HDFS. Por ejemplo:
```sh
# Mostrar los ficheros del directorio examples en la raíz del sistema de archivos HDFS
hdfs dfs -ls hdfs://localhost:9001/examples
```

## List Files
|COMANDO|DESCRIPCIÓN|
|---|---|
|hdfs dfs -ls / | Lista todos los archivos/directorios de la ruta de destino hdfs dada.|
|hdfs dfs -ls -d /hadoop |Los directorios se listan como archivos planos. En este caso, este comando listará los detalles de la carpeta hadoop.|
|hdfs dfs -ls -h /data|Formatee el tamaño de los archivos de forma legible para el ser humano (por ejemplo, 64,0m en lugar de 67108864).|
|hdfs dfs -ls -R /hadoop|Enumera recursivamente todos los archivos del directorio hadoop y todos los subdirectorios del directorio hadoop.|
|hdfs dfs -ls /hadoop/dat*|Lista todos los archivos que coinciden con el patrón. En este caso, se listarán todos los archivos dentro del directorio de Hadoop que comienzan con 'dat'.|


## Lectura/Escritura de Ficheros
|COMANDO|DESCRIPCIÓN|
|---|---|
|hdfs dfs -text /hadoop/derby.log|Comando HDFS que toma un archivo fuente y lo muestra en formato de texto en la terminal. Los formatos permitidos son zip y TextRecordInputStream.|
|hdfs dfs -cat /hadoop/test|Este comando mostrará el contenido de test del archivo HDFS en su stdout.|
|hdfs dfs -appendToFile /home/ubuntu/test1 /hadoop/text2|Añade el contenido de un archivo local test1 a un archivo hdfs test2.|


## Cargar y Descargar Ficheros
|COMANDO|	DESCRIPCIÓN|
|---|---|
|hdfs dfs -put /home/file1 /hadoop|	Copia el fichero ‘file1’ del sistema de ficheros local a hdfs|
|hdfs dfs -put -f /home/file1 /hadoop|	Copia el fichero ‘file1’ del sistema de ficheros local a hdfs y lo sobreescribe en el caso de que ya exista|
|hdfs dfs -put -l /home/file1 /hadoop|	Copia el fichero ‘file1’ del sistema de ficheros local a hdfs. Fuerza replicación 1 y permite al DataNode persistir los datos de forma perezosa.|
|hdfs dfs -put -p /home/file1 /hadoop|	Copia el fichero ‘file1’ del sistema de ficheros local a hdfs. Mantiene los tiempos de acceso, de modificación y propietario original|
|hdfs dfs -get /file1 /home/|	Copia el fichero ‘file1’ de hdfs al sistema de ficheros local|
|hdfs dfs -get -p /newfile /home/ubuntu/|Copia el archivo de HDFS al sistema de archivos local. Pasando -p se conservan los tiempos de acceso y modificación, la propiedad y el modo.|
|hdfs dfs -get /hadoop/*.txt /home/ubuntu/|Copia todos los archivos que coinciden con el patrón del sistema de archivos local a HDFS.|
|hdfs dfs -copyFromLocal /home/ubuntu/sample /hadoop|Funciona de forma similar al comando put, excepto que la fuente está restringido a una referencia de archivo local.|
|hdfs dfs -copyToLocal /newfile /home/ubuntu/|Funciona de forma similar al comando put, excepto que el destino está restringido a una referencia de archivo local.|
|hdfs dfs -moveFromLocal /home/file1 /hadoop|	Copia el fichero ‘file1’ del sistema de ficheros local a hdfs y luego lo borra del sist. ficheros local|


## Gestión de Ficheros
|COMANDO|DESCRIPCIÓN|
|---|---|
|hdfs dfs -cp /hadoop/file1 /hadoop1	|Copia el fichero al directorio destino en hdfs|
|hdfs dfs -cp -p /hadoop/file1 /hadoop1	|Copia el fichero al directorio destino en hdfs conservando tiempos de acceso y de modificación, propietario y modo|
|hdfs dfs -cp -f /hadoop/file1 /hadoop1|Copia el archivo del origen al destino en HDFS. Pasando -f se sobreescribe el destino si ya existe.|
|hdfs dfs -mv /hadoop/file1 /hadoop1|Mueve los archivos que coinciden con el patrón de archivo especificado <src> a un destino <dst>. Cuando se mueven varios archivos, el destino debe ser un directorio.|
|hdfs dfs -rm /hadoop/file1	|Elimina el fichero ‘file1’ de hdfs y lo envía a la papelera|
|hdfs dfs -rm -r /hadoop o hdfs dfs -rm -R /hadoop|	Elimina el directorio y su contenido en hdfs|
|hdfs dfs -rm -skipTrash /file1|	Elimina el fichero sin dejarlo en la papelera|
|hdfs dfs -rm -f /hadoop|Si el archivo no existe, no muestre un mensaje de diagnóstico ni modificar el estado de salida para reflejar un error.|
|hdfs dfs -rmdir /hadoop1|Borrar un directorio.|
|hdfs dfs -mkdir /hadoop2|Crea un directorio en hdfs|
|hdfs dfs -mkdir -f /hadoop2|Crea un directorio en la ubicación HDFS especificada. Este comando no falla incluso si el directorio ya existe.|
|hdfs dfs -touchz /hadoop3|	Crea un fichero en hdfs con tamaño 0|


## Filesystem
|COMANDO|DESCRIPCIÓN|
|---|---|
|hdfs dfs -df /hadoop|Muestra la capacidad, el espacio libre y el utilizado del sistema de archivos.|
|hdfs dfs -df -h /hadoop|Muestra la capacidad, el espacio libre y el utilizado del sistema de archivos. -h formatea los tamaños de los archivos de forma legible para el ser humano.|
|hdfs dfs -du /hadoop/file|Muestra la cantidad de espacio, en bytes, utilizado por los archivos que coinciden con el patrón de archivo especificado.|
|hdfs dfs -du -s /hadoop/file|En lugar de mostrar el tamaño de cada archivo individual que coincide con el patrón, muestra el tamaño total (resumen).|
|hdfs dfs -du -h /hadoop/file|Muestra la cantidad de espacio, en bytes, utilizado por los archivos que coinciden con el patrón de archivo especificado. Formatea los tamaños de los archivos de forma legible para el ser humano legible para el ser humano.|


## Gestión de Permisos y Validación
|COMANDO|DESCRIPCIÓN|
|---|---|
|hdfs dfs -checksum /hadoop/file1|	Muestra la información checksum del fichero|
|hdfs dfs -chmod 775 /hadoop/file1|	Cambia los permisos del fichero en hdfs|
|hdfs dfs -chmod -R 755 /hadoop|	Cambia los permisos de los ficheros recursivamente|
|hdfs dfs -chown hadoop:hadoop /file1|	Cambia el propietario y el grupo del fichero|
|hdfs dfs -chown -R hadoop:hadoop /file1|	Cambia el propietario y el grupo recursivamente
|hdfs dfs -chgrp hadoop /file1|	Cambia el grupo del fichero|


## Comandos de Administración
|COMANDO|DESCRIPCIÓN|
|---|---|
|hdfs balancer -threshold 30|Ejecuta una utilidad de balanceo de cluster. Porcentaje de capacidad de disco. Este sobrescribe el umbral por defecto.|
|hdfs dfs -df /hadoop|	Muestra la capacidad y el espacio libre y usado del sistema de ficheros|
|hdfs dfs -df -h /hadoop|	Muestra la capacidad y el espacio libre y usado del sistema de ficheros en formato legible|
|hadoop version|	Muestra la versión de hadoop|
|hdfs fsck /|	Comprueba el estado de salud del sistema de ficheros|
|hdfs dfsadmin -safemode leave|	Deshabilita el modo seguro del NameNode|
|hdfs dfsadmin -refreshNodes|Vuelva a leer los archivos de hosts y de exclusión para actualizar el conjunto de Datanodes que pueden conectarse al Namenode y los que deben ser ser dados de baja o vueltos a dar de alta.|
|hdfs namenode -format|	Formatea el NameNode|


## Referencias
- [HDFS Commands Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HDFSCommands.html)
- [HDFS: Guía de Comandos Básicos](https://aprenderbigdata.com/comandos-hdfs/)
- [Hadoop HDFS Command Cheatsheet - LinOxide](http://images.linoxide.com/hadoop-hdfs-commands-cheatsheet.pdf)
