# big-data-architecture-practica

Los materiales utilizados se encuentran en el siguiente link [https://drive.google.com/open?id=1Zo9X4UgySbc1dv8Ng9T6FkxanCr8zbDd]
Además de encontrarse en el repositorio de gitlab.

Práctica.

# 1. Selección del dataset
   Utilizamos un dataset que se ha obtenido scrapeando de Airbnb. Es un archivo en formato csv que pesa 57.5 MB y que contiene 14.780 registros. 
Además obtenemos un data-set de muestra de la página de milanuncios que se ha obtenido scrapeando.
  Para que los ficheros sean más amigables se ha utilizado Talend Data Preparation para su limpieza, borrando todas las filas que contengan valores vacíos de las columnas que se consideran más relevantes.

# 2.Diseñar, especificar y desplegar un datalake para el procesamiento de datos provenientes de fuentes de datos no estructurados extraídos mediante técnicas de scraping/crawling de sitios de dominio público.
   ## Definición de la estrategia del DAaas
   Se utiliza un dataset de airbnb una plataforma especializada en compra/venta y alquiler de apartamentos y una muestra aleatoria de unos 80 pisos scrapeada en una plataforma no especializada en compra/venta de pisos. La idea del funcionamiento de este datalake es poder analizar las palabras más y menos usadas en la plataforma especializada vs la plataforma no especializada. Para ello se ha montado un cluster y se ha hecho un wordcount. Posteriormente se ha creado un script de R para hacer un gráfico de nube de palabras (que nos muestra en mayor tamaño las palabras más utilizadas y las menos utilizadas). Después de pasar este gráfico a pdf y subirlo a un drive, se enviará este gráfico al departamento de publicidad/marketing o usuarios que quieran comparar el uso de las palabras en plataformas especializadas y no especializadas en la compra venta de pisos
       NOTA: El pdf se sube a drive por la propia estructura del scrip que envia los correos automáticos a los mismos usuarios. Más adelante se explicará su funcionamiento.
   ## Arquitectura DAas
      
De manera local tenemos:
	Dos ficheros csv , uno de ellos (mil anuncios) sacado scrapeando la web y otro de ellos (airbnb) tratado  en talend preparation para limpiar sus datos.
De manera cloud tenemos:
	Un cluster montado en google cloud que cuenta con un nodo maestro y un nodo esclavo . También Se ha subido a Google Storage los archivos para su uso.
Posteriormente:	
	Contamos con un scrip de R que a través de los resultados obtenidos nos genera el gráfico  que guardamos en pdf y subimos a drive.
	Después de subirlo a drive utilizamos la herramienta de Envio de correos (está hecha en hojas de google-excel) para enviarlo a los distintos usuarios

Aqui tenemos el mapa de la arquitectura: [https://drive.google.com/open?id=1k1Ryu6HYV1hT5u0Dw3FycVBCDsPjbakx6QrE_1T1TQc]

   ## DAas Operation Model Design and Rollout
   
Tratar fichero airbnb en talend preparation 
Crawlear los datos de mil anuncios
Cargar los datos en el cluster y hacer wordcount
Con el output obtener la nube de puntos y generar pdf
Subir pdf a una carpeta de drive y copiar enlace para compartir en la herramienta de envio de correos
   
   ## Desarrollo de la plataforma DAas 

El primer paso consiste en realizar la limpieza del fichero airbnb.csv en Talend Preparation.
El segundo paso consiste en scrapear  la página milanuncios, filtrando por pisos de la comunida de Madrid  [Podemos encontrarlo en el collaboratory Scrawling mil anuncios: https://colab.research.google.com/drive/1FavHWZJXa9SJWPZN6OnhwTKHeym-2QWf]

El tercer paso y más laborioso, consiste en montar un cluster, subir los archivos a Google storage y realizar los wordcount: [El desarrollo, aunque aquí también lo ponga,se puede ver aqui más comodamente (En el drive: Desarrollo de PROCESO CLUSTER EN LA NUBE) 
                  







