RocketChat Docker
=========

Ce rôle sert à déployer/remettre en état un serveur Rocket un projet Docker Compose conçu pour un environment de production. 
En résumé, on automatise la procédure décrite ici : https://github.com/frdmn/docker-rocketchat

Requirements
------------

### Matériel
* Minimum : 1 vcore + 1 Go de RAM + 30 Go SSD (50 utilisateurs actifs)
* Recommandé : 2 vcore + 2 Go de RAM + 40 Go SSD (100 utilisateurs actifs)
* Voir la doc officielle pour plus d'infos : 
https://docs.rocket.chat/installing-and-updating/hardware-requirements

### Système d'exploitation
* Ubuntu 20.04 (seul SE testé)

### Docker, Docker Compose, certbot, nginx
* IMPORTANT : Docker, Docker Compose, certbot et nginx NE SONT PAS installés par le rôle
* NOTE : Les paquets .deb disponibles dans Ubuntu 20.04 (universe) sont suffisants

Role Variables
--------------

### defaults/main.yml

Les valeurs par défaut dans defaults/main.yml qu'il est normal d'adapter sont l'utilisateur unix qui exécute Docker et Docker Compose et le nom de l'hôte qui est configuré pour nginx. Vous pouvez les modifier directement dans main.yml ou mieux encore les supplanter ailleurs (par exemple dans votre playbook site.yml).

Dependencies
------------

Aucune dépendance à d'autres rôles Ansible.

Example Playbook
----------------

```
- name: "Deployer un serveur Rocket Chat via Docker Compose"
  hosts: 
    - all
  vars:
    # Supplanter ici les variables du role au besoin

  pre_tasks:
    - name: "Installer Docker, Docker Compose, nginx"
      apt:
        name: docker.io, docker-compose, nginx
        state: present
      become: yes
    - name: "Installer Certbot"
      snap:
        name: certbot
        state: present
      become: yes
  roles:
    - { role: ansible-docker-rocketchat-role, tags: "rocketchat" }
```

License
-------

GPL-3.0-only

Author Information
------------------

Mathieu GP, admin. sys. pour Coderbunker
