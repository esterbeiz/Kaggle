# Kaggle
Trabajos realizados en el proyecto Kaggle
Explicación de Notebooks adjuntos:

1.- 1_carga: Partimos de los datos facilitados por el tutor inicialmente con los que realizamos la carga incial de esos mismos datos. Con ellos obtenemos los archivos: 'teams.csv' y 'competitions.csv'. Con ambos realizamos los primeros EDA's y nos permiten obtener una aproximación al problema.

2.- 2_teams: Como indicamos en el punto 1, partimos del fichero 'teams.csv'. Tenemos un fichero de 148336 filas y 13 columnas, descrito en el propio notebook. Con el presente notebook hemos realizado un análisis somero con los siguientes pasos:

    -Evolución de los equipos participantes en las diferentes competiciones en cada uno de los años.
    -Equipos con más medallas de oro.
    -Cómo se comportan estos equipos, si están formados por varios competidores o por uno solo.
    
 Con este dataframe, finalmente no hemos continuado avanzando por el momento al realizar el scrapeo de datos detallado en la memoría y que serían nuestros datos definitivos.
 
3.- 3_competitions: Dataframe obtenido a partir del 'competitions.csv'. Estamos ante un dataframe con 149 filas (competiciones) y 25 columnas. Tras una limpieza inicial de los datos, realizamos los siguientes análisis:

    -Número de equipos que participan en cada una de las competiciones.
    -Posible relación entre el número de participantes en cada una de las competiciones y su premio asignado.
    -Evolución de las competiciones a lo largo del tiempo. Notándose un incremento de las mismas sobre todo a partir del año 2015.
     
 Igual que con el dataframe descrito en el punto 2, no continuamos, ya que la intención es obtener una mayor cantidad de datos con el scrapeo realizado y poder realizar un análisis mucho más amplio.
 
 En ambos casos, no los descartamos del todo, ya que pueden resultar útiles para análisis futuros.
 
 
 
4.- 4_Dataframe_Competitions_INFO: Partimos de 'info_competitions.xlsx', fichero en formato excel que obtenemos realizando el scrapeo desde la plataforma de Kaggle (detallado en la memoría). Con esto obtenemos el total de las competiciones activas actualmente en Kaggle, un total de 339 filas (competiciones) con 7 columnas (descritas en notebook).
 Realizamos una exhaustiba limpipieza de los datos para obtener aquellos que nos interesan para nuestros análisis futuros y así obtener el archivo 'Competitions_limpio.csv'. Archivo que usaremos en notebooks que detallaremos más adelante, y que se usará para realizar un análisis previos con uso de herramientas de visualización y para el estudio de series temporales (descrito en la memoria).
 
 
5.- 5_Dt_LeaderBoard_Public_limpio: Iniciamos el Notebook con el archivo 'Dt_leaderBoard_public.csv', obtenido igualmente realizando el scrapeo desde la plataforma de Kaggle (detallado en la memoria). 
 Con ello tenemos un dataframe compuesto de 1.258.620 filas (aportaciones de cada uno de los equipos a cada una de las competicones) y 6 columnas.
 La intención incial con este conjunto de datos es obtener los siguientes datos:
    -Score: Puntuación obtenida por cada uno de los equipos en la competición Public.
    -Total de 'entries' por competición: Número de kernels que cada equipo aporta a la competición. Totalizado por competiciones (en este punto nos estamos encontrando con problemas, ya que no coinciden con los datos esperados).
    -TeamName: Nombre del equipo.
    -TeamId: Id del equipo.
    
 Con los datos una vez limpios, se pretende unir con el dataframe descrito en el punto 4 (4_Dataframe_Competitions_INFO) y con el info_teams_Private, para realizar los análisis predictivos y estudio en cuanto a variación de los equipos entre las clasificaciones inciales y finales (Public vs Private).
 
 Se genera 'public_para_join.csv' para su posterior uso.
 
 
6.- 6_JOIN_DT: Basicamente se trata de la unión de los dataframes descritos en el punto 4 y 5, una vez limpios y preparados para su uso en estudios posteriores y desarrollo de los objetivos fijados en el presente trabajo.


7.- 7_info_teams_Private: Partimos del fichero de texto 'private.txt', con este cargamos un primer dataframe, que tras las modificaciones oportunas nos permite generar el fichero 'Dt_Teams_Private_Info_Raw.csv', este sí, punto de partida para el notebook.
 Es necesario indicar, que en esta extracción de datos se continua trabajando actualmente, para obtener el total de competiciones y los equipos que participan en ella.
 En profundidad, tendríamos:
    -Evaluation Score: Método usado para evaluar la competición
    -entries: Total de entries por equipo en cada una de las competiciones.
    -Nombre del equipo.
    -El ranking que ha ocupado finalmente el equipo (Private).
    -Score private.
    -Miembros del equipo.
    -Nombre de la competición, que nos servirá para realizar un posterior 'join'.
    -Cambio de posiciones en Public vs Private.
    -Fecha.
    
 Tenemos un dataframe con 795 filas y 9 columnas. ('Dt_Teams_Private_Info_Raw_LIMPIO.csv')
 
 Finalmente, filtramos datos y agrupamos para obtener un nuevo dataframe con los siguientes datos ('title_entries_team.csv'):
    -Nombre de la competición.
    -Entries totales por competición.
    -Número de equipos participantes.
    
 COMO INDICAMOS AL PRINCIPIO DE ESTE PUNTO, SE TRATA DE UN ANÁLISIS REALIZADO CON UNA MUESTRA DE 3 COMPETICIONES. La finalidad es realizar la unión con el dataframe descrito en el punto 6. Puede unirse con dataframe 4_Dataframe_Competitions_INFO para posteriormente realizar la unión con el 5_Dt_LeaderBoard_Public_limpio.
 PROBLEMAS ENCONTRADOS: El objetivo es realiza la unión con el dataframe del punto 6 mediante TeamId o TeamName y entries, de forma que tengamos una doble comprobación y perdamos la menor cantidad de datos posibles. 
 Las ENTRIES, no coinciden por lo que habrá que revisar el dataframe del punto 5(5_Dt_LeaderBoard_Public_limpio), de forma que podamos llegar a la unión que se pretende.
 
 
8.- 8_Prueba_join_competitions_private: Realizado con 'Dt_competitions_info.csv' y 'title_entries_team.csv'. Se realiza con éxito la únion de ambos dataframe obteniendo uno nuevo con la siguiente información:

    -Fecha.
    -Nombre de la competición.
    -Premio de la competición.
    -Topic. Tipo de competición.
    -Total de entries por en cada competición.
    -Número de equipos participantes: Aquí puede existir variación entre el número de equipos debido a que estos varian según la fecha de extracción de datos.
    
 COMO SE INDICA ANTERIORMENTE ESTA PRUEBA SE REALIZA CON UNA MUESTRA DE LAS COMPETICIONES (3 COMPETICIONES)
 
 
9.- 9_EDA_Dt_Competitions: Con el dataframe '4_Dataframe_Competitions_INFO', realizamos un EDA en el que podemos ver, equipos participantes por competición, como evoluciona el número de las competiciones en el tiempo y el número de participantes por año. Se puede ver un repunte significativo a partir del año 2015.
    
    
    
A FUTURO:

10_Cadena_teams Y 11_TeamMembers. Aproximación básica a la extración y generación de datos para aplicar al objetivo de generación de grafos explicado en el presente trabajo.
 
    
 
 
