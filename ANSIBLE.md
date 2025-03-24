## ANSIBLE
Ansible es una herramienta de automatización de TI de código abierto que permite gestionar la configuración, implementar aplicaciones y organizar sistemas de manera eficiente.

## Automatización sin agentes
No requiere la instalación de software adicional en los nodos que gestiona, lo que simplifica su uso.

## Playbooks
Utiliza archivos de texto llamados playbooks para definir las tareas que se deben realizar. Estos playbooks están escritos en un lenguaje sencillo y fácil de entender.

## Conexión mediante SSH
Se conecta a los nodos usando SSH (o WinRM en sistemas Windows) para ejecutar las tareas de manera directa.

## Módulos Ansible 
utiliza módulos para realizar tareas específicas en los nodos. Estos módulos pueden ser escritos en varios lenguajes de programación como Python, Ruby o Bash.

## Objetivo Principal

## Automatización de la configuración: 
Facilitar la configuración y gestión de servidores y dispositivos de red.
## Despliegue de aplicaciones: 
Automatizar el proceso de despliegue de aplicaciones en diferentes entornos.
## Orquestación: 
Coordinar múltiples tareas en diferentes sistemas para asegurar que se ejecuten en el orden correcto.
## Gestión de la infraestructura: 
Proporcionar una manera eficiente de gestionar y mantener la infraestructura de TI, reduciendo errores humanos y mejorando la consistencia.


## Como integrarlo con CyberkArk: 01-cybark_auth.yaml
- name: Autenticar en CyberArk
  hosts: localhost
  vars_files:
    - /etc/ansible/credentials.yml
  tasks:
    - name: Obtener token de autenticación
      cyberark.pas.cyberark_authentication:
        api_base_url: "https://asesuisa.cyberark.cloud/"
        username: "{{ username_cybark }}"
        password: "{{ password_cybark }}"
      register: cyberark_token

    - name: Recuperar cuenta segura
      cyberark.pas.cyberark_account:
        api_base_url: "https://asesuisa.cyberark.cloud/"
        auth_token: "{{ cyberark_token.token }}"
        safe_name: "SV-WIN-DO-PAMCA"
        account_name: "pam_ca"
      register: server_account
    
    - name: Hacer ping a un servidor de prueba
      
    


## El uso de ansible vault para almacenar contraseñas de usuario
ansible-vault create /etc/ansible/credentials.yml

## Dentro de archivo credencials.yml
username_cybark: giotomato
password_cybark: hola1234

### ejecucion de script
ansible-playbook --vault-password-file /tmp/vault_pass 01-cybark_auth.yaml

