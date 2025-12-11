

Primer hem de posar el segon adaptador de xarxa en nomes per l'anfitrio i configurar la xarxa amb la comanda:
sudo nano /etc/netplan/50

<img width="335" height="180" alt="image" src="https://github.com/user-attachments/assets/13c4d09e-b888-4d52-9d0f-e30a8b1e4f1a" />

--

i configurar la xarax en la red del client
<img width="772" height="587" alt="image" src="https://github.com/user-attachments/assets/ba8407b6-f304-4331-b97d-39150443eff9" />


després actualitzar el servidor y el client

<img width="748" height="218" alt="image" src="https://github.com/user-attachments/assets/7ebd9d0d-3e97-468c-a985-3f2f8c47a45d" />

<img width="653" height="390" alt="image" src="https://github.com/user-attachments/assets/2b03e203-0bd6-4e28-a737-b2a0d5a5e668" />

ara creem els grups dev i admins

<img width="597" height="93" alt="image" src="https://github.com/user-attachments/assets/d0236fd7-f17c-4234-8ab5-ac833be03ff1" />
ara configurem els permisos

<img width="703" height="108" alt="image" src="https://github.com/user-attachments/assets/8fb8d417-b3f5-4e98-95f9-f8d1f3b8f2c4" />

ara els directoris 

<img width="606" height="74" alt="image" src="https://github.com/user-attachments/assets/75c2ed03-e8b7-40c3-ace6-0520daadbd55" />


i els permisos

<img width="495" height="84" alt="image" src="https://github.com/user-attachments/assets/6adbddb1-8e2d-4031-879d-267dccc503ec" />

per comprobar si esta bé farem:

<img width="559" height="78" alt="image" src="https://github.com/user-attachments/assets/b9a4acef-2374-4493-9bfd-49c909db4f83" />

## Instalacio del Servidor NFS

sudo apt install nfs-kernel-server -y

ara en el client farem:
````
sudo apt update && sudo apt upgrade -y
sudo apt install nfs-common -y
````
Editem l'arxiu fent 
````
sudo nano /etc/exports
````
<img width="757" height="196" alt="image" src="https://github.com/user-attachments/assets/e3079a65-0b71-43e2-9479-3ba64ad1bc99" />

fent sudo exportfs -ra

<img width="771" height="34" alt="image" src="https://github.com/user-attachments/assets/c7fc5cb3-2d55-45d5-9f91-92c4932eff78" />

estaba creando el touch
