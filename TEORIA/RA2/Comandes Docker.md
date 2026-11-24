### **Comandes per gestionar contenidors**

**docker compose up \-d**

**docker compose \-p \<nombre-del-contenedor\> up \-d**

* Crea los contenedores definidos en el **`docker-compose.yml`**   
* Conecta los contenedores / servicios en red (**`odoo`, `db`, etc**.)  
* Aplica los mapeos de puertos  
* Los arranca en segundo plano gracias al **\-d** (detached)

**docker compose down**

* Detiene todos los contenedores del **docker-compose.yml**  
* Elimina los contenedores  
* Elimina la red interna  
* Elimina los volúmenes anónimos  
* Mantiene los volúmenes nombrados en **docker-compose.yml**

**docker compose down \--volumes**

* Detiene todos los contenedores del **docker-compose.yml**  
* Elimina los contenedores  
* Elimina la red interna  
* Elimina los volúmenes anónimos  
* Elimina los volúmenes nombrados en **docker-compose.yml**

**docker compose stop**

* Detiene los contenedores  
* Conserva su estado, volúmenes y red  
  **docker compose rm**  
* Elimina los contenedores ya parados  
* Conserva su estado, volúmenes y red  
  **docker compose rm \-v**  
* Elimina los contenedores ya parados y sus volúmenes anónimos  
* Conserva los volúmenes nombrados en **docker-compose.yml** y la red  
  **docker compose rm \--volumes**  
* Es la forma larga de **-v**: hace exactamente lo mismo (contenedores parados y volúmenes anónimos; conserva los volúmenes nombrados y la red)

**docker compose start**

* Reactiva los contenedores detenidos  
* Restaura la red interna

**docker ps**

* Contenedores en ejecución  
* Puertos mapeados  
* Nombres y estado  
  **docker exec \<nom\_del\_contenidor\> bash**  
* Abrir un shell dentro del contenedor de la base de datos:

### **Comandes per gestionar volums**

Cuando levantamos un contenedor, se crea un volumen que coje el nombre que le demos dentro del archivo yml en volúmenes 

**Ejemplo: volumes:  odoo-db-data:**

y a ese nombre se le añade el nombre de la carpeta donde hemos levantado el contenedor, así los volúmenes siempre son únicos. A no ser que nombremos el contenedor al levantarlo.  
	

**docker volume ls**

* Lista los volúmenes de cada contenedor

**docker prune**

* Elimina todos los volúmenes huérfanos (su identificador es un nombre largo alfanumérico)  
* **IMPORTANTE:** Hay algunos que parecen huérfanos pero en realidad están asociados a contenedores y entonces hay que pararlos con un **docker stop** y eliminarlos con un **docker rm**

**docker ps \-a \--filter volume=\<nombre del volumen\>**

* Nos dice a qué contenedor pertenece el volumen

**docker volume rm \<nombre\_del\_volumen\>**

* Elimina el volumen

