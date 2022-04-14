# Actividad dirigida 2
En este apartado de la actividad dirigida 2 ponemos el **código en bruto completo en la parte de abajo** para explicar lo que hemos realizado en la otra actividad llamada [scraping.ipynb](https://github.com/nebrijas/Periodismodedatos_juancamilobohorquez/blob/main/scraping.ipynb).

# Librerías 
Este es el primer paso, importamos la **librería requests** para identificar el sitio web con el que haremos el scraping. Además, importamos la **lebrería BeautifulSoup** para analizar los datos obtenidos en formato HTML o XML. 

# Variables
El siguiente paso es definir las variables, definimos la URL de donde queremos sacar los datos ("https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/") y es la misma URL donde haremos la peticion `request.get` para obtener los datos. Damos la instrucción de que si el status code es distino **if (req.status_code != 200)** no se puede hacer web scraping y si **req.status_code == 200** el código imprimirá "Vamos a por ello".

# Datos
Las variables escogidas son **países, oros, platas, bronces y medallas totales**, para identificarlas debemos poner la función find_all() para que las busque en el sitio escogido y las seleccione. Se va a repetir la instrucción 20 veces (**for ifor i in range (20)**), esto quiere decir, que es un bucle. El código imprimirá los números con %d y el texto con %s.

# Pregunta
La pregunta es para que haya interacción con el usuario y sepa que datos estamos mostrando. Hacemos la pregunta "¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?". En el caso de que la persona pulse la tecla s, entonces significará que sí, el código imprime "De acuerdo".

```
from bs4 import BeautifulSoup
import requests
#Datos sobre los Juegos Olímpicos en 2020

respuesta=input('¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?\n \n Si tu respuesta es Sí, presiona "s" \n')
if(respuesta == 's'):
  print('\nRESULTADOS DE LOS DATOS DE LOS JUEGOS OLÍMPICOS 2020\n')
  print ('PAÍSES')
  URL = "https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"
  # Realizamos la petición a la web
  req = requests.get(URL)
  # Si el estatus code no es 200 no se puede leer la página
  if (req.status_code != 200):
    raise Exception("No se puede hacer Web Scraping en"+ URL)
  # Pasamos el contenido HTML de la web a un objeto BeautifulSoup()
  html = BeautifulSoup(req.text, "html.parser")
  # Obtenemos todos los divs donde están las entradas
  paises = html.find_all("th",{"class":"pais"})
  oros = html.find_all("td",{"class":"m_oro"})
  platas = html.find_all("td",{"class":"m_plata"})
  bronces = html.find_all("td",{"class":"m_bronce"})
  totales = html.find_all("td",{"class":"m_total"})
  for i in range (20):
    # Con el método "getText()" no nos devuelve el HTML
    print("%d. %s \nOro: %s Plata: %s Bronce: %s \n Total: %s \n " % (i+1, paises[i+1].text.strip(),oros[i].text.strip(),platas[i].text.strip(),bronces[i].text.strip(), totales[i].text.strip()))

else:z
  print('Qué lástima, y...')
  
```
