# Fase 1: Resolució Simplificada del Cas Pràctic

## 1. Què copiar? (Priorització) 

Hem de centrar-nos en allò que és vital per a l'empresa i que seria impossible o molt car de refer.

### A. Servidor (El més important)

És on hi ha tota la informació de l'empresa. Cal copiar-ho tot, però prioritzant així:

- **Els Comptes i els Clients (Bases de Dades):**  
  PRIORITAT MÀXIMA. Són les dades que canvien a cada moment i, si es perden, l'empresa es queda sense saber a qui cobrar o què li deu.  
  Només podem perdre 4 hores de feina com a màxim.

- **Els Projectes (Plànols i Especificacions):**
  Molt important. Si es perden els plànols, s'ha de tornar a fer la feina des de zero.

- **Les Carpetes de la Gent (Feina Diària):**
  Important. La feina que fan els empleats cada dia.

### B. Els 10 Ordinadors dels Clients (PCs Windows)

- **Cal copiar-los?**  
  NO, no completament.
- No té sentit copiar el Windows ni els programes de cada ordinador. Si un ordinador es trenca, instal·lem un Windows nou ràpidament.
- **Què sí que cal fer?**
  - Els tècnics guarden documents locals. L'ideal és que guardin aquesta feina directament al Servidor, així ja estaria copiada automàticament.
  - Si no és possible, farem una còpia de seguretat només de la carpeta "Documents" d'aquests PCs, ja que la resta no és crítica.

---

## 2. Quan i Com Copiar? (Periodicitat i Tipus) 

Ens basarem en les necessitats de recuperació: la informació general pot perdre 24 hores (una nit), però els Comptes/Clients només poden perdre 4 hores.

### Estratègia per als Comptes/Clients (BBDD)

- Per complir les 4 hores, hem de fer còpies molt sovint i que siguin ràpides.
- **Periodicitat:** 3 cops al dia durant la feina (per exemple, 10:00, 14:00 i 18:00).
- **Tipus de Còpia:** Incremental. Només es copien els pocs canvis que s'han fet des de l'última còpia de fa 4 hores. És molt ràpid.

### Estratègia per a la Resta (Projectes i Carpetes)

- **Periodicitat:** Cada nit, un cop la gent ha plegat (cap a les 22:00).

| Dia                    | Hora               | Què es copia?          | Tipus de Còpia | Per què?                                                        |
|------------------------|--------------------|------------------------|---------------|-----------------------------------------------------------------|
| Dilluns - Divendres    | 3 cops al dia      | Els Comptes/Clients    | Incremental   | Per no perdre més de 4 hores de dades.                          |
| Dilluns - Dijous       | Nit (22:00)        | Tota la resta (Projectes, etc.) | Incremental   | Desa ràpidament només la feina del dia.                         |
| Divendres              | Nit (22:00)        | Tota la resta          | Diferencial   | Ajuda a restaurar més ràpidament si hi ha un problema, només necessites la còpia del cap de setmana passat i aquesta. |
| Dissabte o Diumenge    | Madrugada          | Tota la informació     | Completa      | Còpia de seguretat total que serveix de base per a tota la setmana següent. (Això ho guardem durant 5 setmanes). |

---

## 3. On Guardar? (Mitjans i Ubicació - Regla 3-2-1) 

Utilitzarem la Regla 3-2-1 (3 còpies, en 2 llocs diferents, 1 fora de l'oficina) perquè estem parlant de la supervivència del negoci.

| Regla      | Mitjà proposat      | Ubicació                                       | Funció                                                                                                                           |
|------------|---------------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| 3 Còpies   | 1. Les dades originals   | Al Servidor Ubuntu                             | El dia a dia.                                                                                                                    |
| 2 Mitjans  | 2. Disc Dur en Xarxa (NAS) | Dins de l'oficina, en un lloc diferent del servidor | Per complir el Temps de Recuperació ràpid (RTO < 4h). Si el servidor cau, arrenquem des d'aquí ràpidament.                       |
| 1 Fora     | 3. Núvol (Cloud)         | Fora de l'oficina (un servei d'internet)       | Protegeix contra robatoris, incendis o inundacions que afectin tot el local. La fibra de 600 Mbps és ideal per pujar aquesta còpia cada nit. |

---

### Fase 2: Treball per trio

| Element | Proposta del trio | Justificació |
| :-- | :-- | :-- |
| Dades Crítiques | Bases de Dades de Comptabilitat i Clients | Són essencials per al funcionament diari i canvien sovint |
| Periodicitat (BD) | Cada 4 hores (incremental) + còpia completa diària | Permet recuperar fins a l’última actualització sense perdre més de 4 h |
| Tipus de Còpia (BD) | Incremental + Completa | Redueix temps i espai de còpia |
| Mitjà 1 (Local) | NAS dins de la sala de servidors | Accés ràpid per a recuperacions menors |
| Mitjà 2 (Extern) | Cloud (Google Cloud) | Garantia d’una còpia fora de lloc, segura i automàtica |


***

### Fase 3: Treball en grup

1. Debat i selecció
Després de compartir les propostes, hem coincidit que el NAS local i el núvol són la millor combinació qualitat-preu. Les cintes LTO serien més segures a llarg termini, però massa cares per l’empresa.
2. Política final de còpies de seguretat

#### Dades objecte de còpia

Servidor:
    - Comptabilitat i Clients (crítiques): còpia incremental cada 4 h, completa cada dia.
    - Projectes i plànols (no crítiques): còpia diferencial diària i completa setmanal.
Equips clients: només els documents importants de cada tècnic (sincronitzats un cop al dia amb el servidor).


#### Cronograma setmanal detallat

| Dia | Dades | Tipus de còpia | Mitjà |
| :-- | :-- | :-- | :-- |
| Dilluns | BD i Documents crítics | Completa | NAS |
| Dimarts | BD | Incremental | NAS |
| Dimecres | BD i Documents | Diferencial | NAS |
| Dijous | BD | Incremental | NAS |
| Divendres | BD i Documents | Diferencial | NAS |
| Dissabte | BD | Incremental | Cloud |
| Diumenge | Tot (completa) | Completa | Cloud |

#### Elecció de mitjans i ubicació (regla 3-2-1)

Mitjà 1 (Local): NAS intern amb discs redundants.
Mitjà 2 (Extern): Còpia automàtica al núvol (Google Cloud).
Ubicació fora de lloc: còpia al núvol gestionada pel responsable de seguretat.


#### Estratègia de recuperació (RTO/RPO)

RTO (Temps de recuperació): Les còpies al NAS permeten restablir bases de dades en menys de 4 h.
RPO (Pèrdua màxima de dades): Còpies incrementals cada 4 h asseguren una pèrdua màxima de només aquest marge.
