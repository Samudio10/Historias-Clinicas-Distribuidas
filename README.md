# Historias-Clinicas-Distribuidas
Este proyecto académico plantea el desarrollo de un sistema de historias clínicas distribuidas, diseñado para permitir el acceso seguro a la información médica de los pacientes desde múltiples ubicaciones. Su finalidad es optimizar la gestión y organización de los datos clínicos, contribuyendo a una atención sanitaria más eficiente, ágil y estructurada.

Nota: Todos los procedimientos y comandos fueron verificados en el entorno Debian GNU/Linux 13 (Trixie). Se recomienda emplear esta versión o una distribución compatible para garantizar el correcto funcionamiento.

# Instalación del proyecto.
### 1. Actualizazamos el sistema.
Este comando sincroniza la lista de paquetes disponibles con los repositorios oficiales y actualiza todo el sistema a las versiones más recientes, Garantiza que el entorno tenga las últimas correcciones de seguridad y compatibilidad antes de instalar dependencias críticas como Docker y Python.
```
sudo apt update && sudo apt upgrade-y
```

### 2. Instalamos las utilidades y herramientas de desarrollo.
Instala herramientas básicas necesarias para desarrollo, descarga de recursos, edición de archivos y ejecución del entorno Python.
```
sudo apt install -y curl wget git vim htop unzip ca-certificates python3 python3-pip python3-venv libcairo2 libpango-1.0-0 libgdk-pixbuf-2.0-0 libffi-dev shared-mime-info libjpeg-dev libxml2 libxslt1.1
```

### 3. Creamos un directorio seguro para claves GPG.
Crea un directorio protegido donde se almacenarán las claves criptográficas (GPG) utilizadas para verificar la autenticidad de los repositorios externos.
```
sudo install -m 0755 -d /etc/apt/keyrings
```

### 4. Importamos la clave GPG de Docker.
Descarga la clave oficial de Docker y la convierte al formato que APT puede utilizar para verificar la autenticidad de los paquete, Permite que el sistema confíe en el repositorio de Docker y evite la instalación de software malicioso o alterado.
```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

### 5. Agregamos un repositorio oficial de Docker e instalamos.
### ¿Qué hace esto?

1. Agrega el repositorio oficial de Docker al sistema.

2. Actualiza la lista de paquetes para incluir Docker.

3. Instala Docker Engine, CLI, Containerd y plugins modernos (Buildx y Compose).

4. Activa el servicio de Docker para que inicie automáticamente.

5. Agrega el usuario actual al grupo docker para poder ejecutar contenedores sin usar sudo.
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian $(. /etc/os-release && echo $VERSION_CODENAME) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl enable --now docker
sudo usermod -aG docker $USER
newgrp docker
```
