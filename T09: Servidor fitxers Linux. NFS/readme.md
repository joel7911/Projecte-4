# Projecte04: Servidor NFS
## El Cas Client: DevOptimize Solutions
El nostre client, DevOptimize Solutions, és una petita startup de desenvolupament de programari que treballa exclusivament amb Linux. Tenen un problema crític: el seu codi font i els seus actius (documents de disseny, scripts) estan descontrolats. Cada desenvolupador té còpies locals, cosa que provoca errors de versió constants i una pèrdua d'eficiència brutal. Ens han contractat per implementar un servidor de fitxers centralitzat. Atès que tot l'entorn és Linux, la solució nativa, més ràpida i eficient del sector és NFS (Network File System). El client ha insistit en que treballa sense un entorn d’autenticació centralitzada i que, de moment, no té previst fer aquest pas.

Per mostrar al client com quedarà la solució proposada a partir de les seves demandes i poder mostrar també les seves limitacions, se t’encarrega fer una demostració del sistema.

Crearàs un servidor NFS (NFSv3) i un client Linux que consumeixi els recursos compartits. Hauràs de crear usuaris i grups per simular l'entorn del client i demostrar el control d'accés utilitzant les opcions d'exportació (/etc/exports) i els permisos del sistema de fitxers (chmod, chown).

## Fases del projecte
### Fase 1: Preparació de l'entorn
Per preparar aquesta prova de concepte, necessitaràs dues màquines virtuals Linux: tot i que pel servidor podríem fer servir qualsevol distribució, ens decantarem per Ubuntu Server 24.04 LTS per la seva facilitat d'ús i popularitat. Per al client, utilitzarem Zorin OS 18. Els dos equips els configurarem amb dues interfícies de xarxa: una NAT per a l'accés a Internet i una adaptador de xarxa només-amb-amfitrió per a la comunicació entre ells i potencialment, treballar via terminal SSH amb el servidor.

Tots dos equips els instal·larem seguint els requisits recomanats. L'idioma triat serà espanyol (Espanya) i amb l'idioma per defecte en espanyol. En el cas d'Ubuntu Server, seleccionarem la instal·lació del servei SSH durant el procés d'instal·lació per facilitar la gestió remota.

Ens assegurarem que ambdues màquines tinguin accés a Internet i que es puguin comunicar entre elles a través de la xarxa només-amb-amfitrió i actualitzarem els sistemes amb les últimes actualitzacions disponibles.

## Fase 2: Preparació del servidor
Abans de compartir res, hem de preparar els usuaris i els directoris al Servidor.

Creació de Grups: Crear dos grups per al client: devs i admins.

Creació d'Usuaris: Crear un usuari dev01 (membre del grup devs).

Crear un usuari admin01 (membre del grup admins). Creació de Directoris (al Servidor):

Crear el directori per als projectes de desenvolupament: /srv/nfs/dev_projects

Crear el directori per a les eines d'administració: /srv/nfs/admin_tools

Permisos del Servidor (El punt clau):

Es vol que els developers tinguin control total sobre els seus projectes.
Es vol que els administradors tinguin control sobre les seves eines.
En tots dos casos, l'usuari propietari serà root.
Com a pas final, s'instal·laran els paquets necessaris per al servei NFS al servidor i es configurarà l'exportació dels directoris amb les opcions adequades.

Nota: Perquè aquesta pràctica funcioni correctament, heu de replicar aquests usuaris i grups al client, o, idealment, assegurar-vos que els UID i GID (els números d'identificació) coincideixin a les dues màquines.

## Fase 3: L'Exportació d'Administració (El Dilema del root_squash)
El client necessita que el directori /srv/nfs/admin_tools sigui accessible per l'equip d'administradors. A vegades, l'usuari root del client (que sou vosaltres, els consultors) necessitarà escriure en aquest directori per instal·lar eines. Aquí mostrarem un error típic i la seva solució.

Prova 1 (L'error comú)
Exportar el directori /srv/nfs/admin_tools amb les opcions 'rw,sync'.
Des del client, muntar aquest recurs compartit a /mnt/admin_tools. Com a root del client, intentar crear un fitxer dins d'aquest directori muntat.
Verificar quin és el propietari del fitxer creat. Per què? Justificar la resposta amb l'explicació tècnica de 'root_squash'.
Prova 2 (La Solució)
Modificar l'exportació del directori /srv/nfs/admin_tools per incloure l'opció 'no_root_squash'.
Al client, desmuntar i tornar a muntar el recurs compartit.
Com a root del client, intentar crear un fitxer dins d'aquest directori muntat. Observeu quin és el propietari del fitxer creat aquesta vegada. Ha canviat alguna cosa? Justificar la resposta amb l'explicació tècnica de 'no_root_squash'.
## Fase 4: L'Exportació de Desenvolupament (Permisos rw vs ro)
Editar /etc/exports per afegir dues exportacions per al mateix directori. El client vol que la xarxa d'administració (p.ex., 192.168.56.0/24) hi pugui escriure, però que la xarxa de consultors (simularem que és una altra IP, p.ex., 192.168.56.100) només pugui llegir.
Des del client, muntar el recurs compartit a /mnt/dev_projects i provar d'escriure-hi com a usuari dev01. Hauria de funcionar.
Desmuntar el recurs i canviar manualment la IP del client a 192.168.56.100. Tornar a provar d'escriure al directori muntat com a usuari dev01 i comprovar que només funciona la lectura.
Canvieu d'usuari al client a admin01 i torneu a provar d'escriure al directori muntat. Comproveu que no es pot escriure, ja que admin01 no és membre del grup devs (permisos locals del sistema de fitxers).
## Fase 5: Muntatge Automàtic amb /etc/fstab
És evident que els usuaris no poden estar muntant manualment els recursos compartits cada vegada que reinicien el sistema. Per això, es configurarà el muntatge automàtic mitjançant el fitxer /etc/fstab al client.

Editar el fitxer /etc/fstab al client per afegir les entrades necessàries per muntar automàticament els recursos compartits NFS al directori /mnt/admin_tools i /mnt/dev_projects durant l'inici del sistema.
Executar la comanda mount -a per provar les entrades sense reiniciar.
Reiniciar el client i verificar que els recursos compartits s'han muntat correctament.
Conclusió
En aquesta prova de concepte s'ha demostrat el funcionament amb els requisits que ha demanat l'empresa client, però ja ets un tècnic prou experimentat per saber que aquesta solució té moltes limitacions i problemes de seguretat. Quines recomanacions faries al client per millorar aquesta solució en un futur? Pensa en termes d'autenticació centralitzada i gestió d'usuaris i permisos.

Com lliurar la tasca
Documenta tot el procés seguint les fases descrites anteriorment. Per les comandes, escriu la comanda com un codi, això et permetrà copiar posteriorment amb facilitat. Per exemple:

sudo apt update
Inclou captures de pantalla dels passos més importants, especialment dels resultats que demostren el correcte funcionament.

Respon les preguntes plantejades en les diferents fases.

Redacta una conclusió raonada amb les teves recomanacions per al client.

Nota: Els termes 'redacta' i 'raonada' indiquen clarament que s'espera que escriguis amb les teves pròpies paraules i que aportis un pensament crític al teu treball. Pensa que si les conclusions les redacta directament una IA, ens plantejarem seriosament substiuir-te per ella.
