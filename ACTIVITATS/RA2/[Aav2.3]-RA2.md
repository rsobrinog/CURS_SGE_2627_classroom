# Activitat 2.3 — Tipus d'instal·lació d'un ERP-CRM

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

### 1. Comparativa teòrica

Ompliu una taula comparant els tres tipus d'instal·lació:

| Tipus | Descripció breu | Avantatges | Inconvenients | Exemple d'ús típic |
| :---- | :---- | :---- | :---- | :---- |
| Monolloc | | | | |
| Client-servidor | | | | |
| Al núvol | | | | |

### 2. Identificació de la vostra instal·lació actual

La instal·lació d'Odoo amb Docker que heu fet servir durant el curs (contenidor `odoo` + contenidor `db`, accessible des del vostre navegador):

1. A quin dels tres tipus s'assembla més? Justifiqueu-ho.
2. Quins elements farien que fos "al núvol" de veritat (en lloc de local)?

### 3. Passar de Monolloc a Client-servidor

Suposeu que un company vostre, a la mateixa xarxa local, vol accedir també al vostre Odoo des del seu ordinador.

1. Seguiu els passos ja vistos a la teoria (RA2) per **compartir l'accés a l'Odoo a través de la xarxa local** (regles de firewall, IP i port).
2. Comproveu, des d'un altre dispositiu de la mateixa xarxa (mòbil, un altre PC), que podeu accedir-hi.

   **IMPORTANT!!** Si a la xarxa del centre els dispositius no es veuen entre ells, feu la prova connectant els dos dispositius a la xarxa de dades mòbils d’un mòbil (punt d’accés) o feu-la a casa.

3. Expliqueu per què, un cop fet això, la vostra instal·lació ha passat de comportar-se com un **monolloc** a comportar-se com un **client-servidor**.
