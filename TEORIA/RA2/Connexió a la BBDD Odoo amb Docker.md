# **Connexió a la BBDD Odoo amb Docker**

## **1. Comandes a Docker**

* Llistar els contenidors actius:
  `docker ps`
* Obrir un shell dins del contenidor de la base de dades:
  `docker exec -it odoo-docker-test-db-1 bash`
* Sense connectar-nos a la base de dades:

  * Llistar les bases de dades del contenidor:
    `docker exec -it odoo-docker-test-db-1 psql -U odoo -l`
  * Connectar-se al contenidor:

    `docker exec -it odoo-docker-test-db-1 psql -U odoo -d mydb`

## **2. Comandes bàsiques a psql (ja dins del contenidor)**

* Llistar totes les bases de dades disponibles des del shell del contenidor:
  `psql -U odoo -l`
  Això mostra totes les bases de dades. Exemples típics: `postgres`, `template0`, `template1`, i la base de dades real d'Odoo (per exemple `mydb`, `odoo`, `odoo19`).
* Connectar-se a la base de dades correcta:
  `psql -U odoo -d nombre_de_la_base`

Exemple: `psql -U odoo -d mydb`

* Sortir del client psql:
  `\q`
* Reiniciar el buffer de consulta si el prompt canvia a `mydb-#`:
  `\r`
* Veure a quina base de dades estàs connectat:
  `SELECT current_database();`

## **3. Exploració de la base de dades**

* Llistar totes les taules de l'esquema actual:
  `\dt`
* Llistar les taules de tots els esquemes:
  `\dt *.*`
* Veure l'estructura d'una taula concreta:
  `\d res_partner`

## **4. Consultes SQL útils**

* Veure alguns registres de la taula res_partner:
  `SELECT id, name, email, is_company, customer_rank FROM res_partner LIMIT 10;`
* Veure alguns registres de la taula res_partner:
  `select id, name, description, description_sale, categ_id, list_price, volume, weight, company_id from produt_tmplate order by id;`;

## **5. Consells**

* `docker exec … psql`: entrar a la base de dades correcta
* `\dt`: llistar taules
* `\d nombre_tabla`: veure l'estructura
* `SELECT …`: consultar registres
* `\q` i `\r`: sortir o reiniciar quan el prompt canvia a `-#`
