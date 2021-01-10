---
title:  "¡Hello World!"
date:   2016-08-25
published: true
---

El siguiente post tiene como finalidad analizar logs de apache  y le permitirán a un [**CERT**](https://es.wikipedia.org/wiki/Equipo_de_Respuesta_ante_Emergencias_Inform%C3%A1ticas) toma decisiones en base a los análisis de los mismos y también responder algunas preguntas comunes cuando somos víctimas de un ataque o simplemente queremos saber: Tendencias, flujo de trafico y muchas cosas mas.

Si bien es cierto que existen miles de herramientas y con resultados mejores de los que mostrare acá , nunca esta demás crear o diseñar algo que se controle completamente y en su momento superar a las herramientas ya existentes. R es rápido consume pocos recursos también es importante para respuestas tipo estadísticas.

Entonces, ¿Qué me puede enseñar este post?

+ Cómo podemos utilizar el análisis de datos para acelerar nuestras respuesta y mejorar en base a las lecciones aprendidas
+ Cómo debemos aprovechar la programación  con más frecuencia en respuesta a incidentes
+ Cómo podemos desarrollar nuestras propias herramientas y metodología analítica

Esto no está tratando de reemplazar tus practicas y programas actuales. Simplemente añadirá una herramienta más en su caja de herramientas y depende de ti de cómo  usarlo.

Lo primero que debemos hacer es cargar las librerías/bibliotecas necesarias 

+ library(readr)
+ library(rgeolocate)
+ library(dplyr)
+ library(IPtoCountry)
+ library(lubridate)
+ library(ggplot2)

Una vez hecho esto comenzamos a cargar nuestros datos, pero hay que tener algunos detalles en cuenta:

Los datos que usare de muestra son reales (El archivo de logs).

Debemos conocer el formato de los logs (Web/Apache). Aca esta: [**Common Log Format**](https://en.wikipedia.org/wiki/Common_Log_Format)

Procederemos a cargar los datos ("access.log").

~~~R
logs <- read_log("access.log", skip=0, col_names=FALSE)
~~~

Una vez cargados necesitaremos saber cual es el nombre de las columnas de nuestro dataframe/tabla con lo siguiente:

~~~R
colnames(logs)
[1] "X1"  "X2"  "X3"  "X4"  "X5"  "X6"  "X7"  "X8"  "X9"  "X10"
~~~

Luego filtramos los datos que nos interesan, puede ser en una variable distinta o en la misma ya que dependerá de los gustos, pero yo prefiero conservar el original para otras pruebas. 

~~~R
final <- logs[,c('X1','X4','X5','X6','X7','X8','X9')]
~~~

Teniendo casi listo los datos procederemos a colocar nombre a las columnas para hacerlo mas amigable.

~~~R
filtrado <- setNames(final, c("ip_address", "date_time", "to_url","http_status","client_size","URL", "User-agent"))
~~~

Ahora acá lo que haré sera tratar de insertar una columna adicional la cual este asociada a la ip a la ciudad/país.(Vea que creo otra variable, pero la puedes hacer en la misma).

~~~R
city <-mutate(.data = filtrado,country = IP_country(ip_address))
~~~

Ahora viene una parte que debo confesar da algo de dolor de cabeza y es trabajar con datos tipo fecha/date. No porque **R** no pueda, mas bien porque siempre he tenido problemas con ello, así que colocare varias maneras de hacerlo.

la columna `date_time` ahora está registrado como tipo de datos "carácter", pero sabemos que esto se supone que es información de fecha y hora que registra cuando se hicieron las solicitudes. Y dbemos cambiarla a tipo `POSIXct` que es un formato date para R Para verificar el tipo de dato usamos:

~~~R
class(city$date_time)
~~~

Ahora hay varias maneras de hacer esto: 

Si tenemos algo como esto 03/Mar/2016:18:22:16 en la columna `date_time` se puede usar esto:

~~~R
as.POSIXct(gsub('Mar','03',city$date_time))  
~~~

Eso se hace para cambiar/reemplazar la palabra 'Mar' por '03' que es el numero del mes de Marzo

También podemos usar un formato específico.

~~~R
as.POSIXct(strptime(city2$date_time,"%d/%m/%Y:%H:%M:%S"))
~~~

Una vez visto las maneras en que se puede hacer (Existen mas), decidí hacerlo así:

~~~R
city2$date_time <-(gsub('Mar','03',city$date_time))
~~~

~~~R
city2$date_time = as.POSIXct(strptime(city2$date_time,"%d/%m/%Y"))
~~~

Lo cual se traduce a: Crear una variable nueva llamada city2 (por si dañaba la anterior) y transformar la columna `date_time` a el formato correcto `as.POSIXct`

Y ahora tenemos un dataframe/tabla mas manejable para hacer nuestro gráficos sencillos y complejos. Acá solo esta una muestra de lo que se puede hacer, ya que en post anteriores se han  hecho mapas y otras representaciones mas amigable de este tipo de datos.

Se muestran a continuación:

~~~R
table(city2$http_status)
reqs=as.data.frame(table(city2$date_time))
n=23
~~~

~~~R
counts <- table(city2$country, city2$date_time)
barplot(counts, main="Ciudad vs http_status",xlab="Dias",ylab = "http_status", col=c(topo.colors(n)),legend = rownames(counts)) 
~~~

**HTTP-STATUS**

![](/images/http.png)

~~~R
ggplot(data=reqs, aes(x=as.Date(Var1), y=Freq), title('trafico del sistio')) + geom_line() + xlab('Date') + ylab('Requests')
~~~

**REQUEST**

![](/images/req.png)


**Numero de ataques por ciudad/país** 

~~~R
mytable <- table(city2$country)
lbls <- paste(names(mytable), "\n", mytable, sep="")
pie(mytable[1:10], labels = lbls,
    main="Ciudades / Países\n (Nº ataques)")
~~~

![](/images/torta.png)

~~~R
HACKED!
~~~
