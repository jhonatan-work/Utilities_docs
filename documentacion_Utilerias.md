# Utilerías

Contenido clase Utilerías


- [Inicio](#inicio)
- [Fecha](#fecha)
- [Usuario de ejecucion](#usuarioEjecucion)
- [Registro de Ejecuciones](#registroejecuciones)
- [Semanas Proceso](#semanasproceso)
- [Var Semanas Proceso](#varsemanasproceso)
- [Var Anio Proceso](#anioProceso)
- [Guardar Siguiente Ejecucion](#savesiguienteejecucion)
- [Semana Proceso de una Tabla](#semanaProcesoDF)




<hr>


## Inicio

Iniciar e importar la clase.

```python
spark.sparkContext.addPyFile("utilerias.py")
from utilerias import Utilerias
initClass = Utilerias(spark)
```

<hr>


## fecha

Devuelve la fecha actual en formato datetime y unixtime.

Uso:
``` python
fecha_dt, fecha_unix, dia_unix = initClass.fecha()
fecha_dt = initClass.fecha()[0]
fecha_unix = initClass.fecha()[1]
dia_unix = initClass.fecha()[2]
```

Salida fecha_dt:
```python
datetime.datetime(2023, 1, 26, 12, 7, 9, 378540, tzinfo=<DstTzInfo 'America/Mexico_City' CST-1 day, 18:00:00 STD>)
```

Salida fecha_unix:
```python
1674756429
```

Salida dia_unix:
```python
1674712800
```

<hr>


## usuarioEjecucion

Devuelve el nombre de usuario de ejecucion

No necesita ningun parametro de entrada

Uso:
```python
usuario_ejecucion = initClass.usuarioEjecucion()
```

Salida usuario_ejecucion:
```python
'94179'
```

<hr>


## registroEjecuciones

Devuelve el nombre del proceso y la fecha de su ejecución, únicamente para ciertos procesos semanales.

Parámetros de entrada: Nombre del proceso a ejecutar.

Procesos registrados actualmente:
 - 'wf_cu_portafolio_fenix_master_portafolios'
 - 'wf_cu_portafolio_fenix_indicadores_territoriales'
 - 'cu_portafolio_fenix_acampaniamiento_proceso'

Uso:
```python
nombre_proceso, ejecucion = initClass.registroEjecuciones(
				'cu_portafolio_fenix_acampaniamiento_proceso')
nombre_proceso = initClass.registroEjecuciones(
				'cu_portafolio_fenix_acampaniamiento_proceso')[0]
ejecucion = initClass.registroEjecuciones(
				'cu_portafolio_fenix_acampaniamiento_proceso')[1]
```
Salida nombre_proceso:
```python
'cu_portafolio_fenix_acampaniamiento_proceso'
```

Salida ejecucion:
```python
datetime.date(2022, 12, 11)
```

<hr>


## semanasProceso

Calculo de un numero especifico de semanas proceso a partir del día indicado.

Parámetros de entrada: Numero de semanas a calcular y fecha de la que partirá el calculo.

Uso:
```python
semanasprocesos = initClass.semanasProceso(3, fecha_dt)

```

Salida:
```python
['202303', '202302', '202301']
```

<hr>


## varSemanasProceso

Cambia el formato de las semanas proceso calculadas anteriormente, a únicamente 2 dígitos en formato string. 

Parámetros de entrada: Semanas proceso calculadas anteriormente.

Uso:
```python
varSemanasProceso = initClass.varSemanasProceso(semanasprocesos)
```
Salida:
 ```python
['03', '02', '01']
 
```

<hr>


## anioProceso

Devuelve los 4 digitos del anio en formato string.

Parámetros de entrada: Semanas proceso calculadas anteriormente.

Uso:
```python
var_anioproceso = initClass.anioProceso(semanasprocesos)
```
Salida:
 ```python
['2023', '2023', '2023']
 
```

<hr>


## saveSiguienteEjecucion

Guarda la fecha de ejecución siguiente para la generación de semanas proceso

Parámetros de entrada: Numero de dias para la siguiente ejecución, ejecución anterior y nombre del proceso que se ejecuta.

Uso:
```python
initClass.saveSiguienteEjecucion(7,ejecucion,nombre_proceso)
```

 <hr>


## semanaProcesoDF

Parámetros de entrada: Tabla de la cual se requiere traer la semana proceso maxima.

Uso:
```python
TABLA_ENTRADA = ENV + 'cu_portafolio_fenix_relaciones_establecidas_historica'
semanaproceso_max, semana_proceso, semana_encurso = initClass.semanaProcesoDF(TABLA_ENTRADA)

semanaproceso_max = initClass.semanaProcesoDF(TABLA_ENTRADA)[0]

semana_proceso = initClass.semanaProcesoDF(TABLA_ENTRADA)[1]

semana_encurso  = initClass.semanaProcesoDF(TABLA_ENTRADA)[2]
```

Salida semanaproceso_max:
```python
'202303'
```

Salida semana_proceso:
```python
2023
```

Salida semana_encurso:
```python
3
```

<hr>
