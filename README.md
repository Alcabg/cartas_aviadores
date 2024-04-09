# Juego de cartas de aviadores de la Primera Guerra Mundial.

Este proyecto (work in progress) se basa en un juego de cartas donde se puede seleccionar a dos aviadores para que compitan entre ellos haciendo click en los botones de selección. Gana aquel aviador que tenga más victorias. 
Además cuenta con un input para que se pueda filtra la carta deseada.

## Sobre el proyecto
Dentro del directorio *src* hay un fichero JSON llamado *pilots* donde hay 15 ases de la aviación con la siguiente estructura:
"id": 1,
  "nombre_aviador": "Manfred von Richthofen",
  "victorias": 80,
  "nacionalidad": "Alemana",
  "fecha_nacimiento": "02/05/1892",
  "fecha_muerte": "21/04/1918",
  "avion_pilotado": "Fokker Dr.I",
  "img":"src/assets/manfred.jpg"
  }

  Para añadir más aviadores tan solo se deben incluir aquellos que se deseen en el fichero JSON y automáticamente se renderizarán.
