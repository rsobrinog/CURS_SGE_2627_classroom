# Activitat 2.7 — Entorns de desenvolupament, proves i explotació

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

Partint d'una de les vostres bases de dades d'Odoo ja creades (amb dades):

### 1. Crear els tres entorns

1. Dupliqueu la base de dades des del **Gestor de bases de dades** d'Odoo (Database Manager) per crear-ne dues còpies més (us demanarà la **Master Password**), de manera que tingueu:
   * `empresa_PROD` (la base de dades "real")
   * `empresa_PRE` (còpia per a proves abans de passar canvis a producció)
   * `empresa_DEV` (còpia per a desenvolupar/provar mòduls i configuracions noves)

### 2. Provar un canvi a l'entorn de desenvolupament

1. A `empresa_DEV`, instal·leu o configureu alguna cosa nova (un mòdul o un canvi de configuració).
2. Comproveu que funciona correctament **només** en aquest entorn.

### 3. Passar el canvi a preproducció i, finalment, a producció

1. Repetiu el mateix canvi a `empresa_PRE` i verifiqueu-lo de nou (simulant que és l'últim pas abans de producció).
2. Un cop verificat, apliqueu el canvi a `empresa_PROD`.

### 4. Reflexió

Responeu per escrit (4-5 línies): quins avantatges té aquesta manera de treballar (DEV → PRE → PROD) enfront de fer els canvis directament a la base de dades de producció? Poseu un exemple concret de problema que aquesta pràctica evitaria.
