# Manual de usuario de dbrecover for oracle

Manual de uso de DBRECOVER for Oracle 0.5

## descripción general

DBRECOVER for Oracle es un software de recuperación de desastres de datos de Oracle a nivel empresarial. Puede extraer y recuperar datos directamente desde los archivos de datos (datafile) de la base de datos de Oracle 8i a 21c, sin necesidad de ejecutar SQL a través de una instancia de base de datos de Oracle para recuperar datos. DBRECOVER, desarrollado en Java, no requiere instalación adicional, y se puede usar directamente después de descargar y descomprimir.

DBRECOVER utiliza una interfaz gráfica de usuario intuitiva (GUI), operación simple y conveniente. Los usuarios no necesitan aprender un conjunto adicional de comandos, ni necesitan entender los principios de la estructura de datos subyacente de Oracle, pueden recuperar fácilmente los datos de la base de datos a través del Asistente de Recuperación (Recovery Wizard).

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image1.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image1.png)

## ¿Por qué elegir DBRECOVER?

Quizás te preguntes, ¿acaso no es suficiente la recuperación y respaldo de RMAN, el administrador de recuperación tradicional de Oracle? ¿Por qué necesitamos elegir DBRECOVER? Permíteme aclarar tus dudas.

Con el rápido crecimiento de los sistemas de TI empresariales, la capacidad de los datos está aumentando a una tasa geométrica. Los DBA de Oracle a menudo se enfrentan a problemas como la insuficiencia de la capacidad del sistema de almacenamiento de disco existente para almacenar una copia de seguridad completa, y el tiempo medio de reparación requerido para la recuperación de datos basada en cintas de respaldo que excede las expectativas.

'Para las bases de datos, el respaldo es lo más importante', es un proverbio que todos los DBA guardan en su corazón. Sin embargo, los entornos reales varían enormemente. En el entorno de la base de datos de la empresa, la falta de espacio de respaldo de datos, la imposibilidad de que los equipos de almacenamiento comprados lleguen a corto plazo, e incluso la situación en la que se descubre que la copia de seguridad no está realmente disponible durante el proceso de recuperación de datos, son todas situaciones comunes.

Para resolver estos problemas comunes de recuperación de datos en el mundo real, el software DBRECOVER aprovecha plenamente su comprensión de la estructura de datos interna de la base de datos Oracle, el proceso de inicio central y otros principios internos. Puede enfrentar situaciones en las que no hay respaldo, como la pérdida del espacio de tablas SYSTEM, operaciones erróneas en las tablas del diccionario de datos de Oracle, y la inconsistencia del diccionario de datos causada por cortes de energía, lo que hace que la base de datos no se pueda abrir sin problemas. Puede recuperar operaciones erróneas como truncar/borrar/tablas de datos comerciales y recuperar datos con calma.

Incluso los no DBA que solo han estado en contacto con la base de datos Oracle durante unos días pueden usar DBRECOVER con facilidad. Esto se debe a la instalación simple de DBRECOVER y la interfaz de interacción hombre-máquina completamente gráfica. El personal que implementa la recuperación no necesita conocimientos profesionales de bases de datos, no necesita aprender ningún comando, y no necesita entender la estructura de almacenamiento subyacente de la base de datos. Solo necesitas hacer unos pocos clics con el ratón para recuperar los datos con calma. DBRECOVER rompe la restricción de que solo un pequeño número de profesionales pueden realizar tareas de recuperación de la base de datos, acorta en gran medida el tiempo desde el fallo de la base de datos hasta la recuperación completa de los datos, y reduce el costo total de recuperación de datos de la empresa.

DBRECOVER puede recuperar datos en dos formatos. El método tradicional de extracción extrae datos completos de los archivos de datos y los escribe en archivos de texto plano, luego usa herramientas como SQLLDR para importarlos nuevamente a la base de datos. Este método es simple e intuitivo, pero requiere un espacio dos veces el tamaño de los datos existentes: uno es el espacio ocupado por los datos de texto plano, y el otro es el espacio necesario para importar los datos de texto a la base de datos; al mismo tiempo, en términos de tiempo, es necesario extraer primero los datos originales del archivo de datos y luego importarlos a la nueva base de datos, lo que generalmente requiere el doble de tiempo.

Recomendamos encarecidamente otro método, es decir, el innovador método DataBridge de DBRECOVER. Este método carga directamente los datos extraídos a una nueva base de datos u otra base de datos disponible a través de DBRECOVER, evitando el almacenamiento de datos en el suelo. En comparación con el método tradicional, ahorra efectivamente el espacio y el tiempo necesarios para la recuperación de datos.

La tecnología ASM (Automatic Storage Management) de Oracle está siendo adoptada por cada vez más empresas. En comparación con los sistemas de archivos tradicionales, las bases de datos que utilizan almacenamiento ASM tienen un alto rendimiento, soportan clústeres y tienen ventajas de gestión conveniente. Sin embargo, el problema con ASM es que su estructura de almacenamiento es demasiado compleja y difícil de entender para los usuarios comunes. Una vez que la estructura de datos interna de un Disk Group en ASM se daña y no se puede montar con éxito, los datos importantes del usuario se "bloquearán" en esta "caja negra" de ASM. En esta situación, generalmente se requiere que los ingenieros senior de Oracle, que están familiarizados con la estructura de datos interna de ASM, lleguen al sitio del usuario para reparar manualmente la estructura interna de ASM; y comprar el servicio en el lugar de Oracle es a menudo caro y requiere mucho tiempo para los usuarios comunes.

Debido a que el equipo de desarrollo de DBRECOVER tiene una comprensión profunda de la estructura de datos interna de Oracle ASM, DBRECOVER ha agregado una función de recuperación de datos específica para ASM.

Actualmente, las funciones de recuperación de datos ASM que soporta DBRECOVER incluyen:

1. Incluso si Disk Group no puede montarse normalmente, todavía puede leer directamente los metadatos disponibles en el disco ASM a través de DBRECOVER, y copiar los archivos ASM en Disk Group basándose en estos metadatos.
2. Incluso si Disk Group no puede montarse normalmente, todavía puede leer directamente los archivos de datos en ASM a través de DBRECOVER y extraer datos de ellos, y soporta tanto el método de extracción tradicional como el método de DataBridge.

## 

## **Introducción al software DBRECOVER For Oracle**

DBRECOVER For Oracle se desarrolla en base a JAVA, lo que asegura que puede ejecutarse en múltiples plataformas, ya sea en plataformas Unix como AIX, Solaris, HPUX, plataformas Linux como Redhat, Oracle Linux, SUSE, o incluso en la plataforma Windows.

Las plataformas de sistema operativo que admite DBRECOVER son:

| Nombre de la Plataforma | ¿Está soportado? |
| --- | --- |
| Windows | Sí |
| AIX | Sí |
| Solaris Sparc/X86 | Sí |
| Linux x86/64 | Sí |
| HPUX | Sí |
| MacOS | Sí |

Las versiones de base de datos que actualmente soporta DBRECOVER son: 8i ~ 21C

DBRECOVER viene con su propio entorno JAVA, por lo que no es necesario instalar software JAVA adicional en Windows/Linux.

En Windows, haga doble clic para ejecutar start_dbrecover_windows_local_java.bat

En Linux, ejecute: sh start_dbrecover_linux_local_java.sh

Para entornos UNIX como AIX/HPUX/Solaris, los usuarios necesitan instalar el entorno JAVA 8 por sí mismos.

Los conjuntos de caracteres de la base de datos que admite DBRECOVER son:

| dioma | Juego de caracteres | Codificación |
| --- | --- | --- |
| Chino simplificado/tradicional | ZHS16GBK | GBK |
| Chino simplificado/tradicional | ZHS16DBCS | CP935 |
| Chino simplificado/tradicional | ZHT16BIG5 | BIG5 |
| Chino simplificado/tradicional | ZHT16DBCS | CP937 |
| Chino simplificado/tradicional | ZHT16HKSCS | CP950 |
| Chino simplificado/tradicional | ZHS16CGB231280 | GB2312 |
| Chino simplificado/tradicional | ZHS32GB18030 | GB18030 |
| Japonés | JA16SJIS | SJIS |
| Japonés | JA16EUC | EUC_JP |
| Japonés | JA16DBCS | CP939 |
| Coreano | KO16MSWIN949 | MS649 |
| Coreano | KO16KSC5601 | EUC_KR |
| Coreano | KO16DBCS | CP933 |
| Francés | WE8MSWIN1252 | CP1252 |
| Francés | WE8ISO8859P15 | ISO8859_15 |
| Francés | WE8PC850 | CP850 |
| Francés | WE8EBCDIC1148 | CP1148 |
| Francés | WE8ISO8859P1 | ISO8859_1 |
| Francés | WE8PC863 | CP863 |
| Francés | WE8EBCDIC1047 | CP1047 |
| Francés | WE8EBCDIC1147 | CP1147 |
| Alemán | WE8MSWIN1252 | CP1252 |
| Alemán | WE8ISO8859P15 | ISO8859_15 |
| Alemán | WE8PC850 | CP850 |
| Alemán | WE8EBCDIC1141 | CP1141 |
| Alemán | WE8ISO8859P1 | ISO8859_1 |
| Alemán | WE8EBCDIC1148 | CP1148 |
| Italiano | WE8MSWIN1252 | CP1252 |
| Italiano | WE8ISO8859P15 | ISO8859_15 |
| Italiano | WE8PC850 | CP850 |
| Italiano | WE8EBCDIC1144 | CP1144 |
| Tailandés | TH8TISASCII | CP874 |
| Tailandés | TH8TISEBCDIC | TIS620 |
| Árabe | AR8MSWIN1256 | CP1256 |
| Árabe | AR8ISO8859P6 | ISO8859_6 |
| Árabe | AR8ADOS720 | CP864 |
| Español | WE8MSWIN1252 | CP1252 |
| Español | WE8ISO8859P1 | ISO8859_1 |
| Español | WE8PC850 | CP850 |
| Español | WE8EBCDIC1047 | CP1047 |
| Portugués | WE8MSWIN1252 | CP1252 |
| Portugués | WE8ISO8859P1 | ISO8859_1 |
| Portugués | WE8PC850 | CP850 |
| Portugués | WE8EBCDIC1047 | CP1047 |
| Portugués | WE8ISO8859P15 | ISO8859_15 |
| Portugués | WE8PC860 | CP860 |

Tipos de almacenamiento de tablas soportados por DBRECOVER:

| Tipo de almacenamiento de la tabla | ¿Soportado? |
| --- | --- |
| Tabla de clúster (Cluster Table) | SÍ |
| Tabla organizada por índice, particionada o no particionada | NO |
| Tabla de montón común, particionada o no particionada | SÍ |
| Tabla de montón común con compresión básica habilitada | NO |
| Tabla de montón común con compresión avanzada habilitada | NO |
| Tabla de montón común con compresión de columnas mixtas habilitada | NO |
| Tabla de montón común con cifrado habilitado | NO |
| Tabla con campo virtual (virtual column) | NO |
| Filas encadenadas, filas migradas (chained rows, migrated rows) | SÍ |

Consideraciones: Para columnas virtuales, columnas con valores predeterminados optimizados en 11g, la extracción de datos puede ser posible, pero se perderán los campos correspondientes. Estos son características nuevas después de 11g, y no son ampliamente utilizados.

Tipos de datos de columnas soportados por DBRECOVER:

| Tipo de datos | ¿Es compatible? |
| --- | --- |
| BFILE | No |
| XML binario | No |
| BINARY_DOUBLE | Sí |
| BINARY_FLOAT | Sí |
| BLOB | Sí |
| CHAR | Sí |
| CLOB y NCLOB | Sí |
| Colecciones (incluyendo VARRAYS y tablas anidadas) | No |
| Fecha | Sí |
| INTERVALO DE DÍA A SEGUNDO | Sí |
| INTERVALO DE AÑO A MES | Sí |
| LOBs almacenados como SecureFiles | Sí |
| LONG | Sí |
| LONG RAW | Sí |
| Tipos de datos multimedia (incluyendo Spatial, Image, y Oracle Text) | No |
| NCHAR | Sí |
| Número | Sí |
| NVARCHAR2 | Sí |
| RAW | Sí |
| ROWID, UROWID | Sí |
| TIMESTAMP | Sí |
| TIMESTAMP CON ZONA HORARIA LOCAL | Sí |
| TIMESTAMP CON ZONA HORARIA | Sí |
| Tipos definidos por el usuario | No |
| VARCHAR2 y VARCHAR | Sí |
| XMLType almacenado como CLOB | No |
| XMLType almacenado como Objeto Relacional | No |

Soporte de DBRECOVER para ASM:

| Función | ¿Soportado? |
| --- | --- |
| Soporte para la extracción directa de datos de ASM, sin necesidad de copiar al sistema de archivos | SÍ |
| Soporte para la copia de archivos de datos de ASM | SÍ |

## 

## **Instalación y inicio de DBRECOVER**

Dado que DBRECOVER es un software puro basado en JAVA, no requiere una instalación adicional. Los usuarios solo necesitan descomprimir el archivo ZIP del software después de descargarlo para recuperar los datos.

En Windows, haga doble clic para ejecutar start_dbrecover_windows_local_java.bat

En un entorno Linux, puede usar la interfaz gráfica de usuario local o herramientas de gráficos remotos como Xmanager/VNC

1. Asegúrese de que puede abrir el pequeño programa de reloj gráfico xclock
2. Ejecute en el directorio de descompresión del software: sh start_dbrecover_linux_local_java.sh

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image2.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image2.png)

En un entorno AIX/HPUX/Solaris, puede usar la interfaz gráfica de usuario local o herramientas de gráficos remotos como Xmanager/VNC

1. Asegúrese de que ha instalado el entorno JAVA 8 correspondiente a la plataforma y confirme con el comando: java -version
2. Asegúrese de que puede abrir el pequeño programa de reloj gráfico xclock
3. Ejecute en el directorio de descompresión del software: sh start_dbrecover.sh

## ****Registro de licencia de DBRECOVER****

DBRECOVER For Oracle es un software comercial. La versión comunitaria de DBRECOVER está disponible para pruebas y aprendizaje.

Actualmente solo ofrecemos un tipo de licencia, la licencia corporativa. Puede visitar el sitio web [https://www.dbrecover.com/](https://www.dbrecover.com/) para obtener información de compra.

Una vez que el usuario obtiene la clave de licencia, puede registrarse por sí mismo en el software Register, el método de uso específico es el siguiente:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image3.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image3.png)

En la barra de menú Ayuda => Registro, ingrese el NOMBRE DB y la clave según la información enviada a usted después de la compra y haga clic en el botón Registro. Una vez que se completa el registro, DBRECOVER detectará automáticamente la información de registro de la licencia cuando se reinicie en el futuro, no es necesario volver a registrarse.

La información de registro exitosa se puede encontrar en Ayuda => Acerca de:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image4.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image4.png)

# **Introducción al uso de DBRECOVER basado en diferentes escenarios de recuperación de bases de datos Oracle**

## **Escenario de recuperación 1: el archivo de datos de ORACLE está dañado, lo que hace que la base de datos no se pueda abrir**

La base de datos de producción de la empresa A se ejecuta en modo no archivado durante todo el año, ocasionalmente realiza una copia de seguridad lógica de EXP, pero nunca realiza una copia de seguridad física. Un día, después de que la energía del servidor se apaga y se reinicia, la base de datos no se puede usar normalmente, y después de la inspección, se encuentra que el espacio de tablas SYSTEM está gravemente dañado. En este momento, puedes usar DBRECOVER para transferir rápidamente los datos de la base de datos dañada a una nueva base de datos, con el objetivo de recuperar rápidamente las operaciones.

En escenarios similares a este, si te encuentras con errores como ORA-01194, ORA-01110, ORA-01033, ORA-01115, ORA-00368, ORA-00600 kcbzib_kcrsds_1, ORA-00333, ORA-01113, ORA-01122, ORA-27027, etc., que hacen que la base de datos no pueda abrirse, puedes intentar recuperar los datos utilizando los métodos empleados en este escenario de recuperación.

Los pasos breves son los siguientes:

1. Utiliza dbca para crear una nueva base de datos ORACLE, ten en cuenta que el conjunto de caracteres debe ser el mismo que el de la base de datos dañada.
2. Crea usuarios y espacios de tablas correspondientes en la nueva base de datos, se recomienda otorgar temporalmente el rol de DBA a estos usuarios.
3. Inicia el programa de escucha (LISTENER), asegúrate de que el servicio de la base de datos se haya registrado para escuchar.
4. Inicia DBRECOVER en modo de diccionario y carga todos los archivos de datos de la base de datos dañada original.
5. En DBRECOVER, selecciona el nombre de usuario que deseas recuperar, haz clic con el botón derecho y selecciona puente de datos.
6. En la interfaz del puente de datos, haz clic en el icono de suma, agrega la información de conexión de la nueva base de datos (Conexión).
7. Haz clic en Data Bridge para iniciar el trabajo de transferencia, espera a que todas las tablas de SCHEMA se transfieran al SCHEMA objetivo de la base de datos objetivo.
8. Selecciona el SCHEMA correspondiente, haz clic con el botón derecho y selecciona la función EXPORTDDL, elige el tipo de objeto que deseas recuperar y haz clic en EXPORT.
9. Basado en el archivo SQL DDL generado por EXPORTDDL, ejecuta manualmente en el SCHEMA objetivo de la base de datos objetivo.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image5.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image5.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image6.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image6.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image7.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image7.png)

`// Inicia el programa de escucha (LISTENER), asegúrate de que el servicio de base de datos se haya registrado para escuchar.`

`C:\Users\testenv>lsnrctl status`

`LSNRCTL for 64-bit Windows: Version 11.2.0.1.0 - Production on 12-MAY-2023 10:01:48`

`Copyright (c) 1991, 2010, Oracle. All rights reserved.`

`Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=DESKTOP-testenv)(PORT=1521)))`

`STATUS of the LISTENER`

`-----------------------`

`Alias LISTENER`

`Version TNSLSNR for 64-bit Windows: Version 11.2.0.1.0 - Production`

`Start Date 12-MAY-2023 10:00:49`

`Uptime 0 days 0 hr. 0 min. 59 sec`

`Trace Level off`

`Security ON: Local OS Authentication`

`SNMP OFF`

`Listener Parameter File D:\app\testenv\product\11.2.0\dbhome_2\network\admin\listener.ora`

`Listener Log File d:\app\testenv\diag\tnslsnr\DESKTOP-testenv\listener\alert\log.xml`

`Listening Endpoints Summary...`

`(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=DESKTOP-testenv)(PORT=1521)))`

`(DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(PIPENAME=\\.\pipe\EXTPROC1521ipc)))`

`Services Summary...`

`Service "CLRExtProc" has 1 instance(s).`

`Instance "CLRExtProc", status UNKNOWN, has 1 handler(s) for this service...`

`Service "ORCL1XDB" has 1 instance(s).`

`Instance "orcl1", status READY, has 1 handler(s) for this service...`

`Service "ORCLXDB" has 1 instance(s).`

`Instance "orcl", status READY, has 1 handler(s) for this service...`

`Service "orcl" has 1 instance(s).`

`Instance "orcl", status READY, has 1 handler(s) for this service...`

`Service "orcl1" has 1 instance(s).`

`Instance "orcl1", status READY, has 1 handler(s) for this service...`

`The command completed successfully`

`// En la nueva base de datos, crea usuarios y espacios de tabla correspondientes a la base de datos, se recomienda otorgar roles de DBA a estos usuarios temporalmente.`

`set ORACLE_SID=ORCL1`

`sqlplus / as sysdba`

`SQL> create user pd identified by oracle;`

`User created.`

`SQL> grant dba to pd;`

`Grant succeeded.`

`SQL> create tablespace pdtbs datafile size 500M autoextend on next 100M;`

`Tablespace created.`

`SQL> alter user pd default tablespace pdtbs;`

`User altered.`

---

Inicia DBRECOVER y selecciona Herramientas => Asistente de recuperación

Haz clic en Siguiente

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image8.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image8.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image9.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image9.png)

En el siguiente paso, necesitamos seleccionar el orden de los bytes ENDIAN correcto; Dado que los archivos de datos de ORACLE utilizan diferentes formatos de orden de bytes de Endian en diferentes plataformas de sistemas operativos, la lista de correspondencia entre el orden de bytes y la plataforma es la siguiente:

| plataforma | endian |
| --- | --- |
| Solaris[tm] OE (32 bits) | Grande |
| Solaris[tm] OE (64 bits) | Grande |
| Microsoft Windows IA (32 bits) | Pequeño |
| Linux IA (32 bits) | Pequeño |
| Sistemas basados en AIX (64 bits) | Grande |
| HP-UX (64 bits) | Grande |
| HP Tru64 UNIX | Pequeño |
| HP-UX IA (64 bits) | Grande |
| Linux IA (64 bits) | Pequeño |
| HP Open VMS | Pequeño |
| Microsoft Windows IA (64 bits) | Pequeño |
| IBM zSeries Based Linux | Grande |
| Linux x86 64 bits | Pequeño |
| Apple Mac OS | Grande |
| Microsoft Windows x86 64 bits | Pequeño |
| Solaris Operating System (x86) | Pequeño |
| IBM Power Based Linux | Grande |
| HP IA Open VMS | Pequeño |
| Solaris Operating System (x86-64) | Pequeño |
| Apple Mac OS (x86-64) | Pequeño |

Solo ten en cuenta que las plataformas más comunes que utilizamos, Windows y Linux, son ambas Little Endian, por lo que no necesitas hacer ninguna configuración y puedes dejarlo por defecto.

En las plataformas de mainframe, incluidos los sistemas basados en AIX (64 bits) y HP-UX (64 bits), se utiliza el orden de bytes Big Endian, por lo que debes seleccionar Big Endian aquí.

Nota: Si tus archivos de datos se generaron en AIX (es decir, Big Endian) y copiaste estos archivos de datos a un servidor Windows para recuperar datos con DBRECOVER, aún debes seleccionar el formato Big Endian original.

Aquí, como necesitamos recuperar archivos de base de datos Oracle en la plataforma Linux x86-64, seleccionamos Endian como Little.

Haz clic en Siguiente

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image10.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image10.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image11.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image11.png)

Haz clic en Choose Files, generalmente recomendamos que si la base de datos no es grande, entonces selecciona todos los archivos de datos de esa base de datos; si tu base de datos es grande y sabes en qué archivos de datos están tus tablas, entonces puedes seleccionar únicamente los archivos de datos del espacio de tabla SYSTEM (¡es necesario!) y los archivos de datos donde se encuentran los datos.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image12.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image12.png)

Ten en cuenta que la interfaz Choose admite operaciones de teclado como Ctrl + A y Shift.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image13.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image13.png)

Nota: una vez que hayas agregado todos los archivos de datos, si no entiendes los otros parámetros en esta interfaz, déjalos todos por defecto, ¡no es necesario modificarlos!

Luego necesitas especificar el tamaño de bloque (Block Size) para los archivos de datos especificados, que es el tamaño de los bloques de datos de ORACLE. Aquí puedes modificarlo según la situación real, por ejemplo, si tu DB_BLOCK_SIZE es 8K, pero algunos espacios de tabla especifican 16K como el tamaño del bloque de datos, solo necesitas cambiar el BLOCK_SIZE para esos archivos de datos que no son de 8k.

Si estás utilizando un sistema de archivos convencional, no necesitas especificar OFFSET aquí. El parámetro OFFSET es principalmente para aquellos escenarios que utilizan dispositivos sin formato para almacenar archivos de datos, por ejemplo, en AIX, si usas un LV basado en VG convencional como archivo de datos, entonces hay un OFFSET de 4k que necesita ser especificado aquí.

Si estás utilizando archivos de datos de dispositivo sin formato y no sabes cuánto es el OFFSET, puedes usar la herramienta dbfsize que viene con $ORACLE_HOME/bin para verlo.

`$ dbfsize /dev/lv_control_01`

`Database file: /dev/lv_control_01`

`Database file type: raw device without 4K starting offset`

`Database file size: 334 16384 byte blocks`

---

Debido a que en este escenario todos los archivos de datos tienen un BLOCK SIZE de 8K y se basan en el sistema de archivos, por lo tanto, no tienen OFFSET, haz clic en Load.

En la fase Load, DBRECOVER leerá la información del diccionario de datos de ORACLE desde el espacio de tabla SYSTEM y creará un diccionario de datos en su propio Derby, lo que le permite a DBRECOVER analizar varios tipos de datos en la base de datos ORACLE.

Después de completar Load, aparece un árbol agrupado por usuarios de la base de datos en el lado izquierdo de la interfaz de DBRECOVER:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image14.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image14.png)

Selecciona una tabla que deseas recuperar y haz doble clic para ver los datos:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image15.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image15.png)

Sin haber comprado la licencia de software, podemos inspeccionar si DBRECOVER puede recuperar suficientes datos mediante la visualización de las tablas, la extracción de al menos diez mil filas de datos y la verificación del número de filas que se pueden recuperar.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image16.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image16.png)

Después de seleccionar la tabla, haz clic con el botón derecho en UNLOAD, lo que exportará los datos de la tabla en formato de texto:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image17.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image17.png)

Sin registrar la licencia de software, se pueden extraer un máximo de diez mil filas de datos de una sola tabla.

Para las tablas que contienen más de diez mil filas de datos, puedes verificar aún más a través de la función de verificación del número de filas recuperables. Selecciona la tabla que deseas verificar, haz clic con el botón derecho en EXAMINE RECORDS COUNT:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image18.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image18.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image19.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image19.png)

Desde Oracle 10g, se introdujo la característica de recolección automática de estadísticas, y podemos utilizar esta característica para ver las estadísticas históricas de la tabla, que incluyen el número de filas. En el modo de diccionario, cada vez que ejecutamos operaciones de visualización, extracción, verificación, etc. en una tabla, alguna información de esa tabla se registrará en el registro de software log_dbrecover.txt. El archivo de registro se almacena en el directorio del software:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image20.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image20.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image21.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image21.png)

Información del registro:

`object information user#:106 object_name: EMP object_id:74042 data_object_id:74042 object_type:2`

`table information object_id:74042 data_object_id:74042 ts#:4 rfile#:7 block#:386 rowcnt:114688 blkcnt:751 analyzetime:2023-05-19 12:41:29.0`

`TABLE PD.EMP 666 rows unloaded`

---

El registro contiene mucha información útil:

| object_id número de objeto | 74042 |
| --- | --- |
| data_object_id número de objeto de datos | 74042 |
| ts# número del espacio de tabla | 4 |
| rfile# número de archivo relativo donde se encuentra el encabezado de la tabla | 7 |
| block# número de bloque de datos donde se encuentra el encabezado de la tabla | 386 |
| rowcnt número de filas registradas en la información estadística (la información estadística es un valor estimado) | 114688 |
| blkcnt número total de bloques de esta tabla | 751 |
| analyzetime tiempo de recolección de información estadística | 2023-05-19 12:41:29.0 |

Por lo general, el error en la información estadística no supera el 10%, por lo que podemos comparar el resultado de la verificación del número de filas basándonos en rowcnt aquí. Por ejemplo, si rowcnt es 114688 (para tablas con menos de 1 millón de filas, el error en la información estadística es pequeño) y el resultado de EXAMINE es 114688 filas, entonces podemos validar la autenticidad de este resultado.

Los usuarios pueden realizar la verificación anterior en cada tabla de datos importante según sus necesidades. Recomendamos a los usuarios que verifiquen completamente la integridad de los datos recuperables antes de comprar la licencia del software.

Después de completar la verificación anterior, comenzamos la transmisión de datos del puente de datos a nivel de usuario SCHEMA. Selecciona el nombre de usuario que deseas recuperar y haz clic con el botón derecho en Data Bridge.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image22.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image22.png)

En la interfaz de transferencia de datos a nivel SCHEMA, haz clic en el botón "+", para agregar la información de conexión de la base de datos de destino:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image23.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image23.png)

Ingresa la información de conexión de la nueva base de datos que creaste anteriormente, aquí estamos utilizando el usuario PD.

Nota: El software DBRECOVER solo transferirá datos al usuario especificado en la información de conexión de la base de datos, es decir, si ingresamos PD aquí, los datos se transferirán a PD. Los clientes deben seguir un principio simple de uno a uno aquí. Por ejemplo, si hay un usuario de base de datos que necesita ser recuperado, como EAS, deben crear un usuario EAS y su espacio de tabla en la base de datos de destino y otorgar los permisos necesarios (rol DBA), y luego ingresar EAS en esta conexión de base de datos, para asegurarse de que los datos se transfieran a EAS. PD aquí es solo un ejemplo. Si los clientes necesitan recuperar varios usuarios de base de datos, como EAS, MES, NC001, etc., deben crear estas cuentas y sus espacios de tabla en la base de datos de destino de manera correspondiente, y otorgar los permisos necesarios (rol DBA). Luego, deben crear múltiples informaciones de conexión de base de datos (DB Connection) en DBRECOVER, y especificar la información de conexión de base de datos correspondiente (DB Connection) cuando transfieran a nivel de usuario SCHEMA.

Haz clic en TEST para probar la disponibilidad de la conexión de la base de datos de destino:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image24.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image24.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image25.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image25.png)

Si es exitoso, haz clic en SAVE para guardar:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image26.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image26.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image27.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image27.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image28.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image28.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image29.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image29.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image30.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image30.png)

Comprobar datos:

`SQL> show parameter db_name`

`NAME TYPE VALUE`

`----------------------------------- ---------------------- ------------------------------`

`db_name string ORCL1`

`SQL> select count(*) from pd.emp;`

`COUNT(*)`

`---------`

`14`

---

**Introducción al modo WIDE TABLE**

Nota: La transferencia de datos anterior asume por defecto el modo de tabla ancha (wide table mode) para transferir datos, es decir, convierte todos los tipos de campos CHAR, NCHAR, VARCHAR, NVARCHAR a su longitud máxima, es decir, 2000 o 4000. El propósito de esto es evitar el problema de no poder insertar cadenas recuperadas debido a campos demasiado cortos.

Si no deseas utilizar el modo de tabla ancha, puedes hacer clic en la barra de menú Options => Preferences.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image31.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image31.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image32.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image32.png)

Si seleccionas "Sí" en el menú desplegable "Create table in restricted mode", no se utilizará el modo de tabla ancha para crear la tabla de datos.

**Introducción a la función EXPORT DDL**

Hemos realizado operaciones de recuperación para las tablas de datos de un solo SCHEMA, los objetos de recuperación incluyen: la creación de las tablas de datos correspondientes e inserción de los datos recuperables.

Para la recuperación de objetos como índices, restricciones, vistas, triggers, etc., puedes utilizar la función EXPORT DDL.

Selecciona el SCHEMA que deseas recuperar, haz clic con el botón derecho y selecciona la función EXPORT DDL:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image33.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image33.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image34.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image34.png)

Los tipos de objetos que se pueden recuperar incluyen:

- Declaración de creación de tabla (create table statement) (nota: no incluye información de partición)
- Declaración de creación de índice (create index statement) (nota: no incluye información de partición)
- Restricciones (constraint)
- Vistas (view)
- Paquetes, procedimientos almacenados y funciones (Package & Stored Procedure & Function)
- Secuencias (sequence)
- Triggers (trigger)
- Sinónimos (synonym)
- Enlaces a bases de datos (DBlink)

Aquí también debes seleccionar la información de conexión a la base de datos que ingresaste anteriormente, para el procesamiento temporal de la información DDL.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image35.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image35.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image36.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image36.png)

Una ventana emergente te mostrará la ruta del archivo DDL SQL, mira este archivo:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image37.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image37.png)

Nota: ¡La función EXPORTDDL solo se puede usar normalmente después de registrar una licencia comercial válida (LICENSE KEY)!

Las declaraciones para crear índices, vistas y otros objetos en el archivo DDL SQL mencionado anteriormente, necesitan ser copiadas y ejecutadas por el usuario en la base de datos correspondiente.

Si el usuario tiene archivos dmp antiguos de exp o expdp, se recomienda importar la información de metadatos desde los archivos dmp (usa rows=no para imp, y content=metadata_only para impdp para solo importar la información de estructura). La función exportddl carece de cierta información de metadatos, como la autorización de objetos y las claves foráneas, etc.

**Introducción a la función LOAD FROM EXIST DICTS:**

Si te encuentras con situaciones como la falta de respuesta del programa, bloqueos o errores durante el proceso de recuperación real, puedes usar la función LOAD FROM EXIST DICTS para cargar directamente el estado de recuperación anterior después de reiniciar DBRECOVER.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image38.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image38.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image39.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image39.png)

Los estados de recuperación se ordenan en función de la hora, y puedes seleccionar el apropiado y hacer clic en el botón LOAD para cargarlo. Tanto el modo de diccionario (DICTIONARY-MODE) como el modo no diccionario (NON-DICTIONARY MODE) pueden utilizar esta función de carga rápida para evitar operaciones repetidas.

## 

## **Escenario de recuperación 2: Eliminación errónea o pérdida total del espacio de tablas SYSTEM**

El administrador del sistema SA de la empresa D eliminó por error el archivo de datos donde se encuentra el espacio de tablas SYSTEM de una base de datos, lo que hizo que la base de datos no se pudiera abrir completamente y que los datos no se pudieran extraer. En ausencia de una copia de seguridad, se pueden utilizar DBRECOVER para recuperar los datos.

En este escenario, después de iniciar DBRECOVER, debes seleccionar el modo "Non-Dictionary mode" (modo no diccionario) en el Recovery Wizard:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image40.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image40.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image41.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image41.png)

A continuación, debes seleccionar el conjunto de caracteres correcto, de lo contrario, los datos futuros aparecerán codificados.

En el modo NoN-dictionary, el usuario debe especificar el conjunto de caracteres y el conjunto de caracteres nacionales, porque después de perder el espacio de tablas SYSTEM, la información del conjunto de caracteres de la base de datos no se puede obtener normalmente, por lo que se necesita la entrada del usuario. Solo con la configuración correcta del conjunto de caracteres y la instalación del paquete de idioma necesario, se puede garantizar la extracción normal de varios idiomas en el modo No-Dictionary.

Al igual que en la demostración del escenario 1, introduce todos los archivos de datos disponibles para el usuario (sin incluir los archivos temporales) y configura correctamente el tamaño de bloque (Block Size) y el OFFSET:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image42.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image42.png)

A continuación, haz clic en SCAN. La función SCAN es para escanear toda la información de datos en todos los archivos de datos.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image43.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image43.png)

Luego selecciona el nodo de la base de datos en el diagrama de árbol de la izquierda y haz clic derecho en SCAN EXTENT. Solo usa el modo SCAN TABLE FROM SEGMENTS cuando puedas confirmar que todos los archivos de datos (excepto SYSTEM01.DBF) están disponibles. La ventaja de este modo es que es un poco más rápido, pero su nivel de recuperación es inferior al modo SCAN EXTENT en caso de que los archivos de datos estén incompletos o dañados.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image44.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image44.png)

Después de completar Scan Tables From Extents, puedes abrir el diagrama de árbol en el lado izquierdo de la interfaz principal:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image45.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image45.png)

Cada nodo en el diagrama de árbol representa un fragmento de datos de una tabla heap normal o una partición, y su nombre es obj + el DATA OBJECT ID registrado en el segmento de datos.

Selecciona un nodo y observa la barra lateral derecha de la interfaz principal:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image46.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image46.png)

Análisis de tipos de campos

Debido a la pérdida del espacio de tablas SYSTEM, en el modo Non-Dictionary faltan información de la estructura de la tabla de datos, esta información incluye el nombre del campo y el tipo de campo en la tabla, y en ORACLE, esta información solo se guarda como información de diccionario y no se almacena en la tabla de datos. Cuando el usuario solo tiene el espacio de tablas donde se encuentran los datos de la aplicación, necesita adivinar el tipo de cada campo basado en los datos ROW en el segmento de datos. Aquí podemos analizar hasta más de 10 tipos de datos principales:

- String (cadena): incluye char, varchar
- NString (cadena en idioma nacional): nchar, nvarchar
- Number (tipo numérico)
- Date (tipo fecha)
- TimeStamp (tipo de marca de tiempo)
- TimeStamp Zone (tipo de marca de tiempo conzona horaria)
- CLOB
- BLOB

Análisis de datos de muestra (Sample Data Analysis):

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image47.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image47.png)

Esta sección analiza 10 datos basándose en los resultados del análisis de los tipos de campos, y muestra los resultados del análisis. Los datos de muestra pueden ayudar al usuario a comprender la situación actual de los datos almacenados en este segmento de datos. Si hay menos de 10 registros en el segmento de datos, se mostrarán todos los registros.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image48.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image48.png)

TRATAR DE ANALIZAR el tipo de columna desconocida:

Esta sección se refiere a los campos cuyos tipos no se pueden confirmar completamente con la función de análisis de campo, se intenta analizar con varios tipos de campo y se presenta al usuario para que pueda determinar qué tipo es realmente.

Los campos cuyo tipo no se puede confirmar generalmente se encuentran en las siguientes situaciones:

1. RAW o LONG RAW
2. Tipos de datos no compatibles, que incluyen: XDB.XDB$RAW_LIST_T, XMLTYPE, tipos definidos por el usuario, etc.
3. El bloque de datos en sí está seriamente dañado

En este modo "Non-Dictionary Mode" (modo no diccionario), también se pueden utilizar los modos convencional y de puente de datos. En comparación con el modo de diccionario, la principal diferencia es que en el modo no diccionario, el usuario puede determinar el tipo de campo por sí mismo durante el puenteo de datos. Como se muestra en la siguiente figura, algunos tipos de campos son UNKNOWN, es decir, desconocidos.

Si el usuario conoce la estructura de la tabla en el momento del diseño (también puede provenir de la documentación del proveedor de la aplicación), entonces puede seleccionar el tipo correcto de Column Type para que los datos de la tabla se puedan enlazar de manera exitosa a la base de datos objetivo.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image49.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image49.png)

## 

## **Escenario de recuperación 3: Caso de encriptación y daño a los archivos de datos por software de ransomware**

El software de ransomware (ransomware malware) puede encriptar y dañar parcial o totalmente el contenido de los archivos de datos de ORACLE. Debido a que el tamaño de los archivos de datos de ORACLE generalmente es bastante grande, la encriptación completa puede llevar mucho tiempo, por lo que algunos softwares de ransomware optan por encriptar solo el espacio continuo o aleatorio en la cabecera de los archivos de datos de ORACLE.

Para este tipo de daño de encriptación parcial, podemos intentar usar DBRECOVER para recuperar los datos de los mismos.

Debido a que la cabecera del archivo de datos está dañada, necesitamos observar el contenido de SYSTEM01.DBF para entender la información como el número de espacio de tablas (TS#) y el número de archivo relativo (RFILE#) de cada archivo de datos.

Aquí está la lista de archivos de datos:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image50.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image50.png)

`O1_MF_APP01_L782YY4Y_.DBF.eking`

`O1_MF_APP01_L782ZBM3_.DBF.eking`

`O1_MF_APP01_L782ZCP1_.DBF.eking`

`O1_MF_APP02_L782ZO7W_.DBF.eking`

`O1_MF_APP02_L7830DTG_.DBF.eking`

`O1_MF_APP02_L7830FJ6_.DBF.eking`

`O1_MF_DBRECOVE_L6G7B1Q3_.DBF.eking`

`O1_MF_SYSAUX_L5VP5QJ8_.DBF.eking`

`O1_MF_SYSTEM_L5VP4N7Y_.DBF.eking`

`O1_MF_TEMP_L5VPCQGO_.TMP.eking`

`O1_MF_UNDOTBS1_L5VP66PM_.DBF.eking`

`O1_MF_USERS_L5VP67TJ_.DBF.eking`

---

El ejemplo de arriba tiene el sufijo de encriptación como eking.

Ten en cuenta que TEMP, UNDOTBS1, SYSAUX no tienen nada que ver con nuestra tarea de recuperación, por lo que podemos ignorar estos archivos.

Primero iniciamos DBRECOVER, usando el modo de diccionario DICT-MODE:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image51.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image51.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image52.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image52.png)

Elegimos DB VERSION según la situación real. Para instancias con versiones superiores a 12c, como 18c, 19c, etc., elige 12.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image53.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image53.png)

Solo agregamos SYSTEM01.DBF, y especificamos su TS# = 0 rFILE# = 1 (ten en cuenta que esto es fijo).

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image54.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image54.png)

La opción "SCAN BASE TABLES" marcada anteriormente puede manejar de manera más efectiva la situación de daño.

Después de hacer clic en el botón LOAD, DBRECOVER escaneará todo SYSTEM01.DBF y encontrará los datos de la tabla de base del diccionario de datos en él.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image55.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image55.png)

Abrimos el nodo del usuario SYS y buscamos las 2 tablas base TS$ y FILE$:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image56.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image56.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image57.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image57.png)

La tabla TS$ almacena la información del espacio de tablas, la columna TS# es el número del espacio de tablas, de la cual se puede obtener la siguiente información:

| TS# | NAME |
| --- | --- |
| 0 | SYSTEM |
| 1 | SYSAUX |
| 2 | UNDOTBS1 |
| 3 | TEMP |
| 4 | USERS |
| 5 | UNDOTBS2 |
| 6 | DBRECOVER_TEST |
| 7 | APP01 |
| 8 | APP02 |

Es decir, el espacio de tablas APP01 tiene TS# = 7, mientras que el espacio de tablas APP02 tiene TS# = 8

La tabla FILE$ almacena la información del archivo de datos:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image58.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image58.png)

Lo que necesitamos son las columnas TS# y RELFILE#.

| TS# | RELFILE# |
| --- | --- |
| 0 | 1 |
| 1 | 3 |
| 6 | 5 |
| 4 | 7 |
| 7 | 2 |
| 2 | 4 |
| 7 | 8 |
| 7 | 9 |
| 8 | 10 |
| 8 | 11 |
| 8 | 12 |

Al combinar y mapear los datos de estas dos tablas, se puede obtener:

| TS# | RELFILE# | Tablespace Name |
| --- | --- | --- |
| 0 | 1 | SYSTEM |
| 1 | 3 | SYSAUX |
| 6 | 5 | DBRECOVER_TEST |
| 4 | 7 | USERS |
| 7 | 2 | APP01 |
| 2 | 4 | UNDOTBS1 |
| 7 | 8 | APP01 |
| 7 | 9 | APP01 |
| 8 | 10 | APP02 |
| 8 | 11 | APP02 |
| 8 | 12 | APP02 |

Eliminamos los espacios de tablas innecesarios SYSAUX, UNDOTBS1 y SYSTEM que ya conocemos, luego solo queda:

| TS# | RELFILE# | Tablespace Name |
| --- | --- | --- |
| 6 | 5 | DBRECOVER_TEST |
| 4 | 7 | USERS |
| 7 | 2 | APP01 |
| 7 | 8 | APP01 |
| 7 | 9 | APP01 |
| 8 | 10 | APP02 |
| 8 | 11 | APP02 |
| 8 | 12 | APP02 |

Lista de nombres de archivos de datos correspondientes:

`O1_MF_APP01_L782YY4Y_.DBF.eking`

`O1_MF_APP01_L782ZBM3_.DBF.eking`

`O1_MF_APP01_L782ZCP1_.DBF.eking`

`O1_MF_APP02_L782ZO7W_.DBF.eking`

`O1_MF_APP02_L7830DTG_.DBF.eking`

`O1_MF_APP02_L7830FJ6_.DBF.eking`

`O1_MF_DBRECOVE_L6G7B1Q3_.DBF.eking`

`O1_MF_USERS_L5VP67TJ_.DBF.eking`

---

Al comparar las dos tablas anteriores, no es difícil encontrar la relación correspondiente. Para los archivos de datos que utilizan la gestión de archivos OMF db_create_file_dest, los múltiples archivos de datos debajo de un espacio de tablas se pueden ordenar por su nombre de archivo, y su orden es consistente con el orden de RELFILE#. Para los nombres de archivos gestionados por el usuario (es decir, en casos en los que no se utiliza OMF), generalmente se nombrarán de la manera APP01{XX} (como APP0101, APP0102) para facilitar la gestión, por lo que también se puede obtener su relación correspondiente.

A través de la suposición anterior, obtenemos la tabla de información completa:

| TS# | RFILE# | Tablespace Name | FILE NAME |
| --- | --- | --- | --- |
| 6 | 5 | DBRECOVER_TEST | O1_MF_DBRECOVE_L6G7B1Q3_.DBF.eking |
| 4 | 7 | USERS | O1_MF_USERS_L5VP67TJ_.DBF.eking |
| 7 | 2 | APP01 | O1_MF_APP01_L782YY4Y_.DBF.eking |
| 7 | 8 | APP01 | O1_MF_APP01_L782ZBM3_.DBF.eking |
| 7 | 9 | APP01 | O1_MF_APP01_L782ZCP1_.DBF.eking |
| 8 | 10 | APP02 | O1_MF_APP02_L782ZO7W_.DBF.eking |
| 8 | 11 | APP02 | O1_MF_APP02_L7830DTG_.DBF.eking |
| 8 | 12 | APP02 | O1_MF_APP02_L7830FJ6_.DBF.eking |

Reabrimos DBRECOVER y entramos en el modo de diccionario:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image59.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image59.png)

Aún necesitamos seleccionar la versión de la base de datos DB VERSION.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image60.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image60.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image61.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image61.png)

Incluye todos los archivos de datos necesarios (todos los archivos que puedan contener datos de usuario, UNDOTBS1, TEMP, SYSAUX no necesitan ser incluidos), asegúrate de no olvidar SYSTEM01.DBF (debe ser incluido).

De acuerdo con la tabla que organizamos anteriormente, completa la información de TS# y RFILE# aquí:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image62.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image62.png)

Si completa correctamente la información relevante y el grado de daño de cifrado no es alto, entonces puedes leer directamente los datos:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image63.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image63.png)

Debido a las diferentes características del ransomware, es posible que se necesiten más pasos en la operación real. Te invitamos a comunicarte con nosotros por correo electrónico si tienes problemas: **[service@parnassusdata.com](mailto:service@parnassusdata.com)**

## 

## **Escenario de recuperación 4: Recuperación de filas de datos eliminadas por error DELETE FROM TABLE**

Un desarrollador de la compañía D ejecutó un script para eliminar datos del entorno de prueba, pero se conectó por error al entorno de producción (PROD DATABASE) y eliminó todos los datos de una tabla con DELETE.

En este escenario, podemos usar DBRECOVER para recuperar los datos de las filas que se han eliminado con DELETE.

Sin embargo, necesitamos que el usuario realice las siguientes operaciones para proteger los datos de ser sobrescritos en la mayor medida posible:

1. Configura el espacio de tablas donde se encuentra la tabla en modo solo lectura READ ONLY, el comando es: ALTER TABLESPACE {TABLESPACE_NAME} READ ONLY
2. Detén la instancia de la base de datos: SHUTDOWN IMMEDIATE

El usuario puede elegir uno de los dos planes anteriores.

Reproducir el escenario:

`SQL> select count(*) from pd.emp;`

`COUNT(*)`

`---------`

`114688`

`SQL>`

`SQL> delete from pd.emp;`

`114688 rows deleted.`

`SQL> commit;`

`Commit complete.`

`SQL> alter system checkpoint;`

`System altered.`

`SQL> select count(*) from pd.emp;`

`COUNT(*)`

`---------`

`0`

---

Antes de comenzar la recuperación, primero configuramos el espacio de tablas en modo de solo lectura para proteger el entorno de recuperación:

`SQL> select tablespace_name from dba_segments where owner='PD' and segment_name='EMP';`

`TABLESPACE_NAME`

`-----------------------------`

`DBRECOVER_TEST`

`SQL> alter tablespace DBRECOVER_TEST read only;`

`Tablespace altered.`

---

Iniciamos DBRECOVER, seleccionamos el modo de diccionario e incluimos todos los archivos de datos disponibles:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image64.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image64.png)

Al revisar los datos de la tabla de ejemplo, podemos ver que también están vacíos. Selecciona la tabla, haz clic con el botón derecho y selecciona Unload Deleted Data.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image65.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image65.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image66.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image66.png)

En ausencia de una licencia válida de la edición empresarial, la función UNLOAD DELETED DATA está limitada a 100 filas de datos por tabla.

Los datos extraídos se almacenan en la ruta mostrada en la ventana emergente:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image67.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image67.png)

El usuario debe revisar los resultados de la recuperación y utilizar herramientas como SQLLDR o SQLDEVELOPER para insertar los datos de texto en la base de datos.

## 

## **Escenario de recuperación 5: Recuperación de una tabla truncada por error**

Un empleado de mantenimiento de la compañía D confundió la base de datos de producción con la base de datos de prueba y TRUNCATE todos los datos en una tabla por error. El DBA intentó recuperar los datos pero descubrió que la copia de seguridad más reciente no estaba disponible, por lo que no pudo recuperar los registros de la tabla a partir de la copia de seguridad. En este punto, el DBA decidió utilizar DBRECOVER para recuperar los datos que se habían truncado.

Dado que todos los archivos de la base de datos en este entorno están disponibles y son saludables, el usuario solo necesita cargar el archivo de datos del espacio de tablas SYSTEM y el archivo de datos de la tabla truncada en el modo de diccionario, por ejemplo:

`SQL> select count(*) From pd.salgrade;`

`COUNT(*)`

`---------`

`655360`

`SQL> select tablespace_name from dba_segments where owner='PD' and segment_name='SALGRADE';`

`TABLESPACE_NAME`

`-----------------------------`

`APP01`

`SQL> truncate table pd.salgrade;`

`Table truncated.`

`SQL>`

`SQL> alter system checkpoint;`

`System altered.`

`SQL> select count(*) from pd.salgrade;`

`COUNT(*)`

`---------`

`0`

---

En este escenario de TRUNCATE no se utilizó el almacenamiento ASM, por lo que solo es necesario seleccionar el "Modo de diccionario" (《Dictionary Mode》):

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image68.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image68.png)

En la mayoría de los casos, no es necesario modificar ningún parámetro:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image69.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image69.png)

Agrega todos los archivos de datos disponibles:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image70.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image70.png)

Al abrir USERS, puedes ver varios nombres de usuario. Por ejemplo, si el usuario necesita recuperar una tabla bajo el esquema PD, abre PD y haz doble clic en el nombre de la tabla:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image71.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image71.png)

Dado que esta tabla ya ha sido truncada, hacer doble clic no mostrará datos. En este caso, haz clic derecho en la tabla y selecciona "Unload truncated data":

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image72.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image72.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image73.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image73.png)

DBRECOVER intentará escanear el espacio de tablas donde se encuentra la tabla y extraer los datos que ya han sido truncados: Como se muestra en la imagen anterior, DBRECOVER extrajo un total de 655360 registros completos de la tabla que había sido truncada y los almacenó en la ruta especificada en la notificación.

El usuario puede revisar este archivo DAT para confirmar los resultados de la recuperación.

La clave para recuperar datos truncados es confirmar el DATA_OBJECT_ID de la tabla antes de ser truncada, como en este ejemplo:

`SQL> select object_id ,data_object_id from dba_objects where owner='PD' and object_name='SALGRADE';`

`OBJECT_ID DATA_OBJECT_ID`

`--------- --------------`

`76112 76113`

---

Antes de la operación de TRUNCATE, tanto el OBJECT_ID como el DATA_OBJECT_ID de esta tabla eran 76612. Después de la operación de TRUNCATE, el DATA_OBJECT_ID cambió.

Por lo tanto, el DATA_OBJECT_ID original aquí es 76612; pero si una tabla ha sido truncada muchas veces y necesitas recuperar los datos antes de la última operación de TRUNCATE, no puedes simplemente usar el OBJECT_ID para adivinar el DATA_OBJECT_ID original.

Puedes utilizar técnicas como consultas de flashback, recuperación de diccionario, minería de logs, etc. para determinar el DATA_OBJECT_ID; aquí hay un ejemplo de una consulta de flashback:

`SQL> select user# from sys.user$ where name='PD';`

`USER#`

`---------`

`106`

`SQL> select obj#,dataobj# from sys.obj$ as of timestamp systimestamp -1/24 where name='SALGRADE' and owner#=106;`

`OBJ# DATAOBJ#`

`--------- ----------`

`76112 76112`

---

Como se muestra arriba, hemos obtenido el DATAOBJ# original, es decir, el DATA_OBJECT_ID, a través de una consulta de flashback.

Luego necesitamos usar la característica Data Bridge para insertar los datos a recuperar en la base de datos objetivo. Consideraciones al usar Data Bridge para recuperar datos truncados: ten en cuenta que cuando recuperes datos truncados de la base de datos de origen, si usas la opción Data Bridge para transferir los datos de vuelta a tu base de datos de origen (si los datos no se transfieren de vuelta a la base de datos de origen, este problema no existe), debes asegurarte de que el espacio de tablas en el que se inserta la nueva tabla no sea el espacio de tablas en el que se encuentran los datos truncados en la base de datos de origen, y evita insertar en la tabla original, de lo contrario, puedes tener el problema de que los datos truncados que estás recuperando sean sobrescritos por nuevos datos, lo que puede resultar en la imposibilidad total de recuperar los datos en este escenario de recuperación. Por lo tanto, ten en cuenta que cuando uses Data Bridge + recuperar datos a la base de datos de origen, ¡¡¡¡¡¡¡nunca uses el espacio de tablas donde se encuentran los datos a recuperar cuando especifiques el espacio de tablas en Data Bridge!!!!!!!

Por lo tanto, aquí primero creamos un nuevo espacio de tablas para almacenar la tabla de datos recuperada:

`SQL> create tablespace pd_recover_data datafile size 600M;`

`Tablespace created.`

---

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image74.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image74.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image75.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image75.png)

Crea la información de inicio de sesión necesaria, ten en cuenta que el usuario de la base de datos debe tener los permisos necesarios (se recomienda otorgar el rol de DBA).

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image76.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image76.png)

Después de que la prueba sea exitosa, haz clic en SAVE para guardar.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image77.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image77.png)

Elige el espacio de tablas para almacenar la tabla de datos que se recuperará de TRUNCATE.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image78.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image78.png)

Aquí, debemos seleccionar "if need to scan data" y proporcionar el DATA_OBJECT_ID original que obtuvimos anteriormente. De esta manera, DBRECOVER escaneará específicamente los datos correspondientes a ese ID para nosotros.

Al mismo tiempo, debemos seleccionar "if need to remap table" e ingresar un nuevo nombre de tabla. Esto permite que los datos se inserten en una nueva tabla (en un nuevo espacio de tablas), eliminando cualquier posibilidad de sobrescribir datos.

*Nota:*

1. Para los casos en los que ya existe un nombre de tabla correspondiente en la base de datos objetivo, DBRECOVER no recreará la tabla, sino que insertará los datos a recuperar sobre la base de la tabla existente. Debido a que la tabla ya ha sido creada, el espacio de tablas especificado no será efectivo.
2. Para los casos en los que aún no existe un nombre de tabla correspondiente en el SCHEMA de la base de datos objetivo, DBRECOVER intentará crear una tabla en el espacio de tablas especificado e insertar los datos recuperados.

Después de completar los pasos anteriores, haz clic en el botón Data Bridge.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image79.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image79.png)

Confirma el número de filas a recuperar:

`SQL> select count(*) from pd.salgrade_recover;`

`COUNT(*)`

`---------`

`655360`

---

El principio general de los datos Truncate es que cuando ocurre Truncate, ORACLE solo actualizará el Data Object ID de la tabla en el diccionario de datos y Segment Header, pero no modificará la parte de los bloques de datos reales. Debido a que el DATA_OBJECT_ID en el diccionario de datos y el encabezado de segmento no coincide con los bloques de datos posteriores, el proceso de servicio ORACLE no leerá los datos que han sido truncados pero que en realidad aún no han sido sobrescritos cuando lee todos los datos de la tabla. Por lo tanto, DBRECOVER puede recuperar los datos en ellos a través de las áreas de disco de datos (Data Extent) que no han sido modificadas ni sobrescritas.

## 

## **Escenario de recuperación 6: Recuperación de una tabla eliminada por error (Drop)**

Un desarrollador de aplicaciones de la empresa D eliminó una tabla de aplicación central en el sistema sin ninguna copia de seguridad. En este caso, DBRECOVER puede recuperar la mayoría de los datos de la tabla que se eliminó inmediatamente. A partir de 10g, se proporciona la característica de la papelera de reciclaje (recycle bin), que se puede verificar primero consultando la vista DBA_RECYCLEBINS para determinar si la tabla eliminada está en la papelera de reciclaje. Si está allí, se debe priorizar el flashback a antes de la eliminación mediante la papelera de reciclaje. Si no está en la papelera de reciclaje, se debe utilizar DBRECOVER para recuperar los datos lo antes posible.

La recuperación de una tabla eliminada (Drop) es similar a la recuperación de una tabla truncada (Truncate). Necesitamos determinar el DATA_OBJECT_ID original de la tabla eliminada.

El procedimiento de recuperación es el siguiente:

1. Primero, establezca el espacio de tablas donde se encuentra la tabla eliminada en modo de solo lectura (ALTER TABLESPACE {TABLESPACE_NAME} READ ONLY) o haga una copia de todos los archivos de datos en el espacio de tablas lo antes posible.
2. Encuentra el DATA_OBJECT_ID de la tabla eliminada consultando el diccionario de datos o LOGMINER.
3. Inicie DBRECOVER en modo NON-DICT, y agregue todos los archivos de datos del espacio de tablas donde se encuentra la tabla eliminada. Luego, SCAN DATABASE + SCAN TABLE from Extent MAP.
4. Use DATA_OBJECT_ID para ubicar la tabla correspondiente en el árbol de objetos desplegado, y recupérela en la base de datos original en modo Data Bridge.

Puedes obtener el DATA_OBJECT_ID aproximado utilizando LOGMINER. El script para usar LOGMINER es el siguiente:

`EXECUTE DBMS_LOGMNR.ADD_LOGFILE( LOGFILENAME => '/oracle/logs/log1.f', OPTIONS => DBMS_LOGMNR.NEW);`

`EXECUTE DBMS_LOGMNR.ADD_LOGFILE( LOGFILENAME => '/oracle/logs/log2.f', OPTIONS => DBMS_LOGMNR.ADDFILE);`

`Execute DBMS_LOGMNR.START_LOGMNR(DBMS_LOGMNR.DICT_FROM_ONLINE_CATALOG+DBMS_LOGMNR.COMMITTED_DATA_ONLY);`

`SELECT * FROM V$LOGMNR_CONTENTS ;`

`EXECUTE DBMS_LOGMNR.END_LOGMNR;`

---

También puedes intentar obtener el DATA_OBJECT_ID excavando datos de AWR:

`Select * from`

`(select object_name,object# from DBA_HIST_SQL_PLAN`

`UNION select object_name,object# from GV$SQL_PLAN) V1 where V1.OBJECT# IS`

`NOT NULL minus select name,obj# from sys.obj$;`

`select obj#,dataobj#, object_name from WRH$_SEG_STAT_OBJ where object_name`

`not in (select name from sys.obJ$) order by object_name desc;`

`SELECT tab1.SQL_ID,`

`current_obj#,`

`tab2.sql_text`

`FROM DBA_HIST_ACTIVE_SESS_HISTORY tab1,`

`dba_hist_sqltext tab2`

`WHERE tab1.current_obj# NOT IN`

`(SELECT obj# FROM sys.obj$`

`)`

`AND current_obj#!=-1`

`AND tab1.sql_id =tab2.sql_id(+);`

//Las tres consultas anteriores comparan los datos de AWR con la tabla base del diccionario OBJ$ para descubrir las tablas eliminadas.

---

Hagamos una demostración práctica:

`SQL> create table dropit as select * from dba_objects;`

`Table created.`

`SQL> select count(*) from pd.dropit;`

`COUNT(*)`

`---------`

`73095`

`SQL> select tablespace_name from dba_segments where owner='PD' and segment_name='DROPIT';`

`TABLESPACE_NAME`

`-----------------------------`

`USERS`

`SQL> select object_id ,data_object_id from dba_objects where owner='PD' and object_name='DROPIT';`

`OBJECT_ID DATA_OBJECT_ID`

`--------- --------------`

`76116 76116`

`SQL> drop table dropit;`

`Table dropped.`

`SQL> alter system checkpoint;`

`System altered.`

---

Iniciamos DBRECOVER en modo de diccionario (DICTIONARY-MODE). Aquí solo necesitamos agregar SYSTEM01.DBF y el espacio de tablas USERS donde se encuentra la tabla:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image80.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image80.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image81.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image81.png)

Una vez que se completa la carga, podemos ver que la tabla que queremos recuperar no existe bajo el esquema PD. Esto es normal.

Selecciona el nodo de la base de datos y haz clic con el botón derecho en SCAN Data.

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image82.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image82.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image83.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image83.png)

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image84.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image84.png)

Luego aparecerá un nodo EXTENTS, busca el nodo OBJ76116:

![Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image85.png](Manual%20de%20usuario%20de%20dbrecover%20for%20oracle%20bb43ca104735411fa827d12a357c147b/image85.png)

Luego podemos usar la característica Data Bridge para insertarla de nuevo en la base de datos de origen.

## **Escenario de recuperación 7: Recuperación de un espacio de tablas eliminado por error (DROP TABLESPACE)**

Un empleado de la empresa D necesita eliminar un espacio de tablas inútil, es decir, realizar la operación DROP TABLESPACE INCLUDING CONTENTS. Pero después de la operación DROP TABLESPACE, el departamento de desarrollo informa que en realidad había datos de un SCHEMA útiles e importantes en el espacio de tablas que se eliminó, pero ahora el espacio de tablas se ha eliminado y no hay ninguna copia de seguridad.

En este caso, podemos usar el modo NON-DICTIONARY de DBRECOVER para extraer los datos de todos los archivos de datos correspondientes al espacio de tablas eliminado. A través de este método, podemos recuperar la mayoría de los datos, pero dado que es un modo NON-DICTIONARY, necesitamos hacer coincidir las tablas recuperadas con las tablas de datos de la aplicación una por una. En este momento, generalmente se necesita la intervención del personal de mantenimiento de desarrollo de aplicaciones, quienes identifican manualmente a qué tabla pertenecen los datos. Como la operación DROP TABLESPACE modificó el diccionario de datos y eliminó los objetos en OBJ$ correspondientes al espacio de tablas, no podemos obtener la relación correspondiente entre DATA_OBJECT_ID y OBJECT_NAME desde OBJ$. En este momento, podemos usar el método introducido en el escenario DROP TABLE para obtener tantas relaciones correspondientes entre DATA_OBJECT_ID y OBJECT_NAME como sea posible.

El proceso aproximado es el siguiente:

Si los archivos de datos también se eliminaron físicamente cuando se eliminó el TABLESPACE, entonces es necesario recuperar primero los archivos de datos. Se puede intentar con un software de recuperación a nivel de sistema de archivos, o utilizar el software PRMSCAN para escanear y reorganizar los archivos de datos desde el nivel de bloque de datos de ORACLE.

PRMSCAN es una herramienta de escaneo y fusión de fragmentos de bloque de datos de ORACLE, que es aplicable a los siguientes escenarios:

1. Se eliminó manualmente el archivo de datos en el sistema de archivos (cualquier sistema de archivos NTFS, FAT, EXT, UFS, JFS, etc.) o ASM por error.
2. El sistema de archivos está dañado, lo que hace que el tamaño del archivo de datos se convierta en 0 bytes, es decir, el archivo de datos se borra.
3. El sistema de archivos está dañado, lo que hace que el sistema de archivos no pueda MOUNT.
4. Los metadatos de almacenamiento ASM están dañados, lo que hace que el diskgroup no pueda montarse.
5. El LV o PV del sistema de archivos o ASM está físicamente dañado o perdido.
6. Todos los escenarios anteriores pueden utilizar prmscan para escanear directamente los bloques de oracle residuales no sobrescritos en el PV o LV correspondiente del sistema de archivos o ASM, para lograr la fusión y reorganización de estos bloques de datos de oracle, con el fin de lograr la recuperación de datos.

PRMSCAN se desarrolla en lenguaje JAVA, puede cruzar todos los sistemas operativos que admiten JDK 1.6 y posteriores, incluyendo Windows, Linux, Solaris, AIX, HP-UX.

Actualmente, este producto no se ofrece al por menor, puede ponerse en contacto con nosotros para proporcionar servicios de recuperación.

Por ejemplo, en el siguiente caso, /dev/sdb1 es una partición del sistema de archivos ext4, pero debido a que el sistema de archivos ext4 está dañado, SDB1 no puede montarse, pero este sistema de archivos almacena los archivos de datos de una base de datos oracle. Si no se puede montar el sistema de archivos, la base de datos oracle tampoco se puede utilizar.

Aquí utilizamos la función de escaneo y fusión de bloques de archivos de datos de oracle de prmscan, para reorganizar directamente los archivos de datos desde el sistema de archivos dañado.

Escanea todo el disco:

`[oracle@dbdao01 ~]$ java -jar PRMScan.jar –scan /dev/sdb1 –guess 8k`

`–scan opción representa escanear el dispositivo /dev/sdb1, y especificar Oracle blocksize como 8k`

`[oracle@dbdao01 ~]$ java -jar PRMScan.jar –outputsh ./8kfull.txt`

`–outputsh representa escribir un archivo SHELL que puede fusionar la información ya escaneada, es decir, aquí 8kfull.txt`

`[oracle@dbdao01 ~]$ sh 8kfull.txt`

`Ejecutar 8kfull.txt puede generar todos los archivos de datos que necesitan ser fusionados en el directorio actual`

`Como se muestra abajo`

`[oracle@dbdao01 ~]$ ls -ll PD*`

`rw-r–r– 1 oracle oinstall 295428096 Jul 28 00:37 PD_DBF1.dbf`

`rw-r–r– 1 oracle oinstall 83427328 Jul 28 00:37 PD_DBF2.dbf`

`rw-r–r– 1 oracle oinstall 220266496 Jul 28 00:37 PD_DBF3.dbf`

`rw-r–r– 1 oracle oinstall 1324482560 Jul 28 00:38 PD_DBF4.dbf`

---

Si el archivo de datos no ha sido eliminado físicamente, puede agregarlo directamente al DBRECOVER en modo sin diccionario (NON-DICTIONARY MODE) y escanear los datos dentro.

Los siguientes pasos se pueden referir a la operación DROP TABLE anterior, la diferencia es que el objeto de recuperación de DROP TABLESPACE será muchas tablas.
