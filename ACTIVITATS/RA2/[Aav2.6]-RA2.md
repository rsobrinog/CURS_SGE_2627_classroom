# Activitat 2.6 — Serveis d'accés al sistema ERP-CRM

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

### 1. Accés per xarxa local

Si no ho heu fet ja a l'activitat 2.3, compartiu l'accés a la vostra instal·lació d'Odoo a través de la xarxa local (IP + port, regles de firewall) i comproveu-ho des d'un altre dispositiu.

**IMPORTANT!!** Si a la xarxa del centre els dispositius no es veuen entre ells, feu la prova connectant els dos dispositius a la xarxa de dades mòbils d’un mòbil (punt d’accés) o feu-la a casa.

### 2. Usuari de tipus Portal

1. Creeu un contacte (client) nou.
2. Convertiu-lo en usuari de tipus **Portal** (des de la fitxa del contacte, "Concedir accés al portal" o equivalent). El contacte ha de tenir un correu al camp *Email*, que serà el seu usuari.
3. Com que no tenim cap servidor de correu configurat, el contacte no rebrà el correu d'invitació per triar la contrasenya. Poseu-li-la vosaltres des de **Settings > Users & Companies > Users** (traieu el filtre per veure també els usuaris de portal), obrint l'usuari i fent servir **Change password**.
4. Accediu a Odoo amb aquest usuari (en una finestra privada del navegador) i compareu què pot veure respecte a un usuari intern normal.
5. Expliqueu (3-4 línies) per a quins casos d'ús serveix un usuari de portal.

### 3. Accés extern segur (HTTPS)

Sense necessitat de fer-ho realment, expliqueu per escrit:

1. Per què **no** és recomanable exposar directament el port 8069 d'Odoo a internet tal com està configurat per defecte.
2. Quins elements caldria afegir (proxy invers, certificat SSL/TLS...) per exposar-lo de manera segura amb HTTPS.
3. Quina alternativa hi hauria si no es vol exposar el servidor directament a internet (pista: vegeu la teoria del RA2, apartat de serveis d'accés).
