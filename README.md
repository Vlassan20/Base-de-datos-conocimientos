# Base-de-datos-conocimientos
Base de datos donde estan ubicadas las configuraciones para crear, configurar y poner en marcha servidores en debian
# Fundamentos

 - Debes planificar siempre la estructura de Directorios en GNU/Linux (Filesystem Hierarchy):

/               Jerarquía primaria, la raíz o root, y directorio raíz o contenedor de todo el sistema de jerarquía.
/etc/   Contiene archivos de configuración del sistema
/home/  Contiene los directorios de trabajo de todos los usuario
Swap    Area de intercambio.
/opt/   Contiene Paquetes de programas opcionales de aplicaciones
/usr/   Jerarquía secundaria de los datos de usuario; contiene la mayoría de las utilidades y aplicaciones
/var/   Jerarquía importante, Archivos variables, todos los programas se montan en este directorio, como por Ej. Docker, Postgresql, MariaDB, etc.
/tmp/   Archivos temporales

- El arquitecto debe tener una planificacion BASE y luego dependiendo de la necesidad lo ajusta

Un ejemplo BASE, con valores muy generosos:

/               10G
Swap    2G
home    5G
var             10G
usr             10G
tmp             10G

 - Cuando se este instalando una distribución de GNU/Linux ya debe tener claro cual es la estructura de Directorios.

Es altamente recomendable utilizar LVM (Logical Volume Manager)

Un LVM siempre el Disco se debe:

Particionar.
Crear los VG
Crear los LV
Formatear en XFS
Montar el LVM en un punto de montura

- Los Discos en GNU/Linux se identifican como:

sda     como el primer disco
sdb     como el segundo disco
sdc como el tercer disco
y asi sucesivamente

- Cuando en un disco lo vemos acompañado de numeros, esto nos indica el numero de la particion Ej:


sda1
sda2
sda3
Significa que tienes un Disco y hay tres (3) particiones

- Luego que instalemos una distribucion de GNU/Linux, debemos entonarla, es decir, tunning:


consultamos que ip tenemos con **ip addr**
        ip addr

consultamos que tengamos el DNS
        cat /etc/resolv.conf

hacemos un ping a google para estar seguros que tenemos salida al internet
        ping google.com
apt     -       sources.list    -       agregar el repositorio: deb http://deb.debian.org/debian bullseye main contrib non-free
apt-get update  -       busca los indices del repositorio que se agrego y lo descarga a local
apt-get upgrade -       Busca todos los paquetes obsoletos y los actualiza con la ayuda del nuevo repositorio

Instalamos las utilidades de admon y/o diagnostico net-tools bindutils
        apt-cache search net-tools bindutils
        apt-get install net-tools
        apt-cache search bindutils
        apt-get install bindutils

ahora probabos las siguientes utilizades
        ifconfig
        netstat -natp
        dig google.com

Instalamos el SSH server
        apt-cache search sshd
        apt-get install openssh-server

Todos los GNU/Linux no permite que el root utilice el ssh y por eso lo vamos habilitar
        nano /etc/ssh/sshd_config

Buscamos esta linea: PermitRootLogin y le decimos que yes
Reniciamos el sshd
        systemctl restart sshd
        systemctl status sshd
        netstat -natp

Verificamos que no este SELINUX, que es como un firewall de directorios
        sestatus

Verificamos que no este el Firewalld
        systemctl status firewalld
        
        











