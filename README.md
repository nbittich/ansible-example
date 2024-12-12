# Ansible exemple

Exemple de projet ansible avec 2 servers (2 containers ubuntu).

`docker compose up -d`

### vérifier son inventaire:

`docker compose exec ansible-inventory -i inventory.ini --list`

Dans ce cas nous avons 2 hosts.

### Lancer le master playbook

Le master playbook (`playbooks/master.yml`) va nous permettre de lancer nos playbooks dans un ordre
déterminé.

J'ai volontairement désinstaller python sur les server1 & server2 (voir `Dockerfiles/ubuntu/Dockerfile`).

Ansible a besoin de python installé pour fonctionner correctement.

Pour ce faire, nous avons le playbook `install-python.yml` qui bypass le `gather_facts` d'Ansible et installe
python sur les hosts cibles (`dockerhosts`).

Ce playbook doit être lancer en premier dans notre master playbook. Les tâches suivantes pourront ainsi utiliser
ansible pleinement.

Nous pouvons lancer le playbook avec la commande suivante:

`docker compose exec ansible ansible-playbook -i inventory.ini master.yml`

### pinger les hosts:

Nous pouvons pinger nos hosts de cette manière:

`docker compose exec ansible ansible dockerhosts -m ping -i inventory.ini`
