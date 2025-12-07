 # Acutalitzar l’entorn


installar ssh
sudo apt install ssh
<img width="850" height="202" alt="image" src="https://github.com/user-attachments/assets/bca693d2-380a-4719-8091-399a38293bba" />

comprovar que està instalado
 sudo apt systemctl status ssh
<img width="698" height="187" alt="image" src="https://github.com/user-attachments/assets/9b8132fb-accf-4adf-84a7-a1a195771677" />

Aqui hem de treure un asteriscos i afegir unes lineas tal i com es veu a les captures
sudo nano /etc/ssh/sshd_config
<img width="539" height="432" alt="image" src="https://github.com/user-attachments/assets/12a1c6ba-858e-4154-b4f7-95e6ca1c125b" />
<img width="668" height="435" alt="image" src="https://github.com/user-attachments/assets/348bf0cf-441d-45a4-bdf7-0b5ee502ebe7" />


i fem sudo systemctl restart ssh per reiniciar el servidor

## TASCA A REALITZAR
Desactiva l’accés al root (ja explicat amb PermitRootLogin no).
Crea un nou usuari usuari2:
posar contraseña l'usuari root

Posem contraseny a l’usuari root i iniciem sesio per comprovar que funcioni
<img width="363" height="115" alt="image" src="https://github.com/user-attachments/assets/d8971afb-cb3f-479e-a805-2c51771e365e" />


ara creem un segon usuari i li posem contrasenya
<img width="461" height="127" alt="image" src="https://github.com/user-attachments/assets/c0ab895d-9e07-4147-9216-d6d911ea9b09" />






ara intentem fer ssh amb l’usuari creat i veurem com no ens deixa
<img width="658" height="209" alt="image" src="https://github.com/user-attachments/assets/f392f4af-f26b-4868-ab9a-27ec4cb39731" />




# 3.Configuració Tunel
Anirem al buscador de windows i buscarem "Opciones de internet" i una vegada entrat anirem a conexiones i en configuración de LAN, Opciones avanzadas i posar:
<img width="373" height="510" alt="image" src="https://github.com/user-attachments/assets/073c582d-2d2b-4ec0-ac65-e320dd4bd208" />

Un cop fet obrirem el terminal i farem un:
ssh -D 9876 usuari@la_teva_ip

Despres  anirem al navegador i anirem a descarregar el "Wireshark"(o tambe ho podem fer amb el comando “winget wireshark”)
<img width="683" height="490" alt="image" src="https://github.com/user-attachments/assets/0ec09e97-d706-4142-8dd2-062013a91e11" />

Un cop acabat de descarregar el wireshark, obrirem i seleccionarem el ethernet i la barra de busqeuda posarem el seguent text “tcp.stream eq 1” i veruem el paquets 
















## Com iniciar sesió 

Generar el Pac de Claus en linux desde windows
ssh-keygen -t rsa
<img width="619" height="431" alt="image" src="https://github.com/user-attachments/assets/55403ce5-c96f-4165-a533-b597fb7fb81a" />


ls .\.ssh\
<img width="659" height="299" alt="image" src="https://github.com/user-attachments/assets/dfbd6cee-c470-4405-a9f6-a79811dddc26" />

scp .\.ssh\id_rsa.pub usuari@la_teva_ip
<img width="659" height="299" alt="image" src="https://github.com/user-attachments/assets/c9b56e1d-31b5-4f91-a744-b80e1b2c6bdd" />


### Un cop fet aixo animer al servidor i farem les seguents comandes:
mkdir .ssh
touch .ssh/authorized_keys
ls
cat id_rsa.pub
cat id_rsa.pub >> .ssh/authorized_keys
<img width="1086" height="285" alt="image" src="https://github.com/user-attachments/assets/0f4f6664-c024-436f-b70e-b9e2a53d86e5" />


Quant estem anem un altre cop al client farem:
ssh usuari@192.168.56.109
<img width="778" height="403" alt="image" src="https://github.com/user-attachments/assets/96d9559b-e958-4c2d-b56f-393097f76bf0" />

Si ho hem fet tot be no us hauria de demanar la contrasenya








## Servidor OpenSSH

Entrem a la configuracio i busquem “caracteristiques opcionals” → “ver caracteristiques disponibles” → busquem el “Servidor OpenSSH” i el agreguem. 
<img width="616" height="426" alt="image" src="https://github.com/user-attachments/assets/15ac11e2-5784-4c15-9767-061784e80dc9" />


Un cop fet aixo obrirem el powershell com a administrador i farem 
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automatic'
I per Comprobar farem:
Get-Service sshd 
<img width="620" height="137" alt="image" src="https://github.com/user-attachments/assets/2e3a8d87-405b-480c-8c46-75b1003f37f3" />


Una vegada acabat afegirem un adaptador més que serà l'adaptador només amfitrió.

New-NetFirewallRule -Name "OpenSSH-Server" -DisplayName "OpenSSH Server (sshd)" -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
<img width="620" height="304" alt="image" src="https://github.com/user-attachments/assets/c176430c-0aa1-405b-bfa7-693d765f5d38" />



i el reiniciem
Restart-Service sshd

Ara farem un
ipconfig | findstr "IPv4"
<img width="778" height="370" alt="image" src="https://github.com/user-attachments/assets/d32be081-5b03-4ca5-9a23-197077bd7fe4" />


