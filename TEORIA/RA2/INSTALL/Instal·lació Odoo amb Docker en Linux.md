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
    volumes:
      - ./config:/etc/odoo
      - odoo-web-data:/var/lib/odoo
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
  odoo-web-data:
```

**IMPORTANT!!** Abans d'aixecar els contenidors, creeu la carpeta `config` al costat d'aquest `docker-compose.yml` amb el fitxer `odoo.conf` a dins (vegeu la teoria del RA2, apartat «Fitxer de configuració odoo.conf»).

**IMPORTANT!!** El volum `odoo-web-data` guarda les imatges, adjunts i sessions d'Odoo; sense ell es perden cada vegada que es torna a crear el contenidor. No feu servir mai `docker compose down -v`, perquè esborra els volums i, amb ells, totes les bases de dades.

### **4. Aixecar els contenidors**

Executar:

`docker compose up -d`

Verificar que els contenidors estan en marxa:

`docker ps`

### **5. Accedir a Odoo**

Obrir el navegador a:

**http://localhost:8069**

Configurar la base de dades inicial i començar a fer servir Odoo. Al camp **Master Password** cal posar la mateixa contrasenya que l'`admin_passwd` de l'`odoo.conf`; els altres camps del formulari s'expliquen a la teoria del RA2.
