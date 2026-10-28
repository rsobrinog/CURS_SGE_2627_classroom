# Activitat 2.5 — Actualització del sistema ERP-CRM

## MÒDUL: Desenvolupament d'aplicacions multiplataforma

RA2: Implanta sistemes ERP-CRM interpretant la documentació tècnica i identificant les diferents opcions i mòduls.

## RECURSOS

 - Teoria RA2

## CONDICIONS DE TREBALL

 - Treball individual.
 - Entregar al Moodle l'enllaç del github.
 - Github:
   - Treballar en el mateix repositori de la **RA1**.
   - Treballar en la branca **ra2**.
   - En acabar l'activitat, fusionar la branca **ra2** a la branca **main** del github.    

## AVALUACIÓ

 - Activitat avaluable amb **A** (Apte) o **NA** (No Apte).
 - Condicions per a **Apte**:
   - 100% de l'activitat demanada.
   - Entregar l'activitat a la data indicada.
   - Treballar amb branca i l'ús de commits.
 - Entregar en format **.md** (markdown) amb la mateixa nomenclatura que el de l'activitat actual.

## ENUNCIAT

Utilitzeu una de les instal·lacions d'Odoo que ja teniu (per exemple, la de l'activitat 2.4).

### 1. Backup previ

1. Feu una còpia de seguretat de la base de dades abans de fer cap canvi, seguint el procediment de `pg_dump` ja vist a la teoria del RA2.

### 2. Actualitzar un mòdul ja instal·lat

1. Abans d'actualitzar, creeu algunes dades en un mòdul que ja tingueu instal·lat (per exemple, dos contactes al mòdul Contactes o una comanda a Vendes).
2. Actualitzeu el mòdul des d'**Apps**: obriu el mòdul i feu servir l'opció **Actualitzar** (*Upgrade*). Si no us apareix, activeu el mode desenvolupador (Settings, al final de la pàgina, «Activar el mode desenvolupador»).
3. Comproveu que el mòdul continua funcionant i que no s'ha perdut cap de les dades que havíeu creat.

**IMPORTANT!!** L'opció «Actualitzar llista d'aplicacions» no actualitza cap mòdul: només refresca la llista de mòduls disponibles (per exemple, quan s'afegeix un mòdul nou a la carpeta d'addons).

### 3. Instal·lar un mòdul nou

1. Instal·leu un mòdul que encara no tinguéssiu (p. ex. Projectes, si no el teníeu).
2. Comproveu que no ha trencat cap funcionalitat existent (proveu algun procés que ja funcionava abans, com crear una comanda de venda).

### 4. Reflexió

Responeu per escrit (5-6 línies):

* Quina diferència hi ha entre **actualitzar un mòdul** i **actualitzar la versió d'Odoo** (per exemple, de la versió 17 a la 18)?
* Quins riscos té actualitzar la versió major d'Odoo, i com es podrien mitigar?
