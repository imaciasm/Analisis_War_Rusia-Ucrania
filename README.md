# Analisis_War_Rusia-Ucrania
Análisis de redes sociales - Minería de datos con Tweepy y Networkx y visualización de grafos mediante la herramienta Gephi.

## Caso de estudio

El tema elegido para enfocar esta práctica es la guerra entre Rusia y Ucrania
que comenzó el 24 de febrero del 2022 y que sigue siendo noticia en la actualidad.
Este conflicto permite realizar diferentes estudios de relaciones y comunidades desde
distintos enfoques y perspectivas, teniendo en cuenta cómo los actores del conflicto
interactúan, además de observar como sus acciones y decisiones afectan al resto de
comunidades y sociedades involucradas en la lucha.

Para llevar a cabo este estudio se ha recogido información dentro de la red
social twitter de varias fuentes distintas, entre las que se encuentran los gobiernos
asociados, periodistas de guerra implicados a este evento y otros usuarios de la red,
los cuales comparten sus opiniones acompañados de etiquetas o más comúnmente
llamados hashtags, que permiten identificar estos hechos. Los datos mencionados han
sido recolectados cerca de algunas fechas importantes a tener en cuenta:

* 21 de diciembre de 2022- El presidente de Ucrania, Volodymyr Zelensky viajó a Washington y se reunió con el presidente de Estados Unidos, Joe Biden y se pronunció ante el Congreso. Biden y Zelensky mostraron un frente unido en su planteamiento sobre la guerra que Rusia mantiene en Ucrania.

* 23 de diciembre de 2022- El presidente de Rusia, Vladimir Putin, utilizó la
palabra "guerra" para referirse al conflicto en Ucrania, la primera vez que se
alejó públicamente de su descripción cuidadosamente elaborada de la invasión
de Moscú como una "operación militar especial" 10 meses después de que esta
comenzara.
* 26 de diciembre de 2022- Las defensas anti-aéreas rusas abaten sobre el
aeródromo "Engels" (región de Sarátov) un dron ucraniano que, al caer, mata a
tres militares, según el Ministerio de Defensa de Rusia.
* 27 de diciembre de 2022- Las tropas ucranianas confirman la toma de Dibrova
y Chervonopopivka, pequeñas localidades al oeste y al norte de Kreminná,449
en el Óblast de Lugansk.
* 29 de diciembre de 2022- Cuando se encrudece más la guerra y Rusia propina
un ataque masivo con misiles contra Ucrania. Lo que provocó que Ucrania
sufriera una nueva jornada de ira e indignación, luego de que Rusia sometiera a
la población a uno de los mayores ataques desde que comenzó la
guerra, disparando decenas de misiles.
* 1 de enero de 2023- Un bombardeo masivo ucraniano con misiles HIMARS
sobre Makéyevka (Donetsk) mata a 63 militares rusos, según fuentes rusas, o a
400 según fuentes ucranianas.
* 4 de enero de 2023- El presidente de Francia, Emmanuel Macron, le confirma a
Zelenski que enviará a Ucrania vehículos blindados sobre ruedas AMX-10 RC.

Extracción de información y preparación del grafo

El primer paso antes de proceder a cualquier tipo de operación es obtener las credenciales de Twitter, ya que son estas las que nos van a dar permiso para poder utilizar su API. Para ello se ha seguido los siguientes pasos:

1. Crear una cuenta de Twitter: para utilizar la API de Twitter, primero debes tener una cuenta de Twitter. De no tener una cuenta, se debe crear una en la página web de Twitter.
2. Crear una cuenta de desarrollador: Una vez creada la cuenta tenemos que acceder a la página de desarrolladores de Twitter, aplicar y seguir las instrucciones que proporcionan.
3. Crear una aplicación: Una vez creada la cuenta de desarrollador, se debe crear un proyecto y una aplicación en nuestro sitio web de desarrolladores.
4. Obtener credenciales: una vez que hayas creado tu aplicación, debes obtener las credenciales necesarias para autenticarte y utilizar la API. Estas credenciales incluyen tu clave de consumidor y tu clave secreta de consumidor, así como tu token de acceso y tu token secreto de acceso.
5. Autenticación: para poder utilizar la API, debes autenticarte utilizando tus credenciales.

Para llevar a cabo la recolección se ha hecho uso de la biblioteca de Python tweepy mediante la debida autenticación para acceder a la API de Twitter en combinación con la biblioteca de Python Networkx que nos permite analizar y manipular los datos obtenidos. Se han utilizado funciones de tweepy que permiten hacer cosas como buscar y recuperar tweets e información sobre ellos como puede ser el ID único del tweet, la suma de likes y retweets que contienen, la fecha en la que se creó o la ubicación entre otras opciones. Por otro lado, también nos permite obtener información sobre el usuario que creo el tweet como nombre de usuario, su ID, el número de seguidores y el número de usuarios a los que se sigue entre las opciones disponibles.

Finalmente se ha obtenido un total de 3 grafos distintos con diferentes puntos de información entorno al mismo tema. Para la descarga y procesado de cada uno de ellos se ha llevado unos procesos y tiempos distintos por lo que se ha tenido que llevar a cabo estrategias diferentes.

1. Grafo Gobiernos

Este grafo se ha generado a raíz de las relaciones que tienen los usuarios @KremlinRussia_E y @DefenceU con otros usuarios a los que se sigue dentro de la red social. Cada usuario (target) representa un nodo y cada relación de amistad (source) se representa como una arista, creando una conexión entre ambos. A su vez, una vez obtenida las primeras relaciones, se ha procedido a hacer lo mismo con cada amigo recogido, generando de esta manera un árbol genealógico de amistad. Esta puede ser una herramienta útil para visualizar como las personas están conectadas entre sí y como se comunican, además de ayudar a identificar patrones, tendencias en las relaciones de amistad y comprender mejor la dinámica del grupo.

Para la descarga se ha utilizado la función get_friends de tweepy, esta es una función que se utiliza para obtener información sobre los usuarios que sigue a otro usuario determinado, sus nombres de usuario, nombres reales, sus descripciones, etc., además, se ha combinado con la función cursor que permite obtener un gran número de resultados de la API en una única petición, puesto que por norma general tan solo se puede obtener un número limitado por cada solicitud. Finalmente se obtienen dos conjuntos de datos distintos, el del usuario @KremlinRussia_E con un total de 11442 registros y un tiempo de descarga de aproximadamente 5 horas y el del usuario @DefenceU con un total de 29689 registros y un tiempo de descarga aproximado de 12 horas. Una vez combinados obtenemos el conjunto de datos final con un total de 41130 registros, de los cuales obtenemos el siguiente grafo de 28886 nodos y 39116 aristas.

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/a6b1ede9-e9bb-4362-ad6c-dfcaa5c0e1bc)

2. Grafo Periodistas

Para generar este grafo se han seleccionado usuarios de la red que son reporteros de guerra y se dedican a cubrir las noticias sobre los acontecimientos que están ocurriendo de manera profesional, de esta de manera, obtenemos tweets creados por dichas cuentas y que están relacionados directamente con el tema a tratar. Entre ellos se encuentran:

* @marcmarginedas (Marc Marginedas)
* @fpleitgenCNN (Frederik Pleitgen)
* @CristianSeguraA (Cristian Segura)
* @mchancecnn (Matthew Chance)

Para la descarga se ha utilizado la función user_timeline de tweepy, esta función permite obtener tweets de usuarios específicos en Twitter. Junto con la función cursor, la API retorna un objeto con todos los tweets encontrados que hayan sido creados por el usuario en cuestión, también se han excluido los tweets replicados e incluido los retweets de dichos usuarios. Una vez obtenida la información se ha accedido a ellos utilizando una estructura de datos de lista, pudiendo elegir las características de los tweets que más nos interesaban para el estudio. Finalmente se obtienen 4 conjuntos de datos distintos, un total de 2467 tweets y retweets del usuario @marcmarginedas (Marc Marginedas), 2894 tweets y retweets del usuario @fpleitgenCNN (Frederik Pleitgen), 2876 tweets y retweets del usuario @CristianSeguraA (Cristian Segura) y 2473 tweets y retweets del usuario @mchancecnn (Matthew Chance). Una vez combinados se ha obtenido un conjunto de datos con un total de 10710 tweets y retweets, el tiempo total invertido para estas descargas ha sido de aproximadamente 30-40 minutos. Para terminar y antes de proceder a la creación del grafo se han separado los datos obtenidos en dos conjuntos de datos diferentes, estos contienen información de los usuarios (nodos) e información de los tweets y retweets (aristas) por separado. A continuación, se muestra el grafo generado a raíz de los datasets mencionados con los que se obtienen 1879 nodos y 2071 aristas.

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/26098409-7216-4fe0-8367-2411205a4eeb)

3. Grafo Hashtags

Para generar este grafo se ha utilizado palabras clave o combinaciones de estas, de manera que obtenemos los tweets que están relacionados directamente con el tema seleccionado, entre las opciones se encuentran:

* #UkraineRussiaWar 
* #Guerra #Putin #Ucrania 
* #Guerra #Rusia #Ucrania 
* #Putin #Zelenski

Para la descarga se ha utilizado la función search_tweets de tweepy, esta función permite buscar tweets que cumplan ciertos requisitos, en este caso, tweets que contengan los hashtags mencionados. Junto con la función cursor, la API retorna un objeto con todos los tweets encontrados que cumplen con los criterios de búsqueda especificados en la consulta. Se han excluido los tweets replicados e incluido los retweets. Una vez obtenida la información se ha accedido a ellos utilizando una estructura de datos de lista, pudiendo elegir las características de los tweets que más nos interesaban para el estudio. Finalmente se obtienen 4 conjuntos de datos distintos, tweets con el hashtag #UkraineRussiaWar y un total de 16650 registros, tweets con la combinación de hashtags #Guerra #Putin #Ucrania con un total de 103 registros, tweets con la combinación de hashtags #Guerra #Rusia #Ucrania con un total de 550 registros y tweets con la combinación de hashtags #Putin #Zelenski con un total de 169 registros. Una vez combinados se ha obtenido un conjunto de datos con un total de 17472 registros, el tiempo total invertido para estas descargas es de aproximadamente 1 hora. Para terminar y antes de proceder a la creación del grafo se ha separado la información obtenido en dos conjuntos diferentes que contienen información de los usuarios (nodos) e información de los tweets (aristas). A continuación, se muestra el grafo dirigido generado con el que obtenemos 9164 nodos y 10451 aristas.

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/6e99b041-9ae2-4a2d-a7f8-9f4008e4347e)

## Memoria

1. Grafo gobiernos

Características:

Inicialmente, el grafo está compuesto por 28886 nodos y 39116 aristas. Tiene un grado medio de 1,354, lo que indica que cada nodo se conecta a ese número de nodos en promedio. Esto es debido a la gran cantidad de nodos que tiene la red. En cuanto a la densidad, es prácticamente 0 y el diámetro de la red es de 7 con una longitud media de camino de 3,12.

Para una mejor visualización del grafo, se ha aplicado una distribución ForceAtlas 2 y se aplica un filtrado k-core de 3. Esto provoca una reducción de nodos y aristas, quedando 1721 (5,96% visible) y 9673(24,75% visible) respectivamente.

Identificación de comunidades:

El grafo tiene una modularidad de 0,764 lo que identifica 24 comunidades sin modificar ningún parámetro. Debido a que resulta un número muy elevado, en primer lugar, se ha aplicado una resolución de 6, obteniendo una modularidad de 0,504 y 7 grupos pero, como en este conflicto, además de los 2 países combatientes, intervienen muchas más partes se ha aplicado únicamente una resolución de 2, obteniendo así una modularidad de 0,73 y 12 comunidades diferentes.

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/996007f8-d65f-4f7b-adde-cb4e70e5cd09)

Como se puede observar, es muy difícil ver de una forma clara la composición de cada comunidad por lo que es necesario, mediante el “Laboratorio de datos”, comprobar a quién representa cada nodo para tener una idea aproximada de la descripción de cada comunidad.

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/62805570-206d-4df6-af6a-705c5e4c759a)

Los más influyentes

Además de conocer las distintas comunidades que pueden salir de este grafo, se ha estudiado qué nodos han sido más influyentes durante las fechas de las que se han extraído los datos. Para realizar esto, se ha hecho uso del mismo grafo de los gobiernos, pero, en esta ocasión y aprovechando los cálculos anteriores se seleccionan, mediante el Laboratorio de Datos, los 25 nodos con un mayor valor en Betweenness Centrality (medida utilizada en nodos no ponderados), ya que son aquellos nodos que sirven de puente para el paso de la información.

Tras la obtención del grafo se puede observar que NATO y DefenceU son los nodos más influyentes. Tras estos se encuentran otros como jensstoltenberg, oleksiireznikov, mblaszczak, Obama o EmmanuelMacron. Todos ellos organizaciones y altos cargos de algunos países afines a Ucrania (Polonia o Finlandia), menos mfa_russia como gobierno ruso.

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/6d91c3c0-460b-4a2b-9aca-c30f515a71be)

2. Grafo Periodistas

Características:

Este grafo está compuesto por 1879 nodos y 2071 aristas. El grado medio es de 1,1 y tiene un diámetro de 2, por lo que es un grafo pequeño. Tiene una modularidad de 0,636 y su densidad es de 0,001.

Estos grafos permiten estudiar la interacción en twitter que han tenido 4 periodistas de guerra. Para ello ha sido necesario obtener las menciones hacía distintos medios o personalidades que hacían en sus tweets. Tras esto, se han generado 4 distintos (1 por periodista). De cada uno se ha tenido que obtener la componente gigante ya que contenían nodos aislados y, además, distribuciones ForceAtlas 2 y Noverlap (con margin de 100) y Ajuste de etiquetas para mejorar la visibilidad.

Grafo Cristian Segura

Compuesto, tras limpiar, por 77 nodos y 201 aristas. Tiene un rango medio de 1,37 y un diámetro de 21. Tiene una densidad de 0,034 ya que es más pequeño que los anteriores. Su modularidad es de 0,684.

Destacan en el grafo las interacciones con los otros periodistas estudiados @marcmarginedas, @fpleitgenCNN, @mchancecnn (mucha interacción), así como con algunos medios de comunicación tales como @elperiodico, @elpais o @CNN

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/5af544bd-4691-4edc-aef9-4ee4ce752c91)

Grafo Frederik Pleitgen

Se ha realizado una reducción del rango de grado a 4 para eliminar algunos nodos menos importantes. Con este cambio el grafo queda compuesto por 66 nodos y 144 aristas. Tiene un grado medio de 1,346 y un diámetro de 12.

Tras aplicar un tamaño de etiqueta en función del grado, se destaca que las interacciones más importantes han sido él mismo (debido a que el mensaje es de tipo Tweet, no solo retweet), y también otros usuarios como @CNN, @ronzheimer o @MAStrackZi. Dentro de su red también destacan usuarios como @Bundeskanzler, @ZelenskyyUA, @SecBlinken o @BorisJohnson.

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/9c6ee89a-8b52-48d4-a4a4-9d770c370d79)

Grafo Marc Marginedas

Para realizar el grafo de este periodista, primero se ha sometido a eliminar aquellos nodos cuyo rango de grado fuera menor de 5. Tras esto se obtiene un grafo pequeño, con 36 nodos y 87 aristas. En este caso, el grado medio es de 1,35 y el diámetro de la red es de 10. La densidad, al igual que casos anteriores es cercana a 0 (0,069)

Una vez realizadas las transformaciones y las modificaciones en las etiquetas, se consigue obtener un grafo donde se observa claramente la alta actividad con @elperiodico. Igual que sucede con Frederik Pleitgen, su nombre aparece muy resaltado por el tipo de mensaje. La interacción principalmente se mantiene con otros periodistas.

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/1e205230-d332-49fa-a4c3-1570f5c79542)

Grafo Matthew Chance

El grafo de Matthew también ha sido filtrado por rango de grado, en este caso 4. Tras esta operación, el grafo resultante tiene 30 nodos y 47 aristas, queda muy pequeño, pero para el caso que ocupa suficiente. Sus características principales son que su diámetro es de 4, con un grado medio de 1,28 y una densidad de 0,054.

Este periodista mantiene interacción con algunos medios de comunicación como @CNN, @XsovietNews, @NATOPress. Como dato a destacar es que bastantes nodos que aparecen forman parte de cnn como @CNNPR, @cnni, @LconeCNN entre otros. También aparece @realDonalTrump o @clarissaWard peridista estadounidense.

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/03b2c800-4f8a-4ea2-a287-6feff953bedd)

3. Grafo Hashtags
   
Características:

El grafo de hashtags está compuesto por 9164 nodos y 10451 aristas. Tiene un grado medio de 1,14 y la red es de diámetro 3. La densidad es prácticamente 0, ya que contiene muchos nodos.

Este gráfico permite realizar un pequeño análisis de los hashtags que los usuarios de Twitter han utilizado durante las fechas de obtención de los datos. Para realizar esto, se han extraído las etiquetas de todos los mensajes que contenían los tweets y se ha creado una matriz. Una vez cargado se realiza un filtrado k-core de 5 y, además, un Rango de grado donde se reduce en 1 el máximo, para que no aparezca la palabra clave #UkraineRussiaWar (ya que ha sido utilizada para capturar los tweets principalmente)

Se puede observar en el grafo que los hashtags con un mayor grado son #Ukraine, #Russia, #Russian. En un nivel algo inferior se encuentran #Putin, #UkraineWar y, finalmente #RussiaUkraineWar, #RussiaIsLossing, #RussianArmy, #StandWithUkraine, #guerra (en español) o #COVID19.

![image](https://github.com/imaciasm86/Analisis_War_Rusia-Ucrania/assets/141320922/1ba166dd-1523-4fbf-a362-bc63896700d0)

## Conclusiones

En este estudio se investigó el conflicto actual entre Rusia y Ucrania a través de diferentes grafos obtenidos de Twitter, con el objetivo de proporcionar diferentes puntos de vista. Podemos destacar varios puntos:

1. Gracias a las comunidades observadas podemos concluir que si bien el conflicto es a nivel nacional tiene un alcance mundial. Se observa colectivos muy concretos, entre los que se encuentran políticos, periodistas o entidades gubernamentales, tanto dentro de la UE como fuera e incluso otras entidades de otros continentes como es el ministerio de defensa de Australia o Canadá.
2. Se ha podido observar que Ucrania y la OTAN tienen una mayor influencia mediática en el conflicto, algo normal teniendo en cuenta el apoyo que está recibiendo el país por parte de la UE, lo que denota un mayor apoyo y una mayor afinidad por Ucrania.
3. Gracias a la red creada por los periodistas se observa quienes son los principales noticiarios que se informan con mayor regularidad y de primera mano por los reporteros de guerra, podemos destacar los periódicos españoles elperiodico, elpais o cadenas de noticias como la CNN.
4. Se aprecia que en la mayoría de resultados el usuario ZelenskyyUA (Presidente de Ucrania) se sitúa de intermediario, lo que denota una alta actividad en la red social utilizando este medio como una herramienta para hacer campaña democrática.
5. Si bien, descartando #UkraineRussiaWar, los hashtags utilizados para las búsquedas son #Guerra #Putin #Zelenski #Rusia y #Ucrania, se ha obtenido como resultado que el hashtag #Ukraine se ha visto utilizado en muchos más tweets que el resto de palabras. Esto nos indica que la mayoría de sucesos y el apoyo de los usuarios de la red social tiene mucho mayor impacto en Ucrania en comparación con Rusia.

De querer ampliar el análisis sería recomendable realizar un estudio más exhaustivo para comprender mejor las diferentes comunidades involucradas en el conflicto. Esto requiere una investigación más a fondo de los actores involucrados y los motivos que los ligan a una determinada comunidad. También se podría utilizar técnicas de análisis de sentimientos para examinar el lenguaje utilizado en los tweets relacionados con el conflicto, lo que podría proporcionar información valiosa sobre las actitudes y las emociones de los usuarios. Además, se podrían comparar los resultados del análisis de Twitter con otras fuentes de información, como encuestas de opinión, noticias y datos de otras redes sociales, para obtener una visión más completa de la opinión pública en torno al conflicto.

## Bibliografía

Documentación sobre uso de API Twitter:

https://developer.twitter.com/en/docs

Documentación sobre uso de Tweepy:

https://docs.tweepy.org/en/stable/

Información sobre el conflicto:

https://www.nytimes.com/article/ukraine-russia-war-timeline.html

Búsqueda reporteros guerra ruso-ucraniana:

https://www.google.es/search?q=reportero+guerra+ucrania+rusia&sxsrf=ALiCzsYtx0jTjltDT_7-vnKAGdpoNSVFkQ%3A1672911057131&source=hp&ei=0Zi2Y8X2BfKhkdUPyrKUoAw&iflsig=AJiK0e8AAAAAY7am4e2Ofu6hnRPmzJ1V4k8AilsylL_8&oq=&gs_lcp=Cgdnd3Mtd2l6EAEYAjIHCCMQ6gIQJzIHCCMQ6gIQJzIHCCMQ6gIQJzIHCCMQ6gIQJzIHCCMQ6gIQJzIHCCMQ6gIQJzIHCCMQ6gIQJzIHCCMQ6gIQJzIHCCMQ6gIQJzIHCCMQ6gIQJ1AAWABgrA9oAXAAeACAAQCIAQCSAQCYAQCwAQo&sclient=gws-wiz
