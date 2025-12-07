 # Acutalitzar l’entorn


installar ssh
sudo apt install ssh



comprovar que està instalado
 sudo apt systemctl status ssh


Aqui hem de treure un asteriscos i afegir unes lineas tal i com es veu a les captures
sudo nano /etc/ssh/sshd_config


i fem sudo systemctl restart ssh per reiniciar el servidor

TASCA A REALITZAR
Desactiva l’accés al root (ja explicat amb PermitRootLogin no).
Crea un nou usuari usuari2:
posar contraseña l'usuari root

Posem contraseny a l’usuari root i iniciem sesio per comprovar que funcioni

ara creem un segon usuari i li posem contrasenya





ara intentem fer ssh amb l’usuari creat i veurem com no ens deixa
3.Configuració Tunel
Anirem al buscador de windows i buscarem "Opciones de internet" i una vegada entrat anirem a conexiones i en configuración de LAN, Opciones avanzadas i posar:



Un cop fet obrirem el terminal i farem un:
ssh -D 9876 usuari@la_teva_ip

Despres  anirem al navegador i anirem a descarregar el "Wireshark"(o tambe ho podem fer amb el comando “winget wireshark”), un cop acabat de descarregar el wireshark, obrirem i seleccionarem el ethernet i la barra de busqeuda posarem el seguent text “tcp.stream eq 1” i veruem el paquets 


























Com iniciar sesió 

Generar el Pac de Claus en linux desde windows
ssh-keygen -t rsa



















ssh-keygen -t rsa -b 4096 -C "nombre_usuario@cliente_linux"

ssh -D 9876 usuari@la_teva_ip

Inici sessió amb SSH keys
Generar el Pac de Claus en linux desde windows
ssh-keygen -t rsa


scp .\.ssh\id_rsa.pub usuari@la_teva_ip


un cop fet aixo animer al servidor i farem les seguents comandes:

mkdir .ssh
touch .ssh/authorized_keys
ls
cat id_rsa.pub
cat id_rsa.pub >> .ssh/authorized_keys



Quant estem anem un altre cop al client farem:
ssh usuari@192.168.56.109


Si ho hem fet tot be no us hauria de demanar la contrasenya








Servidor OpenSSH

Entrem a la configuracio i busquem “caracteristiques opcionals” → “ver caracteristiques disponibles” → busquem el “Servidor OpenSSH” i el agreguem. 

Un cop fet aixo obrirem el powershell com a administrador i farem 
Start-Service sshd
Set-Service -Name sshd -StartupType 'Automatic'
I per Comprobar farem:
Get-Service sshd 





Una vegada acabat afegirem un adaptador més que serà l'adaptador només amfitrió.

New-NetFirewallRule -Name "OpenSSH-Server" -DisplayName "OpenSSH Server (sshd)" -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22

i el reiniciem
Restart-Service sshd

Ara farem un
ipconfig | findstr "IPv4"


