# Odoo

# Instal·lació

Odoo és un programari que funciona sobre una base de dades, en aquest cas PostgreSQL. Odoo té una interfície visual amb mòduls/apps que es poden activar o desactivar, i on cada mòdul té una sèrie de funcionalitats.

En instal·lar Odoo amb l’instal·lador de Windows podem veure que també s’instal·la PostgreSQL, perquè és la BD on s'emmagatzema la informació. Amb Docker o amb els paquets de Linux, PostgreSQL s’instal·la a part.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_install.png" width="500"/><br>

Una vegada completat el procés d’instal·lació inicial, se’ns demana la creació de la base de dades de la nostra empresa

<img style="border-radius: 5px;" src="../../img/RA2/odoo_install_2.png" width="400"/><br>


**Camps del formulari de creació de la base de dades:**

1. Master Password (Contrasenya mestra)

* **Funció:** Controla l'accés a la gestió de bases de dades des del *Database Manager* d’Odoo.  
* **Serveix per a:**  
  * Crear noves bases de dades  
  * Esborrar bases de dades existents  
  * Fer còpies de seguretat o restaurar-les  
* **Què hi posem:** Una contrasenya que recordem, per exemple `Mestra_2627` (dada inventada). Si Odoo ja n'hi proposa una de generada automàticament, la podem deixar, però **l’hem d’apuntar**.  
* **Important:** No és la contrasenya d’un usuari dins d’Odoo, sinó una clau d’administració global per a la instància.

2. Database Name (Nom de la base de dades)

* **Funció:** És el nom intern de la base de dades de l’empresa. Una mateixa instal·lació d’Odoo pot tenir diverses bases de dades (una per empresa).  
* **Què hi posem:** El nom de l’empresa en minúscules, sense espais ni accents, per exemple `technova` (dada inventada).

3. Email (Correu electrònic)

* **Funció:** És el nom d’usuari (*login*) del primer usuari administrador de la base de dades. És el que escriurem a la pantalla d’inici de sessió.  
* **Què hi posem:** Un correu, per exemple `admin@technova.cat` (dada inventada). No cal que sigui un correu real; també s’hi pot posar simplement `admin`.

4. Password (Contrasenya de l’usuari administrador)

* **Funció:** És la contrasenya del primer usuari administrador que es crea dins la nova base de dades.  
* **Serveix per a:**  
  * Accedir a l’entorn d’Odoo amb l’usuari del camp *Email*  
  * Configurar mòduls, usuaris, permisos, etc.  
* **Què hi posem:** Una contrasenya que recordem, per exemple `Admin_2627` (dada inventada).  
* **Important:** Aquesta contrasenya només afecta la base de dades que estàs creant en aquell moment.

5. Phone number (Telèfon)

* **Funció:** Telèfon de contacte de l’usuari administrador. És opcional.  
* **Què hi posem:** Es pot deixar en blanc o posar-hi, per exemple, `600 000 000` (dada inventada).

6. Language (Idioma)

* **Funció:** Idioma de la interfície d’Odoo per a aquesta base de dades.  
* **Què hi posem:** `Catalan / Català` o `Spanish / Español`.

7. Country (País)

* **Funció:** Determina la localització de l’empresa: moneda, impostos (IVA) i pla comptable que Odoo configurarà per defecte.  
* **Què hi posem:** `Spain`.

8. Demo data (Dades de demostració)

* **Funció:** Si es marca, Odoo omple la base de dades amb dades d’exemple (clients, productes, comandes...) per poder provar els mòduls.  
* **Què hi posem:** El marquem si la base de dades és per practicar. No el marquem si és per a l’empresa amb què treballarem a les activitats, perquè després aquestes dades no es poden esborrar fàcilment.

Finalment, premem **Create database**. Pot trigar uns minuts; quan acabi, entrarem a Odoo amb l’usuari del camp *Email* i la contrasenya del camp *Password*.

# Procés general d’instal·lació d’un sistema ERP-CRM

Més enllà dels passos concrets d’Odoo (contrasenyes i creació de la base de dades), el procés general d’instal·lació d’un ERP-CRM segueix aquests passos:

1. **Comprovació de requisits previs:** maquinari mínim (CPU, RAM, disc) i sistema operatiu compatible.  
2. **Instal·lació del sistema gestor de bases de dades** (PostgreSQL en el cas d’Odoo) i creació de l’usuari que utilitzarà l’aplicació.  
3. **Instal·lació del programari ERP-CRM** (paquet natiu, codi font, o contenidor Docker).  
4. **Primera execució i configuració inicial:** creació de la base de dades de l’empresa i definició de les contrasenyes d’administració.  
5. **Instal·lació/activació dels mòduls necessaris** segons les necessitats de l’empresa.  
6. **Configuració de xarxa i accessos** (port, domini, HTTPS) perquè els usuaris hi puguin accedir.  
7. **Càrrega de dades inicials** (importació de clients, productes, etc.) si es disposa de dades prèvies.

# Fitxer de configuració odoo.conf

Odoo llegeix la seva configuració del fitxer `odoo.conf`. A la imatge Docker oficial, aquest fitxer és a `/etc/odoo/odoo.conf` dins del contenidor. Si el volem modificar, el creem nosaltres a la carpeta del projecte i el muntem al contenidor.

**1. Estructura de carpetes**

```
la_meva_carpeta/
├── docker-compose.yml
└── config/
    └── odoo.conf
```

**2. Contingut de `config/odoo.conf`**

```ini
[options]
admin_passwd = Mestra_2627
db_host = db
db_port = 5432
db_user = odoo
db_password = odoo
addons_path = /mnt/extra-addons
data_dir = /var/lib/odoo
```

* `admin_passwd`: és la **Master Password** (contrasenya mestra) que demanarà el *Database Manager*. `Mestra_2627` és una dada inventada; poseu-hi la vostra.
* `db_host`, `db_port`, `db_user`, `db_password`: connexió amb el contenidor de PostgreSQL. Han de coincidir amb el servei `db` i les variables del `docker-compose.yml`.
* `addons_path`: carpeta on Odoo busca mòduls addicionals (a més dels que porta de sèrie).
* `data_dir`: carpeta on Odoo desa el *filestore* (adjunts i imatges).

**3. Muntar-lo al `docker-compose.yml`**

Al servei `odoo` hi afegim l'apartat `volumes` perquè la carpeta `config` del projecte substitueixi `/etc/odoo` del contenidor:

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

**4. Aplicar els canvis**

Cada vegada que es modifica `odoo.conf` cal reiniciar el contenidor d'Odoo perquè el torni a llegir:

`docker compose restart odoo`

# Tipus d’instal·lació

Els sistemes ERP-CRM es poden instal·lar seguint diferents arquitectures:

* **Monolloc (o monopuesto):** tota l’aplicació (interfície, lògica de negoci i base de dades) s’instal·la en un únic equip, i només aquest equip hi pot accedir. Adequada per a autònoms o microempreses amb un únic lloc de treball.  
* **Client-servidor:** el sistema s’instal·la en un servidor central (que allotja la base de dades i, sovint, la lògica de negoci) i els usuaris hi accedeixen des de diferents equips client de la xarxa local (LAN). Permet treball multiusuari i centralitza la informació.  
* **Al núvol (cloud):** el sistema s’allotja en servidors externs i s’hi accedeix via internet des de qualsevol lloc amb un navegador. Redueix la necessitat d’infraestructura pròpia i facilita l’accés remot i l’escalabilitat.

# Modalitats de desplegament

**Odoo Enterprise**

* Odoo Online (SaaS)  
  * Odoo allotja el sistema al seu propi núvol.  
  * No cal preocupar-se per servidors, actualitzacions ni manteniment: tot està gestionat per Odoo.  
  * El pagament és per usuari/mes + mòduls, i inclou hosting i suport.  
  * És la forma més senzilla i ràpida d’usar Enterprise.  
* Odoo.sh (PaaS)  
  * És una plataforma al núvol gestionada per Odoo, però amb més flexibilitat que el SaaS.  
  * Permet personalitzar codi, instal·lar mòduls propis i fer integracions.  
  * Odoo s’encarrega de la infraestructura, però tu tens més control sobre el projecte.  
* On-premise (instal·lació pròpia)  
  * També pots instal·lar Odoo Enterprise en els teus servidors locals o en un núvol privat.  
  * Aquí el cost de llicència segueix sent per usuari/mes, però el hosting i manteniment van a càrrec teu o del teu partner.

**Odoo Community**

* **On-premise (servidors locals o privats)**  
  * Instal·lació directa en servidors de l’empresa.  
  * Dona control total sobre configuració, seguretat i personalització.  
  * Requereix coneixements tècnics interns o suport d’un partner.  
  * Ideal per organitzacions que volen independència i adaptar el sistema a mida.  
* **Cloud hosting (núvol privat o proveïdor extern)**  
  * Odoo Community es pot allotjar en serveis com AWS, Azure, Google Cloud o proveïdors locals.  
  * Escalabilitat i flexibilitat, amb menys inversió inicial en infraestructura.  
  * El cost depèn del proveïdor de núvol i del manteniment contractat.  
  * Molt utilitzat per pimes que volen evitar la gestió de servidors físics.  
* **Docker / Containers**  
  * Desplegament mitjançant imatges Docker, molt popular per a entorns de desenvolupament i producció.  
  * Facilita la **reproductibilitat** i la gestió de versions.  
  * Permet escalar ràpidament i integrar-se amb pipelines DevOps.  
  * És una opció recomanada per equips tècnics que busquen modularitat i rapidesa en desplegaments.  
* **Entorns híbrids**  
  * Combinació de servidors locals i núvol (per exemple, base de dades en núvol i aplicació en local).  
  * Dona flexibilitat, però requereix una gestió més complexa.

# Actualització del sistema ERP-CRM

Mantenir el sistema actualitzat és fonamental per garantir la seguretat i el bon funcionament de l’ERP-CRM:

* **Actualització de mòduls:** quan es modifica el codi d’un mòdul (propi o de tercers) cal actualitzar-lo perquè Odoo apliqui els canvis a la base de dades (nous camps, vistes, dades per defecte). Es fa des de **Apps**, seleccionant el mòdul i triant l’opció **Actualitzar**.  
* **Actualització de versió major** (p. ex. d’Odoo 17 a Odoo 18): sol requerir un procés de migració, ja que poden canviar l’estructura de dades i l’API.  
* **Bones pràctiques abans d’actualitzar:**  
  * Fer una còpia de seguretat (backup) de la base de dades abans de qualsevol actualització.  
  * Provar l’actualització primer en un entorn de proves/preproducció abans d’aplicar-la a producció.  
  * Revisar el registre de canvis (*changelog*) del mòdul o versió per detectar incompatibilitats.  
* **Odoo Online (SaaS):** les actualitzacions les gestiona el mateix Odoo de forma automàtica. **On-premise / Odoo.sh:** la responsabilitat d’actualitzar recau en l’empresa o el partner tècnic.


# Privilegis

Els privilegis d’un usuari són els següents:

<img style="border-radius: 5px;" src="../../img/RA2/odoo_privi.png" width="400"/><br>

## Grups de seguretat (Rols funcionals)

Els **grups** són conjunts d'usuaris que comparteixen certs permisos o funcionalitats. 

* Usuari de Vendes  
* Usuari d’Inventari  
* Usuari de Comptabilitat  
* Administrador de Projectes

És la **capa superficial**: Controlen quins mòduls, menús i pantalles pot veure un usuari. 

## Regles d’accés

Controlen si pots fer les següents accions sobre objectes com productes, comandes, factures, etc.:

* Llegir  
* Crear  
* Escriure  
* Esborrar

És la **capa mitjana**: controla les accions que pots fer a nivell de model.

## Regles de registre

Controlen **quins registres concrets** pots veure o modificar.

* Només pots veure les teves vendes  
* Només pots editar ordres del teu magatzem  
* Només pots accedir a clients de la teva empresa

És la **capa profunda**: controla les dades que pots accedir

## Grups del sistema

### Superficial (activació de mòduls)

<img style="border-radius: 5px;" src="../../img/RA2/odoo_groups.png" width="800"/><br>

Aquí podem veure tots els grups en una instal·lació nova, sense cap mòdul instal·lat.  
La columna privilege, afegeix extra permisos a sobre dels que ja té el grup per accedir a mòduls.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_group_privi.png" width="800"/><br>

Si entrem a dintre d’un grup, com per exemple Role/Portal podrem veure qui està assignat

<img style="border-radius: 5px;" src="../../img/RA2/odoo_roule.png" width="800"/><br>


Si ens anem a APPS i activem el mòdul Sales, llavors ens apareixen nous grups pertanyents al mòdul sales.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_sales.png" width="800"/><br>

## Privilegis del sistema

### Mitjà i profund (Access Rights + Record Rules)

<img style="border-radius: 5px;" src="../../img/RA2/odoo_privi_2.png" width="150"/><br>

<img style="border-radius: 5px;" src="../../img/RA2/odoo_privi_3.png" width="700"/><br>

# Settings

A l’apartat **Settings** podem accedir a la configuració dels mòduls que ja tenim activats.

Podem configurar tant la plataforma Odoo en **General Settings** com els propis mòduls per separat.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_settings.png" width="200"/><br>

# Contacte

Un contacte és qualsevol persona o organització amb qui la teva empresa interactua.

Pot representar:

* Un usuari del sistema  
* Una empresa  
* Una persona  
* Un client  
* Un proveïdor  
* Un empleat vinculat  
* Una adreça (enviament, facturació, seu)  
* Un subcontacte dins d’una empresa

Tot això és el mateix objecte: res.partner.

## Usuari

Un usuari és qualsevol persona que pot iniciar sessió a Odoo amb credencials pròpies.

* Està basat en un contacte.  
* Té accés a la interfície web.  
* Està vinculat a un grup que defineix què pot veure i fer.  
* Pot ser un administrador, un usuari intern, un usuari de portal, etc.  
* Es crea des de Configuració > Usuaris.


Exemple: Un comptable que accedeix a Odoo per gestionar factures és un usuari.

### Afegir un usuari

* Per afegir un usuari ens anem a **Settings > Users & Companies > Users** o bé a **Manage Users** (a la dreta)

<img style="border-radius: 5px;" src="../../img/RA2/odoo_add_usr.png" width="750"/><br>

* Veurem els actuals usuaris i la opció de crear-ne de nous

<img style="border-radius: 5px;" src="../../img/RA2/odoo_usr.png" width="750"/><br>

* Creem un nou usuari i li donem un nom d’usuari amb el que pugui entrar al sistema.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_create_usr.png" width="800"/><br>

* Li assignem els rols dintre de l’empresa. En aquest cas el rol d’usuari. I a quina delegació pertany.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_roles.png" width="400"/><br>

* Li posem una contrasenya donant a **Change password**. Idealment l’usuari hauria de poder rebre un mail per poder-la canviar, però no tenim un servei de missatgeria vinculat a Odoo encara.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_chng_psswd.png" width="600"/><br>

* Aquí canviem la contrasenya

<img style="border-radius: 5px;" src="../../img/RA2/odoo_chng_psswd_2.png" width="700"/><br>

* Li donem permisos per accedir als documents del mòdul de vendes (en aquest cas podem donar-li accés als documents de vendes perquè el mòdul està activat, per això apareix)  
* Perquè no tingui accés als altres mòduls eliminem qualsevol informació que pugui haver als camps i ho deixem tot en blanc menys el mòdul de vendes.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_usr_info.png" width="700"/><br>

* Dalt de la secció de l’usuari podem veure els grups a que pertany i els permisos que té

<img style="border-radius: 5px;" src="../../img/RA2/odoo_see_info.png" width="400"/><br>

* Si entrem a **grups** podrem veure els privilegis que té i els grups a que pertany:

<img style="border-radius: 5px;" src="../../img/RA2/odoo_see_info_groups.png" width="800"/><br>

La primera línia diu que l’usuari té privilegi per accedir al mòdul de **Vendes (Sales)** i pot administrar aquest mòdul perquè està dintre del grup d’**Administradors**

La següent línia diu que l’usuari té accés al mòdul de **Vendes (Sales)** i està al grup **d’usuaris amb accés a tots els documents**.

En el cas de l’usuari que hem creat abans, en assignar-lo al grup **User: All Documents**, automàticament s’assigna també al grup d’**Usuaris amb accés únicament als seus documents** (*User: Own Documents Only*), perquè un grup inclou els permisos dels grups inferiors. En canvi, **no** s’assigna al grup d’**Administrators**: és al revés, el grup d’Administrators inclou els permisos de *User: All Documents*.

Si treiem l’usuari del grup **Sales / User: All Documents** (deixant en blanc el camp de Vendes), ja no tindrà cap accés al mòdul de Vendes.

Resumint, a la columna de l’esquerra hi ha els privilegis als mòduls i a la dreta els grups als quals pertany, relacionats amb un mòdul o no. Com podem veure, hi ha grups sense privilegi a la columna de l’esquerra. Per exemple: El grup amb el **Rol d’Usuari** al no pertànyer a cap mòdul, només està a la columna de grups, i el mateix passa amb **Quotation Templates**, **Technical Features**, etc.

## Empleat

Un empleat és un registre dins del mòdul de Recursos Humans (HR).

* No necessita tenir accés al sistema (no és obligatori que sigui usuari).  
* S’utilitza per gestionar nòmines, contractes, assistència, departaments, etc.  
* Es crea des de Recursos Humans > Empleats.  
* Pot estar vinculat a un usuari, però no sempre.

Exemple: Un operari de fàbrica que no accedeix a Odoo però cal gestionar la seva jornada laboral és un empleat.

| Cas | Té accés a Odoo? | Apareix com a empleat? |
| :---- | :---- | :---- |
| Usuari intern | Sí | Opcional (si està vinculat) |
| Empleat sense usuari | No | Sí |
| Administrador | Sí | Opcional |
| Portal (client extern) | Limitat | No |

Molts cops no és necessari que un empleat accedeixi a Odoo, un encarregat pot gestionar qualsevol cosa que li correspongui. També d’aquesta manera l’empresa s’estalvia diners.

### Afegir Empleat

* Per afegir un empleat primer activem el mòdul **Employees** (Empleats)

<img style="border-radius: 5px;" src="../../img/RA2/odoo_add_employee.png" width="550"/><br>


* Si hem carregat la demo data prèviament podrem veure ara molts treballadors

<img style="border-radius: 5px;" src="../../img/RA2/odoo_see_employees_2.png" width="800"/><br>

* Anem a Departments i podem veure els que hi ha en aquests moments, podent crear de nous.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_departmnts.png" width="800"/><br>

* Creem un empleat doncs  
* Podríem crear un usuari al vol a la vegada que creem l’empleat a través del botó **Create User** però ara ho fem per separat.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_new_employee.png" width="800"/><br>

Aquí vindria la part on omplim la fitxa de l’empleat, amb el seu departament, càrrec, nom del seu rol professional i qui té per sobre (responsable)

<img style="border-radius: 5px;" src="../../img/RA2/odoo_info_employee.png" width="800"/><br>


* Omplim dades a partir del que ens ofereix la base de dades quan volem accedir a un camp

<img style="border-radius: 5px;" src="../../img/RA2/odoo_work.png" width="800"/><br>

* En aquestes pestanyes (Resume, Certifications, Personal i Payroll) podem emplenar la resta de dades de l’empleat

<img style="border-radius: 5px;" src="../../img/RA2/odoo_personla.png" width="400"/><br>

### Vinculació de l’usuari i l’empleat

* Després anem a la pestanya **Settings** (*HR Settings*) de la fitxa de l’empleat

<img style="border-radius: 5px;" src="../../img/RA2/odoo_personal_settings.png" width="700"/><br>

* Aquí ja podem assignar-li l’usuari abans creat

<img style="border-radius: 5px;" src="../../img/RA2/odoo_personal_settings_2.png" width="700"/><br>

* Ja tenim l’empleat vinculat amb l’usuari!

# Mòduls

Odoo és un sistema de gestió empresarial format per mòduls. Molts venen amb el propi software i d’altres es poden importar o desenvolupar específicament per a cada cas.

Cap mòdul ve activat per defecte, els hem d’activar nosaltres. Però apareixen visibles, almenys per poder veure quins estan disponibles.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_moduls.png" width="700"/><br>


Els mòduls activats apareixen visibles en el desplegable quan cliquem a sobre de la icona del menú.

<img style="border-radius: 5px;" src="../../img/RA2/odoo_moduls_act.png" width="200"/><br>

## Dependències

Molts dels mòduls depenen entre si.

**Mòdul d’Inventari**

El mòdul d’inventari sempre depèn de:

* Mòdul de productes.

Perquè no pots gestionar estoc si abans no existeixen:

* Productes.

**Mòdul de Vendes**

El mòdul de vendes depèn de:

* Productes  
* Clients  
* Facturació (en alguns ERPs)

Perquè per fer una venda necessites:

* Un producte  
* Un client  
* Un document de venda/factura


**CRM**

El CRM depèn del mòdul:

* Contactes

Perquè una oportunitat comercial normalment està vinculada a (a Odoo el client no és obligatori):

* Un contacte  
* Una empresa


# Bases de dades

Odoo permet crear diverses bases de dades, cadascuna amb una o diverses empreses associades. D’aquesta manera es crea un aïllament entre les empreses que corresponen a cada BD.

## Avantatges de fer servir diferents bases de dades

### Aïllament total entre empreses (seguretat i confidencialitat)

Ideal quan tens **clients diferents** o **projectes independents**.

Exemple:

Ets una consultoria i tens:

* Client A → BD_A  
* Client B → BD_B  
* Client C → BD_C

Cap client pot veure dades dels altres.  
Cap error de configuració pot afectar-los.  
Cap usuari pot accedir a una empresa que no és la seva.

### Separar entorns: Producció, Preproducció i Desenvolupament

Aquí no es crea la BD de zero, sinó que es duplica per poder treballar sobre les dades clonades i veure si els canvis no trenquen res.

Exemple:

* BD_PROD → dades reals  
* BD_PRE → proves abans de passar a producció  
* BD_DEV → proves de programació, mòduls, scripts

Així pots:

* Provar mòduls sense trencar res  
* Fer migracions de versió  
* Testejar fluxos de vendes o inventari

Evites desastres en producció

### Empreses que no tenen cap relació entre elles

Si tens empreses que no comparteixen:

* Productes  
* Clients  
* Comptabilitat  
* Inventari  
* Usuaris

Llavors no té sentit posar-les a la mateixa base de dades.

Exemple:

* Una empresa de reformes  
* Una botiga online  
* Una acadèmia

Si totes són teves però no tenen res a veure, millor separar-les.

### Diferents països amb fiscalitats incompatibles

Hi ha casos on la multiempresa dins la mateixa BD és un maldecap:

* IVA diferent  
* Llibres comptables diferents  
* Normatives locals  
* Idiomes i formats de data  
* Localitzacions que xoquen entre si

Exemple:

* Empresa a Espanya  
* Empresa a Mèxic  
* Empresa a Alemanya

És molt més net tenir:

* BD_ES  
* BD_MX  
* BD_DE

Evites conflictes de localització i configuració **PERÒ** el problema és que les empreses no estan interconnectades. Llavors s’han de valorar els pros i els contres.

### Quan una empresa vol “reiniciar” sense perdre l’històric

Això passa molt sovint.

Exemple:

* L’empresa ha fet servir Odoo 3 anys  
* Té dades brutes, proves, errors, duplicats  
* Vol començar de zero però conservar l’històric

Solució:

* BD_ANTIGA (només lectura)  
* BD_NOVA (operativa)

És com tenir un arxiu i un sistema net.

### Quan vols comparar configuracions o provar escenaris

Per exemple:

* Provar un nou flux de vendes  
* Testejar un mòdul de comptabilitat  
* Comparar dues configuracions d’inventari

Tens:

* BD_TEST1  
* BD_TEST2

Ideal per a docència i consultoria.

## Compartir Bases de dades

### Compartir l’accés a l’Odoo a través de la xarxa local

Permet que altres persones accedeixin al teu Odoo des d’una altra màquina de la mateixa xarxa.

* Els dos PC han d’estar connectats a la mateixa xarxa.  
* La connexió (wifi o cable) dels dos PC ha de tenir el perfil de xarxa privada activat.  
* S’ha de crear una regla d’entrada al tallafoc del PC amfitrió que permeti l’entrada des de fora al port on estigui corrent l’Odoo.  
* Al PC convidat normalment no cal cap regla, perquè el tallafoc deixa sortir el trànsit per defecte. Si s’ha restringit, s’ha de crear una regla de sortida que permeti la connexió al port de l’Odoo del PC amfitrió.  
* Al PC convidat accedim al PC amfitrió: **http://ip_de_l’amfitrio:port_que_sigui**  
  * Exemple: **http://192.168.1.10:8069** (8069 és el port per defecte d’Odoo; si a Docker l’heu mapejat a un altre port, per exemple el 8070, poseu aquell).

### Compartir la BD entre dockers de diferents persones

El nom dels contenidors depèn del `docker-compose.yml` de cadascú; es pot consultar amb `docker ps`. A les comandes següents, `nom_contenidor_postgres` és el contenidor de la base de dades i `nom_de_la_bd` és la base de dades de l’empresa que vam crear al formulari (per exemple `technova`), no la base de dades `postgres`.

* Entrem dins del contenidor de Postgres (la BD):

  `docker exec -it nom_contenidor_postgres bash`

* Fem un backup de la base de dades que volem:

  `pg_dump -U odoo -Fc nom_de_la_bd > /tmp/backup.dump`

* Sortim del contenidor de la base de dades (`exit`) i copiem el backup a la carpeta on tenim l’arxiu yml:

  `docker cp nom_contenidor_postgres:/tmp/backup.dump .`

<img style="border-radius: 5px;" src="../../img/RA2/odoo_backup.png" width="600"/><br>

Li passem l’arxiu al nostre company.

* El nostre company posa l’arxiu backup.dump en el mateix lloc i l’importa a la BD del seu contenidor. Amb l’opció `--clean` s’esborren primer els objectes que ja hi ha, de manera que se sobreescriu la seva base de dades actual:

  `docker exec -i nom_contenidor_postgres pg_restore -U odoo --clean -d nom_de_la_bd < backup.dump`

* Si es vol aplicar sobre una BD nova, primer la creem:

  `docker exec -it nom_contenidor_postgres createdb -U odoo nova_bd`

* Ara restaurem sobre aquesta nova BD:

  `docker exec -i nom_contenidor_postgres pg_restore -U odoo -d nova_bd < backup.dump`

**IMPORTANT!!** `pg_dump` només copia la base de dades, no el *filestore* (adjunts i imatges). Si també els voleu passar, feu el backup des del *Database Manager* d’Odoo (`http://localhost:8069/web/database/manager`), que genera un zip amb tot.

# Altres serveis d’accés al sistema ERP-CRM

A banda de l’accés per xarxa local ja descrit, un sistema com Odoo pot oferir altres serveis d’accés que cal conèixer i configurar:

* **Accés web (HTTP/HTTPS):** Odoo s’exposa per defecte pel port 8069 (HTTP); en un entorn de producció es recomana posar-hi al davant un servidor web (Nginx/Apache) que faci de proxy invers i xifri la connexió amb HTTPS (certificat SSL/TLS).  
* **API externes (XML-RPC, JSON-RPC):** Odoo permet connectar-se des d’aplicacions externes (webs, scripts, altres sistemes) mitjançant aquests protocols per llegir o escriure dades sense passar per la interfície web.  
* **Accés de portal (usuaris externs):** Odoo permet crear usuaris de tipus **Portal**, pensats perquè clients o proveïdors externs puguin consultar informació concreta (comandes, factures) sense tenir accés complet al sistema intern.  
* **Accés remot / VPN:** en instal·lacions on-premise, si no es vol exposar el servidor directament a internet, es pot configurar l’accés mitjançant una xarxa privada virtual (VPN) perquè els usuaris externs es connectin de manera segura com si fossin a la xarxa local.

# Verificació del funcionament de l’ERP-CRM

Un cop instal·lat i configurat el sistema, cal verificar que funciona correctament:

* **Verificació de l’accés:** comprovar que els usuaris es poden autenticar correctament i que veuen només els mòduls i dades que els correspon segons els seus grups/permisos.  
* **Verificació dels mòduls instal·lats:** comprovar que els mòduls activats es carreguen sense errors i que les seves funcionalitats bàsiques operen correctament (p. ex. crear un client, un producte o una comanda de prova).  
* **Verificació de la connexió a la base de dades:** comprovar que les dades es desen i es recuperen correctament, i que no hi ha errors de connexió amb PostgreSQL.  
* **Verificació de les rutes logístiques i automatismes:** provar que les regles de proveïment (reactiu/preventiu) s’executen quan toca.  
* **Verificació dels serveis d’accés:** comprovar que l’accés per xarxa local o des de fora (si escau) funciona amb els ports i regles de tallafoc configurats.  
* **Registre de proves:** deixar constància de les proves realitzades i el resultat obtingut, per poder detectar regressions en actualitzacions futures.

# Documentació de les operacions i incidències

## Documentació de les operacions realitzades

Cal registrar les instal·lacions i configuracions fetes (versió d’Odoo instal·lada, mòduls activats, usuaris i grups creats, paràmetres de configuració modificats) perquè quedi constància del que s’ha fet i es pugui reproduir o auditar en el futur.

## Documentació de les incidències

* **Què s’ha de documentar d’una incidència:** data i hora, descripció del problema, passos per reproduir-lo (p. ex. un mòdul que no s’activa, un usuari que no té els permisos esperats, un error en importar dades), missatge d’error o log associat, causa detectada i solució aplicada.  
* **Eines habituals:** un document/wiki intern, un sistema de tiquets (Jira, Redmine, GLPI), o els propis registres (logs) d’Odoo.  
* **Per què és important:** facilita el manteniment, permet donar suport a altres tècnics o al client, i genera un historial útil per a futures instal·lacions o migracions similars.
