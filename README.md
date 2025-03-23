
# Instrucciones para crear una VM y correr Mario Bros en Docker

Este documento proporciona una guía paso a paso para crear una máquina virtual (VM), configurarla con Terraform, y luego ejecutar un contenedor Docker con el juego de Mario Bros utilizando Ansible.

## 1. Crear y configurar la Máquina Virtual (VM) con Terraform

### 1.1 Clonar el repositorio

Lo primero que necesitamos es clonar el repositorio que contiene los archivos de configuración de la VM.

```bash
git clone https://github.com/Juandap19/Ingesoft-5.git
```

### 1.2 Navegar al directorio de la VM

Accedemos al directorio `vm-tf` que contiene los archivos necesarios para crear la VM.

```bash
cd vm-tf
```

### 1.3 Inicializar Terraform

Ejecutamos el comando `terraform init` para inicializar Terraform y descargar los proveedores necesarios.

```bash
terraform init
```

### 1.4 Validar la configuración de Terraform

Verificamos que los archivos de configuración sean correctos con el comando `terraform validate`.

```bash
terraform validate
```

### 1.5 Obtener el ID de la cuenta de Azure

Es importante conocer el ID de la cuenta y la suscripción que vamos a utilizar. Para obtener esta información, ejecutamos el siguiente comando:

```bash
az account show
```

### 1.6 Aplicar la configuración de Terraform

Finalmente, aplicamos la configuración de Terraform para crear la VM en Azure. Durante este paso, se nos pedirá ingresar el ID de usuario y el ID de la suscripción que obtuvimos en el paso anterior.

```bash
terraform apply
```

---

## 2. Correr el contenedor de Mario Bros en Docker

Para ejecutar Mario Bros en un contenedor Docker, seguimos los siguientes pasos en la VM que acabamos de crear.

### 2.1 Acceder a la VM

Nos conectamos a la VM mediante SSH utilizando la dirección IP pública de la máquina.

```bash
ssh usuario@ip_maquina_virtual
```

### 2.2 Clonar el repositorio de Ansible

Una vez dentro de la VM, clonamos el repositorio que contiene los archivos de configuración de Ansible.

```bash
git clone https://github.com/ChristianFlor/training-ansible.git
```

### 2.3 Navegar al directorio de inventario

Accedemos al directorio `inventory` donde se encuentran los archivos de configuración de Ansible.

```bash
cd training-ansible/inventory
```

### 2.4 Configurar el archivo `hosts.ini`

Editamos el archivo `hosts.ini` con `nano` y ajustamos los valores para que coincidan con la configuración de nuestra máquina virtual.

```bash
nano hosts.ini
```

### 2.5 Actualizar el sistema

Realizamos una actualización del sistema para asegurarnos de que todos los paquetes estén al día.

```bash
sudo apt update && sudo apt upgrade -y
```

### 2.6 Instalar Ansible y Dependencias

Instalamos Ansible y las dependencias necesarias, como `sshpass`, que se utilizará en los playbooks.

```bash
sudo apt install ansible -y
sudo apt install -y sshpass
```

### 2.7 Ejecutar el Playbook para instalar Docker

Ahora, ejecutamos el playbook de Ansible que instalará Docker en la máquina virtual.

```bash
ansible-playbook -i hosts.ini playbooks/install_docker.yml
```

### 2.8 Ejecutar el Playbook para iniciar el contenedor de Mario Bros

Finalmente, ejecutamos el segundo playbook de Ansible que configurará y ejecutará el contenedor Docker con Mario Bros.

```bash
ansible-playbook -i hosts.ini playbooks/run_container.yml
```

---

¡Con esto, tu contenedor Docker con Mario Bros estará en funcionamiento en la VM!

http://213.199.130.104:8787/

![image](https://github.com/user-attachments/assets/78c1c3fc-a87d-4488-917f-cf0806f18672)
