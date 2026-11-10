## **Instal·lació d'Odoo amb Docker a Linux**

### **1. Preparació de l'entorn**

Actualitzar els paquets:

`sudo apt update && sudo apt upgrade -y`

Instal·lar Docker i Docker Compose:

`sudo apt install docker.io docker-compose-v2 -y`  
`sudo systemctl enable docker`  
`sudo systemctl start docker`

**IMPORTANT!!** Cal el paquet `docker-compose-v2` (no `docker-compose`), perquè és el que permet fer servir la comanda `docker compose` (amb espai). Si la vostra distribució no el té, instal·leu `docker-compose` i, a la resta de la guia, escriviu la comanda amb guió: `docker-compose up -d`.

Afegir el vostre usuari al grup `docker` per poder fer servir Docker sense `sudo`:

`sudo usermod -aG docker $USER`

Perquè el canvi tingui efecte, cal tancar la sessió i tornar-la a obrir (o reiniciar l'equip). Si no, les comandes `docker` donaran l'error «permission denied».

### **2. Crear els directoris de treball**

Carpeta principal per a Odoo:

`mkdir ~/odoo-docker && cd ~/odoo-docker`

### **3. Configurar `docker-compose.yml`**

Dins de la carpeta d'Odoo, crear el fitxer docker-compose.yml:

```yaml
services:
  odoo:
    image: odoo:19
    depends_on:
      - db
    ports:
      - "8069:8069"
    environment:
      - HOST=db
      - USER=odoo
      - PASSWORD=odoo
  db:
    image: postgres:15
    environment:
      - POSTGRES_USER=odoo
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_DB=postgres
    volumes:
      - odoo-db-data:/var/lib/postgresql/data
volumes:
  odoo-db-data:
```

**IMPORTANT!!** Si voleu fer servir un fitxer de configuració `odoo.conf` (per exemple, per fixar la Master Password), cal afegir un volum al servei `odoo` d'aquest `docker-compose.yml`. Vegeu la teoria del RA2, apartat «Fitxer de configuració odoo.conf».

### **4. Aixecar els contenidors**

Executar:

`docker compose up -d`

Verificar que els contenidors estan en marxa:

`docker ps`

### **5. Accedir a Odoo**

Obrir el navegador a:

**http://localhost:8069**

Configurar la base de dades inicial fent servir **admin** per a les contrasenyes i **mydb** com a nom de la base de dades, i començar a fer servir Odoo.
