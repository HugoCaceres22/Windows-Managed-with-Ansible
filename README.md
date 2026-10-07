# Windows Managed with Ansible

Proyecto de administración centralizada de equipos Windows desde un servidor Ubuntu utilizando Ansible.

La solución permite gestionar máquinas Windows pertenecientes a un dominio de Active Directory mediante una conexión segura basada en:

- Ansible
- WinRM sobre HTTPS
- Kerberos
- Active Directory
- Group Policy (GPO)
- Active Directory Certificate Services (AD CS)
- Certificados de equipo
- Firewall de Windows

## Objetivo

El objetivo principal del proyecto es evitar la configuración manual de cada equipo Windows y centralizar su administración desde un único nodo de control Ubuntu.

Para ello, los equipos del dominio se preparan automáticamente mediante políticas de grupo y certificados, de forma que puedan ser administrados posteriormente con Ansible de manera segura y escalable.

La comunicación se realiza únicamente mediante WinRM sobre HTTPS y utiliza Kerberos como método de autenticación.

## Arquitectura

El proyecto está formado principalmente por:

- Un servidor Ubuntu que actúa como nodo de control de Ansible.
- Un dominio de Active Directory.
- Una Autoridad de Certificación mediante AD CS.
- Equipos Windows unidos al dominio.
- GPO específicas para preparar automáticamente los equipos.
- Certificados de equipo utilizados por WinRM sobre HTTPS.

Flujo simplificado:

```text
Ubuntu + Ansible
        |
        | Kerberos
        | WinRM HTTPS :5986
        v
Windows Domain
        |
        +-- Active Directory
        +-- GPO
        +-- AD CS
        +-- Certificates
